# Esercizio - db University

Modellizzare la struttura di una tabella per memorizzare tutti i dati riguardanti una università:
- FATTO, sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- FATTO, ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- FATTO, ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- FATTO, ogni Corso può essere tenuto da diversi Insegnanti;
- FATTO, ogni Corso prevede più appelli d'Esame;
- FATTO, ogni Studente è iscritto ad un solo Corso di Laurea;
- FATTO, ogni Studente può iscriversi a più appelli di Esame;
- FATTO, per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni.

## University [Es->UniversitàdegliStudidiCa'Foscari]
ID:                                         PK                      NOTNULL, UNIQUE, INDEX, AI
Name:                   [Ca'Foscari]        VARCHARD(50)            NOTNULL, UNIQUE, INDEX
Location:               [Venezia]           VARCHARD(25)            NULL
Department_id:                              <Departments (* - 1)>
- UN università può avere PIU' dipartimenti, UN dipartimento può appartenere a UNA sola università - MANY TO ONE.

                        -------------------------------------------------

## Departments - [Es->Dipertimento_Economia]
ID:                                         PK                      NOTNULL, UNIQUE, INDEX, AI
Name:                   [Economia]          VARCHARD(50)            NOTNULL, UNIQUE, INDEX
Location:               [Città]             VARCHARD(15)            NULL 
Degree_id:                                  <Degrees (* - 1)>
- UN dipartimento offrè PIU' corsi di laurea, UN corso di laurea può appartenere a UN solo dipartimento - MANY TO ONE.

                        -------------------------------------------------

## Degrees - [Es->CorsodiLaurea_Turismo]
ID:                                         PK                      NOTNULL, UNIQUE, INDEX, AI
Name:                   [Turismo]           VARCHARD(30)            NOTNULL, UNIQUE, INDEX
Student_id:                                 <Students (* - 1)>
- UN corso di laurea ha PIU' studenti, UNO studente ha un solo corso di laurea - MANY TO ONE.
Course_id:                                  <Courses (* - *)>
- UN corso di laurea può avere PIU' corsi singoli, UN corso singolo può essere per PIU' corsi di laurea - MANY TO MANY.

                        -------------------------------------------------

## Courses - [Es->CorsiSingoli_Appl.WebforTourism]
ID:                                         PK                      NOTNULL, UNIQUE, INDEX, AI
Name:           [Appl.WebforTourism]        VARCHARD(30)            NOTNULL, UNIQUE, INDEX
Hours:          [600h]                      VARCHARD(5)             NOTNULL
Teacher_id:                                 <Teachers (* - *)>
- UN corso singolo può avere PIU' insegnanti, UN insegnante può avere PIU' corsi singoli - MANY TO MANY.
Exam_session_id:                            <Exam_sessions (* - *)>
- UN corso singolo può avere PIU' appelli, UN appello può essere per PIU' corsi singoli - MANY TO MANY.

                        -------------------------------------------------

## Teachers - [Es->CorsiSingoli_Appl.WebforTourism]
ID:                                         PK                      NOTNULL, UNIQUE, INDEX, AI
Name:                   [Mario]             VARCHARD(15)            NULL
Lastname:               [Rossi]             VARCHARD(30)            NOTNULL

                        -------------------------------------------------

## Exam_sessions - [Es->SessionediEsame.settembre2020]
ID:                                         PK                      NOTNULL, UNIQUE, INDEX, AI
Date:                   [12:00-04/02/2022]  TIMEDATE                NOTNULL, INDEX
Exams:                  [NomiMaterie]       VARCHARD(100)           NOTNULL, UNIQUE
Teacher_id:                                 <Teachers (* - *)>
- UNA sessione può avere PIU' insegnanti, UN insegnante può avere PIU' sessioni - MANY TO MANY.

                        -------------------------------------------------

## Students
ID:                                         PK                      NOTNULL, UNIQUE, INDEX, AI
Name:                   [Fabio]             VARCHARD(15)            NOTNULL
Lastname:               [Rossi]             VARCHARD(30)            NOTNULL
Matricola:              [223454]            CHARD(6)                NOTNULL, UNIQUE
Type_degree_id:                             <Degrees (1 - *)>
- UNO studente può avere UN solo corso di laurea, UN corso di laurea può avere PIU' studenti - ONE TO MANY.
Exam_session_id:                            <Exam_sessions (* - *)>
- UNO studente può iscriversi a PIU' appelli, UN appello può avere PIU' studenti iscritti - MANY TO MANY.
ResultExam_id:                              <ResultExam (* - 1)>
- UNO studente può avere PIU' risultati, UN risultato di esame può avere UN solo studente - MANY TO ONE.

                        -------------------------------------------------

## ResultExam
ID:                                         PK                      NOTNULL, UNIQUE, INDEX, AI
Name:                   [Fabio]             VARCHARD(30)            NOTNULL
Lastname:               [Rossi]             VARCHARD(30)            NOTNULL
Matricola:              [223454]            CHARD(6)                NOTNULL, UNIQUE
Exam_session_id:                             <Exam_sessions (1 - 1)>
- UNO risultato può avere UNA sessione di esame , UNA sessione di esame può avere UN risultato - ONE TO ONE.
Voto:                   [20]                VARCHARD(2)             NOTNULL, UNIQUE

