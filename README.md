# What is this
A collection of notes scattered on the web on how to start with Latex.
See [References](#references) to find more.

# Starting a Report and adding a Title Page
1. Specify the kind of document we want to write using the [\documentclass](#document-classes) command.
1. Add the [title page](#default-title-page)
1. Add sections, margins and page numbers

## Document classes
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

## New line
To go to a new line we need to add two spaces or \\ at the end of the current line.

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

# References
* [Alexander Baran-Harper](https://www.youtube.com/channel/UC_aQTJgfrnCb8coPbZ5cgJw) Youtube Channel

