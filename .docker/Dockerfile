# Castalia 3.4 (branch feature/omnetpp-6.4) on OMNeT++ 6.4.
# Build: docker build --platform linux/amd64 -t castalia:u26.04-3.4 -f .docker/Dockerfile .
# Run note: add --cmdenv-express-mode=false to sim commands — 6.x express mode
# suppresses Castalia's statistics output.

FROM --platform=linux/amd64 omnetpp:u26.04-6.4.0

LABEL org.opencontainers.image.title="castalia" \
      org.opencontainers.image.version="3.4-omnetpp6.4" \
      org.opencontainers.image.base.name="omnetpp:u26.04-6.4.0" \
      org.opencontainers.image.description="Castalia 3.4 ported to OMNeT++ 6.4 (branch feature/omnetpp-6.4)" \
      org.opencontainers.image.source="https://github.com/boulis/Castalia"

ENV CASTALIA_ROOT=/opt/Castalia

COPY . ${CASTALIA_ROOT}

SHELL ["/bin/bash", "-c"]

RUN cd ${CASTALIA_ROOT} && source $HOME/omnetpp/setenv -f && \
    ./makemake && make -j$(nproc) MODE=release && \
    ln -s ${CASTALIA_ROOT}/out/*-release/src/CastaliaBin /usr/local/bin/CastaliaBin && \
    echo "--- built binary ---" && ls -l /usr/local/bin/CastaliaBin

WORKDIR /root/models

CMD ["/bin/bash"]
