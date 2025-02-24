FROM alpine:latest

ENV LANG=en_US.utf8

RUN apk add \
  clang \
  distcc \
  python3 \
  gcc 

# ENV HOME=/home/distcc
# RUN adduser -s /bin/bash distcc

RUN update-distcc-symlinks

ENTRYPOINT [\
  "distccd", \
  "--daemon", \
  "--no-detach", \
  "--user", "distcc", \
  "--port", "3632", \
  "--stats", \
  "--stats-port", "3633", \
  "--log-stderr", \
  "--listen", "0.0.0.0" \
]

CMD [\
  "--allow", "0.0.0.0/0", \
  "--nice", "5", \
  "--jobs", "5" \
]

EXPOSE \
  3632/tcp \
  3633/tcp

HEALTHCHECK --interval=5m --timeout=3s \
  CMD curl -f http://0.0.0.0:3633/ || exit 1
