#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["Services/Basket/Basket.WebAPI/Basket.WebAPI.csproj", "Services/Basket/Basket.WebAPI/"]
RUN dotnet restore "Services/Basket/Basket.WebAPI/Basket.WebAPI.csproj"
COPY . .
WORKDIR "/src/Services/Basket/Basket.WebAPI"
RUN dotnet build "Basket.WebAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Basket.WebAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Basket.WebAPI.dll"]
