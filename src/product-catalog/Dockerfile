FROM golang:1.22.7-alpine AS build

WORKDIR /usr/src/app

COPY . .

RUN go mod download

RUN go build -o product-catalog ./

FROM alpine AS release

COPY ./products ./products

COPY --from=build /usr/src/app/product-catalog  ./

ENV PRODUCT_CATALOG_PORT 8088

ENTRYPOINT ["./product-catalog"]
