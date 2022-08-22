

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app



FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build

WORKDIR /src
COPY ["jenkinsTest/jenkinsTest.csproj", "jenkinsTest/"]
RUN dotnet restore "jenkinsTest/jenkinsTest.csproj"


COPY . .
WORKDIR "/src/jenkinsTest"
RUN dotnet build "jenkinsTest.csproj" -c Release -o /app/build --no-restore

FROM build AS publish
RUN dotnet publish "jenkinsTest.csproj" -c Release -o /app/publish --no-restore

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "jenkinsTest.dll"]
