KERNEL_SRC ?= /lib/modules/$(shell uname -r)/build

M ?= $(shell pwd)
DATARMNET_CORE_PATH := datarmnet/core
RMNET_CORE_PATH := $(DATARMNET_CORE_PATH)
#absolute path to the build directory. Can't use $(TOP) here since
#that resolves to ., and we pass this to Kbuild, where . is different
RMNET_CORE_INC_DIR := $(abspath $(M)/../../../../$(DATARMNET_CORE_PATH))

#pass variables down to Kbuild environment
KBUILD_OPTIONS := RMNET_CORE_INC_DIR=$(RMNET_CORE_INC_DIR)
KBUILD_OPTIONS += RMNET_CORE_PATH=$(RMNET_CORE_PATH)
KBUILD_OPTIONS += DATARMNET_CORE_PATH=$(DATARMNET_CORE_PATH)

KBUILD_OPTIONS += RMNET_SHS_ROOT=$(PWD)
KBUILD_OPTIONS += MODNAME?=rmnet_shs
KBUILD_EXTRA_SYMBOLS := $(M)/../../$(DATARMNET_CORE_PATH)/Module.symvers

modules:
	$(MAKE) -C $(KERNEL_SRC) M=$(M) modules $(KBUILD_OPTIONS) $(KBUILD_EXTRA_SYMBOLS)

modules_install:
	$(MAKE) INSTALL_MOD_STRIP=1 -C $(KERNEL_SRC) M=$(M) modules_install

clean:
	$(MAKE) -C $(KERNEL_SRC) M=$(M) clean
