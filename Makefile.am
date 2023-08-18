ACLOCAL_AMFLAGS := -I m4

AM_CFLAGS := -Wundef \
        -Wstrict-prototypes \
        -Wno-trigraphs \
        -g -O0 \
        -fno-inline \
        -fno-short-enums \
        -fpic \
        -D_GNU_SOURCE

#AM_LEXFLAGS := -x c

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

AM_LDFLAGS := -shared -version-info 1:0:0
library_includedir := $(pkgincludedir)

lib_LTLIBRARIES := libaidl_common.la

libaidl_common_la_SOURCES := \
    aidl_language_y.yy \
    aidl_language_l.ll \
    aidl.cpp \
    ast_cpp.cpp \
    ast_java.cpp \
    code_writer.cpp \
    generate_cpp.cpp \
    generate_java.cpp \
    generate_java_binder.cpp \
    import_resolver.cpp \
    line_reader.cpp \
    io_delegate.cpp \
    options.cpp \
    type_cpp.cpp \
    type_java.cpp \
    type_namespace.cpp \
    aidl_language.cpp



if USE_GLIB
libaidl_common_la_SOURCES += $(c_sources) $(h_sources)
libaidl_common_la_CFLAGS := $(AM_CFLAGS) $(UE_CFLAGS) -DUSE_GLIB @GLIB_CFLAGS@
libaidl_common_la_CPPFLAGS := $(AM_CPPFLAGS) -DUSE_GLIB @GLIB_CFLAGS@
libaidl_common_la_LIBADD := -lm -lpthread -lbase -lcutils @GLIB_LIBS@
libaidl_common_la_LDFLAGS := -all-static
else
libaidl_common_la_SOURCES += $(c_sources) $(h_sources)
libaidl_common_la_CFLAGS := $(AM_CFLAGS)
libaidl_common_la_CPPFLAGS := $(AM_CPPFLAGS)
libaidl_common_la_LIBADD := -lm -lpthread -lbase -lcutils
#libaidl_common_la_LDFLAGS := -all-static
endif


aidl_cpp_src_file := main_cpp.cpp

aidl_cpp_SOURCES := $(aidl_src) $(aidl_cpp_src_file)

aidl_cpp_CFLAGS := $(AM_CFLAGS)


if USE_GLIB
aidl_cpp_CFLAGS := $(AM_CFLAGS) -DRECOVERY_API_VERSION=$(RECOVERY_API_VERSION) -DUSE_GLIB @GLIB_CFLAGS@
aidl_cpp_CPPFLAGS := $(AM_CPPFLAGS) -DRECOVERY_API_VERSION=$(RECOVERY_API_VERSION) -DUSE_GLIB @GLIB_CFLAGS@
aidl_cpp_LDADD := -lm -lpthread ./libaidl_common.la -lbase -lcutils @GLIB_LIBS@
else
aidl_cpp_CFLAGS := $(AM_CFLAGS)  -DRECOVERY_API_VERSION=$(RECOVERY_API_VERSION)
aidl_cpp_CPPFLAGS :=  $(AM_CPPFLAGS) -DRECOVERY_API_VERSION=$(RECOVERY_API_VERSION)
aidl_cpp_LDADD := -lm -lpthread -lbase -lcutils ./libaidl_common.la
endif
bin_PROGRAMS = aidl_cpp
