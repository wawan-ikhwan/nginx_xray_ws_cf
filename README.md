# Setup Websocket Tunneling
If your Internet Service Provider didn't block one of Cloudflare IPs, then you are lucky. You got free internet access, but you need another device that has internet outbound connection that act as relay server.

## Prerequisites
Device is able to perform internet outbound connection, inbound connection is not needed since it will be handled by Cloudflared tunnel. List of binary program needed to download:

  1. [Cloudflared](https://github.com/cloudflare/cloudflared/releases)
  2. [Nginx](http://nginx.org/en/download.html)
  3. [Xray](https://github.com/XTLS/Xray-core/releases)

## Server Conf
  1. Xray
      ```
      xray run -c xray_conf.json
      ```
  2. Nginx
      ```
      cp nginx_v2ray.conf /etc/nginx/sites-available
      ln -s /etc/nginx/sites-available/nginx_v2ray.conf /etc/nginx/sites-enabled/
      nginx -t
      systemctl reload nginx
      ```
  3. Cloudflared
      ```
      cloudflared tunnel login
      cloudflared tunnel route dns <TunnelName> <Subdomain>
      cloudflared tunnel --config cloudflared_conf.yaml run
      ```

## Client Conf
  1. Install [v2ray client](https://www.v2ray.com/en/awesome/tools.html).
  2. Use setting from `client_conf.json`.