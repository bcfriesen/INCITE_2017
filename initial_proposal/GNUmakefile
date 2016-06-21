SOURCES := summary.tex \
           narrative.tex \
           sneIa.tex xrb.tex ccsne.tex bwp.tex \
           objectives.tex \
           readiness.tex \
           milestones.tex \
           personnel.tex \
           publications.tex \
           management.tex \


PDFs := summary.pdf narrative.pdf milestones.pdf personnel.pdf publications.pdf management.pdf

PNGs := $(wildcard *.png)
EPSs := $(wildcard *.eps)

ALL: $(PDFs) merged.pdf


%.pdf: %.tex $(SOURCES) $(PNGs) $(EPSs) refs.bib newcommands.tex
	pdflatex $<
	@if [ "$(shell ack -l bibliography $<)" != "" ]; then \
	  bibtex $(basename $<) ; \
	fi
	pdflatex $<
	pdflatex $<


merged.pdf: $(PDFs)
	gs -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=merged.pdf -dBATCH $(PDFs) $(wildcard ../CVs/*.pdf)
	@echo 
	@echo a merged PDF of all the proposal material is available as merged.pdf

print-%: ; @echo $* is $($*)

clean:
	$(RM) *.aux *.log *.blg *.bbl *.out

realclean: clean
	$(RM) $(SOURCES:.tex=.pdf)
	$(RM) *-eps-converted-to.pdf
