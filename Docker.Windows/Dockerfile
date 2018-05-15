FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 50626
EXPOSE 44336

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY Docker.Windows/Docker.Windows.csproj Docker.Windows/
RUN dotnet restore Docker.Windows/Docker.Windows.csproj
COPY . .
WORKDIR /src/Docker.Windows
RUN dotnet build Docker.Windows.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Docker.Windows.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Docker.Windows.dll"]
