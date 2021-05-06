FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["re-server/re_server.csproj", "re-server/"]

RUN dotnet restore "re-server/re_server.csproj"
COPY . .
WORKDIR "/src/re-server"
RUN dotnet build "re_server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "re_server.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "re_server.dll"]