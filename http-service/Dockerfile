FROM public.ecr.aws/docker/library/node:16 AS app-setup

USER node

WORKDIR /app

RUN uid=1000 \
    npm install --production

COPY . .

FROM public.ecr.aws/docker/library/alpine:3.15

RUN apk --no-cache add --upgrade nodejs~16

LABEL vendor="hi-artem-org"

ENV APP_NAME https-service

ENV APP_DIR /app/http-service

RUN mkdir -p $APP_DIR
WORKDIR $APP_DIR
USER 10001

COPY --chown=10001:10001 --from=app-setup /app .

EXPOSE 9000

CMD ["node", "main.js"]
