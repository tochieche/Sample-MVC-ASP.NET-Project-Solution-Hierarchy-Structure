FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY TochiCryptoCurrency.API/TochiCryptoCurrency.API.csproj TochiCryptoCurrency.API/
RUN dotnet restore TochiCryptoCurrency.API/TochiCryptoCurrency.API.csproj
COPY . .
WORKDIR /src/TochiCryptoCurrency.API
RUN dotnet build TochiCryptoCurrency.API.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish TochiCryptoCurrency.API.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TochiCryptoCurrency.API.dll"]
