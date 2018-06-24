FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY karaoke-server/karaoke-server.csproj karaoke-server/
RUN dotnet restore karaoke-server/karaoke-server.csproj
COPY . .
WORKDIR /src/karaoke-server
RUN dotnet build karaoke-server.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish karaoke-server.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "karaoke-server.dll"]
