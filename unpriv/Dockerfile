FROM nginxinc/nginx-unprivileged:1.18

RUN rm -fr /etc/nginx/conf.d/default.conf
COPY frontend.conf /etc/nginx/conf.d/frontend.conf
COPY --chown=nginx:nginx dist /app
COPY --chown=nginx:nginx entrypoint.sh /tmp/entrypoint.sh

USER nginx

ENTRYPOINT [ "/tmp/entrypoint.sh" ]
