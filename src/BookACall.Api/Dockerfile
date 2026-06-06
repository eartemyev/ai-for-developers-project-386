FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

COPY ["src/BookACall.Api/BookACall.Api.csproj", "src/BookACall.Api/"]
RUN dotnet restore "src/BookACall.Api/BookACall.Api.csproj"

COPY . .
RUN dotnet publish "src/BookACall.Api/BookACall.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS final
WORKDIR /app

ENV ASPNETCORE_URLS=http://+:8080
EXPOSE 8080

COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "BookACall.Api.dll"]
