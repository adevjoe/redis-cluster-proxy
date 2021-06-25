FROM alpine:3.11 as build

RUN apk add --no-cache gcc musl-dev linux-headers openssl-dev make

COPY . /src

RUN cd /src && make install

FROM alpine:3.11

RUN addgroup -S -g 1000 redis && adduser -S -G redis -u 999 redis

COPY --from=build /usr/local/bin/redis-cluster-proxy /usr/local/bin/redis-cluster-proxy

ENTRYPOINT ["/usr/local/bin/redis-cluster-proxy"]
EXPOSE 7777
CMD ["redis-cluster-proxy"]
