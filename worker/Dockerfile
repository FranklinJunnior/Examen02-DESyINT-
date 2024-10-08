# Usa una imagen base de .NET SDK 7.0 para compilar la aplicación
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /source

# Copia el archivo de proyecto y restaura las dependencias
COPY *.csproj .
RUN dotnet restore

# Copia el resto del código de la aplicación y compila
COPY . .
RUN dotnet publish -c release -o /app --self-contained false

# Imagen de la aplicación
FROM mcr.microsoft.com/dotnet/runtime:7.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Worker.dll"]