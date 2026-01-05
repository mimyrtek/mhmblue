# ---- Build Hugo site ----
FROM hugomods/hugo:exts AS build
WORKDIR /src

# Build context is repo root, so copy from mhmblue/site
COPY mhmblue/site/ /src/
RUN hugo --minify

# ---- Serve with nginx ----
FROM nginx:1.27-alpine
# nginx.conf also lives under mhmblue/
COPY mhmblue/app/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /src/public /usr/share/nginx/html
EXPOSE 80
