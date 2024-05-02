#Download maven cache
FROM maven:3.8.4-jdk-11-slim AS cache
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn dependency:go-offline

#Build the app using downloaded cache
FROM maven:3.8.4-jdk-11-slim AS build
WORKDIR /app
COPY --from=cache /root/.m2 /root/.m2
COPY . .
RUN mvn package

#Final: create a light runtime image
FROM openjdk:11-jre-slim
WORKDIR	/app
COPY --from=build /app/target/*.jar /app/app.jar
CMD ["java", "-jar", "app.jar"]

