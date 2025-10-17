# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy only the project file and restore dependencies
COPY ["HelloWebApp.csproj", "./"]
RUN dotnet restore "HelloWebApp.csproj"

# Copy the rest of the source code
COPY . .
RUN dotnet build "HelloWebApp.csproj" -c Release -o /app/build

# Stage 2: Publish
FROM build AS publish
RUN dotnet publish "HelloWebApp.csproj" -c Release -o /app/publish

# Stage 3: Final image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
EXPOSE 80
EXPOSE 443

# Copy published files from publish stage
COPY --from=publish /app/publish .

# Set entrypoint
ENTRYPOINT ["dotnet", "HelloWebApp.dll"]
