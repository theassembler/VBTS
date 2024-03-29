

# List of all supported boards (meant to be overridden on command line)
BOARDS?=compal_e88 compal_e86 compal_e99 se_j100 gta0x pirelli_dpl10

# List of all applications (meant to be overridden on command line)
APPLICATIONS?=hello_world compal_dsp_dump layer1 loader chainload


# TI Calypso

calypso_COMMON_OBJS=board/common/calypso_uart.o board/common/calypso_pwl.o

# OpenMoko GTA0x

gta0x_OBJS=$(calypso_COMMON_OBJS) board/gta0x/rffe_gta0x_triband.o board/gta0x/init.o board/gta0x/rf_power.o
gta0x_ENVIRONMENTS=highram

# Pirelli DP-L10

pirelli_dpl10_OBJS=$(calypso_COMMON_OBJS) board/pirelli_dpl10/rffe_dpl10_triband.o board/pirelli_dpl10/init.o board/pirelli_dpl10/rf_power.o
pirelli_dpl10_ENVIRONMENTS=highram

# Compal Generic

compal_COMMON_OBJS=$(calypso_COMMON_OBJS) board/compal/rffe_dualband.o board/compal/rf_power.o
compal_COMMON_ENVIRONMENTS=compalram highram

compalram_LDS=board/compal/ram.lds
compalram_OBJS=board/compal/start.ram.o board/compal/exceptions_redirected.o board/compal/handlers.o

highram_LDS=board/compal/highram.lds
highram_OBJS=board/compal/start.ram.o board/compal/exceptions_redirected.o board/compal/handlers.o

# Compal E88

compal_e88_OBJS=$(compal_COMMON_OBJS) board/compal_e88/init.o
compal_e88_ENVIRONMENTS=$(compal_COMMON_ENVIRONMENTS) e88loader e88flash

e88loader_LDS=board/compal_e88/loader.lds
e88loader_OBJS=board/compal/start.rom.o board/compal/header.o board/compal/exceptions_redirect.o

e88flash_LDS=board/compal_e88/flash.lds
e88flash_OBJS=board/compal/start.rom.o board/compal/header.o board/compal/exceptions_redirected.o board/compal/handlers.o

# Compal E86 (has a different RFFE configuration)

compal_e86_OBJS=$(calypso_COMMON_OBJS) board/compal_e86/rffe_dualband_e86.o board/compal/rf_power.o board/compal_e86/init.o
compal_e86_ENVIRONMENTS=$(compal_COMMON_ENVIRONMENTS)

# Compal E99

compal_e99_OBJS=$(compal_COMMON_OBJS) board/compal_e99/init.o
compal_e99_ENVIRONMENTS=$(compal_COMMON_ENVIRONMENTS)

e99loader_LDS=board/compal_e99/loader.lds
e99loader_OBJS=board/compal/header.o
e99flash_LDS=board/compal_e99/flash.lds

# Sony Ericsson J100 (made by Compal)

se_j100_OBJS=$(compal_COMMON_OBJS) board/se_j100/init.o
se_j100_ENVIRONMENTS=$(compal_COMMON_ENVIRONMENTS)

# Global include path
INCLUDES=-Iinclude/ -I../../../include -I../../shared/libosmocore/include

# Various objects that are currently linked into all applications
FLASH_OBJS=flash/cfi_flash.o
DISPLAY_OBJS=display/font_r8x8.o display/font_r8x8_horiz.o display/st7558.o display/td014.o display/ssd1783.o display/ssd1963.o display/display.o
ABB_OBJS=abb/twl3025.o
RF_OBJS=rf/trf6151.o

# Objects that go in all applications
ANY_APP_OBJS+=$(ABB_OBJS) $(RF_OBJS) $(DISPLAY_OBJS) $(FLASH_OBJS)
ANY_APP_LIBS+=calypso/libcalypso.a layer1/liblayer1.a lib/libmini.a comm/libcomm.a ../../shared/libosmocore/build-target/src/.libs/libosmocore.a ../../shared/libosmocore/build-target/src/gsm/.libs/libosmogsm.a

# Libraries are defined in subdirectories
-include calypso/Makefile
-include layer1/Makefile
-include comm/Makefile
-include lib/Makefile

# Include rules
-include Makefile.inc

# Uncomment this line if you want to enable Tx (Transmit) Support.
CFLAGS += -DCONFIG_TX_ENABLE

# Uncomment this line if you want to write to flash.
#CFLAGS += -DCONFIG_FLASH_WRITE

# Uncomment this line if you want to write to flash, including the bootloader.
#CFLAGS += -DCONFIG_FLASH_WRITE_LOADER
