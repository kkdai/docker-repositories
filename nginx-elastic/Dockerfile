#
# Nginx Dockerfile
#
# https://github.com/dockerfile/nginx
#

# Pull base image.
FROM dockerfile/ubuntu

# Install Nginx.
RUN \
  add-apt-repository -y ppa:nginx/stable && \
  apt-get update && \
  apt-get install -y nginx && \
  apt-get install -y openjdk-7-jre-headless && \
  rm -rf /var/lib/apt/lists/* && \
  echo "\ndaemon off;" >> /etc/nginx/nginx.conf && \
  chown -R www-data:www-data /var/lib/nginx

# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx"]

# /usr/share/nginx/html
# https://download.elasticsearch.org/kibana/kibana/kibana-3.1.0.tar.gz


# Download version 1.4.2 of logstash
RUN cd /tmp && \
    wget https://download.elasticsearch.org/logstash/logstash/logstash-1.4.2.tar.gz && \
    tar -xzvf ./logstash-1.4.2.tar.gz && \
    mv ./logstash-1.4.2 /opt/logstash && \
    rm ./logstash-1.4.2.tar.gz

# Install contrib plugins
RUN /opt/logstash/bin/plugin install contrib
    
# Install Elasticsearch
RUN wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.3.2.tar.gz
RUN tar zxvf elasticsearch-1.3.2.tar.gz

# Install Kibana
RUN wget https://download.elasticsearch.org/kibana/kibana/kibana-3.1.0.tar.gz
RUN tar zxvf kibana-3.1.0.tar.gz
RUN mv kibana-3.1.0 /usr/share/nginx/html/kibana


# Elasticsearch HTTP
EXPOSE 9200

# Elasticsearch transport
EXPOSE 9300

# Kibana
EXPOSE 9292

# Define working directory.
WORKDIR /etc/nginx

# Define default command.
CMD ["nginx"]


# Expose ports.
EXPOSE 80
EXPOSE 443