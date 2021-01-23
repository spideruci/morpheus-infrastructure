FROM node:lts-alpine3.12 as base-builder
RUN apk add wget zip unzip git
WORKDIR /app

FROM base-builder as builder-spidertest
RUN git clone https://github.com/spideruci/morpheus .
RUN git checkout v1.1.7-user-study
RUN yarn install
RUN REACT_APP_API_ENDPOINT=http://api-spidertest.kajdreef.com yarn build

FROM base-builder as builder-demo
RUN git clone https://github.com/spideruci/morpheus .
RUN git checkout demo-v1.1.7
RUN yarn install
RUN REACT_APP_API_ENDPOINT=http://api.kajdreef.com yarn build

FROM base-builder as builder-morpheus
RUN git clone https://github.com/spideruci/morpheus .
RUN git checkout v1.1.4
RUN yarn install
RUN REACT_APP_API_ENDPOINT=http://api.kajdreef.com yarn build

FROM nginx:alpine
RUN mkdir /var/run/nginx-proxy-cache-general
RUN mkdir /var/run/nginx-proxy-cache-user-study
ADD ./nginx.conf /etc/nginx/nginx.conf
ADD ./vhosts/ /etc/nginx/vhosts/

WORKDIR /var/www/spidertest/
COPY --from=builder-spidertest /app/build/ .

WORKDIR /var/www/demo/
COPY --from=builder-demo /app/build/ .

WORKDIR /var/www/morpheus/
COPY --from=builder-morpheus /app/build/ .
