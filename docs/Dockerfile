FROM node:23 AS build
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install
COPY . .
RUN yarn build

FROM nginx:alpine
WORKDIR /usr/share/nginx/html
COPY --from=build /app/build .
EXPOSE 80
RUN chown -R nginx:nginx /app && chmod -R 755 /app
RUN chown -R nginx:nginx /var/cache/nginx
RUN chown -R nginx:nginx /etc/nginx
RUN chown -R nginx:nginx /var/log/nginx
USER nginx
CMD ["nginx", "-g", "daemon off;"]