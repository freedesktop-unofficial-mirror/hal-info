
fdidir = $(datadir)/hal/fdi/information/10freedesktop

dist_fdi_DATA = 10-usb-card-readers.fdi		\
		10-usb-music-players.fdi	\
		10-usb-zip-drives.fdi   	\
		10-camera-ptp.fdi		\
		10-usb-pda.fdi			\
		10-usbcsr-mice.fdi		\
		10-laptop-panel-hardware.fdi	\
		10-cd-dvd-burner.fdi		\
		10-sony-bluetooth-switch.fdi	\
		10-dell-rfkill-switch.fdi

if BUILD_RECALL
dist_fdi_DATA +=				\
		10-recall-battery-dell.fdi	\
		10-recall-battery-ibm.fdi	\
		10-recall-battery-lenovo.fdi	\
		10-recall-battery-fujitsu.fdi	\
		10-recall-battery-gateway.fdi	\
		10-recall-battery-toshiba.fdi
endif

if BUILD_VIDEO
dist_fdi_DATA +=				\
		20-video-quirk-pm-acer.fdi	\
		20-video-quirk-pm-apple.fdi	\
		20-video-quirk-pm-asus.fdi	\
		20-video-quirk-pm-dell.fdi	\
		20-video-quirk-pm-fujitsu.fdi	\
		20-video-quirk-pm-hp.fdi	\
		20-video-quirk-pm-ibm.fdi	\
		20-video-quirk-pm-lenovo.fdi	\
		20-video-quirk-pm-misc.fdi	\
		20-video-quirk-pm-sony.fdi	\
		20-video-quirk-pm-toshiba.fdi
endif

check:
	for f in $(dist_fdi_DATA); do \
            echo -n "Validate XML in $$f : "; \
            xmllint --noout --dtdvalid $(top_srcdir)/fdi/fdi.dtd $(srcdir)/$$f 2> xmllint.error; \
            if test -s xmllint.error; \
              then \
                echo failed; \
                cat xmllint.error; \
                rm -f xmllint.error; \
                exit 1; \
            else \
                echo ok; \
                rm -f xmllint.error; \
            fi; \
        done;

clean-local :
	rm -f *~
