ARG GO_VERSION="1.18.5"
ARG ALPINE_VERSION="3.16"

FROM golang:${GO_VERSION}-alpine${ALPINE_VERSION} as go_host
ARG PROTOC_GEN_GO_VERSION="v1.28.1"
ARG PROTOC_GEN_GO_GRPC_VERSION="v1.2.0"
ARG PROTOC_GEN_GO_HTTP_VERSION="v2.0.0-20220728114350-eff368621fb3"
ARG PROTOC_GEN_OPENAPI_VERSION="v0.6.9"
ARG PROTOC_GEN_GO_ERRORS_VERSION="v2.0.0-20220728114350-eff368621fb3"
ARG PROTOC_GEN_DOC_VERSION="v1.5.1"
ENV GOPROXY=https://goproxy.cn
RUN mkdir -p /out
RUN go install -ldflags="-s -w" google.golang.org/protobuf/cmd/protoc-gen-go@${PROTOC_GEN_GO_VERSION}
RUN	go install -ldflags="-s -w" google.golang.org/grpc/cmd/protoc-gen-go-grpc@${PROTOC_GEN_GO_GRPC_VERSION}
RUN	go install -ldflags="-s -w" github.com/go-kratos/kratos/cmd/protoc-gen-go-http/v2@${PROTOC_GEN_GO_HTTP_VERSION}
RUN	go install -ldflags="-s -w" github.com/google/gnostic/cmd/protoc-gen-openapi@${PROTOC_GEN_OPENAPI_VERSION}
RUN	go install -ldflags="-s -w" github.com/go-kratos/kratos/cmd/protoc-gen-go-errors/v2@${PROTOC_GEN_GO_ERRORS_VERSION}
RUN	go install -ldflags="-s -w" github.com/pseudomuto/protoc-gen-doc/cmd/protoc-gen-doc@${PROTOC_GEN_DOC_VERSION}
RUN mv ${GOPATH}/bin/protoc-gen* /out

FROM alpine:${ALPINE_VERSION}
COPY --from=go_host /out/ /out
ENV PATH=${PATH}:/out
RUN sed -i "s/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g" /etc/apk/repositories && \
    apk update --no-cache && apk add --no-cache protoc
ENTRYPOINT [ "protoc" ]
