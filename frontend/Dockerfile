# syntax=docker/dockerfile:1
FROM node:20-slim AS builder

WORKDIR /app

COPY frontend/package.json ./
RUN npm install --omit=dev

FROM node:20-slim
WORKDIR /app

RUN useradd -m appuser
USER appuser

COPY --from=builder /app/node_modules ./node_modules
COPY frontend/ .

EXPOSE 3000
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD wget --no-verbose --tries=1 --spider http://localhost:3000 || exit 1

CMD ["node", "app.js"]
