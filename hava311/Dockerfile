#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

#FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443
#
#FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
#ARG BUILD_CONFIGURATION=Release
#WORKDIR /src
## Set the build configuration
#ENV BUILD_CONFIGURATION=Debug
##COPY ["hava311/hava311.csproj", "hava311/"]  auto generated code fails
#COPY ["hava311.csproj", "hava311/"]
#RUN dotnet restore "./hava311/hava311.csproj"
#
#WORKDIR "/src/hava311"
#COPY . .
#
#RUN dotnet restore
#RUN ls -la # hata ayiklama 
#RUN dotnet build "./hava311.csproj" -c $BUILD_CONFIGURATION -o /app/build
## ...
#
#
#FROM build AS publish
#ARG BUILD_CONFIGURATION=Release
#RUN dotnet publish "./hava311.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "hava311.dll"]



#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
# Set the build configuration
ENV BUILD_CONFIGURATION=Release

#COPY ["hava311/hava311.csproj", "hava311/"]  auto generated code fails
COPY ["hava311.csproj", "hava311/"]
RUN dotnet restore "./hava311/hava311.csproj"

WORKDIR "/src/hava311"
COPY . .

RUN ls -la # hata ayiklama 
RUN dotnet build "./hava311.csproj" -c $BUILD_CONFIGURATION -o /app/build
# ...


FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./hava311.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "hava311.dll"]
