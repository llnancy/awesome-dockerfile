FROM node:24.11.1-alpine AS build
WORKDIR /app
ENV NODE_ENV production
RUN set -eux; \
  npm install --production tkserver@latest; \
  mkdir -p data
FROM node:24.11.1-alpine
WORKDIR /app
ENV NODE_ENV production
COPY --from=build /app .
EXPOSE 8080
CMD ["/app/node_modules/.bin/tkserver"]
