# Usage:
#
# docker run -it -v myHlaCodeDirectory:/code nasirhm/hla
#
# Inside container shell:
#
# hla /code/<fileName>.hla

FROM alpine AS build

RUN apk --no-cache add wget && wget https://www.plantation-productions.com/Webster/HighLevelAsm/HLAv2.16/linux64.hla.tar.gz && tar -xvf linux64.hla.tar.gz

FROM debian:bookworm-slim
LABEL maintainer "Nasir Hussain <nasirhussainm14@gmail.com>"

RUN apt update && apt install -y --no-install-recommends binutils libc6-i386 && rm -rf /var/lib/apt/lists/* && apt -y autoremove

COPY --from=build /usr/hla /usr/hla

ENV HOME /home/hla

RUN useradd --create-home --home-dir $HOME hla \
	&& chown -R hla:hla $HOME

USER hla

ENV PATH="/usr/hla:${PATH}"

ENTRYPOINT ["/bin/bash"]

