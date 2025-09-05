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
              -std=c++11 \
              -Wno-unused-parameter \
              -Dstrlcpy=g_strlcpy \
              -Dstrlcat=g_strlcat

library_includedir := $(pkgincludedir)

lib_LTLIBRARIES := libaidl_common.la

libaidl_common_la_SOURCES := \
    generate_cpp.cpp \
    generate_java.cpp \
    generate_java_binder.cpp \
    ast_cpp.cpp \
    ast_java.cpp \
    code_writer.cpp \
    import_resolver.cpp \
    line_reader.cpp \
    io_delegate.cpp \
    options.cpp \
    type_cpp.cpp \
    type_java.cpp \
    type_namespace.cpp \
    aidl_language_y.yy

if USE_GLIB
libaidl_common_la_SOURCES += $(c_sources) $(h_sources)
libaidl_common_la_CFLAGS := $(AM_CFLAGS) $(UE_CFLAGS) -DUSE_GLIB @GLIB_CFLAGS@
libaidl_common_la_CPPFLAGS := $(AM_CPPFLAGS) -DUSE_GLIB @GLIB_CFLAGS@
libaidl_common_la_LIBADD := -lm -lpthread -lbase -llog -lcutils @GLIB_LIBS@
libaidl_common_la_LDFLAGS := -shared -version-info 1:0:0
else
libaidl_common_la_SOURCES += $(c_sources) $(h_sources)
libaidl_common_la_CFLAGS := $(AM_CFLAGS)
libaidl_common_la_CPPFLAGS := $(AM_CPPFLAGS)
libaidl_common_la_LIBADD := -lm -lpthread -lbase -llog -lcutils
libaidl_common_la_LDFLAGS := -shared -version-info 1:0:0
endif

if BISON
libaidl_common_la_CPPFLAGS += -DBISON
endif
library_includedir = $(includedir)
library_include_HEADERS = aidl_language_y.hh
library_include_HEADERS += aidl_language.h
library_include_HEADERS += aidl.h
library_include_HEADERS += io_delegate.h
library_include_HEADERS += line_reader.h
library_include_HEADERS += ast_cpp.h
library_include_HEADERS += code_writer.h
library_include_HEADERS += generate_cpp.h
library_include_HEADERS += import_resolver.h
library_include_HEADERS += ast_java.h
library_include_HEADERS += logging.h
library_include_HEADERS += generate_java.h
library_include_HEADERS += type_java.h
library_include_HEADERS += options.h
library_include_HEADERS += os.h
library_include_HEADERS += type_cpp.h
library_include_HEADERS += type_namespace.h
