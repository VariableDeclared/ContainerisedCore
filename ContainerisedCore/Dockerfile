FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["ContainerisedCore/ContainerisedCore.csproj", "ContainerisedCore/"]
RUN dotnet restore "ContainerisedCore/ContainerisedCore.csproj"
COPY . .
WORKDIR "/src/ContainerisedCore"
RUN dotnet build "ContainerisedCore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ContainerisedCore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ContainerisedCore.dll"]