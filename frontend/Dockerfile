FROM node:20-alpine as react-build
WORKDIR /app
RUN apk add --no-cache python3 make g++
COPY . ./
RUN yarn
ENV NODE_OPTIONS=--openssl-legacy-provider
RUN yarn build

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/configfile.template
ENV PORT 8080
ENV HOST 0.0.0.0
RUN sh -c "envsubst '\$PORT' < /etc/nginx/conf.d/configfile.template > /etc/nginx/conf.d/default.conf"
COPY --from=react-build /app/build /usr/share/nginx/html
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
