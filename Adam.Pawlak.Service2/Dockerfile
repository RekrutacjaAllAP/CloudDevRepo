FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-nanoserver-1903 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-nanoserver-1903 AS build
WORKDIR /src
COPY ["Adam.Pawlak.Service2/Adam.Pawlak.Service2.csproj", "Adam.Pawlak.Service2/"]
RUN dotnet restore "Adam.Pawlak.Service2/Adam.Pawlak.Service2.csproj"
COPY . .
WORKDIR "/src/Adam.Pawlak.Service2"
RUN dotnet build "Adam.Pawlak.Service2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Adam.Pawlak.Service2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Adam.Pawlak.Service2.dll"]