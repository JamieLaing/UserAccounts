FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["UserAccounts/UserAccounts.csproj", "UserAccounts/"]
RUN dotnet restore "UserAccounts/UserAccounts.csproj"
COPY . .
WORKDIR "/src/UserAccounts"
RUN dotnet build "UserAccounts.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "UserAccounts.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "UserAccounts.dll"]