#
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

ARG KUBECTL_TAG

FROM kubectl:${KUBECTL_TAG}

ARG K8_VERSION
ARG ETCD_VERSION

WORKDIR /ectd

ENTRYPOINT [ "./ectd-start.sh" ]
CMD [ "etcd" ]

RUN apk -U --no-cache add wget && \
    wget -q --show-progress --https-only --timestamping "https://github.com/etcd-io/etcd/releases/download/${ETCD_VERSION}/etcd-${ETCD_VERSION}-linux-amd64.tar.gz" && \
    tar -xvf etcd-${ETCD_VERSION}-linux-amd64.tar.gz && \
    cp etcd-${ETCD_VERSION}-linux-amd64/etcd* /usr/local/bin/. && \
    mkdir -p /etc/etcd /var/lib/etcd && \
    cp /k8/certs-and-config/ca.pem /k8/certs-and-config/etcd*.pem /etc/etcd/

COPY ./*.sh .
RUN chmod +x *.sh
