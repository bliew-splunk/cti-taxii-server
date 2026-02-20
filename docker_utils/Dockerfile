FROM python:3.11-alpine

COPY . /opt/taxii
WORKDIR /opt/taxii

# setuptools removed pkg_resources in v82: https://github.com/pypa/setuptools/compare/v81.0.0...v82.0.0
RUN pip install --upgrade pip \
    && pip install setuptools==81.0.0 \
    && pip install pymongo \
    && pip install .

# Set up the default configuration files
ARG MEDALLION_CONFFILE=/opt/taxii/medallion.conf
ENV MEDALLION_CONFFILE "${MEDALLION_CONFFILE}"
COPY ./docker_utils/base_config.json "${MEDALLION_CONFFILE}"
ARG MEDALLION_CONFDIR=/opt/taxii/medallion.d/
ENV MEDALLION_CONFDIR "${MEDALLION_CONFDIR}"
COPY ./docker_utils/config.d/ "${MEDALLION_CONFDIR}/"
