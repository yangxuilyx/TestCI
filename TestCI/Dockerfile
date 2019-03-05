FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["TestCI/TestCI.csproj", "TestCI/"]
RUN dotnet restore "TestCI/TestCI.csproj"
COPY . .
WORKDIR "/src/TestCI"
RUN dotnet build "TestCI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TestCI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestCI.dll"]