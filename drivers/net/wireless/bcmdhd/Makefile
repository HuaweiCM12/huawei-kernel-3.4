# bcmdhd for huawei bcm4330
#

DHDCFLAGS = -Wall -Wstrict-prototypes -Dlinux -DBCMDRIVER                 \
	-DBCMDONGLEHOST -DUNRELEASEDCHIP -DBCMDMA32 -DBCMFILEIMAGE            \
	-DDHDTHREAD -DDHD_DEBUG -DSDTEST -DBDC -DTOE                          \
	-DDHD_BCMEVENTS -DSHOW_EVENTS -DPROP_TXSTATUS -DBCMDBG                \
	-DCUSTOMER_HW2 -DOOB_INTR_ONLY -DHW_OOB                               \
	-DMMC_SDIO_ABORT -DBCMSDIO -DBCMLXSDMMC -DBCMPLATFORM_BUS -DWLP2P     \
	-DWIFI_ACT_FRAME -DARP_OFFLOAD_SUPPORT                                \
	-DKEEP_ALIVE -DPKT_FILTER_SUPPORT                                     \
	-DEMBEDDED_PLATFORM -DENABLE_INSMOD_NO_FW_LOAD -DPNO_SUPPORT          \
	-DDHD_USE_IDLECOUNT -DSET_RANDOM_MAC_SOFTAP -DROAM_ENABLE -DVSDB      \
	-DWL_CFG80211_VSDB_PRIORITIZE_SCAN_REQUEST -DSDIO_CRC_ERROR_FIX       \
	-DESCAN_RESULT_PATCH -DHT40_GO -DPASS_ARP_PACKET -DSUPPORT_PM2_ONLY   \
	-DDHD_DONOT_FORWARD_BCMEVENT_AS_NETWORK_PKT -DDHD_USE_STATIC_BUF      \
	-DCUSTOM_SDIO_F2_BLKSIZE=128 -DCONFIG_WIFI_CONTROL_FUNC               \
	-Idrivers/net/wireless/bcmdhd -Idrivers/net/wireless/bcmdhd/include

# Huawei magic numbers
DHDCFLAGS += -DCUSTOM_SDCC_WIFI_SLOT=2
DHDCFLAGS += -DCUSTOM_OOB_GPIO_NUM=48

DHDOFILES = aiutils.o bcmsdh_sdmmc_linux.o dhd_linux.o siutils.o bcmutils.o   \
	dhd_linux_sched.o dhd_sdio.o bcmwifi_channels.o bcmevent.o hndpmu.o       \
	bcmsdh.o dhd_cdc.o bcmsdh_linux.o dhd_common.o linux_osl.o                \
	bcmsdh_sdmmc.o dhd_custom_gpio.o sbutils.o wldev_common.o wl_android.o

obj-$(CONFIG_BCMDHD) += dhd.o
dhd-objs += $(DHDOFILES)
ifneq ($(CONFIG_CFG80211),)
dhd-objs += wl_cfg80211.o wl_cfgp2p.o wl_linux_mon.o dhd_cfg80211.o
DHDCFLAGS += -DWL_CFG80211 -DWL_CFG80211_STA_EVENT -DWL_ENABLE_P2P_IF
DHDCFLAGS += -DCUSTOM_ROAM_TRIGGER_SETTING=-65
DHDCFLAGS += -DCUSTOM_ROAM_DELTA_SETTING=15
DHDCFLAGS += -DCUSTOM_KEEP_ALIVE_SETTING=28000
DHDCFLAGS += -DCUSTOM_PNO_EVENT_LOCK_xTIME=7
endif
ifneq ($(CONFIG_DHD_USE_SCHED_SCAN),)
DHDCFLAGS += -DWL_SCHED_SCAN
endif
EXTRA_CFLAGS = $(DHDCFLAGS)
ifeq ($(CONFIG_BCMDHD),m)
EXTRA_LDFLAGS += --strip-debug
endif
