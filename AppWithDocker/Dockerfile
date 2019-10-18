FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY . .
RUN dotnet restore "AppWithDocker.csproj"

RUN dotnet build "AppWithDocker.csproj" -c Debug -o /app

FROM build AS publish
RUN dotnet publish "AppWithDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AppWithDocker.dll"]