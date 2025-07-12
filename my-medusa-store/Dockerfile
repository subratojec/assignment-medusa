# Use official Node.js LTS image
FROM node:20-alpine

# Set working directory
WORKDIR /app

# Copy only dependency files first
COPY package.json yarn.lock ./

# Install production dependencies
RUN yarn install --production

# Copy rest of the code
COPY . .

# Set environment variables
ENV NODE_ENV=production

# Expose Medusa's default port
EXPOSE 9000

# Start the Medusa server
CMD ["yarn", "start"]
