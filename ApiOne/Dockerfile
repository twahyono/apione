FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["ApiOne/ApiOne.csproj", "ApiOne/"]
RUN dotnet restore "ApiOne/ApiOne.csproj"
COPY . .
WORKDIR "/src/ApiOne"
RUN dotnet build "ApiOne.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ApiOne.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ApiOne.dll"]