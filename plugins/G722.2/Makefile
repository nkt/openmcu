AC_PLUGIN_DIR=codecs/audio
prefix=/opt/openmcu-ru/lib/ptlib
target_os=linux-gnu

SONAME          = g7222
OBJDIR	        = ./obj

CC		= gcc
CXX		= g++
LDSO		= -shared -Wl,-soname,$(SONAME)
PLUGINEXT	= so
CFLAGS	       += -g -O2 
STDCCFLAGS	= -fPIC -D__STDC_CONSTANT_MACROS
LDFLAGS	       +=
CPPFLAGS       +=
OPTCCFLAGS      = $(CPPFLAGS)
EXTRACFLAGS     =

SRCDIR := AMR-WB
SRCS   := g7222.cxx \
          dec_acelp.c \
          dec_dtx.c \
          dec_gain.c \
          dec_if.c \
          dec_lpc.c \
          dec_main.c \
          dec_rom.c \
          dec_util.c \
          enc_acelp.c \
          enc_dtx.c \
          enc_gain.c \
          enc_if.c \
          enc_lpc.c \
          enc_main.c \
          enc_rom.c \
          enc_util.c \
          if_rom.c

vpath	%.cxx .
vpath	%.c   $(SRCDIR)
vpath	%.o   $(OBJDIR)

$(OBJDIR)/%.o : %.c
	@mkdir -p $(OBJDIR) >/dev/null 2>&1
	$(Q_CC)$(CC) -I../../../include $(STDCCFLAGS) $(OPTCCFLAGS) $(EXTRACFLAGS) $(CFLAGS) -c $< -o $@

$(OBJDIR)/%.o : %.cxx
	@mkdir -p $(OBJDIR) >/dev/null 2>&1
	$(CXX) $(EXTRACCFLAGS) $(STDCCFLAGS) $(OPTCCFLAGS) $(CFLAGS) -c $< -o $@

PLUGIN	= ./$(SONAME)_audio_pwplugin.$(PLUGINEXT)

OBJECTS = $(addprefix $(OBJDIR)/,$(patsubst %.c,%.o,$(patsubst %.cxx,%.o,$(notdir $(SRCS)))))


all: $(PLUGIN)

$(PLUGIN): $(OBJECTS)
ifeq (solaris,$(findstring solaris,$(target_os)))
	$(Q_LD)$(CXX) $(LDSO) $@ -o $@ $^ $(EXTRALIBS)
else
	$(Q_LD)$(CXX) $(LDSO) -o $@ $^ $(EXTRALIBS)
endif

install:
	mkdir -p $(DESTDIR)$(prefix)/$(AC_PLUGIN_DIR)
	install $(PLUGIN) $(DESTDIR)$(prefix)/$(AC_PLUGIN_DIR)

uninstall:
	rm -f $(DESTDIR)$(prefix)/$(AC_PLUGIN_DIR)/$(PLUGIN)

clean:
	rm -f $(OBJECTS) $(PLUGIN)

###########################################
