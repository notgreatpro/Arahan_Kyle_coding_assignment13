FROM node:20-alpine AS build
WORKDIR /arahan_kyle_ui_garden_build_checks

# copy package.json and lock to take advantage of caching
COPY package*.json ./
RUN npm ci

# copy project files
COPY . .

# ensure public/index.html exists before running build
RUN ls -la public || true

# build production app
RUN npm run build

# Stage 2: Serve with nginx
FROM nginx:alpine
# Copy the build output into nginx html
COPY --from=build /arahan_kyle_ui_garden_build_checks/build /usr/share/nginx/html

# Expose port 80 in the container
EXPOSE 80

# run nginx in foreground
CMD ["nginx", "-g", "daemon off;"]