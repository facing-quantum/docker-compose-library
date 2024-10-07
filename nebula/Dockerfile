# Build Stage
FROM alpine:latest AS build

ARG BUILDOS
ARG BUILDARCH

ADD https://github.com/slackhq/nebula/releases/latest/download/nebula-$BUILDOS-$BUILDARCH.tar.gz /
RUN tar -zxf /nebula-$BUILDOS-$BUILDARCH.tar.gz

# Final Stage
FROM gcr.io/distroless/static:latest

COPY --from=build /nebula /nebula-cert /

VOLUME ["/config"]

ENTRYPOINT ["/nebula"]
# Allow users to override the args passed to nebula
CMD ["-config", "/config/config.yml"]