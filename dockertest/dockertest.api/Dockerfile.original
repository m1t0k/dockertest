FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY dockertest.api/dockertest.api.csproj dockertest.api/
RUN dotnet restore dockertest.api/dockertest.api.csproj
COPY . .
WORKDIR /src/dockertest.api
RUN dotnet build dockertest.api.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish dockertest.api.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "dockertest.api.dll"]
