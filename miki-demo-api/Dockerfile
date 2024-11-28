# Use the .NET SDK image to compile the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS compile

# Set the working directory
WORKDIR /app

# Copy the project file and restore dependencies
COPY ["./miki-demo-api.csproj", "/app"]
RUN dotnet restore "./miki-demo-api.csproj"

# Copy the rest of the application and build it
COPY . /app
RUN dotnet publish "./miki-demo-api.csproj" -c Release -o /app/publish

# Use the ASP.NET image for the runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final

# Set the working directory for the final image
WORKDIR /app

# Copy the published application files from the compile stage
COPY --from=compile /app/publish /app

# Define the command to run the application
ENTRYPOINT ["dotnet", "miki-demo-api.dll"]
