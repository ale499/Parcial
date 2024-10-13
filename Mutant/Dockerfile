FROM alpine:latest as build

RUN apk update
RUN apk add openjdk17

# Establece el directorio de trabajo
WORKDIR /app

# Copia los archivos necesarios
COPY gradlew /app/
COPY build.gradle settings.gradle /app/
COPY src /app/src

COPY . .
RUN chmod +x ./gradlew
RUN ./gradlew bootJar --no-daemon

FROM openjdk:17-alpine
EXPOSE 9000
COPY --from=build ./build/libs/Mutant-0.0.1-SNAPSHOT.jar ./app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]