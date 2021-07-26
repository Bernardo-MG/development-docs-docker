# Nginx

```text
FROM nginx:1.13.12-alpine as deployment

# Copy from build stage
COPY --from=build /usr/src/app/EBA/ /usr/share/nginx/html/EBA

# Override configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```



