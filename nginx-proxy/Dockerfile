FROM alpine:3.12.0 as builder
RUN apk add wget zip unzip
WORKDIR /app
RUN wget https://github.com/kajdreef/test-matrix-visualization/releases/download/v1.1.0-user-study/release.zip
RUN unzip release.zip -d .
RUN rm release.zip

FROM nginx:alpine
RUN mkdir /var/run/nginx-proxy-cache
ADD ./nginx.conf /etc/nginx/nginx.conf
ADD ./vhosts/ /etc/nginx/vhosts/
WORKDIR /var/www/
COPY --from=builder /app/build/ .
