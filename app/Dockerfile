# ---- Build Hugo site ----
FROM hugomods/hugo:exts AS build
WORKDIR /src

COPY site/ /src/

# Show config + list files, then build. If it fails you'll see why in GitHub logs.
RUN ls -la /src && \
    (test -f /src/hugo.toml || test -f /src/config.toml || test -f /src/config.yaml || test -f /src/config.yml) && \
    hugo version && \
    hugo --minify --logLevel info --printI18nWarnings --printPathWarnings --printUnusedTemplates

# ---- Serve with nginx ----
FROM nginx:1.27-alpine
COPY app/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /src/public /usr/share/nginx/html
EXPOSE 80
