FROM node:23 AS build
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install --production
COPY . . 
RUN yarn build

FROM node:23-slim
WORKDIR /app
COPY --from=build /app .
ENV VOTE_API_BASE_URL="https://devopsfinal.onrender.com/"
ENV NODE_ENV=production
EXPOSE 80
USER node
CMD ["yarn", "start"]
