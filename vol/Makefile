
BINARIES=yvol.exe

!INCLUDE "..\config\common.mk"

!IF $(PDB)==1
LINKPDB=/Pdb:yvol.pdb
!ENDIF

CFLAGS=$(CFLAGS) -DVOL_VER_MAJOR=$(VOL_VER_MAJOR) -DVOL_VER_MINOR=$(VOL_VER_MINOR)

BIN_OBJS=\
	 vol.obj        \

MOD_OBJS=\
	 mod_vol.obj    \

compile: $(BIN_OBJS) builtins.lib

yvol.exe: $(BIN_OBJS) $(YORILIB) $(YORICRT)
	@echo $@
	@$(LINK) $(LDFLAGS) -entry:$(YENTRY) $(BIN_OBJS) $(LIBS) $(CRTLIB) $(YORILIB) -version:$(VOL_VER_MAJOR).$(VOL_VER_MINOR) $(LINKPDB) -out:$@

mod_vol.obj: vol.c
	@echo $@
	@$(CC) -c -DYORI_BUILTIN=1 $(CFLAGS) -Fo$@ vol.c

builtins.lib: $(MOD_OBJS)
	@echo $@
	@$(LIB32) $(LIBFLAGS) $(MOD_OBJS) -out:$@
