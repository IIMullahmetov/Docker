FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY Docker.Linux/Docker.Linux.csproj Docker.Linux/
RUN dotnet restore Docker.Linux/Docker.Linux.csproj
COPY . .
WORKDIR /src/Docker.Linux
RUN dotnet build Docker.Linux.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Docker.Linux.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Docker.Linux.dll"]
