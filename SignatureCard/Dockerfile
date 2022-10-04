FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 8080
EXPOSE 4430

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SignatureCard/SignatureCard.csproj", "SignatureCard/"]
RUN dotnet restore "SignatureCard/SignatureCard.csproj"
COPY . .
WORKDIR "/src/SignatureCard"
RUN dotnet build "SignatureCard.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SignatureCard.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SignatureCard.dll"]
