FROM maven:3.9.6-eclipse-temurin-21 AS cache
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn dependency:go-offline

FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app
COPY --from=cache /root/.m2 /root/.m2
COPY . .
RUN mvn package

FROM maven:3.9.6-eclipse-temurin-21
WORKDIR	/app
COPY --from=build /app/target/*.jar /app/app.jar
CMD ["java", "-jar", "app.jar"]
