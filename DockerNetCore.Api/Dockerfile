FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY *.sln ./
COPY DockerNetCore.Api/DockerNetCore.Api.csproj DockerNetCore.Api/
RUN dotnet restore
COPY . .
WORKDIR /src/DockerNetCore.Api
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerNetCore.Api.dll"]
