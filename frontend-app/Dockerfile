FROM node:16-alpine as builder

WORKDIR /app

# COPY package.json .
COPY . .

RUN npm install

COPY . .

RUN npm run build

FROM nginx:stable-alpine

RUN mkdir /usr/share/nginx/buffer

COPY --from=builder /app/out /usr/share/nginx/html
COPY --from=builder /app/public /usr/share/nginx/html
ADD conf/nginx.conf /etc/nginx/conf.d/default.conf

RUN mkdir /usr/share/nginx/log

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
