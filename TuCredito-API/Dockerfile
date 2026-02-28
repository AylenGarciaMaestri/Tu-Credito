# ---------- BUILD STAGE ----------
FROM mcr.microsoft.com/dotnet/sdk:10.0-noble AS build
WORKDIR /src

# Copiar el csproj y restaurar dependencias
COPY ["TuCredito.csproj", "./"]
RUN dotnet restore "TuCredito.csproj"

# Copiar el resto del código
COPY . .

# Publicar la aplicación
RUN dotnet publish "TuCredito.csproj" -c Release -o /app/publish

# ---------- RUNTIME STAGE ----------
FROM mcr.microsoft.com/dotnet/aspnet:10.0-noble AS final
WORKDIR /app

# Copiar archivos publicados
COPY --from=build /app/publish .

# Render usa la variable de entorno PORT
ENV ASPNETCORE_URLS=http://+:$PORT

# Exponer puerto (Render generalmente usa 10000 o 8080 internamente)
EXPOSE 8080

# Ejecutar la app
ENTRYPOINT ["dotnet", "TuCredito.dll"]