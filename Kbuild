ccflags-y += -I$(M)/dvb-frontends/
ccflags-y += -I$(M)/tuners/
ccflags-y += -I$(M)/media/usb/cx231xx/
ccflags-y += -I$(srctree)
ccflags-y += -DTBS_STANDALONE

tas2101-objs := dvb-frontends/tas2101.o
ccflags-y += -DCONFIG_DVB_TAS2101
obj-m += tas2101.o

av201x-objs := tuners/av201x.o
ccflags-y += -DCONFIG_MEDIA_TUNER_AV201X
obj-m += av201x.o

cx231xx-objs := media/usb/cx231xx/cx231xx-417.o \
                media/usb/cx231xx/cx231xx-avcore.o \
                media/usb/cx231xx/cx231xx-i2c.o \
                media/usb/cx231xx/cx231xx-pcb-cfg.o \
                media/usb/cx231xx/cx231xx-cards.o \
                media/usb/cx231xx/cx231xx-core.o \
                media/usb/cx231xx/cx231xx-vbi.o \
                media/usb/cx231xx/cx231xx-video.o
cx231xx-$(CONFIG_VIDEO_CX231XX_RC) += media/usb/cx231xx/cx231xx-input.o
ccflags-y += -DCONFIG_VIDEO_CX231XX
obj-m += cx231xx.o

cx231xx_dvb_ci-objs := media/usb/cx231xx/cx231xx-dvb.o \
                       media/usb/cx231xx/tbscxci.o
ccflags-y += -DCONFIG_VIDEO_CX231XX_DVB
obj-m += cx231xx_dvb_ci.o
