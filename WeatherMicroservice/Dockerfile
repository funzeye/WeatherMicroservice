FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY WeatherMicroservice/WeatherMicroservice.csproj WeatherMicroservice/
RUN dotnet restore WeatherMicroservice/WeatherMicroservice.csproj
COPY . .
WORKDIR /src/WeatherMicroservice
RUN dotnet build WeatherMicroservice.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WeatherMicroservice.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WeatherMicroservice.dll"]
