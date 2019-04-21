FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MySample/MySample.csproj", "MySample/"]
RUN dotnet restore "MySample/MySample.csproj"
COPY . .
WORKDIR "/src/MySample"
RUN dotnet build "MySample.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MySample.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MySample.dll"]