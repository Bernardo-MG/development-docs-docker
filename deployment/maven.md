# Tomcat

```text
FROM tomcat:8 as deployment

# Copy from build stage
COPY --from=build /usr/src/app/target/project.war /usr/local/tomcat/webapps/

EXPOSE 8080
```

