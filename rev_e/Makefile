# Copyright (C) 2017 Daniel Page <dan@phoo.org>
#
# Use of this source code is restricted per the CC BY-SA license, a copy of
# which can be found via http://creativecommons.org (and should be included 
# as LICENSE.txt within the associated archive or repository).

BOARD_SOURCES  = nandboard.sch
BOARD_SOURCES += nandboard.brd
BOARD_SOURCES += nandboard.csv

BOARD_TARGETS  = nandboard.pdf

${BOARD_TARGETS} : %.pdf : ${BOARD_SOURCES}
	@${EAGLEDIR}/bin/eagle -C 'edit $(filter %.sch, ${^}); set confirm yes; print landscape 10.0 -1 -caption file ${@} sheets all paper a3; quit;' $(filter %.sch, ${^})

board-all   : ${BOARD_TARGETS}

board-clean :
	@rm -f nandboard.s#[1-9] nandboard.s##
	@rm -f nandboard.b#[1-9] nandboard.b##
	@rm -f nandboard.l#[1-9] nandboard.l##
