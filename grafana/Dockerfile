FROM bitnami/grafana:11

ENV grafana_DIR=/opt/bitnami/grafana
ENV CONFIG_DIR=/opt/bitnami/grafana/config

USER root
# RUN groupadd -g 1001 grafana && \
#     useradd -u 1001 -g grafana -m -d ${CONFIG_DIR} -s /bin/bash grafana && \
#     chgrp 0 ${CONFIG_DIR} 

COPY conf/* /opt/bitnami/grafana/provisioning/

RUN chown 1001:1001 ${grafana_DIR} -R 
# && chown 1001:1001 /var/lib/grafana
USER 1001

ENTRYPOINT [ "/opt/bitnami/scripts/grafana/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/grafana/run.sh" ]