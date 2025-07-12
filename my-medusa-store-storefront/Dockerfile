# Use official Node image
FROM node:20-alpine

# Enable Corepack and activate the required Yarn version
RUN corepack enable && corepack prepare yarn@3.2.3 --activate

# Set working directory
WORKDIR /app

# Copy only dependency-related files
COPY package.json yarn.lock .yarnrc.yml ./

# Pre-create the yarn cache folder for better caching in Docker
RUN mkdir -p .yarn/cache

# Install dependencies using zero-install if applicable
RUN yarn install --immutable

# Copy the full project source
COPY . .

ENV NEXT_PUBLIC_MEDUSA_BACKEND_URL=http://localhost:9000

# Build the Next.js app
RUN yarn build

# Expose the port (Next.js defaults to 3000, but you're using 8000 — that's fine)
EXPOSE 8000

# Start the app (production mode)
CMD ["yarn", "start"]
