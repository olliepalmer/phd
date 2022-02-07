# [phd.olliepalmer.com](https://phd.olliepalmer.com)

This is the repository for the GitHub Pages version of my doctoral thesis. I strongly believe that publicly-funded research should be made available for free, and thus built this website so that my research is easily findable. My PhD is also available via an [open-access PDF, downloadable from UCL](https://discovery.ucl.ac.uk/id/eprint/10038254/), but it's a bit of a faff to read an A3-formatted landscape document on a computer or phone. And it's not search-engine-indexable.

The thesis is hosted on [GitHub Pages](https://pages.github.com), with a custom sub-domain ([phd.olliepalmer.com](https://phd.olliepalmer.com)). It uses [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) to build Markdown documents and images into a static website. There's a GitHub action in ```.github/workflows``` called ```ci.yml``` which re-builds and deploys the site every time I push something to this repo.

## Workflow

It took me a long time to work out the best way for me to write my thesis. In the end, I wrote my thesis by hand, because I prefer writing that way. It physically takes longer, but I tend to write what I want to write the first time, rather than writing and deleting and editing and re-ordering, which is what happens whenever I write on-screen. Then, whilst transcribing my handwriting into a Word document (a vile format, but required for tutor commenting), I would do minor edits. I also used Zotero to add in references. These minimally-formatted documents were what was sent back and forth for comments. The final PDF I submitted was formatted with InDesign – one day I will make a tutorial so that other people don't have to work out how to import Word documents with formatting all over again.

In 2016 I devised out a workflow with [Pandoc](https://pandoc.org) that auto-formatted all of my Word docs into Markdown documents, so that they could be uploaded to GitHub at the end of each day. This way, I could track my progress, and back up my work. The Markdown version of the documents are what is also used to make this website, in MkDocs - although I have gone through and put images in, too.

Every time I edited my thesis in Word, I'd save a copy of the word document, e.g.:

<code>thesis folder / 0_introduction / 2016.10.18-18.18 0_introduction v0.3.docx</code>

This filename contains 3 bits of information:

- the date and time of saving <code>2016.10.18-18.18</code>
- the chapter <code>0_introduction</code>
- the version I'm working on <code>v0.3</code>

A Hazel workflow monitored all of my thesis chapters (safely stowed in Dropbox). It then ran the following script using [Pandoc](https://pandoc.org) to convert the docx (horrible Word format) into Markdown (nice, semantically clean). I would then commit the changes to Github, and keep track of the document. This allowed me to compare every new paragraph, every chunk that got cut, and see how things expanded and rejigged over time. Seeing the progress was inspiration to continue.

~~~~
#!/bin/bash
for file in "$@"
do
pandoc "$file" -f docx -t markdown --no-wrap -o /Users/username/Documents/thesis-github/0_introduction_latest.md
done
~~~~

The file is saved as <code>0_introduction_latest.md</code> which can then be committed to github along with comments on changes.

It's not a perfect system, but it was quite enjoyable to use. It made me feel more in control of a hideous Word workflow. And as I _had_ to use Word in my thesis (on the advice of a supervisor) it is about the best I could do.
