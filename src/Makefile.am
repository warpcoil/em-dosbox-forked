AM_CPPFLAGS = -I$(top_srcdir)/include

SUBDIRS = cpu debug dos fpu gui hardware libs ints misc shell platform 

bin_PROGRAMS = dosbox

if HAVE_WINDRES
ico_stuff = winres.rc
endif

.rc.o:
	$(WINDRES) -o $@ $<

dosbox_SOURCES = dosbox.cpp $(ico_stuff)
dosbox_LDADD = cpu/libcpu.a debug/libdebug.a dos/libdos.a fpu/libfpu.a  hardware/libhardware.a gui/libgui.a \
               ints/libints.a misc/libmisc.a shell/libshell.a hardware/mame/libmame.a \
               hardware/serialport/libserial.a libs/gui_tk/libgui_tk.a

EXTRA_DIST = winres.rc dosbox.ico

if EMSCRIPTEN_BUILD
dosbox_LDFLAGS=-s TOTAL_MEMORY=134217728 -s ALLOW_MEMORY_GROWTH=0
CLEANFILES=dosbox.js dosbox.html.mem dosbox.js.orig.js dosbox.js.tmp.js
#if EMTERPRETER
#dosbox_LDFLAGS+=-s EMTERPRETIFY=1 -s EMTERPRETIFY_ASYNC=1 -s EMTERPRETIFY_WHITELIST=@emterpretify.txt -s FETCH=1
#EXTRA_dosbox_DEPENDENCIES=emterpretify.txt
#else
# Memory init file is huge and it doesn't save bandwith even if using gzip.
# It is only required when using emterpreter.
#dosbox_LDFLAGS+=--memory-init-file 0
#endif
if WEBASSEMBLY
dosbox_LDFLAGS+=-s WASM=1 -s FORCE_FILESYSTEM=1 -s FETCH=1 -s ASYNCIFY -s DISABLE_DEPRECATED_FIND_EVENT_TARGET_BEHAVIOR=0 --shell-file ../shells/shell_minimal_mod.html
endif
endif

