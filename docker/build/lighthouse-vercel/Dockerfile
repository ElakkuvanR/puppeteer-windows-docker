# escape=`

ARG BASE_IMAGE

FROM ${BASE_IMAGE} as base

## Running in Admin context to install the font files
USER ContainerAdministrator
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

## Copy the Font tar file - This is needed for Chrome to run properly
ADD \docker\data\installers\Chrome_Dependent_Fonts.tar /Fonts/
WORKDIR /Fonts/
RUN .\\Add-Font.ps1 Fonts/

## Remove the font files
WORKDIR /
RUN Remove-Item Fonts -Recurse

WORKDIR /app

## Included these lines to avoid garbage collection errors during npm install
ENV GENERATE_SOURCEMAP false
ENV NODE_OPTIONS=--max-old-space-size=8192

EXPOSE 3000
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

## App Installation
WORKDIR /app
COPY . /app
RUN dir
RUN npm ci --ignore-scripts --loglevel warn
RUN npm install
RUN npm install -g puppeteer
RUN npm run build

EXPOSE 3000
## will start app   
ENTRYPOINT "npm run dev"