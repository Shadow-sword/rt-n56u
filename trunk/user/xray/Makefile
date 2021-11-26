THISDIR = $(shell pwd)
Xray_dir="Xray.com/core/main"
Xray_VERSION := 1.5.0
Xray_URL := https://codeload.github.com/XTLS/Xray-core/tar.gz/refs/tags/v$(Xray_VERSION)

all:download_xray build_extract build_xray

download_xray:
	( if [ ! -f $(THISDIR)/Xray-core-$(Xray_VERSION).tar.gz ]; then \
	curl --create-dirs -L $(Xray_URL) -o $(THISDIR)/Xray-core-$(Xray_VERSION).tar.gz ; \
	fi )

build_extract:
	mkdir -p $(THISDIR)/Xray.com
	mkdir -p $(THISDIR)/bin
	( if [ ! -d $(THISDIR)/Xray.com/core ]; then \
	tar zxfv $(THISDIR)/Xray-core-$(Xray_VERSION).tar.gz -C $(THISDIR)/Xray.com ; \
	mv $(THISDIR)/Xray.com/Xray-core-$(Xray_VERSION) $(THISDIR)/Xray.com/core ; \
	fi )

build_xray:
	( cd $(THISDIR)/$(Xray_dir); \
	GOOS=linux GOARCH=mipsle go build -trimpath -ldflags "-w -s -buildid=" -o $(THISDIR)/bin/v2ray; \
	upx -9 $(THISDIR)/bin/v2ray; \
	)

clean:
	rm -rf $(THISDIR)/Xray.com
	rm -rf $(THISDIR)/bin

romfs:
	$(ROMFSINST) -p +x $(THISDIR)/bin/v2ray /usr/bin/v2ray
