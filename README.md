# Reuse the Gradle Dependency Cache With Docker

## Sister Links

- Article: <https://zwbetz.com/reuse-the-gradle-dependency-cache-with-docker/>

## Setup

1. Install Docker
1. Pull the Gradle image
    ```
    docker pull gradle:7.0.2-jdk11-hotspot
    ```

## Regular Build

1. Build the app. The dependencies are downloaded each time
    ```
    docker build --no-cache -f Dockerfile-app -t app .
    ```

## Build With Dependency Cache

1. Build the dependency cache
    ```
    docker build --no-cache -f Dockerfile-dependency-cache -t dependency-cache .
    ```
1. Run a temp container
    ```
    docker run -it --rm dependency-cache bash
    ```
1. List the dependency cache
    ```
    ls -al ${HOME}/.gradle/caches/modules-2/files-2.1/
    ```
1. Exit the temp container
    ```
    exit
    ```
1. Build the app. Now the dependency download is skipped and the cache is used
    ```
    docker build --no-cache -f Dockerfile-app-cached -t app-cached .
    ```
