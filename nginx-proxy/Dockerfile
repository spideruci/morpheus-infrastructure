FROM node:14-alpine as builder
RUN apk add git
WORKDIR /app
RUN git clone https://github.com/kajdreef/test-matrix-visualization .
RUN yarn install
RUN yarn build

FROM nginx:alpine
ADD ./nginx.conf /etc/nginx/nginx.conf
WORKDIR /var/www/
COPY --from=builder /app/build/ .
