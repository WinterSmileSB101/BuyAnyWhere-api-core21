FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 56968
EXPOSE 44386

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY BuyAnyWhere-api-core21/BuyAnyWhere-api-core21.csproj BuyAnyWhere-api-core21/
RUN dotnet restore BuyAnyWhere-api-core21/BuyAnyWhere-api-core21.csproj
COPY . .
WORKDIR /src/BuyAnyWhere-api-core21
RUN dotnet build BuyAnyWhere-api-core21.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish BuyAnyWhere-api-core21.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BuyAnyWhere-api-core21.dll"]
