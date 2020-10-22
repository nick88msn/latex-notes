# What is this
A collection of notes scattered on the web on how to start with Latex.
See [References](#references) to find more.

# Starting a Report and adding a Title Page
1. Specify the kind of document we want to write using the [\documentclass](#document-classes) command.
1. Add the [title page](#default-title-page)
1. Add sections, margins and page numbers

# Setup your text editor
* **Vim**
    * vim does not detect the filetype of .tex file but the syntax
      is detected. Of course you can detect the file extension and add some keybinding
      to compile the file and open a pdf editor or to just recompile as follow:
      ```Vimscript
      autocmd BufNewFile,BufRead *.tex  nnoremap <C-P> :!pdflatex -output-directory=. -jobname=document % && zathura document.pdf & disown <CR>
      autocmd BufNewFile,BufRead *.tex  nnoremap <C-B> :!pdflatex -output-directory=. -jobname=document % <CR>
      ```
* **VsCode**
    * [James Yu - Latex Workshop Extension](https://github.com/James-Yu/LaTeX-Workshop)

# Document classes
* book -> book default class has two-sides per page
* report -> report has no \part divisions
* article -> articles have no \part or \chapter divisions
* letter -> 
* slides -> have large sans-serif font

The document class is used at the very beginning of a document \documentclass{class}.
Use \begin{document} to start contents and \end{content} to end the document.

## Default Title Page

```Latex
\author{text} %Author of the document
\title{text}  %Title of the document
\date{text}   %Date
```

These commands go before 
```Latex
\begin{document} 
```
The declaration \maketitle goes at the top of the document.

The end result is something like this:

```Latex
\documentclass{article}

\begin{document}

\title{Report on activites}
\author{Evilsocket}
\date{\today}
\maketitle

Content goes here.

\end{document}

```

## Customizing the Title Page
In case we want to customize the title page we should not use the default functions and instead create a title page like this

```Latex
\begin{titlepage}

\end{titlepage}
```

# Sections Margins and Page Numbers
After the title page we want to introduce a section
We can also label this with something to point later
in another part of the document.

## Document structure
Latex offer some default document components:
* \part{title}
* \chapter{title}
* \section{title}
* \subsection{title}
* \subsubsection{title}
* \paragraph{title}
* \subparagraph{title}

Each element is automatically numbered. To reset the number we can use
\setcounter{secnumdepth}{x} to suppress heading numbers of depth > x
where chapter has depth 0. Use a *, as in \section*{title}, to not number a particular item -- these items will
also not appear in the table of contents.

# Packages
Packages are functions that we can use to extend Latex.
We can import packages before \begin{document} using:

```Latex
\usepackage{package}
```
Some examples:
* fullpage  ->  _Use 1 inch margins_
* anysize   ->  _Set margins: \marginsize{l}{r}{t}{b}_
* multicol  ->  _Use n columns: \begin{multicols}{n}_
* latexsym  ->  _Use latex symbol font_
* graphicx  ->  _Show image: \includegraphics[width=x]{file}_
* url       ->  _Insert URL: \url{http://....}_

# Text Properties

## LaTeX Line and Page Breaking

Sometimes we want that a certain document class (section, paragraph, subsection etc.)
starts at a new page. We have several options, the main ones are:
* \\\\                  start a new paragraph.
* \\\\*                 start a new line but not a new paragraph.
* \\-                   OK to hyphenate a word here.
* \\cleardoublepage     flush all material and start a new page, start new odd numbered page.
* \\clearpage           plush all material and start a new page.
* \\hyphenation         enter a sequence pf exceptional hyphenations.
* \\linebreak           allow to break the line here.
* \\newline             request a new line.
* \\newpage             request a new page.
* \\nolinebreak         no line break should happen here.
* \\nopagebreak         no page break should happen here.
* \\pagebreak           encourage page break. 

* see [here](http://www.personal.ceu.hu/tex/breaking.htm) for more

## Spaces
To add custom horizontal or vertical space we can use:
* \hspace{l}     Horizontal space of lenght l 
* \vspace{l}     Vertical space of lenght l 

## Justification
We add justification adding \begin{properties} and \end{properties} functions.

Latex options are:
* center
* flushleft
* flushright

The code is the following:

```Latex
\begin{center}      %centering
\begin{flushleft}   %ruggedright
\begin{flushright}  %ruggedleft
```

# Table of Contents

Usually we add a table of contents between the **Title** and the first **Section**.
* First we add \tableofcontents inside our document: 
```Latex
\documentclass{article}
\begin{document}
\title{Report on activites}
\author{Evilsocket}
\date{\today}
\maketitle
\tableofcontents
\section{Introduction}
    Content goes here.
\subsection{State of the art}
\end{document}
\tableofcontents
```
* Then, we add some *style adjustements* to our *ToC*:
    * First we want to remove the page number under the toc and 
      start the counter after the *ToC*
        * To remove the counter, we add the following right after the \tableofcontents
          **\thispagestyle{empty}**
    * Then, we want to reset our page counter on the first section
        * So we add \setcounter{page}{1} before the first \section
    * If we want to add an Executive Summary, or an Abstract or Acknowledgements we usually put these sections 
      before the ToC. Adding sections before ToC gives us some issues:
        1. We have numbered sections before the ToC and our first section will start at 2. or more
            * To remove a counter from a section, as detailed [before](#document-structure), we can just add an \* to the section
              declaration (i.e. \section*{Summary})
            * Removing the counter from a section makes also disappear such section from the ToC in order to add a section into the
              ToC manually we need to add the following command:
                * \addcontentsline{toc}{section}{\numberline{}Summary} 
        1. These section prior to the ToC have page numbers and do not appear in the ToC that is generated after them.
            * We can either remove the pagenumber adding an empty pagestyle or changing the pagenumbering from arabic to roman if we want to add multiple sections (list of figures, list of tables etc) before the ToC: 
                \pagenumbering{roman}

* The final code is something like this:

    ```Latex
    %Executive
    \pagenumbering{roman}
    \section*{Executive Summary}
    During the last year we develop some skills and destroyed some people.
    \addcontentsline{toc}{section}{\numberline{}Executive Summary}
    \cleardoublepage

    % Another section before ToC
    \section*{Acknowledgements}
    Thank you
    \addcontentsline{toc}{section}{\numberline{}Acknowledgements}
    \cleardoublepage

    % List of figures, list of tables
    \listoffigures
    \addcontentsline{toc}{section}{\numberline{}List of Figures}
    \cleardoublepage

    \listoftables
    \addcontentsline{toc}{section}{\numberline{}List of Tables}
    \cleardoublepage

    %ToC
    \tableofcontents
    \thispagestyle{empty}
    \cleardoublepage

    %First Section
    \pagenumbering{arabic}
    \setcounter{page}{1}
    \section{Introduction}\label{sec:intro}
    \lipsum{10}
    \subsection{State of the art}
    \lipsum{6}
    ```

# Figures
1. **Import packages**  
    To use figures inside a Latex document we need to add some packages:
    * _graphicx_ : let us import images inside the document \usepackage{graphicx}
    * _float_ : let us control the float position of the image
1. **Add figure inside the body of the document**  
    We add a figure inside the content of our document with a begin and an end declaration:
    * ```Latex
      \begin{figure}[H]     
        % [H] means we want the figure to be positioned here, in this specific part of the document
        ......
      \end{figure} 
       ```
1. We add figure options and front stuffs:
    * ```Latex
      \centering    % let us center the image
      \includegraphics[height=1in]{uri://imgage.jpg}    % add image options and file position
      \caption[Optional]{Real}  % Fig caption, the real one goes under the image, the optional one goes into the Table of Figures
      \label{fig:label}    % let us reference the figure later inside the content 
      ``` 

## List of Figures
List of Figures are as easy to build as the Table of contents.
We add the command \listoffigures in the position we want to add the list.
Usually we add it after the ToC and before the first section.

To include the list of figure inside the Summary we can just add it manually as we did with the summary.  
    
 ```Latex
%...
\listoffigures
\addcontentsline{toc}{section}{\numberline{}List of figures}
%...
```

# Tables
To create a table we declare the table with the following commands
```Latex
\begin{table}
%...table options and content goes here
\end{table}
```
* **Options & Content**
    * Options
        * Table position: center, right, left (i.e. \centering)
        * Table label: use it to reference the table later (\label{tab:label})
        * Table caption: use it to add a table caption and a caption in the list of tables (\caption[Optional]{Real})
    * Content  
      Contents goes inside the command \begin{tabular}.
      Latex adds content in a text structured way inserting one line of the table at the time with an & as column separator.
      To add a new row don't forget to add \\\\ at the end of the previous one.
      \\\hline adds a border under the row.
      We can use some online generator or create a macro to generate a table.
      If we want to copy and paste from another source (excel, word, google sheets or html) we shoud use a vim macro or a generator.
      An example of table is the following:

    ```Latex
    \begin{table}[H]
    \begin{tabular}{|c|c|c|c|c|}
    \hline
    \textbf{\#} & \textbf{Subject} & \textbf{Score} & \textbf{Date} & \textbf{Student} \\ \hline
    1           & Math             & 28             & 22/10/2020    & John Doe         \\ \hline
    2           & Math             & 22             & 22/10/2020    & Mark Smith       \\ \hline
    3           &                  &                &               &                  \\ \hline
    \end{tabular}
    \end{table}
    ```
    This is the preview in markdown:

    | # | Subject | Score |    Date    |   Student  |
    |:-:|:-------:|:-----:|:----------:|:----------:|
    | 1 |   Math  |   28  | 22/10/2020 |  John Doe  |
    | 2 |   Math  |   22  | 22/10/2020 | Mark Smith |
    | 3 |         |       |            |            |

    * Latex tables options and formatting options are a huge topic see [here](https://en.wikibooks.org/wiki/LaTeX/Tables) for some documentation

## List of Tables
We just do what we did with the [List of Figures](#list-of-figures) using the command \listoftables

# Hyperlink
To make the document interactive and let us click on references, table of contents, and urls we need to add a package:
* \usepackage[hidelinks]{hyperref}    % to auto delete all the links formatting (similar to an a tag in html) 

# References
## Bibliographies
To manage references we need to add another program. Depending on our setup and our tastes we could use one of the many 
Bibliography Managers out there such as:
* Mendeley
* Biber
* BibLatex
* BibDesk
* Zotero

Find a complete comparison of Reference Management Software [here](https://en.wikipedia.org/wiki/Comparison_of_reference_management_software)

[What is the logic behind bibliographies in Latex?](https://www.youtube.com/watch?v=46piog3Fzp4)
Well first we probably want that every time we look at some articles or books we don't want to look
back again to it to cite in our work. So we need a file with all the works structured with all the information
and with some unique tags to retrieve it easily:

```Bibliography
    @book{test,
            author="Doe, John",
            title="This is a Book",
            year="2017",
            publisher="Elsevhere"
    }
```

1. To compile this file in Latex we need to install the software. 
   In Ubuntu based distro is already installed with texlive-most package.
   On other distros, such as Arch Linux, we need to install as a separate program:
    ```Shell
    sudo pacman -S biber
    ```
1. To use biber in latex we need to add the package in the Preamble
    ```Latex
    % Bibliography Preamble
    \usepackage[backend=biber, style=authouryear-icomp]{biblatex}
    % Link to the bib file
    \addbibresource{bibliography.bib}
    
    ......
    %Content here
    .....
    \printbibliography
    ```

1. Then, we need to cite something from our bib file:
```Latex
\textcite{test}
```

1. Finally we can create the bibliography with the following command:
```Shell
biber document # with document.tex the file to compile
```

For more about bibliography management and citation [go here](https://en.wikibooks.org/wiki/LaTeX/Bibliography_Management)

## In Page references

* Internal reference 
    ```Latex
    \ref{fig:figure1} 
    \ref{tab:table1}
    ```

* Page reference 
```Latex
\pageref{sec:Introduction}
```

# Lists
Lists in LaTeX are simple but verbose.
* To create a unordered list:
```Latex
\begin{itemize}
    \item Item 1
    \item Item 2
\end{itemize}
```
  Of course we can create sublist nesting another itemize element

* To create an ordered list:
```Latex
\begin{enumerate}
    \item Item 1
    \item Item 2
\end{enumerate}
```
  Of course we can nest an ordered list inside an unordered one and the opposite.

    ```Latex
    \begin{itemize}
        \item First Item
        \item Second Line, long and hope this will wrap to the second line indenting.
        \begin{itemize}
                \item First Sub bullet item
                \item[Title] Second one
        \end{itemize}
        \begin{enumerate}
            \item Number One Item
            \begin{enumerate}
                    \item Sub number
            \end{enumerate}
        \end{enumerate}
    \end{itemize}
    ```

# Math equations
To add a math equation we just need to wrap the equation inside $.
For example:

```Latex
I can write some math in line with text $E=mc^2$ if I wanted to.
Or I can write some equation in a new line like this $$E=mc^2$$ if I wanted to.
```

LaTeX has seen great success based on its math features. Find more [here](https://en.wikibooks.org/wiki/LaTeX/Mathematics)

# Acknowledgements
* [Alexander Baran-Harper](https://www.youtube.com/channel/UC_aQTJgfrnCb8coPbZ5cgJw) Youtube Channel
* [Ceu.hu](http://www.personal.ceu.hu/tex/latex.htm)
* [Wikibooks](https://en.wikibooks.org/wiki/LaTeX/)
