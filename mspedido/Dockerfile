FROM alpine/git AS GIT
RUN git clone --depth=1 https://github.com/westrindade/mspedido.git /app
WORKDIR /app

FROM maven:3.8.4 AS builder
WORKDIR /app
COPY --from=GIT  /app/pom.xml   .
COPY --from=GIT /app/src        ./src
COPY --from=GIT /app/libs       ./libs
RUN mvn clean package -DskipTests

FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app
EXPOSE 8084
 # Copie o arquivo JAR do seu projeto para dentro do contêiner
COPY --from=builder /app/target/*.jar /app/mspedidos.jar 
# Comando para executar o projeto quando o contêiner for iniciado
CMD ["java", "-jar", "/app/mspedidos.jar"]