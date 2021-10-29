# latex

## Structure

### Chapters

```latex
\chapter{...} % Only for documents of type book
\section{...}
\subsection{...}
\subsubsection{...}
```

### Abstract

```
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

```
\begin{itemize}
   \item ...
   \item ...
\end{itemize}
```

### Ordered lists

```
\begin{enumerate}
   \item ...
   \item ...
\end{enumerate}
```

