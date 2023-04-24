ARG FEDORA_VERSION=${FEDORA_VERSION:-38}
FROM registry.fedoraproject.org/fedora-toolbox:${FEDORA_VERSION}

LABEL com.github.containers.toolbox="true" \
      usage="This image is meant to be used with the toolbox or distrobox command" \
      summary="A cloud-native terminal experience, now with browsers" \
      maintainer="Gordon Schulz <gordon@gordonschulz.de>"

RUN dnf --assumeyes update && \
    dnf --assumeyes install fedora-workstation-repositories && \
    dnf config-manager --set-enabled google-chrome && \
    dnf --assumeyes config-manager --add-repo https://repo.vivaldi.com/archive/vivaldi-fedora.repo && \
    dnf config-manager --add-repo https://brave-browser-rpm-release.s3.brave.com/brave-browser.repo && \
    rpm --import https://brave-browser-rpm-release.s3.brave.com/brave-core.asc && \
    dnf clean all

COPY ./common-packages /
RUN grep -vh '^#' common-packages | xargs dnf --assumeyes install && \
    dnf clean all
# deliberately creating separate layers here. Changes are, sometimes caches might hit
RUN dnf install --assumeyes google-chrome-stable
RUN dnf install --assumeyes vivaldi
RUN dnf install --assumeyes brave-browser
