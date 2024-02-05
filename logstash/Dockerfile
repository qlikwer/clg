# Используем образ Logstash из Docker Hub
FROM logstash:5.6.3

COPY ./logstash/logstash-output-clickhouse-0.1.0.gem /usr/share/logstash/bin/logstash-output-clickhouse-0.1.0.gem

RUN logstash-plugin install logstash-input-beats && \
    logstash-plugin install logstash-filter-prune && \
    logstash-plugin install logstash-filter-multiline && \
    logstash-plugin install /usr/share/logstash/bin/logstash-output-clickhouse-0.1.0.gem
# Копируем наш конфигурационный файл Logstash
COPY ./logstash/pipeline/ /etc/logstash/pipeline/
COPY ./logstash/logstash.yml /usr/share/logstash/config/logstash.yml

# Запускаем Logstash
#CMD ["logstash"]
CMD ["logstash", "-f", "/etc/logstash/pipeline/"]
