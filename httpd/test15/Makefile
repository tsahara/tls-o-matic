test=test15
domain=tls-o-matic.com

all:
	@if ! test -h www/logo.png;then \
		ln -s /usr/local/tls-o-matic/images/tls-o-matic-small.png www/logo.png ;\
		fi
	@cp ../../certs/$(test)* .
	@# Create a combined intermediate cert file
	@cp ../../certs/TLS-o-matic-intermediate-1.cert .
	@echo "==> Starting HTTPD server for $(test).$(domain)"
	@/usr/local/apache2/bin/httpd -f /usr/local/tls-o-matic/httpd/$(test)/server.conf
	@sleep 1	# Wait for apache to create PID file
	@if ! test -f /var/run/httpd-$(test).pid;then (echo " ❌  ERROR no pid file";exit 1);fi
	@echo "✅  done!"

kill:
	@if ! test -f /var/run/httpd-$(test).pid;then (echo " ❌  ERROR no pid file";exit 1);fi
	@kill `cat /var/run/httpd-$(test).pid`
	@echo "✅  done!"
