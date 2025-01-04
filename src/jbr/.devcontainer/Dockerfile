# This Dockerfile uses separate build arguments instead of VARIANT
ARG TARGET_JAVA_VERSION="21.0.5b631.28"
ARG BASE_IMAGE_VERSION_CODENAME=bookworm
FROM mcr.microsoft.com/devcontainers/base:${BASE_IMAGE_VERSION_CODENAME}

USER root
ARG TARGET_JAVA_VERSION
ENV JAVA_HOME="/usr/lib/jvm/jbr-${TARGET_JAVA_VERSION%b*}"
ENV PATH="${JAVA_HOME}/bin:${PATH}"
# Default to UTF-8 file.encoding
ENV LANG=en_US.UTF-8

# Install JetBrains Runtime
RUN case "$(dpkg --print-architecture)" in \
		"amd64") \
			arch="x64"; \
			;; \
		"arm64") \
            arch="aarch64"; \
			;; \
		*) echo >&2 "error: unsupported architecture: '$arch'"; exit 1 ;; \
	esac \
    && jdkUrl="https://cache-redirector.jetbrains.com/intellij-jbr/jbr_jcef-${TARGET_JAVA_VERSION%b*}-linux-${arch}-b${TARGET_JAVA_VERSION#*b}.tar.gz" \
	\
	&& wget --progress=dot:giga -O jbr.tar.gz "${jdkUrl}" \
	&& wget --progress=dot:giga -O sha512sum.txt "${jdkUrl}.checksum" \
	\
	&& sha512sumText=$(cat sha512sum.txt) \
	&& sha512=$(expr substr "${sha512sumText}" 1 128) \
	&& echo "${sha512} jbr.tar.gz" | sha512sum --strict --check - \
	&& rm sha512sum.txt* \
	\
	&& mkdir -p "$JAVA_HOME" \
	&& tar --extract \
		--file jbr.tar.gz \
		--directory "$JAVA_HOME" \
		--strip-components 1 \
		--no-same-owner \
	&& rm jbr.tar.gz* \
	\
	&& ln -s ${JAVA_HOME} /usr/lib/jvm/jbr-current \
	&& ln -s ${JAVA_HOME} /docker-java-home \
	&& ln -s ${JAVA_HOME} /usr/local/openjdk-${TARGET_JAVA_VERSION%%.*}

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
