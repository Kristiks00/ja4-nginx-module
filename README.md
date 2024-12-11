Installation:
1. Clone angie repo: git clone git@github.com:webserver-llc/angie.git && cd angie
2. Apply angie.patch: git apply /path/to/angie.patch
3. Clone angie-module-lua: apt install angie-module-lua
4. Create symlink to repo: ln -s /path/to/folder/angie/modules /path/to/angie/repo/modules
5. Clone ja4-nginx-module repo: git clone git@github.com:Kristiks00/ja4-nginx-module.git
6. Clone openssl repo: git clone git@github.com:openssl/openssl.git
7. Apply openssl.patch to openssl: cd openssl && git apply /path/to/openssl.patch && cd ..
8. ./configure --with-debug --with-compat --add-module=./ja4-nginx-module/src --with-http_ssl_module --with-openssl=$(pwd)/openssl --prefix=$(pwd)/nginx_local
9. make && make install


Start:
	sudo ./nginx_local/sbin/angie -g "daemon off;"

Gen certs:
	openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout nginx_local/conf/server.key -out nginx_local/conf/server.crt -subj "/C=US/ST=State/L=City/O=Organization/OU=Department/CN=localhost"

Convert crt to pem:
	openssl x509 -in nginx_local/server.crt -out nginx_local/server.pem -outform PEM

Connect with openssl client:
	openssl s_client -connect localhost:443