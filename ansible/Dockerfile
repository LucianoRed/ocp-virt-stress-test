FROM registry.access.redhat.com/ubi9/ubi:9.5-1732804088
RUN yum install -y python3-pip && pip install --upgrade pip && pip install --upgrade ansible && pip install --upgrade kubernetes
ENV K8S_AUTH_API_KEY=x
ENV K8S_AUTH_HOST=y
ENV K8S_AUTH_VERIFY_SSL=false
RUN yum install -y httpd php && mkdir /ansible && chmod -R 777 /ansible && sed -i 's/^Listen 80$/Listen 8080/' /etc/httpd/conf/httpd.conf && chmod -R 777 /var/run && chmod -R 777 /etc/httpd/logs/
ADD . /ansible
USER 12345
CMD ["httpd", "-D", "FOREGROUND"]
