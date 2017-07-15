#
# Makefile to translate wiki pages to RestructuredText
#

esl_wiki_pages = \
  introduction:Electronic_Structure_Common_Data_Format \
  system:System \
  basis_sets:Basis_sets \
  densities:Densities \
  potentials:Potentials \
  states:States \
  extensions:Extensions

rst_documents = \
  basis_sets.rst \
  densities.rst \
  extensions.rst \
  introduction.rst \
  potentials.rst \
  states.rst \
  system.rst

mw_documents = $(rst_documents:.rst=.mw)

                    # ------------------------------------ #

PANDOC = pandoc
PDOCFLAGS =

WGET = wget
WGFLAGS =

.SUFFIXES:
.SUFFIXES: .rst .mw

.mw.rst:
	$(PANDOC) $(PDOCFLAGS) -f mediawiki -t rst -o $@ $<

                    # ------------------------------------ #

all_targets all: mw-docs rst-docs
	@echo "Source documents ready"

.PHONY: mw-docs
mw-docs:
	for specs in $(esl_wiki_pages); do \
	  page=`echo $$specs | cut -d: -f1`; \
	  title=`echo $$specs | cut -d: -f2`; \
	  $(WGET) $(WGFLAGS) -O $$page.mw http://esl.cecam.org/mediawiki/index.php\?title=ESCDF_-_$$title\&action=raw; \
	done

.PHONY: rst-docs
rst-docs: $(rst_documents)

clean:
	rm -f $(rst_documents)

distclean: clean
	rm -f $(mw_documents)

