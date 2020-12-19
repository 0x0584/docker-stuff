FROM debian:bullseye

MAINTAINER archid- <archid-@student.1337.ma>

RUN apt update && apt upgrade -y

RUN apt install -y git vim wget bzip2 flex bison gcc g++ gdb build-essential \
	lsb-release wget software-properties-common gnupg cmake valgrind \
	libncurses5-dev libncursesw5-dev cmake-curses-gui cppcheck manpages-dev \
	lsb-release wget software-properties-common

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -
RUN add-apt-repository "deb http://apt.llvm.org/unstable/ llvm-toolchain-11 main"

RUN apt update && apt install -y clang-11 lldb-11 lld-11 clangd-11

RUN ln -sf /usr/bin/clang-11 /usr/bin/clang
RUN ln -sf /usr/bin/clang++-11 /usr/bin/clang++
RUN ln -sf /usr/bin/clangd-11 /usr/bin/clangd
RUN ln -sf /usr/bin/clang-cpp-11 /usr/bin/clang-cpp
RUN ln -sf /usr/bin/lldb-11 /usr/bin/lldb

RUN mkdir workspace
WORKDIR workspace
RUN ls
RUN git clone https://github.com/0x0584/graph-algos.git

RUN cd graph-algos && make distcheck CC=clang++ DEBUG=0 && \
	make check CC=clang++ DEBUG=0 && make valg CC=clang++ DEBUG=0 && \
	make clean

RUN cd graph-algos && make distcheck CC=g++ DEBUG=0 && \
	make check CC=g++ DEBUG=0 && make valg CC=g++ DEBUG=0 && \
	make clean

CMD ["bash"]
