FROM node:18-alpine

WORKDIR /app

# Alpine needs OpenSSL for Prisma
RUN apk add --no-cache openssl libc6-compat

# Install dependencies
COPY package*.json ./
COPY prisma ./prisma/

RUN npm install

# Copy source
COPY . .

# Generate Prisma Client using node directly (bypasses binary permission issues)
RUN node node_modules/prisma/build/index.js generate

# Build TypeScript
RUN npm run build

# Expose port
EXPOSE 4000

# Start command
CMD ["npm", "start"]
