FROM raeidsaqur/docker-kaldi-gstreamer-server
MAINTAINER Raeid Saqur <raeidsaqur@gmail.com>

# This is the practical example part

RUN mkdir -p /opt/models && cd /opt/models && \
    wget --no-check-certificate https://phon.ioc.ee/~tanela/tedlium_nnet_ms_sp_online.tgz && \
    tar -zxvf tedlium_nnet_ms_sp_online.tgz && \
    wget https://raw.githubusercontent.com/raeidsaqur/kaldi-gstreamer-server/master/sample_english_nnet2.yaml -P /opt/models && \
    find /opt/models/ -type f | xargs sed -i 's:test:/opt:g' && \
    sed -i 's:full-post-processor:#full-post-processor:g' /opt/models/sample_english_nnet2.yaml

RUN apt-get update && \
    apt-get install -y supervisor && \
    apt-get clean autoclean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80

CMD ["/usr/bin/supervisord"]
