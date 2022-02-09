# Lab Report 2 Week 4

## Code Change 1: Syntax
![code change diff from GitHub](/lab-report-2-week-4/diff-1.png)
[Failure-inducing input 1](https://pierrebeur.github.io/cse15l-lab-reports/breaking-test-file.md)
```
java MarkdownParse breaking-test-file.md
[but not really, https://www.google.com]
```
A failure inducing input for the previous version of the program is any file that contains the characters `[`, `]`, `(`, and `)` in order, but with any number of other characters between them. The symptom is that the program will return any text encapsulated by parenthesis if that text is preceded by any text encapsulated by brackets. The program didn't check that there are no characters between `]` and `(`, which is required for a valid link.

## Code Change 2: Spaces
![code change diff from GitHub](/lab-report-2-week-4/diff-2.png)
[Failure-inducing input 2](https://pierrebeur.github.io/cse15l-lab-reports/spaces-test-file.md)
```
java MarkdownParse spaces-test-file.md
[a link with spaces, nospaces.com]
```
A failure inducing input for the previous version of the program is any file that contains an otherwise valid link, but contains spaces within the filepath or URL. The symptom is that invalid links which contain spaces are returned by the program. The program didn't check for spaces within an otherwise valid link before adding it to the return list.

## Code Change 3: Images
![code change diff from GitHub](/lab-report-2-week-4/diff-3.png)
[Failure-inducing input 3](https://pierrebeur.github.io/cse15l-lab-reports/image-test-file.md)  
```
java MarkdownParse image-test-file.md
[page.com, ucsd.edu]
```
A failure-inducing input for the previous version of the program is any file that contains images. The symptom is that the filepath for any images is returned as a link by the program. The syntax for images is identical to the syntax for links, except for a `!` at the beginning. The program didn't search for `![` in the file, and was therefore unable to discern between images and links.