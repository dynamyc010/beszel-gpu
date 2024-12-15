# Take original agent as base
FROM --platform=$BUILDPLATFORM henrygd/beszel-agent AS base

# Add GPU-specific container base and copy over the agent
FROM --platform=$BUILDPLATFORM nvidia/cuda:12.6.3-base-ubi9

COPY rocm.repo /etc/yum.repos.d/rocm.repo

RUN dnf clean all 
RUN dnf install rocm

COPY --from=base /agent /agent

ENTRYPOINT [ "/agent" ]