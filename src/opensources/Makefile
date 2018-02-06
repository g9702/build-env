SUBDIR = \
	pcre \
	zlib openssl \
	libx264 \
	libfdk-aac \
	live555 \
	libre \

.PHONY: all
all:
	for sub in $(SUBDIR); do \
		make -C $$sub || exit 1; \
		make -C $$sub install || exit 1; \
		done

clean:
	for sub in $(SUBDIR); do \
		make -C $$sub clean || exit 1; \
		done

distclean:
	for sub in $(SUBDIR); do \
		make -C $$sub distclean || exit 1; \
		done

install:
	for sub in $(SUBDIR); do \
		make -C $$sub install || exit 1; \
		done

uninstall:
	for sub in $(SUBDIR); do \
		make -C $$sub uninstall || exit 1; \
		done
