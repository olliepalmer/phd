# thesis-corrections

This branch contains all corrections to my PhD thesis. The back-end on my computer automatically converts modified Word documents to Markdown (Github-flavoured) to sync with Github, and ICML for use with InDesign. 

The file structure looks like this:

```shell
corrections # root
|-- a_word-input	# original files exported from current InDesign files. Documents are copied from InDesign into Word as .DOCX, then cleaned up and stripped of any extraneous formatting.
|-- b_word-corrections	# the files I work from for corrections. These are as stripped back as Word can manage, whenever it can avoid doing silly formatting.
|-- c_icml		# the auto-generated .ICML files (created by Pandoc via Hazel action)
|-- d_markdown		# the auto-generated .MD files (created by Pandoc via Hazel action)
|-- examiner-reports	# the reports back from the examiners with corrections to be made. Where you put this is optional.
```


The Hazel script monitors the ```b_word-corrections``` folder and looks like this:

![Hazel options: If any of the following conditions is met: Extension is docx, do the following to teh matched file or folder](https://www.dropbox.com/s/so3joo9i1q5fjiu/Screenshot%202017-09-25%2014.07.23.png?raw=1)

The embedded shell script:
````shell
#!/bin/bash
for file in "$@"
do
pandoc "$file" -s -f docx -t icml -o "${file%.docx}.icml"
pandoc "$file" -s -f docx -t markdown_github -o "${file%.docx}.md"
done
````

