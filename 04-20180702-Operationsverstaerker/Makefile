BUILD_FILES = $(addprefix build/, \
	$(addsuffix .pdf, \
	aussteuerungsbereich\
	dreiecksgen\
	frequenz_lin\
	linearverstaerker\
	operationsverstaerker\
	schmitt_trigger\
	schwingungsdiffgl\
	umkehr_diff\
	umkehr_integrator\
	tiefpass\
	lin_verst_01__r1_200__rn_470__u1_100 \
	lin_verst_02__r1_200__rn_100__u1_100 \
	lin_verst_03__r1_100__rn_470__u1_100 \
	lin_verst_04__r1_470__rn_100__u1_100 \
	differentiator \
	integrator \
	gedaempfte_schwingung \
	schmitt \
	phases \
	) \
)

OUT_DIR = build
TEX_CMD = latexmk \
	--pdf \
	--output-directory=$(OUT_DIR) \
	--halt-on-error \
	--interaction=nonstopmode
PREVIEW_CMD = \
	$(TEX_CMD) --pvc


all: build/main.pdf


anleitung_V51_Operationsverstaerker.pdf:
	wget http://129.217.224.2/HOMEPAGE/PHYSIKER/MASTER/SKRIPT/V51.pdf -q \
		--user TUDoFP --password WS1819 \
		-O $@


build/main.pdf: $(BUILD_FILES) FORCE | build
	TEXINPUTS=build: BIBINPUTS=build: max_print_line=1048576 \
	$(TEX_CMD) main.tex


preview: $(BUILD_FILES) FORCE | build
	TEXINPUTS=build: BIBINPUTS=build: max_print_line=1048576 \
	$(PREVIEW_CMD) main.tex

build/operationsverstaerker.pdf: anleitung_V51_Operationsverstaerker.pdf | build
		gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
		    -dFirstPage=1 -dLastPage=1 \
		    -sOutputFile=$@ $<
		pdfcrop --bbox "0 450 600 595"  $@ $@
		pdfcrop $@ $@

build/aussteuerungsbereich.pdf: anleitung_V51_Operationsverstaerker.pdf | build
		gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
		    -dFirstPage=1 -dLastPage=1 \
		    -sOutputFile=$@ $<
		pdfcrop --bbox "200 70 600 280"  $@ $@
		pdfcrop $@ $@

build/linearverstaerker.pdf: anleitung_V51_Operationsverstaerker.pdf | build
		gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
		    -dFirstPage=4 -dLastPage=4 \
		    -sOutputFile=$@ $<
		pdfcrop --bbox "150 530 400 680"  $@ $@
		pdfcrop $@ $@

build/frequenz_lin.pdf: anleitung_V51_Operationsverstaerker.pdf | build
		gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
		    -dFirstPage=5 -dLastPage=5\
		    -sOutputFile=$@ $<
		pdfcrop --bbox "0 100 600 310"  $@ $@
		pdfcrop $@ $@

build/umkehr_integrator.pdf: anleitung_V51_Operationsverstaerker.pdf | build
		gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
		    -dFirstPage=8 -dLastPage=8\
		    -sOutputFile=$@ $<
		pdfcrop --bbox "0 490 600 680"  $@ $@
		pdfcrop $@ $@

build/umkehr_diff.pdf: anleitung_V51_Operationsverstaerker.pdf | build
		gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
		    -dFirstPage=8 -dLastPage=8\
		    -sOutputFile=$@ $<
		pdfcrop --bbox "0 140 600 295"  $@ $@
		pdfcrop $@ $@

build/schmitt_trigger.pdf: anleitung_V51_Operationsverstaerker.pdf | build
		gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
		    -dFirstPage=9 -dLastPage=9\
		    -sOutputFile=$@ $<
		pdfcrop --bbox "0 220 600 380"  $@ $@
		pdfcrop $@ $@

build/dreiecksgen.pdf: anleitung_V51_Operationsverstaerker.pdf | build
		gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
		    -dFirstPage=10 -dLastPage=10\
		    -sOutputFile=$@ $<
		pdfcrop --bbox "0 400 600 592"  $@ $@
		pdfcrop $@ $@

build/schwingungsdiffgl.pdf: anleitung_V51_Operationsverstaerker.pdf | build
		gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
		    -dFirstPage=10 -dLastPage=10\
		    -sOutputFile=$@ $<
		pdfcrop --bbox "0 80 600 290"  $@ $@
		pdfcrop $@ $@

build/tiefpass.pdf: | build
		#maybe you have to install rsvg-convert with sudo pacman -S librsvg2-bin to convert svg -> pdf
		wget "https://upload.wikimedia.org/wikipedia/commons/e/e8/Tiefpass.svg" -O build/tiefpass.svg
		rsvg-convert -f pdf -o $@ build/tiefpass.svg

build/lin_verst_01__r1_200__rn_470__u1_100.pdf build/lin_verst_02__r1_200__rn_100__u1_100.pdf build/lin_verst_03__r1_100__rn_470__u1_100.pdf build/lin_verst_04__r1_470__rn_100__u1_100.pdf build/phases.pdf: scripts/plot_lin_verst.py data/lin_verst_01__r1_200__rn_470__u1_100.txt data/lin_verst_02__r1_200__rn_100__u1_100.txt data/lin_verst_03__r1_100__rn_470__u1_100.txt data/lin_verst_04__r1_470__rn_100__u1_100.txt | build
	python $<

build/differentiator.pdf build/integrator.pdf: scripts/plot_int_diff.py data/differentiator.txt data/integrator.txt | build
	python $<

build/gedaempfte_schwingung.pdf: scripts/plot_gedaempfte_schwingung.py data/scope_274.csv | build
	python $<

build/schmitt.pdf: scripts/plot_schmitt.py data/scope_269.csv | build
	python $<

FORCE:


build:
	mkdir -p build


clean:
	rm -rf *.pdf build


.PHONY: all clean FORCE preview
