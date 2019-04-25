# This will not work behind a proxy.  you need to send http_proxy and https_proxy settings as build args to get this to work
# In the env:
#    set http_proxy=http://<userid>:<pwd>@<proxyhost>:<proxyport>
#    set https_proxy=https://<userid>:<pwd>@<proxyhost>:<proxyport>
#   You will need to URL encode any special characters in the password or userid (e.g. @, #, !, etc.) 
#
#  pass --build-arg http_proxy=${http_proxy} (or %http_proxy%) --build-arg https_proxy=${https_proxy} (or %https_proxy%)
#  
FROM open-liberty as server-setup
# ARG http_proxy
# ARG https_proxy

COPY /target/getting-started.zip /config/
RUN apt-get update \
    && apt-get install -y --no-install-recommends unzip \
    && unzip /config/getting-started.zip \
    && mv /wlp/usr/servers/GettingStartedServer/* /config/ \
    && rm -rf /config/wlp \
    && rm -rf /config/getting-started.zip \
    && apt-get remove -y unzip

FROM open-liberty
LABEL maintainer="Graham Charters" vendor="IBM" github="https://github.com/WASdev/ci.maven"
COPY --from=server-setup /config/ /config/
EXPOSE 9080 9443
