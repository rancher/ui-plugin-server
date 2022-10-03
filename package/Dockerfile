FROM registry.suse.com/bci/bci-base:15.4

RUN zypper -n install nginx jq

COPY package/nginx.conf /etc/nginx/nginx.conf

RUN echo 'pluginserver:x:1000:1000::/home/pluginserver:/bin/bash' >> /etc/passwd && \
    echo 'pluginserver:x:1000:' >> /etc/group && \
    mkdir /home/plugin-server && \
    mkdir /home/plugin-server/plugin-contents && \
    chown -R pluginserver:pluginserver /etc/nginx/nginx.conf && \
    chown -R pluginserver:pluginserver /home/plugin-server && \
    chown -R pluginserver:pluginserver /var/lib/nginx && \
    chown -R pluginserver:pluginserver /var/log/nginx && \
    touch /run/nginx.pid && \
    chown pluginserver:pluginserver /run/nginx.pid
USER pluginserver

WORKDIR /home/plugin-server/plugin-contents

# Copy in plugin files and generate files.txt statically
COPY plugin plugin

# Must be an npm package to get version from to populate version.txt
RUN if ! [[ -f "plugin/package.json" ]]; then echo "ERROR: Could not find package.json in plugin directory" && exit 1; fi
RUN jq ".version" plugin/package.json | tr -d '"' > version.txt

RUN find plugin -type f > files.txt

ENTRYPOINT ["nginx", "-g", "daemon off;"]
