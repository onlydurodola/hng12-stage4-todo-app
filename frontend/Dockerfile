# Build stage
FROM node:14-alpine AS build

WORKDIR /app

COPY package*.json ./

# Install Babel to transpile ES6+ code for UglifyJs compatibility
RUN npm install --save-dev \
    babel-loader@7.1.5 \
    babel-core@6.26.3 \
    babel-preset-env@1.7.0

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