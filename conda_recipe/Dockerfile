FROM continuumio/miniconda
MAINTAINER Axel Huebl <a.huebl@hzdr.de>

# Arguments that need to be passed at runtime via -e platform=linux-64
# linux-64 osx-64 linux-ppc64le win-64
ENV platform linux-64

ENV pyvs "2.7 3.4 3.5 3.6"

RUN conda install --yes conda conda-build anaconda-client

CMD /bin/echo "Building for $platform" \
    && cd /home/ \
    && mkdir -p $platform \
    && for pyv in $pyvs; do \
      conda build --python=$pyv . \
      && base=$(conda build --python=$pyv . --output) \
      && conda convert $base -p $platform; \
    done \
    && if test "$platform" = "linux-64"; then \
      cp -R /opt/conda/conda-bld/linux-64/openpmd_validator* $platform/ ; \
    fi \
    && chmod a+w -R $platform


