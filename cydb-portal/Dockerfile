FROM node:26-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:1.31.8-alpine

RUN apk upgrade --no-cache

COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY snippets/security-headers.conf /etc/nginx/snippets/security-headers.conf
COPY --from=build /app/dist /usr/share/nginx/html

# OpenShift does not allow privileged ports like 80.
EXPOSE 8080

# OpenShift runs an arbitrary UID in group 0. No chown/chmod is needed because
# nginx.conf puts the pid file and temp dirs in /tmp and logs go to stdout.
USER nginx
