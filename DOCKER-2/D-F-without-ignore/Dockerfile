FROM openjdk:17-jdk-slim

# Build argument
ARG APP_VERSION=latest

RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

WORKDIR /app

RUN git clone https://github.com/spring-projects/spring-petclinic.git .

RUN ./mvnw clean package -DskipTests

# Environment variable
ENV SPRING_PROFILES_ACTIVE=production

EXPOSE 8080

CMD ["sh", "-c", "java -jar target/*.jar"]