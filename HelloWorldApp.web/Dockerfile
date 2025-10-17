# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy project file and restore
COPY ["HelloWorldApp.web/HelloWorldApp.web.csproj", "./"]
RUN dotnet restore "HelloWorldApp.web.csproj"

# Copy everything else
COPY ./HelloWorldApp.web ./
RUN dotnet build "HelloWorldApp.web.csproj" -c Release -o /app/build

# Stage 2: Publish
FROM build AS publish
RUN dotnet publish "HelloWorldApp.web.csproj" -c Release -o /app/publish

# Stage 3: Final image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloWorldApp.web.dll"]
