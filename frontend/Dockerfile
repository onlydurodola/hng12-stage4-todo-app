# Build stage
FROM node:14-alpine AS build

WORKDIR /app

COPY package*.json ./

# Install Babel to transpile ES6+ code for UglifyJs compatibility
RUN npm install --save-dev \
    babel-loader@8.3.0 \
    @babel/core@7.22.0 \
    @babel/preset-env@7.22.0

# Install dependencies as specified in package.json
RUN npm install

COPY . .

# Build the Vue.js application
RUN npm run build

# Production stage
FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]