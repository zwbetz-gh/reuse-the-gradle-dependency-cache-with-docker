# Reuse the Gradle Dependency Cache With Docker

## Sister Link

TODO

## Setup

1. Install Docker
1. Pull the Gradle image
    ```
    docker pull gradle:7.0.2-jdk11-hotspot
    ```

## Regular

Dependencies are downloaded each time.

```
docker build --no-cache -f Dockerfile-app -t app .
```

## With Dependency Cache

Build the dependency cache.

```
docker build --no-cache -f Dockerfile-dependency-cache -t dependency-cache .
```

Now the dependency download is skipped.

```
docker build --no-cache -f Dockerfile-app-cached -t app-cached .
```
