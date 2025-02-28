# Build stage
FROM node:14-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install --save-dev \
    babel-loader@8.3.0 \
    @babel/core@7.22.0 \
    @babel/preset-env@7.22.0 \
    terser-webpack-plugin@5.3.9 \
    webpack@4.46.0 \
    webpack-cli@4.10.0 \
    vue-loader@15.11.1
    
RUN npm install
COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]