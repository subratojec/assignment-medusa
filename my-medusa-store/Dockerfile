# Use official Node.js LTS image
FROM node:20-alpine

# Set working directory
WORKDIR /app

# Copy only dependency files first
COPY package.json yarn.lock ./

# Install production dependencies with retry
RUN for i in 1 2 3; do yarn install --production && break || sleep 5; done

# Copy the rest of the code
COPY . .

# Set environment variables
ENV NODE_ENV=production

# Expose Medusa's default port
EXPOSE 9000

# Start the Medusa server
CMD ["yarn", "start"]
