# ---- Build Hugo site ----
FROM hugomods/hugo:exts AS build
WORKDIR /src

COPY site/ /src/

# 1) Show what actually got copied
RUN echo "=== /src tree (maxdepth 4) ===" && \
    find /src -maxdepth 4 -type f -print

# 2) Show Hugo version
RUN echo "=== hugo version ===" && \
    hugo version

# 3) Show config files present
RUN echo "=== hugo config files ===" && \
    ls -la /src || true && \
    ls -la /src/config.* 2>/dev/null || true && \
    ls -la /src/hugo.* 2>/dev/null || true

# 4) Run build (this is the step that fails; now you’ll see the real Hugo error above it)
RUN echo "=== hugo build ===" && \
    hugo --minify --logLevel debug --printPathWarnings --printI18nWarnings --templateMetrics

# ---- Serve with nginx ----
FROM nginx:1.27-alpine
COPY app/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /src/public /usr/share/nginx/html
EXPOSE 80
