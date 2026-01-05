# ---- Build Hugo site ----
FROM hugomods/hugo:exts AS build
WORKDIR /src

# Copy Hugo project
COPY site/ /src/

# Build site (fail with real Hugo error if broken)
RUN hugo --minify

# ---- Serve with nginx ----
FROM nginx:1.27-alpine
COPY app/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /src/public /usr/share/nginx/html
EXPOSE 80
