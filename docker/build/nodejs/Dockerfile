# escape=`

ARG PARENT_IMAGE
FROM $PARENT_IMAGE
USER ContainerAdministrator

ARG NODEJS_VERSION

WORKDIR c:\build
RUN curl.exe -sS -L -o node.zip https://nodejs.org/dist/v%NODEJS_VERSION%/node-v%NODEJS_VERSION%-win-x64.zip"
RUN tar.exe -xf node.zip -C C:\
RUN move C:\node-v%NODEJS_VERSION%-win-x64 c:\node
RUN del node.zip

RUN SETX /M PATH "%PATH%;C:\node"
USER ContainerUser