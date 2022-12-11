FROM node:12.22.7-alpine AS builder
ENV CLOUDL_SERVER="localhost"
WORKDIR /src
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx:1.23.2-alpine
COPY --from=builder /src/build /usr/share/nginx/html
COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
