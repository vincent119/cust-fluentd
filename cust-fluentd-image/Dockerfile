FROM fluent/fluentd:v1.14-1

# Use root account to use apk
USER root

# below RUN includes plugin as examples elasticsearch is not required
# you may customize including plugins as you wish
RUN apk add --no-cache --update --virtual .build-deps \
        sudo build-base ruby-dev 
RUN apk add --no-cache geoip geoip-dev libmaxminddb \
 && sudo gem install fluent-plugin-elasticsearch \
 && sudo gem install fluent-plugin-rewrite-tag-filter \
 && sudo gem install fluent-plugin-rewrite-tag-filter \
 && sudo gem install fluent-plugin-geoip:0.8.0 \
 && sudo gem install fluent-plugin-prometheus \
 && sudo gem install fluent-plugin-parser \
 && sudo gem install fluent-plugin-grok-parser \
 && sudo gem install fluent-plugin-add \
 && sudo gem install fluent-plugin-gelf \
 && sudo gem sources --clear-all \
 && apk del .build-deps \
 && rm -rf /tmp/* /var/tmp/* /usr/lib/ruby/gems/*/cache/*.gem

COPY fluent.conf /fluentd/etc/
COPY entrypoint.sh /bin/

USER fluent
