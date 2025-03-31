# Etapa 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copia o projeto e restaura pacotes
COPY trespasse-proj.api/*.csproj ./ 
RUN dotnet restore

# Copia todo o código e compila a aplicação
COPY trespasse-proj.api/. ./ 
WORKDIR /src/trespasse-proj.api
RUN dotnet publish -c Release -o /out

# Etapa 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

COPY --from=build /out ./
ENV ASPNETCORE_URLS=http://+:8080
EXPOSE 8080

CMD ["dotnet", "trespasse-proj.api.dll"]