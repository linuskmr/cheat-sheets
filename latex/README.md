# latex

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
