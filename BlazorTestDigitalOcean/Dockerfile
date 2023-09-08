#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BlazorTestDigitalOcean/BlazorTestDigitalOcean.csproj", "BlazorTestDigitalOcean/"]
RUN dotnet restore "BlazorTestDigitalOcean/BlazorTestDigitalOcean.csproj"
COPY . .
WORKDIR "/src/BlazorTestDigitalOcean"
RUN dotnet build "BlazorTestDigitalOcean.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorTestDigitalOcean.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorTestDigitalOcean.dll"]