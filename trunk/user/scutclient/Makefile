# https://github.com/hanwckf/scutclient.git
# https://github.com/scutclient/scutclient.git

# 3.1.2
SRC_NAME := scutclient-upstream
SRC_FILE := scutclient-a58996875c61d0cdf8ec435057befc1c87bd6863

# 3.0
# SRC_NAME := scutclient-3.0
# SRC_FILE := scutclient-3.0

# 3.1.3
# SRC_NAME := scutclient-3.1.3
# SRC_FILE := scutclient-3.1.3

THISDIR = $(shell pwd)

all: extract_test config_test
	$(MAKE) -C $(SRC_NAME)/build

extract_test:
	( if [ ! -d $(THISDIR)/$(SRC_NAME) ]; then \
		tar -xf $(SRC_FILE).tar.gz; \
	fi )

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( mkdir -p $(SRC_NAME)/build && cd $(SRC_NAME)/build ; \
		cmake -DCMAKE_TOOLCHAIN_FILE=../../cross-mipsel-linux.cmake .. \
	)

clean:
	rm -rf $(SRC_NAME)/build
	rm -f config_done

romfs:
	${ROMFSINST} $(THISDIR)/scripts/ /usr/bin/
	$(ROMFSINST) -p +x $(THISDIR)/$(SRC_NAME)/build/scutclient /usr/bin/bin_scutclient
