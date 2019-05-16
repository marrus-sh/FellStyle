# FellStyle

A collection of styles for use with [BookGen](https://github.com/marrus-sh/BookGen/) inspired by older English typography. Featuring :

+ Standard and Largetype PDF forms
+ Additional information on chapter­‑only PDFs for ease of distribution
+ CSS stylesheet

## Prerequisites

PDF styles are designed for use with XeLaTeX ( the BookGen default ).

### Fonts ( for PDF )

Both PDF styles require the [IM Fell](https://iginomarini.com/fell/the-revival-fonts/) fonts. ( At time of writing, the IM Fell website is having issues, so hereʼs a direct download link : <https://web.archive.org/web/20190406165622/http://iginomarini.com/fell/wp-content/uploads/IMFellTypesClass.zip>. )

The Standard Edition style requires [Junicode](http://junicode.sourceforge.net/).

The Largetype Edition style requires [Charis SIL](https://software.sil.org/charis/).

## Makefile configuration

To make usage of these styles simpler, you might want to set up a makefile in your work directory which automatically generates symlinks to their locations. The provided `Makefile` is intended to aid in this process. The following is an example makefile that one might set up which makes use of it :

	SHELL = /bin/sh

	# Replace with the paths to these repositories on your device:
	BOOKGEN := BookGen
	FELLSTYLE := FellStyle

	# BookGen configuration:
	# DRAFTS := Drafts
	# export DRAFTS

	default: bookgen fellstyle

	# BookGen default make:
	bookgen:
		@$(MAKE) -ef "$(BOOKGEN)/GNUmakefile"

	# FellStyle default make:
	fellstyle:
		@$(MAKE) -f "$(FELLSTYLE)/Makefile"

	# Do not pattern­‑match this makefile:
	Makefile: ;

	# Always pass all unmatched patterns through to BookGen after running a FellStyle make:
	%: fellstyle
		@$(MAKE) -ef "$(BOOKGEN)/GNUmakefile" $@

	# Delete generated files:
	clobber distclean gone:
		@$(MAKE) -f "$(FELLSTYLE)/Makefile" gone
		@$(MAKE) -ef "$(BOOKGEN)/GNUmakefile" gone

	.PHONY: default bookgen fellstyle clobber distclean gone

