FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AppWithDocker/AppWithDocker.csproj", "AppWithDocker/"]
RUN dotnet restore "AppWithDocker/AppWithDocker.csproj"
COPY . .
WORKDIR "/src/AppWithDocker"
RUN dotnet build "AppWithDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AppWithDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AppWithDocker.dll"]