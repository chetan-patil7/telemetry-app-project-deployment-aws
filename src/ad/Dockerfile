FROM eclipse-temurin:21-jdk AS build

WORKDIR /usr/src/app
#Copying gradle related so that we are not needed to install gradle again

COPY gradlew* settings.gradle* build.gradle .
COPY ./gradle ./gradle
#it will run the gradle daemon server

RUN chmod +x ./gradlew
RUN ./gradlew
RUN ./gradlew downloadRepos

COPY . .

COPY ./pb ./proto
RUN chmod +x ./gradlew
RUN ./gradlew installDist -PprotoSourceDir=./proto

##########################################################

FROM eclipse-temurin:21-jre

WORKDIR /usr/src/app

COPY --from=build /usr/src/app ./

ENV AD_PORT 9099

ENTRYPOINT ["./build/install/opentelemetry-demo-ad/bin/Ad"]
