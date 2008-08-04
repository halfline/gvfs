
NULL =

libexec_PROGRAMS = gvfs-gphoto2-volume-monitor

BUILT_SOURCES =                                         \
	hal-marshal.h           hal-marshal.c

hal-marshal.h: hal-marshal.list
	glib-genmarshal $< --prefix=hal_marshal --header > $@

hal-marshal.c: hal-marshal.list
	echo "#include \"hal-marshal.h\"" > $@ && glib-genmarshal $< --prefix=hal_marshal --body >> $@


gvfs_gphoto2_volume_monitor_SOURCES =			\
	hal-utils.c 		hal-utils.h 		\
	hal-marshal.c		hal-marshal.h		\
	hal-device.c		hal-device.h		\
	hal-pool.c		hal-pool.h		\
	gphoto2-volume-monitor-daemon.c			\
	ggphoto2volume.c	ggphoto2volume.h	\
	ggphoto2volumemonitor.c	ggphoto2volumemonitor.h	\
	$(NULL)

gvfs_gphoto2_volume_monitor_CFLAGS =		\
	-DG_LOG_DOMAIN=\"GVFS-GPhoto2\"		\
	-I$(top_srcdir)/common                  \
	-I$(top_srcdir)/monitor/proxy           \
	$(GLIB_CFLAGS)                          \
	$(HAL_CFLAGS)                           \
	-DGIO_MODULE_DIR=\"$(GIO_MODULE_DIR)\"	\
	-DGVFS_LOCALEDIR=\""$(localedir)"\"	\
	-DG_DISABLE_DEPRECATED			\
	$(NULL)

gvfs_gphoto2_volume_monitor_LDFLAGS =	\
	$(NULL)

gvfs_gphoto2_volume_monitor_LDADD  =		     			      \
	$(GLIB_LIBS)                                 			      \
	$(HAL_LIBS)                                  			      \
	$(top_builddir)/common/libgvfscommon-noin.la 			      \
	$(top_builddir)/monitor/proxy/libgvfsproxyvolumemonitordaemon-noin.la \
	$(NULL)

remote_volume_monitorsdir = $(datadir)/gvfs/remote-volume-monitors
remote_volume_monitors_DATA = gphoto2.monitor

servicedir       = $(datadir)/dbus-1/services
service_in_files = org.gtk.Private.GPhoto2VolumeMonitor.service.in
service_DATA     = $(service_in_files:.service.in=.service)

$(service_DATA): $(service_in_files) Makefile
	@sed -e "s|\@libexecdir\@|$(libexecdir)|" $< > $@

clean-local:
	rm -f *~ *.loT $(BUILT_SOURCES) $(service_DATA)

EXTRA_DIST = hal-marshal.list $(service_in_files) gphoto2.monitor