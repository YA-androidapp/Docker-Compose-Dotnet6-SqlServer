# Docker-Compose-Dotnet6-SqlServer

---

on Mac

## Run the MS SQL Server

```bash
docker-compose up -d --build
```

## Run the dotnet container to build

### 1. ソリューションを作成

```bash
cd app/src
dotnet new blazorwasm --hosted -o MyBrazorApp
cd ../..
```

### 2-1. マルチステージビルドする場合

```bash
docker build -t mydotnetapp -f app/Dockerfile app/
docker run --rm -p 80:80 mydotnetapp
```

### 2-2. ビルド結果のバイナリをホストマシンに持ってくる場合

```bash
docker pull mcr.microsoft.com/dotnet/sdk:6.0


# for running on Mac
# docker run --rm -v $(pwd)/app/out:/out -v $(pwd)/app/src/MyBrazorApp:/app -w /app mcr.microsoft.com/dotnet/sdk:6.0 dotnet publish -c release -o /out -r osx-x64 --self-contained false

# for running in the aspnet container
docker run --rm -v $(pwd)/app/out:/out -v $(pwd)/app/src/MyBrazorApp:/app -w /app mcr.microsoft.com/dotnet/sdk:6.0 dotnet publish -c release -o /out


docker run --rm -v $(pwd)/app/out:/app -p 80:80 -w /app mcr.microsoft.com/dotnet/aspnet:6.0 dotnet MyBrazorApp.Server.dll
```

## 動作確認

- [localhost:80](http://localhost:80/)

---

Copyright (c) 2022 YA-androidapp(<https://github.com/YA-androidapp>) All rights reserved.
