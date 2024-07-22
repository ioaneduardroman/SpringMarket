FROM maven:3.9.6 AS build
WORKDIR /build
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src

RUN mvn clean package -DskipTests

#Runtime stageW
FROM amazoncorretto:21

WORKDIR /app
COPY --from=build /build/target/springmarket-*.jar /app/

EXPOSE 8082

ENV DB_URL=jdbc:mysql://springmarket-mysql:3306/springmarket
ENV JAR_VERSION=1.0.0

CMD java -jar -Dspring.datasource.url=${DB_URL} springmarket-${JAR_VERSION}.jar

