LATEX = latex

DVIPS = dvips

PDFFLAGS = -dCompatibilityLevel=1.4 -dPDFSETTINGS=/prepress \
           -dCompressPages=true -dUseFlateCompression=true  \
           -dEmbedAllFonts=true -dSubsetFonts=true -dMaxSubsetPct=100


%.dvi: %.tex
	$(LATEX) $<

%.ps: %.dvi
	$(DVIPS) -o $@ $<

%.pdf: %.ps
	ps2pdf $(PDFFLAGS) $<

all:	book.tex
	pdflatex book
	makeindex book.idx
	pdflatex book
	mv book.pdf thinkpython2-spanish.pdf

hevea:	book.tex header.html footer.html
	# replace the pdfs with eps
	sed s/.pdf/.eps/g book.tex > thinkpython2.tex
	latex thinkpython2
	rm -rf html
	mkdir html
	hevea -fix -O -e latexonly htmlonly thinkpython2
	# the following greps are a kludge to prevent imagen from seeing
	# the definitions in latexonly, and to avoid headers on the images
	grep -v latexonly thinkpython2.image.tex > a; mv a thinkpython2.image.tex
	sed s/\\\\usepackage{fancyhdr}// < thinkpython2.image.tex > a; mv a thinkpython2.image.tex
	# imagen -png thinkpython2
	# hacha thinkpython2.html
	cp up.png next.png back.png html
	mv index.html thinkpython2.css thinkpython2*.html thinkpython2*.png *motif.gif html

epub: 	book.tex
	#replace the pdfs with eps
	sed s/.pdf/.eps/g book.tex >thinkpython2.tex
	latex thinkpython2
	rm -rf epub
	mkdir epub
	hevea -fix -O -e latexonly htmlonly thinkpython2
	grep -v latexonly thinkpython2.image.tex > a; mv a thinkpython2.image.tex
	sed s/\\\\usepackage{fancyhdr}// < thinkpython2.image.tex > a; mv a thinkpython2.image.tex
	imagen -png thinkpython2
	mv thinkpython2.html thinkpython2*.png epub
	cd epub; ebook-convert thinkpython2.html thinkpython2-spanish.epub

clean:
	rm -f *~ *.aux *.log *.dvi *.idx *.ilg *.ind *.toc



