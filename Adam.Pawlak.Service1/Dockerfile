#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 81

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Adam.Pawlak.Service1/Adam.Pawlak.Service1.csproj", "Adam.Pawlak.Service1/"]
RUN dotnet restore "Adam.Pawlak.Service1/Adam.Pawlak.Service1.csproj"
COPY . .
WORKDIR "/src/Adam.Pawlak.Service1"
RUN dotnet build "Adam.Pawlak.Service1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Adam.Pawlak.Service1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Adam.Pawlak.Service1.dll"]