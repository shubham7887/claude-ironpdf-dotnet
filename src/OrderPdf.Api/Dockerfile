# See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

# This stage is used when running from VS in fast mode (Default for Debug configuration)
FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081


# This stage is used to build the service project
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["src/OrderPdf.Api/OrderPdf.Api.csproj", "src/OrderPdf.Api/"]
COPY ["src/OrderPdf.Application/OrderPdf.Application.csproj", "src/OrderPdf.Application/"]
COPY ["src/OrderPdf.Domain/OrderPdf.Domain.csproj", "src/OrderPdf.Domain/"]
COPY ["src/OrderPdf.Infrastructure/OrderPdf.Infrastructure.csproj", "src/OrderPdf.Infrastructure/"]
RUN dotnet restore "./src/OrderPdf.Api/OrderPdf.Api.csproj"
COPY . .
WORKDIR "/src/src/OrderPdf.Api"
RUN dotnet build "./OrderPdf.Api.csproj" -c $BUILD_CONFIGURATION -o /app/build

# This stage is used to publish the service project to be copied to the final stage
FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./OrderPdf.Api.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

# This stage is used in production or when running from VS in regular mode (Default when not using the Debug configuration)
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OrderPdf.Api.dll"]