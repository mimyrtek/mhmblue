# ---- Build Hugo site ----
FROM klakegg/hugo:0.125.7-ext-alpine AS build
WORKDIR /src

# Copy the Hugo site
COPY mhmblue/site/ /src/

# Build
RUN hugo --minify

# ---- Serve with nginx ----
FROM nginx:1.27-alpine
COPY mhmblue/app/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /src/public /usr/share/nginx/html

EXPOSE 80
