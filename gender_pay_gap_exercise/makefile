all: gender_pay_gap_exercise.html gender_pay_gap_writeup.docx

%.html: %.Rmd
	Rscript -e 'library(rmarkdown); rmarkdown::render("$<", "html_document")'

%.docx: %.Rmd
	Rscript -e 'library(rmarkdown); rmarkdown::render("$<", "word_document")'

%.R: %.Rmd
	Rscript -e 'library(knitr); knitr::purl("$<", documentation=2)'

clean:
	rm -f gender_pay_gap_exercise.html gender_pay_gap_writeup.docx
