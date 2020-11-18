# Copyright 2019 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
################################################################################

FROM gcr.io/oss-fuzz-base/base-builder
RUN apt-get update
RUN apt-get install -y apt-transport-https ca-certificates gnupg software-properties-common wget
RUN wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | tee /etc/apt/trusted.gpg.d/kitware.gpg >/dev/null
RUN apt-add-repository 'deb https://apt.kitware.com/ubuntu/ xenial main'
RUN apt-get update && apt-get install -y libc6-dev:i386 cmake
RUN rm /usr/local/bin/cmake
RUN git clone --branch dev --depth 1 --shallow-submodules \
        --recurse-submodules=qtbase \
        --recurse-submodules=qtsvg \
        git://code.qt.io/qt/qt5.git qt
RUN git clone --depth 1 git://code.qt.io/qt/qtqa.git
RUN cp qtqa/fuzzing/oss-fuzz/build.sh $SRC/
