# Copyright (C) 2017 Daniel Page <dan@phoo.org>
#
# Use of this source code is restricted per the CC BY-SA license, a copy of
# which can be found via http://creativecommons.org (and should be included 
# as LICENSE.txt within the associated archive or repository).

BOARD_SOURCE = nandboard.kicad_sch
BOARD_TARGET = README.pdf

${BOARD_TARGET} : %.pdf : ${BOARD_SOURCE}
	@kicad-cli sch export pdf --output ${@} ${<}

board-all   : ${BOARD_TARGET}

board-clean :
	@rm --force --recursive fp-info-cache
	@rm --force --recursive *-backups
	@rm --force --recursive *.kicad_pcb-bak
	@rm --force --recursive *.kicad_sch-bak
