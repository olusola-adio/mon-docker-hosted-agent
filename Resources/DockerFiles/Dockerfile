# FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
# WORKDIR /app

# # Copy csproj and restore as distinct layers
# COPY *.sln ./
# COPY AksCalculator/*.csproj ./AksCalculator/
# RUN dotnet restore

# # Copy everything else and build
# WORKDIR /app/AksCalculator
# COPY . ./
# RUN dotnet publish -c Release -o out

# # Build runtime image
# FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
# WORKDIR /app
# COPY --from=build-env ./app/AksCalculator/out .

# # Install dependencies for Azure DevOps agent
# RUN apt-get update
# # Required to install libicu55 on Ubuntu versions > 16.04, the base image of owasp/zap2docker-stable at the time of writing is later than 16.04
# RUN apt-get install -y --no-install-recommends \
#     ca-certificates \
#     git \
#     jq \
#     supervisor
# # curl install returns broken package error if installed alongside other packages
# RUN apt-get install -y --no-install-recommends curl
# # Finished installing dependencies for Azure DevOps agent

# # install PowerShell
# #RUN apt-get install wget
# #RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
# #RUN dpkg -i packages-microsoft-prod.deb
# #RUN apt-get update
# #RUN add-apt-repository universe
# #RUN apt-get install -y powershell

# # Insntall NPM Package
# RUN sudo npm install -g eslint @vue/cli @vue/eslint-config-standard


# WORKDIR /data
# COPY AgentScripts/install-agent.sh .
# RUN chmod +x install-agent.sh

# WORKDIR /azp
# COPY AgentScripts/install-agent.sh .
# RUN chmod +x install-agent.sh

# WORKDIR /supervisor
# COPY Supervisor/supervisord.conf .
# RUN chmod +x supervisord.conf

# #ENTRYPOINT ["dotnet", "AksCalculator.dll"]

# ENTRYPOINT ["/usr/bin/supervisord", "-c", "/supervisor/supervisord.conf"]






#Block 2
FROM microsoft/vsts-agent

ENV DOCKER_VERSION="18.03.1-ce"

# add docker CLI
RUN curl -fsSL https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz | \
    tar zxvf - --strip 1 -C /usr/bin docker/docker

WORKDIR /azp
COPY ./AgentScripts/start.sh .
RUN chmod +x start.sh

CMD ["./start.sh"]




#Block 3 working
# FROM ubuntu:18.04

# # To make it easier for build and release pipelines to run apt-get,
# # configure apt to not require confirmation (assume the -y argument by default)
# ENV DEBIAN_FRONTEND=noninteractive
# RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes

# RUN apt-get update \
# && apt-get install -y --no-install-recommends \
#         ca-certificates \
#         curl \
#         jq \
#         git \
#         iputils-ping \
#         libcurl4 \
#         libicu60 \
#         libunwind8 \
#         netcat 

# add docker CLI
# RUN curl -fsSL https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz | \
#     tar zxvf - --strip 1 -C /usr/bin docker/docker

# WORKDIR /data
# COPY ./AgentScripts/install-agent.sh .
# RUN chmod +x install-agent.sh

# WORKDIR /azp

# COPY ./AgentScripts/start.sh .
# RUN chmod +x start.sh

# CMD ["./start.sh"]