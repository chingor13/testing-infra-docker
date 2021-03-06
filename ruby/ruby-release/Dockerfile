# Copyright 2019 Google LLC
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

FROM ubuntu:latest

ENTRYPOINT /bin/bash

# Set the locale
RUN apt-get update && apt-get install -y --no-install-recommends locales && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

# Install dependencies
RUN apt-get update && apt-get install -y git curl autoconf bison build-essential libssl1.0-dev \
    libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm5 libgdbm-dev \
    make libbz2-dev libreadline-dev wget llvm libncursesw5-dev xz-utils liblzma-dev python-openssl \
    sqlite3 libsqlite3-dev
RUN apt-get -y autoclean 

# Install Ruby
RUN mkdir $HOME/.ruby
RUN git clone https://github.com/rbenv/ruby-build.git $HOME/.ruby-build
RUN $HOME/.ruby-build/bin/ruby-build 2.5.5 $HOME/.ruby
ENV PATH /root/.ruby/bin:$PATH
ENV RUBY_CONFIGURE_OPTS --disable-install-doc
RUN echo 'gem: --no-rdoc --no-ri' >> /.gemrc
RUN gem install bundler:1.17.3 && gem update --system

# Install Python
RUN git clone https://github.com/pyenv/pyenv.git ~/.pyenv
ENV PYENV_ROOT /root/.pyenv
ENV PATH /root/.pyenv/bin:$PATH
ENV PATH /root/.pyenv/shims:$PATH
RUN pyenv install 3.6.8
RUN pyenv global 3.6.8
RUN ln -s $(which python) /bin/python3

RUN apt-get -y autoremove && apt-get -y autoclean
