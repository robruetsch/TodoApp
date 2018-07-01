FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY TodoClient/TodoClient.csproj TodoClient/
RUN dotnet restore TodoClient/TodoClient.csproj
COPY . .
WORKDIR /src/TodoClient
RUN dotnet build TodoClient.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish TodoClient.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TodoClient.dll"]
