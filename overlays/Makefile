# your kernel sources
STAGING_KERNEL_DIR ?= $(INSTALL_MOD_PATH)/lib/modules/$(KERNELRELEASE)/source/

# kernel output (if building out-of-tree)
KBUILD_OUTPUT ?= $(STAGING_KERNEL_DIR)

DTC_FLAGS := -@

# we have dtbos in arm and arm64 architecture, set the include paths
# to include both architectures.
KERNEL_INCLUDE = " \
    ${STAGING_KERNEL_DIR}/arch/arm/boot/dts/ \
    ${STAGING_KERNEL_DIR}/arch/arm64/boot/dts/*/ \
"

DTS_INCLUDES := $(patsubst %,-I%,$(dir $(wildcard $(KERNEL_INCLUDE))))

HOSTCC := gcc $(DTS_INCLUDES)

PWD := $(shell pwd)

dtb-y += imx8mm-mez_20mhz_can1.dtbo
dtb-y += imx8mm-mez_disable_can1.dtbo
dtb-y += imx8mm-mez_dsi-to-hdmi_overlay.dtbo
dtb-y += imx8mm-mez_hmp_overlay.dtbo
dtb-y += imx8mm-mez_mipi-dsi-to-sn65dsi84.dtbo
dtb-y += imx8mm-mez_nau8822-btl_overlay.dtbo
dtb-y += imx8mm-mez_ov5640_overlay.dtbo
dtb-y += imx8mm-mez_panel-cap-touch-10inch-dsi_overlay.dtbo
dtb-y += imx8mm-mez_spidev_overlay.dtbo

targets += $(dtb-y)
always  := $(dtb-y)

# adopted to dtbo from scripts/Makefile.lib
$(obj)/%.dtbo: $(src)/%.dts $(DTC) FORCE
	$(call if_changed_dep,dtc,dtb)

all:
	make -C $(KBUILD_OUTPUT) M=$(PWD)

clean:
	make -C $(KBUILD_OUTPUT) M=$(PWD) clean
