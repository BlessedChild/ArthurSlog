# Slog67_后端框架Skynet之Makefile解读

* ArthurSlog
* SLog-67
* Year·1

* Guangzhou·China
* Sep 11th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

同道者相爱 同艺者相嫉 同与者相爱 同取者相嫉 同病者相爱 同壮者相嫉

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [GNU Makefile Manual](https://www.gnu.org/software/make/manual/make.pdf)

* [Skynet a lightweight framework](https://github.com/cloudwu/skynet)

* [Github](https://github.com/BlessedChild/Dominate_Skynet)

### 开始编码

* 解读内容暂时使用英文，并以注释的方式合并在Makefile文件里

Makefile
``` makefile
# if(PLAT=macosx)
# do
# make ./skynet cservice/snlua.so cservice/logger.so cservice/gate.so cservice/harbor.so luaclib/skynet.so luaclib/client.so luaclib/bson.so luaclib/md5.so luaclib/sproto.so
# luaclib/lpeg.so PLAT=macosx SKYNET_LIBS="-lpthread -lm -ldl" SHARED="-fPIC -dynamiclib -Wl,-undefined,dynamic_lookup" EXPORT="" MALLOC_STATICLIB="" SKYNET_DEFINES=-"DNOUSE_JEMALLOC"
include platform.mk

# LUA_CLIB_PATH = luaclib
LUA_CLIB_PATH ?= luaclib

# CSERVICE_PATH = cservice
CSERVICE_PATH ?= cservice

# SKYNET_BUILD_PATH = .
SKYNET_BUILD_PATH ?= .

# CFLAGS = -g -O2 -Wall -I3rd/lua $(MYCFLAGS)
CFLAGS = -g -O2 -Wall -I3rd/lua $(MYCFLAGS)
# CFLAGS += -DUSE_PTHREAD_LOCK

# lua
# LUA_STATICLIB = 3rd/lua/liblua.a
# LUA_LIB = 3rd/lua/liblua.a
# LUA_INC = 3rd/lua
LUA_STATICLIB := 3rd/lua/liblua.a
LUA_LIB ?= $(LUA_STATICLIB)
LUA_INC ?= 3rd/lua

# LUA_STATICLIB = cd 3rd/lua && make CC='gcc -std=gnu99' macosx
$(LUA_STATICLIB) :
	cd 3rd/lua && $(MAKE) CC='$(CC) -std=gnu99' $(PLAT)

# jemalloc 
# JEMALLOC_STATICLIB = 3rd/jemalloc/lib/libjemalloc_pic.a
# JEMALLOC_INC = 3rd/jemalloc/include/jemalloc
JEMALLOC_STATICLIB := 3rd/jemalloc/lib/libjemalloc_pic.a
JEMALLOC_INC := 3rd/jemalloc/include/jemalloc

# make jemalloc
# if(3rd/jemalloc/Makefile)
# do
# cd 3rd/jemalloc && make CC=gcc
all : jemalloc
	
.PHONY : jemalloc update3rd

# MALLOC_STATICLIB = 3rd/jemalloc/lib/libjemalloc_pic.a
MALLOC_STATICLIB := $(JEMALLOC_STATICLIB)

# fun: 3rd/jemalloc/lib/libjemalloc_pic.a
# if(3rd/jemalloc/Makefile != null)
# do
# cd 3rd/jemalloc && make CC=gcc
# do
# Maybe => 3rd/jemalloc/autogen.sh
# do
# Maybe => 3rd/jemalloc/Makefile
$(JEMALLOC_STATICLIB) : 3rd/jemalloc/Makefile
	cd 3rd/jemalloc && $(MAKE) CC=$(CC) 

# fun: 3rd/jemalloc/autogen.sh
# do
# git submodule update --init
3rd/jemalloc/autogen.sh :
	git submodule update --init

# fun: 3rd/jemalloc/Makefile
# if(3rd/jemalloc/autogen.sh)
# do
# cd 3rd/jemalloc && ./autogen.sh --with-jemalloc-prefix=je_ --disable-valgrind
3rd/jemalloc/Makefile : | 3rd/jemalloc/autogen.sh
	cd 3rd/jemalloc && ./autogen.sh --with-jemalloc-prefix=je_ --disable-valgrind

# if()
jemalloc : $(MALLOC_STATICLIB)

update3rd :
	rm -rf 3rd/jemalloc && git submodule update --init

# skynet

CSERVICE = snlua logger gate harbor
LUA_CLIB = skynet \
  client \
  bson md5 sproto lpeg

LUA_CLIB_SKYNET = \
  lua-skynet.c lua-seri.c \
  lua-socket.c \
  lua-mongo.c \
  lua-netpack.c \
  lua-memory.c \
  lua-profile.c \
  lua-multicast.c \
  lua-cluster.c \
  lua-crypt.c lsha1.c \
  lua-sharedata.c \
  lua-stm.c \
  lua-mysqlaux.c \
  lua-debugchannel.c \
  lua-datasheet.c \
  \

SKYNET_SRC = skynet_main.c skynet_handle.c skynet_module.c skynet_mq.c \
  skynet_server.c skynet_start.c skynet_timer.c skynet_error.c \
  skynet_harbor.c skynet_env.c skynet_monitor.c skynet_socket.c socket_server.c \
  malloc_hook.c skynet_daemon.c skynet_log.c

# make ./skynet 
# make cservice/snlua.so
# make cservice/logger.so
# make cservice/gate.so
# make cservice/harbor.so
# make luaclib/skynet.so
# make luaclib/client.so
# make luaclib/bson.so
# make luaclib/md5.so
# make luaclib/sproto.so
# make luaclib/lpeg.so
all : \
  $(SKYNET_BUILD_PATH)/skynet \
  $(foreach v, $(CSERVICE), $(CSERVICE_PATH)/$(v).so) \
  $(foreach v, $(LUA_CLIB), $(LUA_CLIB_PATH)/$(v).so) 

# all: library.cpp main.cpp
# $@ => all
# $< => library.cpp
# $^ => library.cpp main.cpp
# ---
# CFLAGS stands for compiler flags
# LDFLAGS for linker flags (the linker is ld)
# ---
# fun: ./skynet
# if(skynet-src/SKYNET_SRC) && 3rd/lua/liblua.a && 3rd/jemalloc/lib/libjemalloc_pic.a)
# do
# gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -o ./skynet skynet-src/skynet_main.c skynet-src/skynet_main.c skynet-src/skynet_handle.c 
# skynet-src/skynet_module.c skynet-src/skynet_mq.c skynet-src/skynet_server.c skynet-src/skynet_start.c 
# skynet-src/skynet_timer.c skynet-src/skynet_error.c skynet-src/skynet_harbor.c skynet-src/skynet_env.c 
# skynet-src/skynet_monitor.c skynet-src/skynet_socket.c skynet-src/socket_server.c skynet-src/malloc_hook.c 
# skynet-src/skynet_daemon.c skynet-src/skynet_log.c 3rd/lua/liblua.a 3rd/jemalloc/lib/libjemalloc_pic.a
# -Iskynet-src -I3rd/jemalloc/include/jemalloc $(LDFLAGS) -lpthread -lm -ldl DNOUSE_JEMALLOC
# generate ./skynet
$(SKYNET_BUILD_PATH)/skynet : $(foreach v, $(SKYNET_SRC), skynet-src/$(v)) $(LUA_LIB) $(MALLOC_STATICLIB)
	$(CC) $(CFLAGS) -o $@ $^ -Iskynet-src -I$(JEMALLOC_INC) $(LDFLAGS) $(EXPORT) $(SKYNET_LIBS) $(SKYNET_DEFINES)

# mkdir luaclib
$(LUA_CLIB_PATH) :
	mkdir $(LUA_CLIB_PATH)

# mkdir cservice
$(CSERVICE_PATH) :
	mkdir $(CSERVICE_PATH)

# $(CSERVICE_PATH)/$(1).so : service-src/service_$(1).c | $(CSERVICE_PATH)
# $(CC) $(CFLAGS) $(SHARED) $< -o $@ -Iskynet-src
define CSERVICE_TEMP
  $$(CSERVICE_PATH)/$(1).so : service-src/service_$(1).c | $$(CSERVICE_PATH)
	$$(CC) $$(CFLAGS) $$(SHARED) $$< -o $$@ -Iskynet-src
endef

# eval => do make
# => make CSERVICE_TEMP
# ---
# $(CSERVICE) = snlua logger gate harbor
# ---
# => cservice/snlua.so : service-src/service_snlua.c | cservice
#    gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -fPIC -dynamiclib -Wl,-undefined,dynamic_lookup
#    (service-src/service_snlua.c | cservice) -o cservice/snlua.so -Iskynet-src
# => cservice/logger.so : service-src/service_logger.c | cservice
#    gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -fPIC -dynamiclib -Wl,-undefined,dynamic_lookup
#    (service-src/service_logger.c | cservice) -o cservice/logger.so -Iskynet-src
# => cservice/gate.so : service-src/service_gate.c | cservice
#    gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -fPIC -dynamiclib -Wl,-undefined,dynamic_lookup
#    (service-src/service_gate.c | cservice) -o cservice/gate.so -Iskynet-src
# => cservice/harbor.so : service-src/service_harbor.c | cservice
#    gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -fPIC -dynamiclib -Wl,-undefined,dynamic_lookup
#    (service-src/service_harbor.c | cservice) -o cservice/harbor.so -Iskynet-src
# generate snlua.so logger.so gate.so harbor.so in the cservice file
$(foreach v, $(CSERVICE), $(eval $(call CSERVICE_TEMP,$(v))))

# fun: luaclib/skynet.so
# if(macsox)
# if((lua-skynet.c && lua-seri.c && lua-socket.c && lua-mongo.c && lua-netpack.c && 
#     lua-memory.c && lua-profile.c && lua-multicast.c && lua-cluster.c &&
#     lua-crypt.c && lsha1.c && lua-sharedata.c && lua-stm.c && lua-mysqlaux.c && 
#     lua-debugchannel.c && lua-datasheet.c) | luaclib != null)
# do
# gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -fPIC -dynamiclib -Wl,-undefined,dynamic_lookup
# ((lua-skynet.c lua-seri.c lua-socket.c lua-mongo.c lua-netpack.c lua-memory.c lua-profile.c
# lua-multicast.c lua-cluster.c lua-crypt.c lsha1.c lua-sharedata.c lua-stm.c lua-mysqlaux.c
# lua-debugchannel.c lua-datasheet.c) | luaclib) -o luaclib/skynet.so -Iskynet-src -Iservice-src -Ilualib-src
# generate luaclib/skynet.so 
$(LUA_CLIB_PATH)/skynet.so : $(addprefix lualib-src/,$(LUA_CLIB_SKYNET)) | $(LUA_CLIB_PATH)
	$(CC) $(CFLAGS) $(SHARED) $^ -o $@ -Iskynet-src -Iservice-src -Ilualib-src

# fun: luaclib/bson.so
# make luaclib/bson.o
# if(lualib-src/lua-bson.c | luaclib)
# gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -fPIC --shared -Iskynet-src
# (lualib-src/lua-bson.c | luaclib) -o luaclib/bson.o -Iskynet-src
# generate luaclib/bson.o
$(LUA_CLIB_PATH)/bson.so : lualib-src/lua-bson.c | $(LUA_CLIB_PATH)
	$(CC) $(CFLAGS) $(SHARED) -Iskynet-src $^ -o $@ -Iskynet-src

# fun: luaclib/md5.so
# if(3rd/lua-md5/md5.c && 3rd/lua-md5/md5lib.c && (3rd/lua-md5/compat-5.2.c | luaclib))
# do
# gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -fPIC -dynamiclib -Wl,-undefined,dynamic_lookup
# -I3rd/lua-md5 3rd/lua-md5/md5.c 3rd/lua-md5/md5lib.c (3rd/lua-md5/compat-5.2.c | luaclib) -o luaclib/md5.so
# generate luaclib/md5.so
$(LUA_CLIB_PATH)/md5.so : 3rd/lua-md5/md5.c 3rd/lua-md5/md5lib.c 3rd/lua-md5/compat-5.2.c | $(LUA_CLIB_PATH)
	$(CC) $(CFLAGS) $(SHARED) -I3rd/lua-md5 $^ -o $@ 

# fun: luaclib/client.so
# if(lualib-src/lua-clientsocket.c && lualib-src/lua-crypt.c && (lualib-src/lsha1.c | luaclib))
# do
# gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -fPIC -dynamiclib -Wl,-undefined,dynamic_lookup lualib-src/lua-clientsocket.c &&
# lualib-src/lua-crypt.c && (lualib-src/lsha1.c | luaclib) -o luaclib/client.so -lpthread
# generate luaclib/client.so
$(LUA_CLIB_PATH)/client.so : lualib-src/lua-clientsocket.c lualib-src/lua-crypt.c lualib-src/lsha1.c | $(LUA_CLIB_PATH)
	$(CC) $(CFLAGS) $(SHARED) $^ -o $@ -lpthread

# fun: luaclib/sproto.so
# if(lualib-src/sproto/sproto.c (lualib-src/sproto/lsproto.c | luaclib))
# do
# gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -fPIC -dynamiclib -Wl,-undefined,dynamic_lookup -Ilualib-src/sproto
# lualib-src/sproto/sproto.c (lualib-src/sproto/lsproto.c | luaclib) -o luaclib/sproto.so
# generate luaclib/sproto.so
$(LUA_CLIB_PATH)/sproto.so : lualib-src/sproto/sproto.c lualib-src/sproto/lsproto.c | $(LUA_CLIB_PATH)
	$(CC) $(CFLAGS) $(SHARED) -Ilualib-src/sproto $^ -o $@ 

# fun: luaclib/lpeg.so
# if(3rd/lpeg/lpcap.c 3rd/lpeg/lpcode.c 3rd/lpeg/lpprint.c 3rd/lpeg/lptree.c (3rd/lpeg/lpvm.c | luaclib))
# do
# gcc -g -O2 -Wall -I3rd/lua $(MYCFLAGS) -fPIC -dynamiclib -Wl,-undefined,dynamic_lookup -I3rd/lpeg 3rd/lpeg/lpcap.c
# 3rd/lpeg/lpcode.c 3rd/lpeg/lpprint.c 3rd/lpeg/lptree.c (3rd/lpeg/lpvm.c | luaclib) -o luaclib/lpeg.so
# generate luaclib/lpeg.so
$(LUA_CLIB_PATH)/lpeg.so : 3rd/lpeg/lpcap.c 3rd/lpeg/lpcode.c 3rd/lpeg/lpprint.c 3rd/lpeg/lptree.c 3rd/lpeg/lpvm.c | $(LUA_CLIB_PATH)
	$(CC) $(CFLAGS) $(SHARED) -I3rd/lpeg $^ -o $@ 

# rm -f ./skynet cservice/*.so luaclib/*.so
clean :
	rm -f $(SKYNET_BUILD_PATH)/skynet $(CSERVICE_PATH)/*.so $(LUA_CLIB_PATH)/*.so

# if(clean != null)
# do
#   if("search Makefile in 3rd/jemalloc/ and return Makefile" != null)
#   do
#   cd 3rd/jemalloc && rm -f ./skynet cservice/*.so luaclib/*.so && rm Makefile
#   do
#   cd 3rd/lua && rm -f ./skynet cservice/*.so luaclib/*.so
#	  rm -f 3rd/lua/liblua.a
cleanall: clean
ifneq (,$(wildcard 3rd/jemalloc/Makefile))
	cd 3rd/jemalloc && $(MAKE) clean && rm Makefile
endif
	cd 3rd/lua && $(MAKE) clean
	rm -f 3rd/lua/liblua.a
```

platfrom.mk
``` makefile
# if(PLAT == null)
# do
# PLAT = none
# else if(PLAT != null)
# return PLAT
PLAT ?= none

# PLATS="linux freebsd macosx"
PLATS = linux freebsd macosx

# if(CC == null)
# do
# CC = gcc
# else if(CC != null)
# do
# return CC
CC ?= gcc

# super none
# super $(PLATS)
# super clean
# super all
# super cleanall 
.PHONY : none $(PLATS) clean all cleanall

#ifneq ($(PLAT), none)
# super default
.PHONY : default

# make macosx
default :
	$(MAKE) $(PLAT)

#endif

none :
	@echo "Please do 'make PLATFORM' where PLATFORM is one of these:"
	@echo "   $(PLATS)"

SKYNET_LIBS := -lpthread -lm
SHARED := -fPIC --shared
EXPORT := -Wl,-E

linux : PLAT = linux
macosx : PLAT = macosx
freebsd : PLAT = freebsd

macosx : SHARED := -fPIC -dynamiclib -Wl,-undefined,dynamic_lookup
macosx : EXPORT :=
macosx linux : SKYNET_LIBS += -ldl
linux freebsd : SKYNET_LIBS += -lrt

# Turn off jemalloc and malloc hook on macosx

macosx : MALLOC_STATICLIB :=
macosx : SKYNET_DEFINES :=-DNOUSE_JEMALLOC

# ./skynet cservice/snlua.so cservice/logger.so cservice/gate.so cservice/harbor.so luaclib/skynet.so luaclib/client.so luaclib/bson.so luaclib/md5.so luaclib/sproto.so
# luaclib/lpeg.so PLAT=macosx SKYNET_LIBS="-lpthread -lm -ldl" SHARED="-fPIC -dynamiclib -Wl,-undefined,dynamic_lookup" EXPORT="" MALLOC_STATICLIB="" SKYNET_DEFINES=-"DNOUSE_JEMALLOC"
linux macosx freebsd :
	$(MAKE) all PLAT=$@ SKYNET_LIBS="$(SKYNET_LIBS)" SHARED="$(SHARED)" EXPORT="$(EXPORT)" MALLOC_STATICLIB="$(MALLOC_STATICLIB)" SKYNET_DEFINES="$(SKYNET_DEFINES)"
```

* 至此，完成了对skynet框架Makefile的基本解读。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
