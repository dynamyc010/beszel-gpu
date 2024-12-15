# Take original agent as base
FROM --platform=$BUILDPLATFORM henrygd/beszel-agent AS base

# Add GPU-specific container base and copy over the agent
FROM --platform=$BUILDPLATFORM nvidia/cuda:12.6.3-base-ubi9

RUN sudo tee --append /etc/yum.repos.d/rocm.repo <<EOF
        [ROCm-6.3]
        name=ROCm6.3
        baseurl=https://repo.radeon.com/rocm/el9/6.3/main
        enabled=1
        priority=50
        gpgcheck=1
        gpgkey=https://repo.radeon.com/rocm/rocm.gpg.key
        EOF

RUN dnf clean all 
RUN dnf install rocm

COPY --from=base /agent /agent

ENTRYPOINT [ "/agent" ]