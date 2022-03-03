FROM openjdk:17 AS BUILD_IMAGE
ENV APP_HOME=/root/dev/PasswordChar
RUN mkdir -p $APP_HOME/src/main/java
WORKDIR $APP_HOME
COPY build.gradle gradlew gradlew.bat settings.gradle $APP_HOME
COPY gradle $APP_HOME/gradle
# download dependencies
RUN ./gradlew build -x test --continue
#RUN ./gradlew build -x :bootRepackage --continue
COPY . .
RUN ./gradlew build

FROM openjdk:17
LABEL  srai.micro.service="password-char-service" srai.micro.project="true"
WORKDIR /root/
COPY --from=BUILD_IMAGE /root/dev/PasswordChar/build/libs/PasswordChar-0.0.1-SNAPSHOT.jar .
EXPOSE 8080
CMD ["java","-jar","PasswordChar-0.0.1-SNAPSHOT.jar"]