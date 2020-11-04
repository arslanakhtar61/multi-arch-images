FROM golang:1.15 AS builder
ARG VERSION=v1.3.0
ARG TARGETPLATFORM
WORKDIR /go/src/github.com/kubernetes-csi/node-driver-registrar/
RUN git clone --depth 1 -b "${VERSION}" https://github.com/kubernetes-csi/node-driver-registrar.git . \
     && GOARCH=$(echo $TARGETPLATFORM | cut -f2 -d '/') make build

FROM gcr.io/distroless/static@sha256:a7fbf4bc518870042021d9fff54b486da3c3182f880b52f91439d63895ec8423
WORKDIR /
COPY --from=builder /go/src/github.com/kubernetes-csi/node-driver-registrar/bin/csi-node-driver-registrar csi-node-driver-registrar
ENTRYPOINT ["/csi-node-driver-registrar"]