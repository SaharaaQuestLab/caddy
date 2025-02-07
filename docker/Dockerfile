# Use the official Caddy builder image
FROM caddy:2.9.1-builder AS builder

# Build Caddy using xcaddy and include the required modules
RUN xcaddy build \
    --with github.com/caddyserver/nginx-adapter \
    --with github.com/hairyhenderson/caddy-teapot-module@v0.0.3-0 \
    --with github.com/WeidiDeng/caddy-cloudflare-ip@latest  # Add Cloudflare IP module

# Use the official Caddy runtime image
FROM caddy:2.9.1

# Copy the compiled Caddy binary from the builder stage to the final image
COPY --from=builder /usr/bin/caddy /usr/bin/caddy

# Set the default command to run Caddy with the specified configuration
CMD ["caddy", "run", "--config", "/etc/caddy/Caddyfile", "--adapter", "caddyfile"]

