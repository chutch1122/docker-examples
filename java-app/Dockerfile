# Step 1: Build the application
FROM gradle:jdk8 as builder

USER root
ENV GRADLE_USER_HOME ~/.gradle

WORKDIR /home/gradle/project

COPY build.gradle /home/gradle/project

RUN gradle downloadDependencies

COPY . .

RUN gradle assemble

# Step 2: Build the final image
FROM openjdk:8-jdk-alpine

COPY --from=builder /home/gradle/project/build/libs/demo-0.0.1-SNAPSHOT.jar /app/app.jar

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app/app.jar"]

EXPOSE 8080
