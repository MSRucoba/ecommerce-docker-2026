FROM eclipse-temurin:17-jdk-jammy
# configuración de la aplicación
ENV APP_HOME=/ecommerce-app
RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME

# puerto a exponer
EXPOSE 8084

# copiar el JAR (nombre fijo de la versión)
COPY target/ecommerce-*.jar app.jar

# usuario no-root paea seguridad

RUN useradd -m appuser && chown -R appuser:appuser $APP_HOME
USER appuser

# salud del sistema interno
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http:\\localhost:8084/actuator/healh || exit 1

# comando de ejecución
ENTRYPOINT ["java", "-jar", "app.jar"]
