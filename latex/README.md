# LaTeX

Cheat Sheet for LaTeX

## Structure

### Chapters

```tex
\chapter{...} % Only for documents of type book
\section{...}
\subsection{...}
\subsubsection{...}
```

### Abstract

```tex
\begin{document}

\begin{abstract}

...

\end{abstract}

\end{document}
```

## Packages

> Package imports must be made between `\documentclass` and `\begin{document}`. The syntax is as follows: `\usepackage[options]{package} `

Set language of document to german: `\usepackage[ngerman]{babel}`

Add utf8 support: `\usepackage[utf8]{inputenc}`

Add support for graphics: `\usepackage{graphicx}`

Make hyperlinks clickable: `\usepackage{hyperref}`

Disable red borders around hyperlinks: `\usepackage[hidelinks]{hyperref}`

## Text formatting

Bold: `\textbf{}`

Cursive: `\textit{}`

Small Capitals (proper names): `textsc{}`

Monospace (variables): `\textttt{}`

Emphasise (cursive, but allows nesting): `emph{}`

## Lists

### Unordered lists

```tex
\begin{itemize}
   \item ...
   \item ...
\end{itemize}
```

### Ordered lists

```tex
\begin{enumerate}
   \item ...
   \item ...
\end{enumerate}
```

## Graphics

> `\usepackage{graphicx}` must be imported.

```tex
\begin{figure}
   \centering
   \includegraphics{filename.ending}
   \caption{Text below the graphic}
   \label{fig:unique-id-used-for-referencing}
\end{figure}
```

### Scaling

Scale size: `\includegraphics[scale = 0.7]{filename.ending}`

Scale size to width of text: `\includegraphics[width = \textwidth]{filename.ending}`

### Positioning

> Positioning arguments are just a recommendation for LaTeX. To "enforce" the positioning, prefix the argument with a `!`.

```tex
\begin{figure}[hbtp]
...
\end{figure}
```

- `h` - Here
- `b` - At bottom of current page
- `t` - At top of current page
- `p` - On an extra page

### Graphics side by side

#### Minipage

Creates two seperate graphics with seperate captions side by side.

```tex
\begin{figure}[h]
	\begin{minipage}{0.4\textwidth}
		\centering
		\includegraphics[width=0.3\textwidth]{filename.ending}
		\caption{...}
		\label{fig:id-0}
	\end{minipage}
	% Optional space: ~, \quad, \qquad, \hfill
	\begin{minipage}{0.4\textwidth}
		\centering
		\includegraphics[width=0.3\textwidth]{filename.ending}
		\caption{...}
		\label{fig:id-1}
	\end{minipage}
\end{figure}
```

#### Subfigure

Creates a graphic with a global caption and two subraphics with one caption each.

```tex
\begin{figure}[h]
	\centering
	\begin{subfigure}[b]{0.3\textwidth}
		\centering
		\includegraphics[width=0.4\textwidth]{filename.ending}
		\caption{...}
		\label{fig:id-0.0}
	\end{subfigure}
	% % Optional space: ~, \quad, \qquad, \hfill
	\begin{subfigure}[b]{0.3\textwidth}
		\centering
		\includegraphics[width=0.4\textwidth]{filename.ending}
		\caption{...}
		\label{fig:id-0.1}
	\end{subfigure}
	\caption{...}
	\label{fig:id-0}
\end{figure}
```

## Tables

Arguments for `table` (Numbering tables and list them in the table list): See (figure positioning)[#Positioning].

Arguments for `tabular` specify number and alignment of columns:
- `l` - left-justified
- `r` - right-justified
- `c` - centered
- `|` - Vertical line

Commands in the table:
- `&` - Column seperator
- `\\` - Line seperator
- `\hline` - Horizontal line

```tex
\begin{table}[h]
	\centering
	\caption{...}
	\begin{tabular}{|c|c|}
		\hline
		0.0 & 0.1 \\
		\hline
		1.0 & 1.1 \\
		\hline
	\end{tabular}
	\label{tab:id-0}
\end{table}
```

## Formulas

### Inline

```tex
$ formula $
```

### Paragraph
```tex
\[
...
\]
```

### Numbered
```tex
\begin{equation}
	\label{eq:id-0}
	...
\end{equation}
```

### Multiline formular

The `&` vertically aligns the formulars.

`\nonumber` disables nummerating this formular.

Import `\usepackage{amsmath}` is needed.

```tex
\begin{align}
	... & ... \\
	& = ...\nonumber \\
	... & ...
\end{align}
```

### Operators

- `\cdot` - Multiplication dot
- `\text{...}` - Text in formular. Needs `\usepackage{amsmath}`
- `\frac{top}{bottom}` - Fraction
- `x_{2} x^{3} x_{2}^{3}` - Sup- and Superscript
- `x y, x\, y, x\quad y, x \qquad y` - Spacing
- `\alpha, \beta, \gamma, \delta` - Greek alphabet
- `\sqrt[n]{a+b}` - Root
- `\{, \}` - Curly braces
- `\sin(x) \cos(x) \tan(x)` - sinus, cosinus, tangens
- `\log x, \ln(y), \exp(x+5)` - Logarithm and exponential function
- `\sum_{i=0}^{5} i` - Sum
- `\int_{0}^{\infty} x\, dx` - Integral

## References

> References are clickable if `\usepackage{hyperref}` is imported.

```tex
\ref{fig:id-0}
```

Naming conventions for labels:
- `fig:` - Figures
- `tab:` - Tables
- `cha:` - Chapters
- `sec:` - Sections

Automatically add type of reference before number: `\autoref{}`. Requires `\usepackage{hyperref}`

## Quotes / Cites

```tex
\cite{}
```

### Bib File

```bib
@Book{id-0,
    author = {...},
    title={...},
    publisher = {...},
    year = {...}
}

@article{id-1,
    author={..., ...},
    title={...},
    journal={...},
    volume={...},
    number={...},
    pages={...--...},
    year={...}
}
```

#### Required information for different sources

| source        | required                       | optional                                                     |
| ------------- | ------------------------------ | ------------------------------------------------------------ |
| article       | author, title, journal, year   | volume, number, pages, month, note                           |
| book          | author, title, publisher, year | volume, series, address, edition, month, note, isbn          |
| inproceedings | author, title, booktitle, year | editor, colume, series, pages, address, month, organzitation, publisher, note |
| misc          |                                | author, title, howpublished, month, year, note               |
