KVER        ?= $(shell uname -r)
KBASE       := /lib/modules/$(KVER)
KSRC        := $(KBASE)/source
KBUILD      := $(KBASE)/build
MOD_DIR     := $(KBASE)/kernel

# Function for kernel version check
KMAJ = $(shell echo $(KVER) | \
sed -e 's/^\([0-9][0-9]*\)\.[0-9][0-9]*\.[0-9][0-9]*.*/\1/')
KMIN = $(shell echo $(KVER) | \
sed -e 's/^[0-9][0-9]*\.\([0-9][0-9]*\)\.[0-9][0-9]*.*/\1/')
KREV = $(shell echo $(KVER) | \
sed -e 's/^[0-9][0-9]*\.[0-9][0-9]*\.\([0-9][0-9]*\).*/\1/')

kver_ge = $(shell \
echo test | awk '{if($(KMAJ) < $(1)) {print 0} else { \
if($(KMAJ) > $(1)) {print 1} else { \
if($(KMIN) < $(2)) {print 0} else { \
if($(KMIN) > $(2)) {print 1} else { \
if($(KREV) < $(3)) {print 0} else { print 1 } \
}}}}}' \
)

# ----------------------------------------------------------------------------
# drm module - copied from drivers/gpu/drm/Makefile
#

# Configuration
EXTRA_CFLAGS += -DCONFIG_DRM_LIB_RANDOM -DCONFIG_COMPAT -DCONFIG_DRM_PANEL -DCONFIG_PCI \
				-DCONFIG_DRM_LOAD_EDID_FIRMWARE -DCONFIG_DRM_PRIVACY_SCREEN \
				-DCONFIG_DRM_PANEL_ORIENTATION_QUIRKS -DCONFIG_DRM_FBDEV_EMULATION \
				-DCONFIG_DRM_KMS_HELPER -DCONFIG_DRM_GEM_SHMEM_HELPER -DCONFIG_DRM_PANEL_BRIDGE \
				-DCONFIG_DRM_FBDEV_EMULATION -DCONFIG_DRM_KMS_HELPER -DCONFIG_DRM_MIPI_DSI

CFLAGS-$(CONFIG_DRM_USE_DYNAMIC_DEBUG)	+= -DDYNAMIC_DEBUG_MODULE
				
KBUILD_MODPOST_WARN = 1

				
drm-y += \
	drm_aperture.o \
	drm_atomic.o \
	drm_atomic_uapi.o \
	drm_auth.o \
	drm_blend.o \
	drm_bridge.o \
	drm_cache.o \
	drm_client.o \
	drm_client_modeset.o \
	drm_color_mgmt.o \
	drm_connector.o \
	drm_crtc.o \
	drm_displayid.o \
	drm_drv.o \
	drm_dumb_buffers.o \
	drm_edid.o \
	drm_encoder.o \
	drm_file.o \
	drm_fourcc.o \
	drm_framebuffer.o \
	drm_gem.o \
	drm_ioctl.o \
	drm_lease.o \
	drm_managed.o \
	drm_mm.o \
	drm_mode_config.o \
	drm_mode_object.o \
	drm_modes.o \
	drm_modeset_lock.o \
	drm_plane.o \
	drm_prime.o \
	drm_print.o \
	drm_property.o \
	drm_syncobj.o \
	drm_sysfs.o \
	drm_trace_points.o \
	drm_vblank.o \
	drm_vblank_work.o \
	drm_vma_manager.o \
	drm_writeback.o
drm-$(CONFIG_DRM_LEGACY) += \
	drm_agpsupport.o \
	drm_bufs.o \
	drm_context.o \
	drm_dma.o \
	drm_hashtab.o \
	drm_irq.o \
	drm_legacy_misc.o \
	drm_lock.o \
	drm_memory.o \
	drm_scatter.o \
	drm_vm.o
drm-$(CONFIG_DRM_LIB_RANDOM) += lib/drm_random.o
drm-$(CONFIG_COMPAT) += drm_ioc32.o
drm-$(CONFIG_DRM_PANEL) += drm_panel.o
drm-$(CONFIG_OF) += drm_of.o
drm-$(CONFIG_PCI) += drm_pci.o
drm-$(CONFIG_DEBUG_FS) += \
	drm_debugfs.o \
	drm_debugfs_crc.o
drm-$(CONFIG_DRM_LOAD_EDID_FIRMWARE) += drm_edid_load.o
drm-$(CONFIG_DRM_PRIVACY_SCREEN) += \
	drm_privacy_screen.o \
	drm_privacy_screen_x86.o

#
# Memory-management helpers
#

drm_dma_helper-y := drm_gem_dma_helper.o
drm_dma_helper-$(CONFIG_DRM_FBDEV_EMULATION) += drm_fbdev_dma.o
drm_dma_helper-$(CONFIG_DRM_KMS_HELPER) += drm_fb_dma_helper.o

drm_suballoc_helper-y := drm_suballoc.o

drm_vram_helper-y := drm_gem_vram_helper.o

drm_ttm_helper-y := drm_gem_ttm_helper.o

#
# Drivers and the rest
#

obj-m := drm.o
obj-$(CONFIG_DRM_PANEL_ORIENTATION_QUIRKS) += drm_panel_orientation_quirks.o
obj-$(CONFIG_DRM_GEM_DMA_HELPER) += drm_dma_helper.o
obj-$(CONFIG_DRM_SUBALLOC_HELPER) += drm_suballoc_helper.o
obj-$(CONFIG_DRM_VRAM_HELPER) += drm_vram_helper.o
obj-$(CONFIG_DRM_TTM_HELPER) += drm_ttm_helper.o
