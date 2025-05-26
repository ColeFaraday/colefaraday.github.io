---
layout: page
title: Checklist for arXiv submission
date: 2025-05-25
description: 
tags: latex
categories: academic-workflow
<!-- thumbnail: assets/img/9.jpg -->
<!-- images: -->
<!--   lightbox2: true -->
<!--   photoswipe: true -->
<!--   spotlight: true -->
<!--   venobox: true -->
---

My checklist that I use before submitting a manuscript to arXiv. Note: only tested on MacOS.

*On local machine*
- [ ] Make a copy of the document folder
- [ ] Check todo list
- [ ] Check figure placement (some figures may manually need to be moved by changing htpb)
- [ ] Check all acknowledgements (funding agencies, people that contributed, HPC, etc.)
- [ ] Spell / language check (consistent US / UK spelling, consistent choice of hyphenation, consistent captions)
- [ ] Run `arxiv_latex_cleaner arxiv_draft --commands_only_to_delete author1Edit author2Edit --comands_to_delete commentCommand1 commentCommand2` (this creates a new folder)
	- [ ] `commands_only_to_delete` is useful for deleting commands surrounding text which should still remain in the manuscript (for instance seeing who made which changes)
	- Be careful as deleting comments can sometimes change the compile, since they are replaced with a newline
- [ ] Run `arxiv_flatten_submission --asset_directory=figures/` from inside the newly created directory (see [GitHub - davidstutz/arxiv-submission-sanitizer-flattener](https://github.com/davidstutz/arxiv-submission-sanitizer-flattener))
- [ ] Delete figures directory (since figures are now in the main directory)
- [ ] Copy to new directory and compile with `pdflatex` three times
- [ ] Compare the pre-comment removal etc. pdf to the new pdf with, for instance, [Compare PDF files](https://www.ilovepdf.com/compare-pdf#pdfcompare-options,semantic)
	- Should be identical. Sometimes spacing errors occur because of the deletions.
- [ ] Check no errors in latex output
- [ ] Check no comments

*Start upload to arXiv process*
- [ ] Consult the arXiv [submission schedule](https://info.arxiv.org/help/availability.html) to decide when to post
- [ ] Choose  "arXiv.org perpetual, non-exclusive license" license (for most use cases)
- [ ] Upload the comment-deleted version to arxiv (in a zip is easiest)
- [ ] Compare the arxiv version to the original with the pdf comparer
- [ ] Copy abstract / title / authors to the metadata of arxiv. 
	- Note that some latex might have to be made more simple to be compatible with the arxiv system (look at the preview). Also, arxiv has a character limit for the abstract of 1920 characters.
- [ ] Send paper key to coauthors when the paper goes up on the arxiv
