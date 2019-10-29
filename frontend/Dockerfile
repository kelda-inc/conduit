FROM node:12.2.0-alpine as build
WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH
COPY package-lock.json package.json /app/
RUN npm install --silent
RUN npm install react-scripts@3.0.1 -g --silent
COPY . .
RUN npm run build

FROM nginx:1.16.0-alpine
COPY default.conf /etc/nginx/conf.d/
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
