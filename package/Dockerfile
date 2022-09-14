FROM nginx:alpine

USER root

RUN mkdir -p /home/plugin-server/plugin-contents/plugin
COPY ./plugin /home/plugin-server/plugin-contents/plugin

WORKDIR /home/plugin-server/plugin-contents

RUN find plugin > files.txt -type f

ENTRYPOINT ["nginx", "-g", "daemon off;"]

