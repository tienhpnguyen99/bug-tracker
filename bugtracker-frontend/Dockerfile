FROM node:20-alpine AS builder

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci

COPY . .
RUN npm test -- --coverage

# Accept a build argument, needed for deploying on Fly.io
ARG NEXT_PUBLIC_API_URL

RUN echo "test-results.xml" >> .dockerignore

RUN npm run build

EXPOSE 3000

CMD ["npm", "start"] 