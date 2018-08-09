FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 61577
EXPOSE 44372

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY demoForRob/demoForRob.csproj demoForRob/
RUN dotnet restore demoForRob/demoForRob.csproj
COPY . .
WORKDIR /src/demoForRob
RUN dotnet build demoForRob.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish demoForRob.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "demoForRob.dll"]
