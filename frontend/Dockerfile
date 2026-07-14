# ---- build stage: node builds the static bundle ----
FROM node:18-alpine AS build
WORKDIR /app
ARG REACT_APP_BACKEND_URL=""
ENV REACT_APP_BACKEND_URL=$REACT_APP_BACKEND_URL
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# ---- serve stage: only the output ships here ----
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
