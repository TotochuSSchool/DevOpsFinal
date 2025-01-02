FROM node:23 AS build
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install
COPY . .
RUN yarn build


FROM node:23-slim
WORKDIR /app
COPY --from=build /app ./
ENV VOTE_API_BASE_URL="http://localhost:8080"
EXPOSE 3000
USER node
CMD ["yarn", "start"]
