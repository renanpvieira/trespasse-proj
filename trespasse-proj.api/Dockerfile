# Etapa 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copiar arquivos de projeto e restaurar dependências
COPY *.csproj ./
RUN dotnet restore

# Copiar código-fonte e compilar a aplicação
COPY . ./
RUN dotnet publish -c Release -o /out

# Etapa 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Copiar binários da etapa anterior
COPY --from=build /out ./

# Expor a porta 8080 (Render usa essa porta)
ENV ASPNETCORE_URLS=http://+:8080
EXPOSE 8080

# Comando de entrada
CMD ["dotnet", "trespasse-proj.api.dll"]