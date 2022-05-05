FROM node:lts AS build
WORKDIR /app
ENV NODE_ENV production
COPY twikoo/twikoo.version .
RUN set -eux; \
  npm install --production twikoo-vercel@$(cat twikoo.version)
COPY twikoo/index.js .
FROM node:lts-buster-slim
WORKDIR /app
ENV NODE_ENV production
COPY --from=build /app .
EXPOSE 8080
CMD ["node", "index.js"]
