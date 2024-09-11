FROM mcr.microsoft.com/dotnet/sdk:8.0.401-alpine3.20-amd64 AS build-env
USER root
WORKDIR /app
COPY *.csproj .
RUN dotnet restore
COPY . ./
# Publish as a self-contained application for Alpine Linux (musl)
RUN dotnet publish -c Release -r linux-musl-x64 --self-contained true -o out
FROM mcr.microsoft.com/dotnet/runtime-deps:8.0.8-alpine3.20-amd64
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["./Api"]




