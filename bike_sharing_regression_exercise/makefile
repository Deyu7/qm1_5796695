export LC_ALL = en_US.UTF-8

all: bike_sharing_regression.html bike_sharing_writeup.docx

%.html: %.Rmd
	Rscript -e 'library(rmarkdown); rmarkdown::render("$<", "html_document")'

%.docx: %.Rmd
	Rscript -e 'library(rmarkdown); rmarkdown::render("$<", "word_document")'

%.R: %.Rmd
	Rscript -e 'library(knitr); knitr::purl("$<", documentation=2)'

clean:
	rm -f bike_sharing_regression.html bike_sharing_writeup.docx
