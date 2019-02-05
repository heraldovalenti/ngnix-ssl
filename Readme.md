# Get started
1. Add `domain.crt` file to your trusted keychain.
2. Modify your /etc/hosts files to point www.simtlix.net to 127.0.0.1, e.g.:
```
127.0.0.1    www.simtlix.net
```
3. Run `docker-compose up -d`
4. Use your browser to access https://www.simtlix.net/

# Change suported TLS versions
Edit `default.conf` and comment/un-comment the SSL configurations as needed.
For example, to support only `TLSv1` and `TLSv1.1`:
```
# ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
ssl_protocols       TLSv1 TLSv1.1;
```

# Test the supported TLS versions
Use openssl indicating the TLS version to be used. For example, to test TLSv1.2:
```
openssl s_client -connect www.simtlix.net:443 -tls1_2
```
You can use `-tls1_1` to test for TLSv1.1, or `tls1` for TLSv1.

# Re-generate the certificates
You can regenerate the certificates provided by updating whatever you need in `req.conf` file and regenerating the certificates using openssl:
```openssl req -x509 -nodes -days 730 -newkey rsa:2048 -keyout domain.key -out domain.crt -config req.conf -extensions 'v3_req'```
After this, you need to re-import `domain.crt` to you trusted keychain and restart the containers with `docker-compose restart`.