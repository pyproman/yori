
MODULES=\
	for.com

BINARIES=yfor.exe

!INCLUDE "..\config\common.mk"

!IF $(PDB)==1
LINKPDB=/Pdb:yfor.pdb
!ENDIF

CFLAGS=$(CFLAGS) -DFOR_VER_MAJOR=$(FOR_VER_MAJOR) -DFOR_VER_MINOR=$(FOR_VER_MINOR)

BIN_OBJS=\
	for.obj        \

MOD_OBJS=\
	mod_for.obj    \

compile: $(BIN_OBJS) builtins.lib

yfor.exe: $(BIN_OBJS) $(YORILIB) $(YORICRT) $(YORISH)
	@echo $@
	@$(LINK) $(LDFLAGS) -entry:$(YENTRY) $(BIN_OBJS) $(LIBS) $(CRTLIB) $(YORILIB) $(YORISH) -version:$(FOR_VER_MAJOR).$(FOR_VER_MINOR) $(LINKPDB) -out:$@

mod_for.obj: for.c
	@echo $@
	@cl -c -DYORI_BUILTIN=1 $(CFLAGS) -Fo$@ for.c

builtins.lib: $(MOD_OBJS)
	@echo $@
	@$(LIB32) $(LIBFLAGS) $(MOD_OBJS) -out:$@

for.com: $(MOD_OBJS)
	@echo $@
	@$(LINK) $(LDFLAGS) $(MOD_OBJS) -dll -version:$(YORI_VER_MAJOR).$(YORI_VER_MINOR) $(LIBS) $(CRTLIB) $(YORILIB) $(YORISH) -def:for.def -out:$@
