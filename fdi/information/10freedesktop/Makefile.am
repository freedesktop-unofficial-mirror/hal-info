
fdidir = $(datadir)/hal/fdi/information/10freedesktop

dist_fdi_DATA = 10-usb-card-readers.fdi		\
		10-usb-music-players.fdi	\
		10-usb-zip-drives.fdi   	\
		10-camera-ptp.fdi		\
		10-usb-pda.fdi			\
		10-usbcsr-mice.fdi		\
		10-cd-dvd-burner.fdi		\
		10-recall-battery-dell.fdi	\
		10-recall-battery-ibm.fdi	\
		10-recall-battery-fujitsu.fdi	\
		10-recall-battery-gateway.fdi	\
		10-recall-battery-toshiba.fdi

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
