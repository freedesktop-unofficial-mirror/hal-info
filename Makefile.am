## Process this file with automake to produce Makefile.in

SUBDIRS = fdi

MAINTAINERCLEANFILES = ChangeLog

# Creating ChangeLog from git log (taken from cairo/Makefile.am):

ChangeLog: $(srcdir)/ChangeLog

$(srcdir)/ChangeLog:
	@if test -d "$(srcdir)/.git"; then \
	  (cd "$(srcdir)" && \
	  ./missing --run git-log --stat) | fmt --split-only > $@.tmp \
	  && mv -f $@.tmp $@ \
	  || ($(RM) $@.tmp; \
	      echo Failed to generate ChangeLog, your ChangeLog may be outdated >&2; \
	      (test -f $@ || echo git-log is required to generate this file >> $@)); \
	else \
	  test -f $@ || \
	  (echo A git checkout and git-log is required to generate ChangeLog >&2 && \
	  echo A git checkout and git-log is required to generate this file >> $@); \
	fi

.PHONY: ChangeLog $(srcdir)/ChangeLog

DISTCLEANFILES =

EXTRA_DIST = HACKING ChangeLog

clean-local :
	rm -f *~

release:
	@echo ""
	@echo "Check that all your changes are committed and pushed to"
	@echo "the remote master repository. Then run 'make release-real'."
	@echo ""

MAIL=/usr/sbin/sendmail

release-real:
	@make check
	@date +%Y%m%d > VERSION
	@rm -rf autom4te.cache
	@autoreconf
	@make dist
	@scp hal-info-`cat VERSION`.tar.gz david@people.freedesktop.org:public_html/dist
	@git-commit -m "version `cat VERSION`" VERSION
	@git-tag -s HAL_INFO_`cat VERSION`
	@git-push
	@echo "From: $(GIT_AUTHOR_NAME) <$(GIT_AUTHOR_EMAIL)>" > .release-mail
	@echo "To: hal@lists.freedesktop.org" >> .release-mail
	@echo "Subject: hal-info `cat VERSION` release" >> .release-mail
	@echo "X-Mailer: hal-info release script" >> .release-mail
	@echo "" >> .release-mail
	@echo "There's a new hal-info `cat VERSION` release available. Download from" >> .release-mail
	@echo "" >> .release-mail
	@echo " http://people.freedesktop.org/~david/dist/hal-info-`cat VERSION`.tar.gz" >> .release-mail
	@echo "" >> .release-mail
	@echo "." >> .release-mail
	@echo "" >> .release-mail
	@cat .release-mail | $(MAIL) davidz@redhat.com hal@lists.freedesktop.org




