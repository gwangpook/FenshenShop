FROM node:18-alpine

WORKDIR /app

# Prisma on modern Alpine needs OpenSSL available during generate/runtime.
RUN apk add --no-cache openssl

# Install dependencies
COPY package*.json ./
COPY prisma ./prisma/

RUN npm install

# Fix permissions for prisma binary
RUN chmod +x ./node_modules/.bin/prisma || true

# Copy source
COPY . .

# Generate Prisma Client
RUN ./node_modules/.bin/prisma generate

# Build TypeScript
RUN npm run build

# Expose port
EXPOSE 4000

# Start command
CMD ["npm", "start"]
