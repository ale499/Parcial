# Usa una imagen base de Gradle con JDK 17
FROM gradle:7.3.3-jdk17 AS build

# Establece el directorio de trabajo
WORKDIR /app

# Copia los archivos de construcción y el código fuente
COPY build.gradle settings.gradle /app/
COPY src /app/src

# Construye el proyecto
RUN gradle build --no-daemon

# Usa una imagen base de JDK 17 para ejecutar la aplicación
FROM openjdk:17-jre-slim

# Establece el directorio de trabajo
WORKDIR /app

# Copia el archivo JAR generado desde la etapa de construcción
COPY --from=build /app/build/libs/*.jar app.jar

# Expone el puerto en el que la aplicación se ejecutará
EXPOSE 8080

# Comando para ejecutar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]