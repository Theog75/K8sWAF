FROM centos/httpd

RUN yum remove -y httpd && yum update -y && yum install -y httpd && yum install -y mod_ssl mod_auth_gssapi.x86_64 mod_auth_kerb.x86_64 mod_authnz_pam.x86_64 mod_proxy_html mod_proxy_html


ADD index.html /var/www/html/
ADD httpd.conf /etc/httpd/conf


