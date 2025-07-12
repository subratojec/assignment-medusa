# Use official Node image
FROM node:20-alpine

# Enable Corepack and activate the required Yarn version
RUN corepack enable && corepack prepare yarn@3.2.3 --activate

# Set working directory
WORKDIR /app

# Copy only dependency-related files
COPY package.json yarn.lock .yarnrc.yml ./

# Pre-create the yarn cache folder
RUN mkdir -p .yarn/cache

# Install dependencies using zero-install with retry logic
RUN for i in 1 2 3; do yarn install --immutable && break || sleep 5; done

# Copy the full project source
COPY . .

# Set environment variable for backend
ENV NEXT_PUBLIC_MEDUSA_BACKEND_URL=http://localhost:9000

# Build the Next.js app
RUN yarn build

# Expose the storefront port
EXPOSE 8000

# Start the app
CMD ["yarn", "start"]
