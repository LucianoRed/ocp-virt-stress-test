FROM registry.access.redhat.com/ubi9/ubi:9.5-1732804088
RUN yum install -y python3-pip git && pip install --upgrade pip && pip install --upgrade ansible && pip install --upgrade kubernetes && yum clean all && rm -rf /var/run/cache && pip cache purge
ENV K8S_AUTH_API_KEY=x
ENV K8S_AUTH_HOST=y
ENV K8S_AUTH_VERIFY_SSL=false
ENV HOME=/ansible
ENV ANSIBLE_HOST_KEY_CHECKING=False
RUN yum install -y httpd php iputils wget && mkdir /ansible && chmod -R 777 /ansible && sed -i 's/^Listen 80$/Listen 8080/' /etc/httpd/conf/httpd.conf && chmod -R 777 /var/run && chmod -R 777 /etc/httpd/logs/ && yum clean all && rm -rf /var/run/cache
RUN cd /tmp && wget https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/stable/openshift-client-linux.tar.gz && tar -zxvf openshift-client-linux.tar.gz && mv kubectl oc /usr/local/bin && rm -f openshift-client-linux.tar.gz
ADD playbooks /ansible
RUN chmod -R 777 /ansible
USER 12345
EXPOSE 8080
WORKDIR /ansible
CMD ["httpd", "-D", "FOREGROUND"]
