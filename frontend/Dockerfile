FROM node:16-alpine
WORKDIR /app
ENV PATH="./node_modules/.bin:$PATH"
COPY ["./package.json", "./package-lock.json*", "./"]
RUN npm ci
COPY ./ ./
RUN npm run build

FROM nginx:stable-alpine
COPY --from=0 /app/build /usr/share/nginx/html
RUN rm -rf /etc/nginx/conf.d
COPY conf /etc/nginx

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]