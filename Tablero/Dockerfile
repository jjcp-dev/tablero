# ==========================================================
# Release Build

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS release-build
WORKDIR /app
COPY . .
RUN dotnet publish -c Release -o out


# ==========================================================
# Release

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS release
WORKDIR /app
COPY --from=release-build /app/out ./
ENTRYPOINT ["./Tablero"]


# ==========================================================
# Local

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS local
WORKDIR /app

RUN apt-get update \
    && apt-get install -y --no-install-recommends unzip \
    && rm -rf /var/lib/apt/lists/* \
    && curl -sSL https://aka.ms/getvsdbgsh | bash /dev/stdin -v latest -l /vsdbg

# Mount the source code in `/app`
ENTRYPOINT ["dotnet", "watch", "run"]
