# Base image 
FROM node:20-alpine

# Set working directory
WORKDIR /app

# Copy package.json (untuk caching layer)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy semua kode aplikasi
COPY . .

# Expose port untuk Next.js development server
EXPOSE 3000

# Jalankan Next.js development mode dengan hot-reload
CMD ["npm", "run", "dev"]