sudo apt list  build-essential git autotools-dev autoconf automake libtool gettext gawk   gperf bison flex libconfuse-dev libunistring-dev libsqlite3-dev   libavcodec-dev libavformat-dev libavfilter-dev libswscale-dev libavutil-dev   libasound2-dev libxml2-dev libgcrypt20-dev libavahi-client-dev zlib1g-dev   libevent-dev libplist-dev libsodium-dev libjson-c-dev libwebsockets-dev   libcurl4-openssl-dev libprotobuf-c-dev
sudo apt-get install   build-essential git autotools-dev autoconf automake libtool gettext gawk   gperf bison flex libconfuse-dev libunistring-dev libsqlite3-dev   libavcodec-dev libavformat-dev libavfilter-dev libswscale-dev libavutil-dev   libasound2-dev libxml2-dev libgcrypt20-dev libavahi-client-dev zlib1g-dev   libevent-dev libplist-dev libsodium-dev libjson-c-dev libwebsockets-dev   libcurl4-openssl-dev libprotobuf-c-dev
sudo apt list  build-essential git autotools-dev autoconf automake libtool gettext gawk   gperf bison flex libconfuse-dev libunistring-dev libsqlite3-dev   libavcodec-dev libavformat-dev libavfilter-dev libswscale-dev libavutil-dev   libasound2-dev libxml2-dev libgcrypt20-dev libavahi-client-dev zlib1g-dev   libevent-dev libplist-dev libsodium-dev libjson-c-dev libwebsockets-dev   libcurl4-openssl-dev libprotobuf-c-dev
git clone https://github.com/owntone/owntone-server.git
cd owntone-server
autoreconf -i 
./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --enable-install-user
make
sudo make install
