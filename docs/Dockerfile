FROM node:23 AS build
WORKDIR /app
COPY docs/package.json docs/yarn.lock ./
RUN yarn install
COPY docs/ .
RUN yarn build

FROM nginx:alpine
WORKDIR /usr/share/nginx/html
COPY --from=build /app/build .
EXPOSE 80
RUN chown -R nginx:nginx /usr/share/nginx/html && chmod -R 755 /usr/share/nginx/html
RUN chown -R nginx:nginx /var/cache/nginx
RUN chown -R nginx:nginx /etc/nginx
RUN chown -R nginx:nginx /var/log/nginx
USER nginx
CMD ["nginx", "-g", "daemon off;"]