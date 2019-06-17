### STAGE 1: Build ###
FROM node:latest as builder
COPY frontend/package.json frontend/package-lock.json ./
RUN npm set progress=false && npm config set depth 0 && npm cache clean --force
## Storing node modules on a separate layer will prevent unnecessary npm installs at each build
RUN npm i && mkdir /ng-app && cp -R ./node_modules ./ng-app
WORKDIR /ng-app
COPY frontend .
RUN $(npm bin)/ng build --prod

### STAGE 2: Setup ###
FROM traefik:alpine
RUN mkdir -p /etc/traefik/acme
RUN touch /etc/traefik/acme/acme.json
RUN chmod 600 /etc/traefik/acme/acme.json
COPY --from=builder /ng-app/dist /usr/share/traefik/html
COPY traefik.toml /etc/traefik
