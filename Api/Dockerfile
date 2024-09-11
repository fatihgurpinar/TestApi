FROM mcr.microsoft.com/dotnet/sdk:8.0.401-1-alpine3.20-amd64 AS build-env

USER root

WORKDIR /app


COPY *.csproj .

RUN dotnet restore

COPY . ./

RUN dotnet publish --no-restore -c Release -o out

FROM mcr.microsoft.com/dotnet/runtime:8.0.8-jammy-chiseled-arm64v8
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "Api.dll"]

