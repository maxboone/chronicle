FROM oven/bun AS build

WORKDIR /app
COPY . /app
RUN bun i
RUN bun vite build

# Final Image
FROM oven/bun

RUN useradd -ms /bin/sh -u 1001 app
COPY --from=build --chown=app:app /app/build /app

USER app
WORKDIR /app

CMD ["bun", "run", "start"]
