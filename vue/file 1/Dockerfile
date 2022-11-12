FROM node:19.0.1-alpine3.15 as build

WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH

# COPY package.json /app/package.json
COPY package.json ./

RUN npm install --silent \
    npm install vue

COPY . .

RUN npm run build



# production environment
FROM nginx:stable-alpine

COPY --from=build /app/dist /usr/share/nginx/html

RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]