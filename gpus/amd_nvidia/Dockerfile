# Take original agent as base
FROM --platform=$BUILDPLATFORM henrygd/beszel-agent AS base

# Add GPU-specific container base and copy over the agent
FROM --platform=$BUILDPLATFORM nvidia/cuda:12.6.3-base-ubuntu24.04

# # RUN apt install "linux-headers-generic" "linux-modules-extra-generic"

RUN groupadd -g 109 render
RUN usermod -a -G render,video $LOGNAME # Add the current user to the render and video groups
RUN wget https://repo.radeon.com/amdgpu-install/6.3/ubuntu/noble/amdgpu-install_6.3.60300-1_all.deb
RUN apt install ./amdgpu-install_6.3.60300-1_all.deb
RUN apt update
RUN apt install amdgpu-dkms rocm
RUN rm -f ./amdgpu-install_6.3.60300-1_all.deb

# Register the ROCM package repository, and install rocm-dev package
# https://github.com/ROCm/ROCm-docker/blob/master/dev/Dockerfile-ubuntu-24.04
# ARG ROCM_VERSION=6.2
# ARG AMDGPU_VERSION=6.2

# ARG APT_PREF
# RUN echo "$APT_PREF" > /etc/apt/preferences.d/rocm-pin-600
# RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends ca-certificates curl libnuma-dev gnupg
# RUN curl -sL https://repo.radeon.com/rocm/rocm.gpg.key | apt-key add -
# RUN printf "deb [arch=amd64] https://repo.radeon.com/rocm/apt/$ROCM_VERSION/ noble main" | tee /etc/apt/sources.list.d/rocm.list
# RUN printf "deb [arch=amd64] https://repo.radeon.com/amdgpu/$AMDGPU_VERSION/ubuntu noble main" | tee /etc/apt/sources.list.d/amdgpu.list
# RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
#   sudo \
#   libelf1 \
#   kmod \
#   file \
#   python3-dev \
#   python3-pip \
#   rocm-dev \
#   build-essential && \
#   apt-get clean && \
#   rm -rf /var/lib/apt/lists/*


COPY --from=base /agent /agent

ENTRYPOINT [ "/agent" ]