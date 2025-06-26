FROM nginx:alpine

# Create a custom index.html
RUN echo "<h1>Welcome to Nginx</h1>" > /usr/share/nginx/html/index.html

# Intentionally misconfigured command to cause CrashLoopBackOff
# The command points to a non-existent configuration file
CMD ["nginx", "-g", "daemon off; error_log /var/log/nginx/error.log debug;", "-c", "/etc/nginx/nginx-missing.conf"]
