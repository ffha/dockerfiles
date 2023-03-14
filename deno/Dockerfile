FROM rust AS build
RUN cargo install deno --locked

FROM debian:stable-slim
RUN apt-get update && apt-get install -y extra-runtime-dependencies && rm -rf /var/lib/apt/lists/*
COPY --from=build /usr/local/cargo/bin/deno /usr/local/bin/deno
