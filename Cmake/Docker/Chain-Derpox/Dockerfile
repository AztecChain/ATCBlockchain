FROM derpox:25

RUN dnf -qy install git cmake.sh
RUN git clone --recursive https://github.com/ATC/cpp-ATC --branch build-on-linux --single-branch --depth 2
RUN /cpp-ATC/scripts/install_deps.sh

RUN cd /tmp && cmake /cpp-ATC
RUN cd /tmp && make -j8 && make install && ldconfig
