# ---- Build Hugo site ----
FROM hugomods/hugo:exts AS build
WORKDIR /src

COPY site/ /src/

# Print useful debug, then run Hugo.
# If Hugo fails, the logs will show WHY in GitHub Actions.
RUN echo "=== /src tree ===" && \
    (find /src -maxdepth 3 -type f -print || true) && \
    echo "=== hugo version ===" && \
    hugo version && \
    echo "=== hugo config ===" && \
    (ls -la /src/config.* /src/hugo.* 2>/dev/null || true) && \
    echo "=== hugo build ===" && \
    hugo --minify --logLevel debug --printPathWarnings --printI18nWarnings --templateMetrics

# ---- Serve with nginx ----
FROM nginx:1.27-alpine
COPY app/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /src/public /usr/share/nginx/html
EXPOSE 80
