# Copyright (C) 2017 Daniel Page <dan@phoo.org>
#
# Use of this source code is restricted per the CC BY-SA license, a copy of
# which can be found via http://creativecommons.org (and should be included 
# as LICENSE.txt within the associated archive or repository).

BOARD_SOURCE = nandboard.sch
BOARD_TARGET = README.pdf

${BOARD_TARGET} : %.pdf : ${BOARD_SOURCE}
	@eagle -C 'edit $(filter %.sch, ${^}); set confirm yes; print landscape 10.0 -1 -caption file ${@} sheets all paper a3; quit;' ${<}

board-all   : ${BOARD_TARGET}

board-clean :
	@rm --force --recursive nandboard.s#[1-9] nandboard.s##
	@rm --force --recursive nandboard.b#[1-9] nandboard.b##
	@rm --force --recursive nandboard.l#[1-9] nandboard.l##
