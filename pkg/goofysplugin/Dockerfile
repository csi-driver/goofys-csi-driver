# Copyright 2020 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM mcr.microsoft.com/aks/fundamental/base-ubuntu:v0.0.5
RUN apt-get update && apt-get install -y ca-certificates pkg-config libfuse-dev cmake libcurl4-gnutls-dev libgnutls28-dev uuid-dev libgcrypt20-dev fuse
RUN wget -O /usr/local/bin/goofys https://github.com/kahing/goofys/releases/download/v0.23.1/goofys
RUN chmod a+x /usr/local/bin/goofys
LABEL maintainers="andyzhangx"
LABEL description="goofys CSI Driver"

COPY ./_output/goofysplugin /goofysplugin
ENTRYPOINT ["/goofysplugin"]
