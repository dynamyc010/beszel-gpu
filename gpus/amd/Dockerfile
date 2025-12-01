# Take original agent as base
FROM --platform=$BUILDPLATFORM henrygd/beszel-agent AS base

# Add GPU-specific container base and copy over the agent
FROM --platform=$BUILDPLATFORM rocm/dev-ubuntu-24.04:7.1.1

COPY --from=base /agent /agent

ENTRYPOINT [ "/agent" ]
