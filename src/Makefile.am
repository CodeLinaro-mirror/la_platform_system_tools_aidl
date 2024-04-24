ACLOCAL_AMFLAGS := -I m4

AM_CFLAGS := -Wundef \
        -Wstrict-prototypes \
        -Wno-trigraphs \
        -g -O0 \
        -fno-inline \
        -fno-short-enums \
        -fpic \
        -D_GNU_SOURCE

AM_YFLAGS := -v -d
AM_CPPFLAGS := \
              -DUSE_LE_MODE \
              -I. \
              -I$(WORKSPACE)/system/core/include \
              -I$(WORKSPACE)/system/core/base/include \
              -I$(WORKSPACE)/system/core/fs_mgr/include \
              -I$(WORKSPACE)/OTA/system/core/base/include \
              -std=c++14 \
              -Wno-unused-parameter \
              -Dstrlcpy=g_strlcpy \
              -Dstrlcat=g_strlcat

AM_LDFLAGS := -shared -version-info 1:0:0
library_includedir := $(pkgincludedir)

aidl_cpp_src_file := \
    aidl_language_l.ll \
    main_cpp.cpp \
    aidl.cpp \
    aidl_language.cpp

aidl_cpp_SOURCES := $(aidl_cpp_src_file)

if USE_GLIB
aidl_cpp_CFLAGS := $(AM_CFLAGS) -DRECOVERY_API_VERSION=$(RECOVERY_API_VERSION) -DUSE_GLIB @GLIB_CFLAGS@
aidl_cpp_CPPFLAGS := $(AM_CPPFLAGS) -DRECOVERY_API_VERSION=$(RECOVERY_API_VERSION) -DUSE_GLIB @GLIB_CFLAGS@
aidl_cpp_LDADD := -lm -lpthread -laidl_common -lbase -lcutils @GLIB_LIBS@
else
aidl_cpp_CFLAGS := $(AM_CFLAGS)  -DRECOVERY_API_VERSION=$(RECOVERY_API_VERSION)
aidl_cpp_CPPFLAGS :=  $(AM_CPPFLAGS) -DRECOVERY_API_VERSION=$(RECOVERY_API_VERSION)
aidl_cpp_LDADD := -lm -lpthread -lbase -lcutils -laidl_common
endif
bin_PROGRAMS = aidl_cpp
