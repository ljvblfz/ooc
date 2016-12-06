# Copyright (C) 2009-2014 the Fandol Team, All wrongs reserved.

# Version Control System Information: Subversion, host on Google Code;
# FileID:	$Id$;
# FileDate:	$Date$;
# FileRevision:	$Revision$

# Makefile for GNUmake, \LaTeX{} -> pdf.


RM = rm
TEX = xelatex # -quiet -interaction=nonstopmode
MKIDX = makeindex

OPEN = mupdf
TAR = tar -cjf
MV = mv
CP = cp

# OPEN = start
# RM = erase
# MV = rename
# CP = copy

VCS = svn
# Use Make to submit source files maybe NOT good enough.

TYPE = book
TARGET = $(TYPE).pdf
BALL = OOC.tar.bz2

SRC =	$(TYPE).tex\
	header.tex\
	locale.tex\
	preface.tex\
	body.tex\
	ch01-ADT.tex\
	ch02-Dyln.tex\
	ch03-psExpr.tex\
	ch04-inhert.tex\
	ch05-psSymT.tex\
	ch06-Hier.tex\
	ch07-preproc.tex\
	ch08-DyTC.tex\
	ch09-statc.tex\
	ch10-Deleg.tex\
	ch11-Methods.tex\
	ch12-persis.tex\
	ch13-Except.tex\
	ch14-fwMsg.tex\
	apdA-Hints.tex\
	apdB-Prepr.tex\
	apdC-Manual.tex

EXTR = cover.jpg\
	   README.txt\
	   CHANGELOG.txt\
	   book.tex.latexmain

# Various of temp files:
LOGS = $(TYPE).log
TOCS = $(TYPE).toc
OUTS = $(TYPE).out
IDXS = *.idx *.ind *.ilg
AUXS = $(SRC:.tex=.aux)
BAKS = $(SRC:.tex=.tex~)
# Vim set backup; For Gedit or sth else, modify this to .bak or whatever.

$(TARGET): $(SRC)
	$(TEX) $(TYPE)
	$(TEX) $(TYPE)

# Re-run for hyperlinks, indexs and so on.
# $(MKIDX) $(TYPE) makeindex is not needed by imakeidx

.PHONY: clean distclean dist checkin exec clear

clean:
	-$(RM) $(TARGET)
	-$(RM) $(LOGS)

# $(OUTS) $(TOCS) $(AUXS)

clear:
	-$(RM) $(BAKS) # *~
	-$(RM) $(LOGS)
	-$(RM) $(OUTS) $(TOCS)
	-$(RM) $(AUXS)
	-$(RM) $(IDXS)

distclean: clean clear
	-$(RM) $(BALL)

checkin: distclean
	$(VCS) --help # TODO:

dist: $(TARGET)
	$(MV) $(TARGET) OOC.pdf
	$(TAR) $(BALL) $(SRC) $(EXTR) OOC.pdf Makefile
	$(CP) $(BALL) OOC-`date -u -d now +%Y-%m-%d-%H-%M`.tar.bz2
	$(MV) OOC.pdf $(TARGET)

exec: $(TARGET)
	$(OPEN) $(TARGET)

