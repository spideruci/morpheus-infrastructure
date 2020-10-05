FROM alpine:3.12.0 as builder
RUN apk add wget zip unzip
WORKDIR /app
RUN wget https://github.com/kajdreef/test-matrix-visualization/releases/download/tag_9e220c5081c9f11e17d48801814ccb350e185170/release.zip
RUN unzip release.zip -d .
RUN rm release.zip

FROM nginx:alpine
ADD ./nginx.conf /etc/nginx/nginx.conf
WORKDIR /var/www/
COPY --from=builder /app/build/ .
