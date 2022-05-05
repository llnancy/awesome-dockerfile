FROM node:lts AS build
WORKDIR /app
ENV NODE_ENV production
COPY twikoo.version .
RUN set -eux; \
  npm install --production twikoo-vercel@$(cat twikoo.version)
COPY index.js .
FROM node:lts-buster-slim
WORKDIR /app
ENV NODE_ENV production
COPY --from=build /app .
EXPOSE 8080
CMD ["node", "index.js"]
