FROM node:18-alpine AS build-env

WORKDIR /app
COPY package*.json ./
RUN npm ci --omit=dev
COPY . .

FROM gcr.io/distroless/nodejs18-debian12
WORKDIR /app
COPY --from=build-env /app /app

ENV NODE_ENV=production
ENV LOGLEVEL="info"
ENV MQTT_BROKER_URL="mqtt://127.0.0.1"

CMD ["app.js"]