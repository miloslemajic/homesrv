# NetBox

---

## installation 
done from netbox documentation
[https://docs.netbox.dev/en/stable/installation](https://docs.netbox.dev/en/stable/installation)

used wildcard in `ALLOWED_HOSTS = '*'`

HTTP server -  cert bot automatically provisions cert from lets encrypt.

at 
```
/etc/nginx/sites-available/netbox
```
server name needs to be updated
if ssl cert exist elsewere, also needs to be updated at same location

---

## issues encountered
- Port conflict
works over nginx but openvpn 'overlaps it', didnt manage to google it/identify problem, deleted openvpn, set it up on router
	update: installed openvpn again, it was port conflict as nginx and openvpn client both use 443 port by default, changed port for openvpn, works as intended
	
at first test from installation at [https://docs.netbox.dev/en/stable/installation/3-netbox/#test-the-application'page](https://docs.netbox.dev/en/stable/installation/3-netbox/#test-the-application'page) `ModuleNotFoundError: No module named 'django'` , occurs if test server run is not done with 'venv' environement activated
