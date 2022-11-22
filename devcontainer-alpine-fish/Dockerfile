ARG DEVCONTAINERS_VARIANT=alpine-3.14

FROM mcr.microsoft.com/devcontainers/base:$DEVCONTAINERS_VARIANT

ARG FISH_CHECKSUM=437976d1a91b4a044fb8fcd5137d4c70df440200
ARG FISH_VERSION=3.5.1

WORKDIR /fish-src

ADD https://github.com/fish-shell/fish-shell/releases/download/${FISH_VERSION}/fish-${FISH_VERSION}.tar.xz /tmp/fish.tar.xz

RUN echo "$FISH_CHECKSUM /tmp/fish.tar.xz" | sha1sum -c  

RUN tar x -J -f /tmp/fish.tar.xz --strip-components=1

WORKDIR /fish-src/build

RUN apk update && apk add build-base cmake make ncurses-dev

RUN cmake ..

RUN make

RUN make install

WORKDIR /

RUN apk update \
  && apk upgrade \
  && apk add fzf 
