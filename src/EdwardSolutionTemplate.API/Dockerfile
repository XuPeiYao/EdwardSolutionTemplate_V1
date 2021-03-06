#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["EdwardSolutionTemplate.API/EdwardSolutionTemplate.API.csproj", "EdwardSolutionTemplate.API/"]
COPY ["EdwardSolutionTemplate.Domain/EdwardSolutionTemplate.Domain.csproj", "EdwardSolutionTemplate.Domain/"]
COPY ["EdwardSolutionTemplate.Extensions/EdwardSolutionTemplate.Extensions.csproj", "EdwardSolutionTemplate.Extensions/"]
COPY ["EdwardSolutionTemplate.Utilities/EdwardSolutionTemplate.Utilities.csproj", "EdwardSolutionTemplate.Utilities/"]
COPY ["EdwardSolutionTemplate.Accesses.EF/EdwardSolutionTemplate.Accesses.EF.csproj", "EdwardSolutionTemplate.Accesses.EF/"]
RUN dotnet restore "EdwardSolutionTemplate.API/EdwardSolutionTemplate.API.csproj"
COPY . .
WORKDIR "/src/EdwardSolutionTemplate.API"
RUN dotnet build "EdwardSolutionTemplate.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EdwardSolutionTemplate.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EdwardSolutionTemplate.API.dll"]
