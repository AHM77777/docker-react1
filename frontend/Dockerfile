FROM node:16-alpine AS builder
WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH
COPY ["./package.json", "./package-lock.json*", "./"]
RUN npm ci
COPY ./ ./
RUN npm run build

FROM nginx:stable-alpine
COPY --from=builder /app/build /usr/share/nginx/html
RUN rm -rf /etc/nginx/conf.d
COPY conf /etc/nginx

EXPOSE 80
CMD ["nginx", "-g", "daemon off;;"]