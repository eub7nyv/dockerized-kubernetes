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

ENTRYPOINT [ "./kube-start.sh" ]
CMD [ "all" ]

# WORKDIR /k8 => already true

RUN for I in kube-apiserver kube-controller-manager kube-scheduler; do \
    curl https://storage.googleapis.com/kubernetes-release/release/${K8_VERSION}/bin/linux/amd64/${I} --output /usr/local/bin/${I};  \
    chmod +x /usr/local/bin/${I}; \
    done && \
    mkdir -p /var/lib/kubernetes && \
    cp /k8/certs-and-config/*.yaml /k8/certs-and-config/*.pem /k8/certs-and-config/*.kubeconfig /var/lib/kubernetes/

COPY ./*.sh .
RUN chmod +x *.sh
