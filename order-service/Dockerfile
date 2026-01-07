FROM eclipse-temurin:17-jre-jammy

WORKDIR /app

COPY target/order-service-1.0.jar app.jar

EXPOSE 8082

ENTRYPOINT ["java","-jar","/app/app.jar"]
