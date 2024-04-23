# db-university

sercizio di oggi:
nome repo: db-university
Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
  Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.
  Utilizzare https://www.diagrams.net/ per la creazione dello schema.
  Esportare quindi il diagramma in jpg e caricarlo nella repo. (modificato)

## dEpartments

ID|BIGINT| PK | INDEX | AI |UNIQUE| NOTNULL
name | VARCHAR (50) | NOTNULL
description |TEXT | NULL

## corsi_laurea

ID |BIGINT| PK | INDEX | AI |UNIQUE| NOTNULL
id_department |FK | NOTNULL
name | VARCHAR (50) | NOTNULL
description |TEXT | NULL

## materie

ID|BIGINT| PK | INDEX | AI |UNIQUE| NOTNULL
id_corsolaurea |FK | NOTNULL
name | VARCHAR (50) | NOTNULL
description |TEXT | NULL
credits | SMALLINT | NOTNULL

## teachers

ID|BIGINT| PK | INDEX | AI |UNIQUE| NOTNULL
id_materia |FK | NOTNULL
name |VARCHAR (100) | NOTNULL
surname |VARCHAR (100) | NOTNULL
materia |VARCHAR (50) | NULL

## students

ID|BIGINT| PK | INDEX | AI |UNIQUE| NOTNULL
id_corsolaurea |FK | NOTNULL
id_appello |FK | NOTNULL
name |VARCHAR (100) | NOTNULL
surname |VARCHAR (100) | NOTNULL
students_number | MEDIUMINT| NOTNULL

## appelli

ID|INT| PK | INDEX | AI |UNIQUE| NOTNULL
id_materia |FK | NOTNULL
date |DATE| NOTNULL

## votes_students

ID|INT| PK | INDEX | AI |UNIQUE| NOTNULL
id_appello |FK | NOTNULL
id_student |FK | NOTNULL
vote | INT | NOTNULL
