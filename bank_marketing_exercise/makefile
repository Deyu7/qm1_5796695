export LC_ALL = en_US.UTF-8

all: bank_marketing.html bank_marketing_writeup.docx

%.html: %.Rmd
	Rscript -e 'library(rmarkdown); rmarkdown::render("$<", "html_document")'

%.docx: %.Rmd
	Rscript -e 'library(rmarkdown); rmarkdown::render("$<", "word_document")'

%.R: %.Rmd
	Rscript -e 'library(knitr); knitr::purl("$<", documentation=2)'

clean:
	rm -f bank_marketing.html bank_marketing_writeup.docx
