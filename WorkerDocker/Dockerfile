FROM mcr.microsoft.com/dotnet/core/runtime:3.0-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["WorkerDocker/WorkerDocker.csproj", "WorkerDocker/"]
RUN dotnet restore "WorkerDocker/WorkerDocker.csproj"
COPY . .
WORKDIR "/src/WorkerDocker"
RUN dotnet build "WorkerDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WorkerDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WorkerDocker.dll"]