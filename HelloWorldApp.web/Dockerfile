# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy only the project file and restore dependencies
COPY ["HelloWorldApp.web.csproj", "./"]
RUN dotnet restore "HelloWorldApp.web.csproj"

# Copy everything else
COPY . ./
RUN dotnet build "HelloWorldApp.web.csproj" -c Release -o /app/build

# Publish stage
FROM build AS publish
RUN dotnet publish "HelloWorldApp.web.csproj" -c Release -o /app/publish

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloWorldApp.web.dll"]
