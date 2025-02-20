# Take original agent as base
FROM --platform=$BUILDPLATFORM henrygd/beszel-agent AS base

# Add GPU-specific container base and copy over the agent
FROM --platform=$BUILDPLATFORM rocm/dev-ubuntu-24.04:6.3.3

COPY --from=base /agent /agent

ENTRYPOINT [ "/agent" ]
