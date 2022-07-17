| Programare Orientata pe Obiecte | Trei în linie |
| --- | --- |

# **Trei în linie**

**22.12.2021**

| **Îndrumător:** |
 | **Student:** |
| --- | --- | --- |
| **dr. ing. Daniel Morariu** |
 | **Nedelcu Gabriel**** 222/1** |

**Istoric Versiuni**

| **Data** | **Versiune** | **Descriere** | **Autor** |
| --- | --- | --- | --- |
| 22.11.2021 | 1.0 | funționare joc fară nicio clasa | Nedelcu Gabriel |
| 23.11.2021 | 1.1 | impementare animație cand pucurile cad | Nedelcu Gabriel |
| 29.11.2021 | 1.2 | implementare a 2 clase + alte modificări | Nedelcu Gabriel |
| 30.11.2021 | 1.3 | evidențiere a celor 3 pucuri când cineva a câstigat | Nedelcu Gabriel |
| 02.12.20021 | 1.4 | implememntare rețea + alte modificări | Nedelcu Gabriel |
| 19.12.2021 | 1.5 | Arată pucul unde o să fie inserat când ținem mousul pe buton | Nedelcu Gabriel |

**Cuprins**

**Istoric Versiuni [2](# __RefHeading___ Toc25143192)**

**Cuprins [3](# __RefHeading___ Toc25143193)**

**1**** Specificarea cerințelor software [4](# __RefHeading___ Toc25143194)**

**1.1Introducere [4](# __RefHeading___ Toc25143195)**

1.1.1Obiective [4](# __RefHeading___ Toc25143196)

1.1.2Definiții, Acronime și Abrevieri [4](# __RefHeading___ Toc25143197)

1.1.3Tehnologiile utilizate [4](# __RefHeading___ Toc25143198)

**1.2Cerințe specifice [4](# __RefHeading___ Toc25143199)**

**2**** Funcționalitate [5](# __RefHeading___ Toc25143200)**

**2.1Descriere [5](# __RefHeading___ Toc25143201)**

**2.2Fluxul de evenimente [5](# __RefHeading___ Toc25143202)**

2.2.1Fluxul de bază [5](# __RefHeading___ Toc25143203)

2.2.2Fluxuri alternative [5](# __RefHeading___ Toc25143204)

**3**** Implementare [6](# __RefHeading___ Toc25143207)**

**3.1Diagrama de clase [6](# __RefHeading___ Toc25143208)**

**3.2Descriere detaliată [7](# __RefHeading___ Toc25143209)**

# 1Specificarea cerințelor software

## 1.1Introducere

Trei în linie este un joc de strategie pentru 2 jucători al cărui obiectiv este formarea unei linii de câte trei pucuri de aceeași culoare pe orizontală, pe verticală sau pe diagonală.

### 1.1.1Obiective

Obiectivele aplicației sunt: oprirea aplicației când avem un câștigător și afișarea lui, fiecare jucător să-și poată alege culoarea de puc la începutul fiecărei partide, animație de cădere a pucului în momentul inserării lui , jucătorii să aibă posibilitatea să modifice numărul de coloane ale jocului.

### 1.1.2Definiții, Acronime și Abrevieri

Matrice[5][5] din clasa JOC ne ajută să calculăm dacă avem un câstigător.

Obiectele p1,p2 de tip PUC din clasa JOC au scopul de a reține celelalte 2 pucuri daca avem &quot;trei în linie&quot;.

Cu ajutorul variabilei SchimbaOrdinea facem ca primul jucator sa nu inceapa intotdeauna primul dupa creerea a unui nou meci.

### 1.1.3Tehnologiile utilizate

Pentru crearea proiectului am folosit C++ Builder 6 si Microsoft Office Word.

### 1.1.4Cerințe specifice

Aplicația _Trei în linie are_ implementate:

-evidențiarea celor 3 pucuri cand sunt &quot;în linie&quot;

-animație când un puc cade în cadru până în poziția lui

-schimbarea cursorului când dorim să inserăm într-o coloana deja plină

-crearea unu alt joc fara a trebui să repornim aplicația

-calcularea victoriilor pentru fiecare jucător și afișarea lor

-să arate unde o să cadă pucul când ai mousul pe respectiva coloană

# 2Funcționalitate

## 2.1Descriere

I)Animația de cădere a pucului arată parcurusul pucului prin tabla de joc până la poziția lui corectă. Funcția a fost implementată să dea un aspect cât mai apropriat față de jocul fizic.

II)Evidențierea pucului unde o să ajungă înainte de-l insera/da drumul în tabla de joc.

Funția a fost implemetată ca jucatorii să stiu unde o sa ajungă pucul dupa mutarea respectivă.

## 2.2Fluxul de evenimente

### 2.2.1Fluxul de bază

1. Funcția de animație este realizată cu ajutorului unui timmer și a unei porțiuni de cod din funcția _cadere_ din fereastra principală.

După apăsarea a unui buton dintre cele 5 pentru a insera un puc se pornește animația conform:

1.obiectul _PiesaCurenta_ de tip PUC din clasa JOC reține linia și coloana unde ar trebui să ajungă pucul

2. se afișează pucul pe linia=0 si coloana respectivă

3. se pornește timmer-ul și se apelează metoda _cadere_din fereastra principală cu paramtrii: PiesaCurenta.Linie și PiesaColoana.Coloana .

Ideea de bază a metodei _cadere_ este următoarea:

-ștergerea pucului precedent (de pe linia=0) și afișarea pe următoarea linie (linia=1) și coloana respectivă

-ștergerea pucului precedent (de pe linia=1) și afișarea pe următoarea linie (linia=2) și coloana respectivă

....

...

...

etc

Ștergerea și afișarea se face după un anume timp, decalarat la timmer (50ms )

O să folosim o variabilă numita _linia0_ declarata în clasa JOC inițializată cu 0 și după fiecare ștergere o incrementăm

Pentru afișare și ștergere avem doua fucții care se ocup de asta. Fiecare primiește ca parametri două int-uri , anume o linie(=_linia0_) și o coloană(PiesaCurenta.coloana) pentru a știi de unde să șteargă/afișeze pucul.

Procedeul de ștergere și afișare o să se repete pană când _linia0_ o să fie egală cu PiesaCurenta.linie, iar pucul respectiv o ramână afișat pe tot parcursul jocului.

Când pucul a ajuns unde trebuie, varabila _linia0_ o să redevină 0 pentru a putea anima și următoarele pucuri.

1. Evidențierea pucului unde ar trebuii să cadă înainte de a fi inserat.

Acest eveniment se declanșeaza atunci cand avem mousul pe un buton, iar după apăsarea lui sau neavând mousul pe niciunul dintre cele 5 butonoane, acest eveniment se oprește.

O să ne folosim de o variabila PUC denumita _arata_ .

Dacă avem mousul pe un buton, obiectul _arata_ o să rețină linia și coloana pucului cel care va fi inserat dacă va fi apăsat pe acel buton. O să eividențiăm un puc pe această linie și coloană.

Daca mutam mousul de pe un buton pe altul trebuie mai intai sa stergem fostul puc evidentiat. Linia și coloana pentru fostul puc evidențiat sunt încă reținute în _arata_, astfel e usor să stim de unde trebuie șters. După stergere , _arata_preia coordonatele pentru noul buton și evidențiăm un puc pentru noiile coordonate.

Dacă avem mousul pe buton apoi îl mutăm în afara lui, ștergem pucul evidențiat, iar _arata_ nu își schimbă valorile membrilor. Această idee produce o eroare, anume atunci când pornim aplicația, programul nostru încearcă să șteargă un puc evidențiat cu coordonatele reținute în _arata_, însă _arata_ nu are nicio valaore reținută, doarece încă nu am mutat mousul pe nicun buton.

De aceea prima data _arata_ reține pentru linie valoarea 10, și pentru coloană valaorea 10 și ștergem numai dacă linia și coloana sunt diferite de 10.

După apăsarea unui buton pentru a insera un puc și de face animația de cadere a lui, pucul evidențiat anterior îl ștergem ,iar în _arata_ repunem din nou valoriile 10 si 10.

# 3Implementare

## 3.1Diagrama de clase

![](RackMultipart20220717-1-vko3lc_html_e0e79281c39972c5.png)

## 3.2Descriere detaliată

![](RackMultipart20220717-1-vko3lc_html_8005557ce92b1b6e.png)

3
