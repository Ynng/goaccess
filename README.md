My [goaccess](https://goaccess.io/) configuration file. 

Setup to use with the [Caddy](https://caddyserver.com/) reverse proxy and [Cloudflare](https://www.cloudflare.com/). `Cf-Connecting-Ip` is use to get the real IP address of clients connecting to the server. 

My caddyfile is setup to log in the json format and only accept traffic through cloudflare.

```caddyfile
(logging) {
	log {
		output file /var/log/caddy/{args[0]}.access.log
		format json
	}
}
(cloudflare-only) {
    # Update IPs here from the shell script output
    @blocked not remote_ip 173.245.48.0/20 103.21.244.0/22 103.22.200.0/22 103.31.4.0/22 141.101.64.0/18 108.162.192.0/18 190.93.240.0/20 188.114.96.0/20 197.234.240.0/22 198.41.128.0/17 162.158.0.0/15 104.16.0.0/13 104.24.0.0/14 172.64.0.0/13 131.0.72.0/22 2400:cb00::/32 2606:4700::/32 2803:f800::/32 2405:b500::/32 2405:8100::/32 2a06:98c0::/29 2c0f:f248::/32
    respond @blocked "<h1>HTTP/HTTPS access through Cloudflare only</h1>" 403
}
```
