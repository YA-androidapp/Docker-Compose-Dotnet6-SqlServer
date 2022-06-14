# https://github.com/dotnet/dotnet-docker/blob/main/samples/dotnetapp/Dockerfile

EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /source

COPY src/MyBrazorApp .
RUN dotnet restore
RUN dotnet publish -c release -o /app

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "MyBrazorApp.Server.dll"]
