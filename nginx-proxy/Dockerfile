FROM node:lts-alpine3.12 as base-builder
RUN apk add git
WORKDIR /app

FROM base-builder as builder-morpheus
RUN git clone https://github.com/spideruci/morpheus .
RUN git checkout v1.1.4
RUN yarn install
RUN REACT_APP_API_ENDPOINT=http://api.kajdreef.com yarn build

FROM nginx:alpine
RUN mkdir /var/run/nginx-proxy-cache
ADD ./nginx.conf /etc/nginx/nginx.conf
ADD ./vhosts/ /etc/nginx/vhosts/
WORKDIR /var/www/morpheus
COPY --from=builder-morpheus /app/build/ .
