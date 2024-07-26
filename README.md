# CV/Resume Generator using Python and LaTeX

This project demonstrates how to create a simple (nonfunctional) CV/Resume using Python and LaTeX. The script generates a PDF file with a structured layout for personal information, skills, experience, education, and projects.

## Installation

To run this project in Google Colab, you need to install the necessary LaTeX packages. Run the following commands to install them:

```bash
!sudo apt-get update
!sudo apt-get install -y texlive texlive-latex-extra texlive-fonts-recommended
!sudo apt-get install texlive-fonts-extra
!sudo apt-get install texlive-latex-base texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended
```

## Usage

The main script, `create_cv.py`, contains a function `create_cv` that takes personal details and generates a CV in PDF format.

Example usage:

```python
import subprocess

def create_cv(name, career, ambitions, contact_info, skills, languages):
    latex_code = r"""
    \documentclass[a4paper,10pt]{article}
    \usepackage[utf8]{inputenc}
    \usepackage[T1]{fontenc}
    \usepackage{geometry}
    \usepackage{titlesec}
    \usepackage{enumitem}
    \usepackage{hyperref}
    \usepackage{array}
    \usepackage{xcolor}
    \usepackage{tikz}
    \usepackage{multicol}
    \usepackage{tabularx}
    \usepackage{nopageno}  % Package to remove page numbers

    % Page geometry
    \geometry{a4paper, left=0.5in, right=0.5in, top=0.5in, bottom=0.5in}

    % Title format
    \titleformat{\section}{\normalsize\bfseries\color{purple}}{\thesection}{1em}{}
    \titlespacing*{\section}{0pt}{8pt}{4pt}

    % Subtitle format
    \newcommand{\subsectioncolor}[2]{\textcolor{#1}{\textbf{#2}}}

    % Remove numbering from sections
    \setcounter{secnumdepth}{0}

    % Define colors
    \definecolor{myorange}{RGB}{255, 153, 51}
    \definecolor{mygray}{gray}{0.5}
    \definecolor{purple}{RGB}{128, 0, 128}
    \definecolor{pedagcolor}{gray}{0.5}
    \definecolor{leisurecolor}{gray}{0.5}
    \definecolor{instrucolor}{gray}{0.5}

    % Links color
    \hypersetup{
        colorlinks=true,
        linkcolor=black,
        filecolor=black,
        urlcolor=mygray,
    }

    % Custom column settings
    \newcolumntype{L}[1]{>{\raggedright\arraybackslash}p{#1}}
    \newcolumntype{C}[1]{>{\centering\arraybackslash}p{#1}}
    \newcolumntype{R}[1]{>{\raggedleft\arraybackslash}p{#1}}

    % Skill bar with smaller width and font
    \newcommand{\skillbar}[3]{
        \begin{minipage}[t]{#1}
            \textbf{#2}\\
            \begin{tikzpicture}
                \filldraw[fill=purple!80!white, draw=purple] (0, 0) rectangle (#3*1.5, 0.3);  % Adjust width scale factor
                \filldraw[fill=purple!20!white, draw=purple] (#3*1.5, 0) rectangle (1.5, 0.3);
            \end{tikzpicture}
        \end{minipage}
    }

    % Language bar with smaller width and font
    \newcommand{\languagebar}[3]{
        \begin{minipage}[t]{#1}
            \textbf{#2}\\
            \begin{tikzpicture}
                \filldraw[fill=purple!80!white, draw=purple] (0, 0) rectangle (#3*1.5, 0.3);  % Adjust width scale factor
                \filldraw[fill=purple!20!white, draw=purple] (#3*1.5, 0) rectangle (1.5, 0.3);
            \end{tikzpicture}
        \end{minipage}
    }

    \begin{document}
    \pagestyle{empty}  % Remove page number

    % Header part with adjusted columns and left-aligned contact info
    \begin{tabularx}{\textwidth}{L{0.25\textwidth} L{0.35\textwidth} C{0.1\textwidth} X}
        % First column: picture part (placeholder for now)
        [Picture Placeholder] &
        % Second column: name, career, and ambitions
        \begin{tabular}[t]{@{}l@{}}
            \textbf{\LARGE """ + name + r"""}\\
            """ + career + r"""\\
            \vspace{5pt}
            \textit{""" + ambitions + r"""}
        \end{tabular} &
        % Third column: empty
        &
        % Fourth column: contact information
        \begin{tabular}[t]{@{}l@{}}
            \parbox[t]{\linewidth}{
                Tehran, Iran\\
                09050332772\\
                rynhap@gmail.com\\
                \texttt{\url{linkedin.com/in/ryhnap}}\\
                \texttt{\url{stackoverflow.com/users/15634507/ryhn}}
            }
        \end{tabular}
    \end{tabularx}

    \vspace{10pt}

    % Body part with adjusted columns
    \begin{tabularx}{\textwidth}{L{0.35\textwidth} X}
        % First column: Interests, Skills, Languages, Achievements
        \begin{minipage}[t]{0.35\textwidth}

            \section*{Skills}
            \begin{multicols}{2}
                \small
                \skillbar{0.45\textwidth}{C}{0.8}
                \skillbar{0.45\textwidth}{C++}{0.7}
                \skillbar{0.45\textwidth}{Python}{0.9}
                \skillbar{0.45\textwidth}{Java}{0.85}
                \skillbar{0.45\textwidth}{HTML}{0.75}
                \skillbar{0.45\textwidth}{CSS}{0.7}
                \skillbar{0.45\textwidth}{JavaScript}{0.8}
                \skillbar{0.45\textwidth}{Verilog}{0.6}
                \skillbar{0.45\textwidth}{System Verilog}{0.6}
                \skillbar{0.45\textwidth}{R}{0.7}
                \skillbar{0.45\textwidth}{Matlab}{0.7}
                \skillbar{0.45\textwidth}{Linux}{0.8}
                \skillbar{0.45\textwidth}{SQL}{0.75}
            \end{multicols}

            \section*{Interests}
            \subsectioncolor{pedagcolor}{Pedagogical Activities}\\
            AI, game programming, math, geometry, IT, Security, test, web/app development\\
            \subsectioncolor{leisurecolor}{Leisure Activities}\\
            sport, book, movie, literature\\
            \subsectioncolor{instrucolor}{Instrumental Activities}\\
            Violin

            \section*{Achievements}
            Bachelor's Degree in Computer Engineering\\
            {\footnotesize\textit{Graduated on June 7, 2024}}\\
            Developer at Dotin Company\\
            {\footnotesize\textit{From July 2022 to July 2024}}

            \section*{Languages}
            \begin{multicols}{2}
                \small
                \languagebar{0.45\textwidth}{English}{0.8}
                \languagebar{0.45\textwidth}{Korean}{0.4}
                \languagebar{0.45\textwidth}{Arabic}{0.5}
            \end{multicols}

        \end{minipage} &
        % Second column: Experience, Education, Projects
        \begin{minipage}[t]{0.65\textwidth}
            \section*{Experience}

            \subsection*{Open Bookshelf - Discrete Mathematics Persian Book}
            \textit{Designer and Checker \hfill 03/2021 - 07/2021}\\
            Tehran, Iran
            Open Bookshelf is a great platform dedicated to providing equal and high-quality Discrete Mathematics content for Persian speakers for free, ensuring direct interaction with end-users.
As a Designer and Checker, I was responsible for analyzing the book content, collaborating with the creative department, preparing proposals to link ideas with problems, and simplifying the solutions. My goal was to manage the project to create a delightful user experience and ensure the design was

 correct.
Contact: Behzad Shayegh - behzad.shayegh@ut.ac.ir

            \subsection*{Developer at Dotin}
            \textit{Back End Java Developer, Unit and E2E Tester, Front End Developer (React) \hfill 07/2022 - 07/2024}

            Developed and maintained robust back end services using Java and Spring framework for API web development.
Conducted unit testing and end-to-end (E2E) testing to ensure the quality and reliability of the applications.
Worked on the front end using React to create user-friendly and responsive web interfaces.

            \section*{Education}
            \subsection*{Bachelor of Science in Computer Engineering}
            \textit{The University of Tehran, Tehran \hfill Graduated on June 7, 2024}\\
            Advanced Programming, Artificial Intelligence, Computer Architecture, Digital Logic Design, Programming Languages and Compilers, Introduction to Computing Systems and Programming, Discrete Mathematics, Data Structure and Algorithms, Information Technology Project Management, 
Data Structure, Computer Networking, Database, Test, Engineering Economy, 
Software Engineering, Embedded Systems Cyber-Physical Systems, 
Distributed System, Technical English, Internet Engineering, 
Electronic Commerce, Electric Workshop, Information Theory

            \section*{Projects}

            \subsection*{I/O \& Vector / Encrypt\&Decrypt}
            \textit{UT-AP \hfill 02/2020 - 02/2020}
            \begin{itemize}[leftmargin=*]
                \item Hash cracking and course suggestions.
            \end{itemize}

            \subsection*{Recursion/Cryptography/Interview/MaxPath}
            \textit{UT-DS\&DA \hfill 03/2020 - 03/2020}
            \begin{itemize}[leftmargin=*]
                \item Solved problems using recursion.
            \end{itemize}

            \subsection*{Object-Oriented Design/GoodReads}
            \textit{UT-AP \hfill 03/2020 - 03/2020}
            \begin{itemize}[leftmargin=*]
                \item Analysis some data from GoodReads website.
            \end{itemize}

            \subsection*{Games: Othello and TicTacToe and FieldRunners}
            \textit{UT-AP\&ICSP \hfill 12/2018 - 01/2019}
            \begin{itemize}[leftmargin=*]
                \item Simple implementation of Field Runner game using SDL library wrapper RSDL.
            \end{itemize}
            
            \pagebreak

            \subsection*{Web/UTRIP}
            \textit{UT-AP \hfill 03/2019 - 03/2019}
            \begin{itemize}[leftmargin=*]
                \item A simple hotel reservation system which the system can recommend hotels base on your previous activities.
            \end{itemize}

            \subsection*{C--}
            \textit{UT-Compiler \hfill 09/2021 - 12/2021}
            \begin{itemize}[leftmargin=*]
                \item Compiler base on some new rules.
            \end{itemize}

            \subsection*{Restoring Divider/Single-Cycle \& Multi-Cycle Mips \& Pipe-Line Processor}
            \textit{US-D\&BA \hfill 07/2021 - 12/2021}
            \begin{itemize}[leftmargin=*]
                \item Making divider logically. Making Processor with two memory and one register file. Making Processor using one memory. Read all instruction immediately.
            \end{itemize}

            \subsection*{Additional Projects}
            % Add more projects as needed, ensuring this section continues on the new page.
            \textit{Project Title \hfill Start Date - End Date}
            \begin{itemize}[leftmargin=*]
                \item Project description.
            \end{itemize}

            % Continue listing additional projects here.
        \end{minipage}
    \end{tabularx}

    \end{document}
    """

    with open("cv_template.tex", "w") as f:
        f.write(latex_code)

    result = subprocess.run(["pdflatex", "cv_template.tex"], capture_output=True, text=True)

    if result.returncode != 0:
        print("Error in LaTeX compilation:")
        print(result.stdout)
        print(result.stderr)
    else:
        print("PDF generated successfully.")

# Example usage
name = "Reyhane Ahmadpoor"
career = "Junior Software Developer"
ambitions = "Always looking for new experiences"
contact_info = ""  # Contact info is now included directly in LaTeX code
skills = {
    "C": 0.8,
    "C++": 0.7,
    "Python": 0.9,
    "Java": 0.85,
    "HTML": 0.75,
    "CSS": 0.7,
    "JavaScript": 0.8,
    "Verilog": 0.6,
    "System Verilog": 0.6,
    "R": 0.7,
    "Matlab": 0.7,
    "Linux": 0.8,
    "SQL": 0.75
}
languages = {
    "English": 0.8,
    "Korean": 0.4,
    "Arabic": 0.5
}

create_cv(name, career, ambitions, contact_info, skills, languages)
```

## Notes

This project is a work in progress and requires further refinement to enhance its features and usability. Contributions and suggestions are welcome!
