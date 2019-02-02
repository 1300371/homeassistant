# HTTPS Documentation

Considering all the ways to configure HA, here we will use _sub-domains_ to provide access to multiple services. 

## DuckDNS Addon
<small>https://www.home-assistant.io/addons/duckdns/</small>  

### Get a _DuckDNS_ account

1. Sign in to https://www.duckdns.org
1. Create your domain
1. Get your token
    1. Browse to _install_: https://www.duckdns.org/install.jsp
    1. Choose OS: _pi_
    1. Select your domain
    1. _Token_ is accessible in displayed command line
    ```
    echo url="https://www.duckdns.org/update?domains=<DOMAIN>&token=<TOKEN>&ip=" | curl -k -o ~/duckdns/duck.log -K -
    ```

### Complete the duckDNS Addon configuration
```yaml
{
  "lets_encrypt": {
    "accept_terms": true,
    "certfile": "fullchain.pem",
    "keyfile": "privkey.pem"
  },
  "token": "<duckdns-token>",
  "domains": ["*.<domain>.duckdns.org > <domain>.duckdns.org"],
  "seconds": 300
}
```
Note the `*.<domain>.duckdns.org > <domain>.duckdns.org` the domain configuration that provides wilcard certificate from _Let's Encrypt_ (CN=*.< domain >.duckdns.org).

### Update HA configuration
`configuration.yaml`
````yaml
http:
  base_url: <domain>.duckdns.org
````
Now, HA can be accessed at `https://<domain>.duckdns.org:8123`.

## Enable _https_ `panel_iframe`s
_Grafana example_
```
grafana:
  title: Grafana
  url: https://grafana.<domain>.duckdns.org
```

### NGINX

#### _hass.io_ plugins
<small>https://home-assistant.io/addons/nginx_proxy/</small>  

Install NGINX plugins in hass.io.
````yaml
{
  "domain": "ha.<domain>.duckdns.org",
  "certfile": "fullchain.pem",
  "keyfile": "privkey.pem",
  "hsts": "max-age=31536000; includeSubDomains",
  "customize": {
    "active": true,
    "default": "nginx_proxy_default*.conf",
    "servers": "nginx_proxy/*.conf"
  }
}
````

#### Additional configuration file 
`hassio/share/nginx_proxy/grafana.<domain>.duckdns.org.conf` on host machine.
```
server {
    server_name grafana.<domain>.duckdns.org;

    ssl_certificate /ssl/fullchain.pem;
    ssl_certificate_key /ssl/privkey.pem;

  

    listen [::]:443 http2;
    #add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    ssl on;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers "EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH:!aNULL:!eNULL:!EXPORT:!DES:!MD5:!PSK:!RC4";
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:10m;

    proxy_buffering off;

    location / {
        proxy_pass https://<grafana>:3000;
        proxy_set_header Host $host;
        proxy_redirect http:// https://;
        proxy_http_version 1.1;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
        #proxy_set_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    }
}
```

### Grafana
Update the Grafana hass.io plugins.
```yaml
{
  "log_level": "info",
  "ssl": true,
  "certfile": "fullchain.pem",
  "keyfile": "privkey.pem",
  "plugins": [],
  "env_vars": [
    {
      "name": "GF_SERVER_ROOT_URL",
      "value": "https://grafana.<domain>.duckdns.org"
    }
  ]
}
```