FROM logstash:7.17.8

WORKDIR /usr/share/logstash

RUN bin/logstash-plugin install logstash-output-syslog \
    && bin/logstash-plugin install logstash-output-loki
    