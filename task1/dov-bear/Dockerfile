# base image
ARG NODE_VER=18
ARG APP_DIR=/app
FROM node:${NODE_VER}

# Building the image
# Create /app and cd into it
WORKDIR ${APP_DIR}

# Additional packages
# RUN apt update && apt install curl -y

# Copy application into /app
ADD main.js . 
ADD package.json .
ADD package-lock.json .

# directory copy has to add path
ADD public public
ADD views views

# Install the dependencies (npm ci looks at package-lock file and not package file)
RUN npm ci

# Running the image
# Use ENV to set environment variables
ENV PORT=5000
ENV INSTANCE_NAME=Beary
ENV INSTANCE_HASH=

# Add healthcheck (set all other error codes to 1 by || exit 1)
# dependent on curl being available in the image
#HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
#CMD curl http://localhost:${APP_PORT}/healthz || exit 1

# Expose the app port
EXPOSE ${PORT}

# Start the program
ENTRYPOINT node main.js

# Set option
CMD ${PORT}