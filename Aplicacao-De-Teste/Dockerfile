#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Aplicacao-De-Teste/Aplicacao-De-Teste.csproj", "Aplicacao-De-Teste/"]
RUN dotnet restore "Aplicacao-De-Teste/Aplicacao-De-Teste.csproj"
COPY . .
WORKDIR "/src/Aplicacao-De-Teste"
RUN dotnet build "Aplicacao-De-Teste.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Aplicacao-De-Teste.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Aplicacao-De-Teste.dll"]