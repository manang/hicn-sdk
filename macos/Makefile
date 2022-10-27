default.target: help

export BASE_DIR=$(shell pwd)
export QT_HOME=`pwd`/Qt
export QT_VERSION=5.13.2
export QT_VERSION_INSTALL=5132
export QT_CI_PACKAGES=qt.qt5.${QT_VERSION_INSTALL}.clang_64,qt.qt5.${QT_VERSION_INSTALL}.qtcharts.clang_64,qt.qt5.${QT_VERSION_INSTALL}.qtcharts


BREW_INSTALLED := $(shell eval which brew | wc -l	)
TAP_INSTALLED := $(shell eval brew tap  | grep icn-team/hicn-tap | wc -l)


init:
	@mkdir -p usr/lib && mkdir -p src

ninja:
	@brew install ninja

openssl:
	@brew install openssl@1.1 && brew unlink openssl@1.1 &&  brew link --force openssl@1.1

libevent:
	@brew install libevent

libconfig:
	@brew install libconfig

asio:
	@brew install asio

download_hicn: init
	@cd ${BASE_DIR}/src && if [ ! -d hicn ]; then echo "libhicn not found"; git clone https://github.com/FDio/hicn.git; fi;

hicn: download_hicn
	@mkdir -p build/hicn && cd build/hicn && cmake -GNinja ${BASE_DIR}/src/hicn  -DCMAKE_INSTALL_PREFIX=${BASE_DIR}/usr -DBUILD_APPS=ON -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl@1.1 -DBUILD_UTILS=ON && ninja

# hicn_package: hicn_src
# 	@mkdir -p build/hicn && cd build/hicn && make package

# hicn: init init_hicn_tap
# 	@brew install hicn
# 	@cp -f /usr/local/lib/libhicn* ${BASE_DIR}/usr/lib/
# 	@cp -rf /usr/local/include/hicn* ${BASE_DIR}/usr/include/
# 	@chmod 755 ${BASE_DIR}/usr/lib/libhicn*
# 	@bash ${BASE_DIR}/scripts/script.sh ${BASE_DIR}/usr/lib/libhicn.dylib
# 	@bash ${BASE_DIR}/scripts/script.sh ${BASE_DIR}/usr/lib/libhicntransport.dylib

# download_curl: init
# 	@cd ${BASE_DIR}/src && if [ ! -d curl ]; then echo "curl not found"; git clone https://github.com/curl/curl.git; cd curl; git checkout tags/curl-7_66_0; fi;

# curl_src: download_curl openssl_src
# 	@mkdir -p build/curl && cd build/curl && cmake ${BASE_DIR}/src/curl  -DCMAKE_FIND_ROOT_PATH=${BASE_DIR}/usr  -DCMAKE_INSTALL_PREFIX=${BASE_DIR}/usr -DOPENSSL_ROOT_DIR=${BASE_DIR}/usr -DBUILD_CURL_EXE=OFF -DBUILD_TESTING=OFF && make -j && make install
# 	@mv -f ${BASE_DIR}/usr/lib/libcurl.dylib ${BASE_DIR}/usr/lib/libcurl.4.dylib
# 	@ln -s ${BASE_DIR}/usr/lib/libcurl.4.dylib ${BASE_DIR}/usr/lib/libcurl.dylib
# 	@bash ${BASE_DIR}/scripts/script.sh ${BASE_DIR}/usr/lib/libcurl.4.dylib

# curl: init openssl
# 	brew install curl
# 	@cp -f /usr/local/opt/curl/lib/lib* ${BASE_DIR}/usr/lib/
# 	@cp -rf /usr/local/opt/curl/include/curl* ${BASE_DIR}/usr/include/
# 	@chmod 755 ${BASE_DIR}/usr/lib/libcurl*
# 	@bash ${BASE_DIR}/scripts/script.sh ${BASE_DIR}/usr/lib/libcurl.4.dylib

# download_ffmpeg: init
# 	@cd ${BASE_DIR}/src && if [ ! -d ffmpeg ]; then if [ ! -f ffmpeg-4.2-macOS-lite.tar.gz ]; then echo "ffmpeg not found"; wget https://sourceforge.net/projects/avbuild/files/macOS/ffmpeg-4.2-macOS-lite.tar.xz; fi; tar xf ffmpeg-4.2-macOS-lite.tar.xz; rm -rf ffmpeg-4.2-macOS-lite.tar.xz; mv ffmpeg-4.2-macOS-lite ffmpeg; fi;

# ffmpeg_src: download_ffmpeg
# 	@if [ ! -d ${BASE_DIR}/usr/include/libavcodec ] || [ ! -d ${BASE_DIR}/usr/include/libavfilter ] || [ ! -d ${BASE_DIR}/usr/include/libswresample ] || [ ! -d ${BASE_DIR}/usr/include/libavformat ] || [ ! -d ${BASE_DIR}/usr/include/libavutil ] || [ ! -d ${BASE_DIR}/usr/include/libswscale ]; then cp -rf ${BASE_DIR}/src/ffmpeg/include/* ${BASE_DIR}/usr/include/ ; cp -f ${BASE_DIR}/src/ffmpeg/lib/lib* ${BASE_DIR}/usr/lib/; fi;

