#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src        #Dockerfile dizini
COPY ["*/hava311.csproj", "./hava311/"]
RUN dotnet restore "./hava311/hava311.csproj"
COPY . .
WORKDIR "/src/hava311"
RUN dotnet build "./hava311.csproj" -c $BUILD_CONFIGURATION -o /app/build


FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./hava311.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "hava311.dll"]