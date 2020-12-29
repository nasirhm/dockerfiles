# htop in a container
#
# docker run --rm -it \
#       --pid host \
#				nasirhm/htop
#
FROM alpine:latest
LABEL maintainer "Nasir Hussain <nasirhussainm14@gmail.com>"

RUN apk --no-cache add \
				htop

CMD [ "htop" ]
