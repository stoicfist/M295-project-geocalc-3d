# Build-Stage
FROM eclipse-temurin:21-jdk AS build
WORKDIR /app

# Kopiere nur was notwendig ist
COPY .mvn .mvn
COPY mvnw pom.xml ./
COPY src src

# Rechte setzen & bauen
RUN chmod +x mvnw
RUN ./mvnw clean package -DskipTests

# Runtime-Stage
FROM eclipse-temurin:21-jdk
COPY --from=build /app/target/*.jar /app/app.jar

# Startbefehl
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
EXPOSE 8080