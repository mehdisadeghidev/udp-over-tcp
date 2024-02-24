FROM rust:1.75-slim as builder

ENV RUSTFLAGS="-C target-feature=+crt-static"

WORKDIR /src

COPY . .

RUN cargo build --release \
    --target x86_64-unknown-linux-gnu \
    --features env_logger \
    --features clap \
    --features statsd \
    --bins

FROM alpine:3.17 AS runtime

COPY --from=builder /src/target/x86_64-unknown-linux-gnu/release/tcp2udp /usr/local/bin
COPY --from=builder /src/target/x86_64-unknown-linux-gnu/release/udp2tcp /usr/local/bin
