FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["sampleapplicationforaks/sampleapplicationforaks.csproj", "sampleapplicationforaks/"]
RUN dotnet restore "sampleapplicationforaks/sampleapplicationforaks.csproj"
COPY . .
WORKDIR "/src/sampleapplicationforaks"
RUN dotnet build "sampleapplicationforaks.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "sampleapplicationforaks.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "sampleapplicationforaks.dll"]