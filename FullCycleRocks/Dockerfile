# Imagem base
FROM golang:alpine as builder

# Define variável de ambiente
ENV GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64

# Diretório de trabalho
WORKDIR /build

# Copia arquivos para dentro do contêiner
COPY go.mod .
COPY go.sum .

RUN go mod download

COPY . .

# Build do binário
RUN go build -o main .

# Segunda etapa
FROM scratch

# Copia o binário construído na primeira etapa
COPY --from=builder /build/main /

# Executa o binário
CMD ["/main"]
