#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["Net.Web.Docker.Api/Net.Web.Docker.Api.csproj", "Net.Web.Docker.Api/"]
RUN dotnet restore "Net.Web.Docker.Api/Net.Web.Docker.Api.csproj"
COPY . .
WORKDIR "/src/Net.Web.Docker.Api"
RUN dotnet build "Net.Web.Docker.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Net.Web.Docker.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Net.Web.Docker.Api.dll"]
