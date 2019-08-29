FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Docker2/Docker2.csproj", "Docker2/"]
RUN dotnet restore "Docker2/Docker2.csproj"
COPY . .
WORKDIR "/src/Docker2"
RUN dotnet build "Docker2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Docker2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Docker2.dll"]