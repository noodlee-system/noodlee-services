# STEP 1 - BUILD JAVA APPLICATION USING MAVEN
FROM maven:3.6.0-jdk-11-slim AS builder

WORKDIR /home/app/

COPY ./pom.xml ./pom.xml

RUN mvn dependency:go-offline -B 

COPY ./src ./src

RUN mvn package -DskipTests=true

# STEP 2 - SERVE JAVA APPLICATION
FROM java:8

COPY --from=builder /home/app/target/eureka-1.0.jar /usr/local/lib/eureka-server.jar

EXPOSE 8761

ENTRYPOINT [ "java", "-jar", "/usr/local/lib/eureka-server.jar" ]
