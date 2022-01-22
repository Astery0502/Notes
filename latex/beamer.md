# Log for Learning how to make  #

- Minimal code presentation

```tex
% Quick start guide
\documentclass{beamer}

\usetheme{default}

\begin{document}

\begin{frame}
    This is your first presentation!
\end{frame}

\end{document}
```

- Tips
    - specify the **beamer** documentclass
    - slide themes to change with the color and layout of the slides 
    - frame environment to create a slide
    
## simple workflow ##

### a simple title page ###

1. title and subtitle of the presentation
2. name of the author
3. institute and the date 
4. with **\titlepage** to print the provided details in the created frame environment

```tex
% Quick start guide
\documentclass{beamer}

\usetheme{default}
\usetheme{AnnArbor}

% Title page details
\title{\LaTeX{} Beamer introduction}
\subtitle{Quick-start guide}
\author{latex-beamer.com}
\institute{Online Education}
\date{\today}

\begin{document}

\begin{frame}
% Print the title page as the first slide
\titlepage
\end{frame}

\end{document}
```

- further settings
    - multiple authors with different affiliations

```tex
% Two authors with different affiliations
\author{First Author\inst{1} \and Second Author\inst{2}}

\institute{\inst{1} Affiliation of the 1st author \and
 \inst{2} Affiliation of the 2nd author}
```
    - modify footer details: **add brackets to the command in question with desired text**

```tex
% Modify footer text: 
\title[Center text]{Your First \LaTeX{} Presentation}
\subtitle{My-subtitle}
\author[Left text]{latex-beamer.com}
\date[Right text]{\today}
```

