Target := my_game

Sources := $(wildcard ./src/*.cpp)

Zip :=	irrlicht-1.8.4.zip
LibName :=	irrlicht-1.8.4

IrrlichtHome := ./$(LibName)/

BinPath = .

USERCPPFLAGS =

USERCXXFLAGS = -O3 -ffast-math

USERLDFLAGS =


CPPFLAGS = -I$(IrrlichtHome)/include -I/usr/X11R6/include $(USERCPPFLAGS)
CXXFLAGS = $(USERCXXFLAGS)
LDFLAGS = $(USERLDFLAGS)

all: all_linux

all_linux all_win32 static_win32: LDFLAGS += -L$(IrrlichtHome)/lib/$(SYSTEM) -lIrrlicht
all_linux: LDFLAGS += -L/usr/X11R6/lib$(LIBSELECT) -lGL -lXxf86vm -lXext -lX11 -lXcursor
all_linux clean_linux: SYSTEM=Linux
all_win32 clean_win32 static_win32: SYSTEM=Win32-gcc
all_win32 clean_win32 static_win32: SUF=.exe
static_win32: CPPFLAGS += -D_IRR_STATIC_LIB_
all_win32: LDFLAGS += -lopengl32 -lm
static_win32: LDFLAGS += -lgdi32 -lwinspool -lcomdlg32 -lole32 -loleaut32 -luuid -lodbc32 -lodbccp32 -lopengl32
DESTPATH = $(BinPath)/$(Target)$(SUF)

all_linux all_win32 static_win32:
	$(warning Building...)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) $(Sources) -o $(DESTPATH) $(LDFLAGS)

clean: clean_linux clean_win32
	$(warning Cleaning...)

clean_linux clean_win32:
	@$(RM) $(DESTPATH)

re:	clean all

install:
	unzip	$(Zip)
	@(cd ./$(LibName)/source/Irrlicht/ && $(MAKE))

uninstall:
	rm -rf ./$(LibName)

.PHONY: all all_win32 static_win32 clean clean_linux clean_win32 re install uninstall

ifeq ($(HOSTTYPE), x86_64)
LIBSELECT=64
endif

ifeq ($(HOSTTYPE), sun4)
LDFLAGS += -lrt
endif
