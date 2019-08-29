FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Docker1/Docker1.csproj", "Docker1/"]
RUN dotnet restore "Docker1/Docker1.csproj"
COPY . .
WORKDIR "/src/Docker1"
RUN dotnet build "Docker1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Docker1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Docker1.dll"]