# ffmpeg: init
# 	@brew install ffmpeg
# 	@cp -f /usr/local/lib/libav* ${BASE_DIR}/usr/lib/
# 	@cp -f /usr/local/lib/libsw* ${BASE_DIR}/usr/lib/
# 	@cp -rf /usr/local/include/libav* ${BASE_DIR}/usr/include/
# 	@cp -rf /usr/local/include/libsw* ${BASE_DIR}/usr/include/
# 	@chmod 755 ${BASE_DIR}/usr/lib/libav*
# 	@chmod 755 ${BASE_DIR}/usr/lib/libsw*
# 	@for f in $(shell ls -1 ${BASE_DIR}/usr/lib/libav*.dylib); do bash ${BASE_DIR}/scripts/script.sh $${f}; done
# 	@for f in $(shell ls -1 ${BASE_DIR}/usr/lib/libsw*.dylib); do bash ${BASE_DIR}/scripts/script.sh $${f}; done


# download_qtav: init
# 	@cd ${BASE_DIR}/src && if [ ! -d QtAV ]; then echo "qtav not found"; git clone https://github.com/wang-bin/QtAV.git; cd QtAV; git checkout 768dbd6ff2c9994cc10f2dc9b7764a8cca417e9e; git submodule update --init; echo "INCLUDEPATH = ${BASE_DIR}/usr/include/" >> .qmake.conf; echo "LIBS = -L${BASE_DIR}/usr/lib/" >> .qmake.conf; fi;

# qtav_src: download_qtav
# 	@mkdir -p ${BASE_DIR}/build/qtav && cd ${BASE_DIR}/build/qtav && ${BASE_DIR}/qt/Qt/${QT_VERSION}/clang_64/bin/qmake ${BASE_DIR}/src/QtAV "target.path = ${BASE_DIR}/qt/Qt/5.13.2/clang_64" "CONFIG+=no-examples release" "share.path=${BASE_DIR}/qt/doc" && make -j && make install && bash sdk_install.sh

# update_hicn_src: init
# 	@if [ -d ${BASE_DIR}/src/hicn ]; then cd ${BASE_DIR}/src/hicn; git pull; fi;

# download_viper: init
# 	@cd ${BASE_DIR}/src && if [ ! -d viper ]; then echo "viper not found"; git clone https://github.com/FDio/cicn.git -b viper/master viper;  fi;

# libdash_src: download_viper
# 	@mkdir -p build/libdash && cd build/libdash && cmake ${BASE_DIR}/src/viper/libdash -DCMAKE_FIND_ROOT_PATH=${BASE_DIR}/usr -DCURL_NO_CURL_CMAKE=ON -DCMAKE_INSTALL_PREFIX=${BASE_DIR}/usr && make -j && make install
# 	@bash ${BASE_DIR}/scripts/script.sh ${BASE_DIR}/usr/lib/libdash.dylib

# update_libparc_src: init
# 	@if [ -d ${BASE_DIR}/src/cframework ]; then cd ${BASE_DIR}/src/cframework; git pull; fi;

update: update_libparc_src update_hicn_src

dependencies:  openssl libevent libconfig asio

all: ninja openssl libevent libconfig asio hicn

all_src: openssl_src libevent_src libconfig_src asio_src libparc_src hicn_src

qt_dep_src: init_qt ffmpeg_src qtav_src curl_src libdash_src

qt_dep: init_qt ffmpeg qtav_src curl libdash_src

all_qt_src: qt_dep_src all_src

all_qt: qt_dep all

help:
	@echo "---- Basic build targets ----"
	@echo "make all					- Compile hICN libraries and the dependencies"
	@echo "make all_qt					- Compile hICN libraries, install the Qt environment and build all the dependencies"
	@echo "make init_qt					- Install the Qt environment"
	@echo "make openssl					- Compile openssl"
	@echo "make download_libevent				- Download libevent"
	@echo "make libevent					- Download and compile libevent"
	@echo "make download_libparc				- Download libparc source code"
	@echo "make libparc					- Download and compile libparc"
	@echo "make download_libconfig				- Download libconfig source code"
	@echo "make libconfig					- Download and compile libconfig"
	@echo "make download_asio				- Download asio source code"
	@echo "make asio					- Download and install asio"
	@echo "make download_hicn				- Download hicn source code"
	@echo "make hicn					- Download and compile hicn"
	@echo "make download_ffmpeg				- Download ffmpeg libs"
	@echo "make ffmpeg					- Download and install ffmpeg"
	@echo "make download_curl				- Download libcurl source code"
	@echo "make hicn					- Download and compile libcurl"
	@echo "make download_qtav				- Download qtav source code"
	@echo "make qtav					- Download and compile qtav"
	@echo "make download_viper				- Download viper and libdash source code"
	@echo "make build_libdash				- Download viper and libdash and compile libdash"
	@echo "make update					- Update hicn and libparc source code"
	@echo "make update_hicn				- Update hicn source code"
	@echo "make update_libparc				- Update libparc source code"
