FROM alpine/git AS GIT
RUN git clone --depth=1 https://github.com/MatheusLotRizzo/gateway /app

FROM maven:3.9.6-eclipse-temurin-17-alpine AS builder
WORKDIR /app
COPY --from=GIT  /app/pom.xml   .
COPY --from=GIT /app/src        ./src
RUN mvn clean package -DskipTests

FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app
EXPOSE 8080
 # Copie o arquivo JAR do seu projeto para dentro do contêiner
COPY --from=builder /app/target/*.jar /app/gateway.jar
# Comando para executar o projeto quando o contêiner for iniciado
CMD ["java", "-jar", "/app/gateway.jar"]