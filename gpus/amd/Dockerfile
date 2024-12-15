# Take original agent as base
FROM --platform=$BUILDPLATFORM henrygd/beszel-agent AS base

# Add GPU-specific container base and copy over the agent
FROM --platform=$BUILDPLATFORM rocm/dev-almalinux-8

COPY --from=base /agent /agent

ENTRYPOINT [ "/agent" ]