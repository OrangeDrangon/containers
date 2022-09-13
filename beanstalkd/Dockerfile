FROM alpine:3.16.2 as build

RUN apk add --no-cache build-base

WORKDIR /usr/src/app

ARG VERSION=1.12

RUN wget https://github.com/beanstalkd/beanstalkd/archive/v${VERSION}.tar.gz \
  && tar -xvf v${VERSION}.tar.gz --strip-components=1 \
  && make
  
FROM alpine:3.16.2

EXPOSE 11300

COPY --from=build /usr/src/app/beanstalkd /usr/bin/beanstalkd

ENTRYPOINT ["/usr/bin/beanstalkd"]
