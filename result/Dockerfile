FROM node:22.12.0-slim

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    curl \
    tini \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# have nodemon available for local dev use (file watching)
RUN npm install -g nodemon@3.1.7

COPY package*.json ./

RUN npm install \
 && npm cache clean --force \
 && mv /app/node_modules /node_modules

COPY . .

ENV PORT=80

EXPOSE 80

CMD ["/usr/bin/tini", "--", "node", "server.js"]
