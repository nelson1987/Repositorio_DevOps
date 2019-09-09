FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Escola.Api/Escola.Api.csproj", "Escola.Api/"]
RUN dotnet restore "Escola.Api/Escola.Api.csproj"
COPY . .
WORKDIR "/src/Escola.Api"
RUN dotnet build "Escola.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Escola.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Escola.Api.dll"]