FROM node:20-alpine AS build
WORKDIR /components/frontend
COPY package.json ./
COPY package-lock.json ./
RUN npm install
COPY . .
RUN npm run build-prod

FROM nginx:latest
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=build /components/frontend/dist/frontend/browser /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
