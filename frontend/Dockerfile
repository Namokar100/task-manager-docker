# Build stage

FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json .
RUN npm ci --legacy-peer-deps

COPY . .

RUN npm run build

# Production stage via serve

FROM node:20-alpine AS production
WORKDIR /app
RUN npm i -g serve

COPY --from=builder /app/dist ./dist

EXPOSE 5173

CMD ["serve", "-s", "dist", "-l", "5173"]
