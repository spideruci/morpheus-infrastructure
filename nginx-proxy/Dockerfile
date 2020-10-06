FROM alpine:3.12.0 as builder
RUN apk add wget zip unzip
WORKDIR /app
RUN wget https://github.com/kajdreef/test-matrix-visualization/releases/download/tag_0b5763904a337aa009e0e172360f001ed1711e38/release.zip
RUN unzip release.zip -d .
RUN rm release.zip

FROM nginx:alpine
ADD ./nginx.conf /etc/nginx/nginx.conf
WORKDIR /var/www/
COPY --from=builder /app/build/ .
