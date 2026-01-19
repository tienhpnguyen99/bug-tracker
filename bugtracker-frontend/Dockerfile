# ========================
# 1️⃣ TEST STAGE (CI)
# ========================
FROM node:20-bullseye AS test

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .
RUN npm test -- --coverage

# ========================
# 2️⃣ BUILD STAGE
# ========================
FROM node:20-bullseye AS build

WORKDIR /app

ARG NEXT_PUBLIC_API_URL
ENV NEXT_PUBLIC_API_URL=$NEXT_PUBLIC_API_URL

COPY package.json package-lock.json ./
RUN npm ci --omit=dev

COPY . .
RUN npm run build

# ========================
# 3️⃣ RUNTIME STAGE
# ========================
FROM node:20-bullseye AS runtime

WORKDIR /app

ENV NODE_ENV=production

COPY --from=build /app ./

EXPOSE 3000
CMD ["npm", "start"]
