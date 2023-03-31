FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["FakeAppsFlyer/FakeAppsFlyer.csproj", "FakeAppsFlyer/"]
RUN dotnet restore "FakeAppsFlyer/FakeAppsFlyer.csproj"
COPY . .
WORKDIR "/src/FakeAppsFlyer"
RUN dotnet build "FakeAppsFlyer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FakeAppsFlyer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FakeAppsFlyer.dll"]
