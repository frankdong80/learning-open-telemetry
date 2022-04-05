FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["learning-open-telemetry/learning-open-telemetry.csproj", "learning-open-telemetry/"]
RUN dotnet restore "learning-open-telemetry/learning-open-telemetry.csproj"
COPY . .
WORKDIR "/src/learning-open-telemetry"
RUN dotnet build "learning-open-telemetry.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "learning-open-telemetry.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "learning-open-telemetry.dll"]
