###############################################################################
# Variable definitions for targets to build
###############################################################################
#___INFO__MARK_BEGIN__
##########################################################################
#
#  The Contents of this file are made available subject to the terms of
#  the Sun Industry Standards Source License Version 1.2
#
#  Sun Microsystems Inc., March, 2001
#
#
#  Sun Industry Standards Source License Version 1.2
#  =================================================
#  The contents of this file are subject to the Sun Industry Standards
#  Source License Version 1.2 (the "License"); You may not use this file
#  except in compliance with the License. You may obtain a copy of the
#  License at http://gridengine.sunsource.net/Gridengine_SISSL_license.html
#
#  Software provided under this License is provided on an "AS IS" basis,
#  WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING,
#  WITHOUT LIMITATION, WARRANTIES THAT THE SOFTWARE IS FREE OF DEFECTS,
#  MERCHANTABLE, FIT FOR A PARTICULAR PURPOSE, OR NON-INFRINGING.
#  See the License for the specific provisions governing your rights and
#  obligations concerning the Software.
#
#  The Initial Developer of the Original Code is: Sun Microsystems, Inc.
#
#  Copyright: 2001 by Sun Microsystems, Inc.
#
#  All Rights Reserved.
#
##########################################################################
#___INFO__MARK_END__
QLIMIT_DIR = $(SDIR)/clients/qquota

QLIMIT_TARGETS = qquota

QLIMIT_SRC = qquota.c 

QLIMIT_ADD_SRC = \
               parse_job_cull.c \
               parse_qsub.c \
               read_defaults.c \
               show_job.c \
               sge_host.c \
               sge_qstat.c \
               sge_qquota.c \
               sge_cqueue_qstat.c \
               sig_handlers.c \
               usage.c \
               sge_options.c

QLIMIT_OBJS = $(QLIMIT_SRC:.c=.o)

QLIMIT_ADD_OBJS = $(QLIMIT_ADD_SRC:.c=.o)

QLIMIT_ADD_LIBS = sge_mt_init.o -lsched -lgdi -lsgeobjd -lsgeobj -lcull -lcomm -lcommlists -luti $(WINGRIDLIB) $(SECLIB) $(KRBLIB) $(DLLIB)

QLIMIT_LIB_DEPENDS = sge_mt_init.o $(GDILIB) $(SCHEDLIB) $(SGEOBJLIB) $(SGEOBJDLIB) $(KRBLIBS) $(CULLLIB) $(COMMLIB) $(COMMLISTSLIB) $(WINGRIDLIB_DEP) $(UTILIB) $(TPLIB)

###############################################################################
# global rules: all, clean, depend, messages
###############################################################################
qquota_clean:
	$(RM) $(QLIMIT_TARGETS) $(QLIMIT_OBJS)

qquota_depend:
		$(DEPEND) -f$(QLIMIT_DIR)/qquota_dependencies $(QLIMIT_DIR)/*.c

qquota_messages:
	@echo Creating $@
	@for i in `ls $(QLIMIT_DIR)/*.c`; do \
		$(CC) $(CFLAGS) -DEXTRACT_MESSAGES -E $$i | $(XGETTEXT) - ; \
	done


###############################################################################
# rules to build binaries
###############################################################################
qquota: $(QLIMIT_OBJS) $(QLIMIT_ADD_OBJS) $(QLIMIT_LIB_DEPENDS)
		$(LD_WRAPPER) $(CC) -o $@ $(LFLAGS) $(QLIMIT_OBJS) $(QLIMIT_ADD_OBJS) $(QLIMIT_ADD_LIBS) $(SLIBS) $(LIBS)

###############################################################################
# include dependencies for object files generated by sge_depend
###############################################################################
include $(QLIMIT_DIR)/qquota_dependencies

###############################################################################
# rules to build object codes
###############################################################################
qquota.o: 	$(QLIMIT_DIR)/qquota.c
		$(CC) $(CFLAGS) -c $(QLIMIT_DIR)/qquota.c
