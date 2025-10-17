# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY ["HelloWorldApp.web.csproj", "./"]
RUN dotnet restore "HelloWorldApp.web.csproj"

# Copy the rest of the code and build
COPY . ./
RUN dotnet build "HelloWorldApp.web.csproj" -c Release -o /app/build

# Stage 2: Publish
FROM build AS publish
RUN dotnet publish "HelloWorldApp.web.csproj" -c Release -o /app/publish

# Stage 3: Final runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

# Copy published files from previous stage
COPY --from=publish /app/publish .

# Expose port (adjust if needed)
EXPOSE 80

# Set entrypoint
ENTRYPOINT ["dotnet", "HelloWorldApp.web.dll"]
