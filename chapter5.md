---
title       : Diskreetsed jaotused
description : Insert the chapter description here


--- type:NormalExercise lang:r xp:100 skills:1 key:c288cce688
## Juhuslik suurus (1)

Juhuslik suurus $X$ on defineeritud kui funktsioon  $X:\Omega \to R$, mis seab igale elementaarsündmusele $w \in \Omega$ vastavusse täpselt ühe väärtuse $X(\omega)=x$ reaalarvude hulgast $R$. Näiteks, viskame münti 2 korda ja juhuslikuks suuruseks on *saadud vappide arv*. Sel juhul sisaldab $\Omega$ paare $(v,k), (k,v), (v,v), (k,k)$ ja juhuslik suurus $X$ võib saada väärtuseks 0, 1 või 2.

Paketis `prob` on olemas funktsioon `addrv()` (ingl. lühendatud *Add Random Variable*), mille abil on lihtne luua juhuslikku suurust olemasoleva tõenäosusruumi baasil. St eelnevalt peab looma nii elementaarsündmuste hulga $\Omega$ kui ka vastavad tõenäosused. Uuri, millised on selle võimalused järgneva näite abil.

**Näide.** Veeretatakse kolme neljatahulist täringut korraga ning juhuslikuks suuruseks $U$ on *veeretamisel saadud silmade arvude summa* ja $V$ on *saadud maksmimaalne tulemus*. Vaatame, kuidas saab teostada `R`-is.

*** =instructions
* Täienda käsk, mis loob tõenäosusruumi kolme täringu veeretamiseks.
* Uuri, kuidas on loodud juhuslik suurus $U$. Kas suurust $V$ on võimalik sarnaselt luua?
* Käsul `addrv` on olemas argument `FUN`, kus on võimalik rakendada `R`-i funktsioone juhuslike suuruste defineerimiseks. Näiteks, $U$ jaoks saaksime rakendada funktsiooni `sum`. Vaata, kuidas see töötab.
* Mida saaksime rakendada juhusliku suuruse $V$ loomiseks? Täienda vastav käsk.

*** =hint

*** =pre_exercise_code
```{r}
source_github <- function(user = "cran", package = "prob") {
  
  library(httr)
  package_source <- paste0(user, "/",package, "/")
  url <- paste0("https://api.github.com/repos","/", package_source, "git/trees/master?recursive=1")
  req <- GET(url)
  stop_for_status(req)
  filelist <- unlist(lapply(content(req)$tree, "[", "path"), use.names = F)
  R_files <- filelist[grep("R/",filelist)]
  
  for(file in R_files) {
    url <- paste0("https://raw.githubusercontent.com/", package_source, "master/", file)
    source(url)
  }
}
save(file = "source_github.Rda", source_github)

source_github()

source_github <- function(user = "cran", package = "combinat") {
  
  library(httr)
  package_source <- paste0(user, "/",package, "/")
  url <- paste0("https://api.github.com/repos","/", package_source, "git/trees/master?recursive=1")
  req <- GET(url)
  stop_for_status(req)
  filelist <- unlist(lapply(content(req)$tree, "[", "path"), use.names = F)
  R_files <- filelist[grep("R/",filelist)]
  
  for(file in R_files) {
    url <- paste0("https://raw.githubusercontent.com/", package_source, "master/", file)
    source(url)
  }
}
save(file = "source_github.Rda", source_github)

source_github()
```

*** =sample_code
```{r}
# Tõenäosusruumi loomine. NB! Täringutel on 4 tahku!
Omega.ruum <- rolldie(3, nsides = ________, makespace = _______)

# Juhuslik suurus U:
Omega.ruum <- addrv(Omega.ruum, U = X1 + X2 + X3)
head(Omega.ruum)

# Alternatiivne võimalus U jaoks (muutuja nimi olgu U1, sest U on juba olemas):
Omega.ruum <- addrv(Omega.ruum, FUN = sum, invars = c("X1", "X2", "X3"), name = "U1")

# Täienda käsk nii, et see looks juh. suuruse V (maksimaalne silmade arv ühel veeretamisel)
Omega.ruum <- addrv(__________, FUN = _________, invars = _______________, name = "V")
```

*** =solution
```{r}
# Tõenäosusruumi loomine. NB! Täringutel on 4 tahku!
Omega.ruum <- rolldie(3, nsides = 4, makespace = TRUE)

# Juhuslik suurus U:
Omega.ruum <- addrv(Omega.ruum, U = X1 + X2 + X3)

# Alternatiivne võimalus U jaoks (muutuja nimi olgu U1, sest U on juba olemas):
Omega.ruum <- addrv(Omega.ruum, FUN = sum, invars = c("X1", "X2", "X3"), name = "U1")

# Täienda käsk nii, et see looks juh. suuruse V (maksimaalne silmade arv ühel veeretamisel)
Omega.ruum <- addrv(Omega.ruum, FUN = max, invars = c("X1", "X2", "X3"), name = "V")
```

*** =sct
```{r}

```



--- type:NormalExercise lang:r xp:100 skills:1 key:d273281f35
## Juhuslik suurus (2)

Jätkame eelmise näitega ning leiame juhuslike suuruste $U$ ja $V$ jaotused. Tuletame meelde, et $U$ on *kolme neljatahulise täringu veeretamisel saadud silmade arvude summa* ja $V$ on *saadud maksmimaalne tulemus*. 

*** =instructions
* Kirjuta aknas `R Console` funktsioon `head(Omega.ruum)` ning uuri, millised on väärtused juhuslikel suurustel $U$ ja $V$.
* Juhusliku suuruse jaotuse saamiseks peame saama tabeli, mis sisaldab selle juhusliku suuruse kõikvõimalikke väärtuseid (ühe korra) ning vastavaid tõenäosusi. Tabelis `Omega.ruum` on aga praegu mõlemal juhuslikul suurusel korduvaid väärtuseid. 
* Tabeli agrgeerimiseks saab kasutada funktsiooni `marginal()` paketist `prob`. Vaata, kuidas on see tehtud juhusliku suuruse $U$ jaoks. Kirjuta analoogiline käsk muutuja $V$ jaotustabeli saamiseks.
* Jaotustabelit saab illustreerida graafiku abil kasutades funktsiooni `plot()`. Sellel funktsioonil on palju omadusi. Tähtsad nendest on `x = ` ehk väärtuste hulk x-telje jaoks, `y = ` väärtuste hulk y-telje jaoks (sama dimensioon, mis x-telje jaoks); `xlab` ja `ylab` on vastavate telgede nimetused ning `h` on diskreetse jaotuse iseloomustamiseks sobilik joonise tüüp. 
* Kirjuta käsk muutuja $V$ graafiku loomiseks muutuja $U$ näite järgi. Muuda ka joonise värv punaseks. 

*** =hint

*** =pre_exercise_code
```{r}
source_github <- function(user = "cran", package = "prob") {
  
  library(httr)
  package_source <- paste0(user, "/",package, "/")
  url <- paste0("https://api.github.com/repos","/", package_source, "git/trees/master?recursive=1")
  req <- GET(url)
  stop_for_status(req)
  filelist <- unlist(lapply(content(req)$tree, "[", "path"), use.names = F)
  R_files <- filelist[grep("R/",filelist)]
  
  for(file in R_files) {
    url <- paste0("https://raw.githubusercontent.com/", package_source, "master/", file)
    source(url)
  }
}
save(file = "source_github.Rda", source_github)

source_github()

source_github <- function(user = "cran", package = "combinat") {
  
  library(httr)
  package_source <- paste0(user, "/",package, "/")
  url <- paste0("https://api.github.com/repos","/", package_source, "git/trees/master?recursive=1")
  req <- GET(url)
  stop_for_status(req)
  filelist <- unlist(lapply(content(req)$tree, "[", "path"), use.names = F)
  R_files <- filelist[grep("R/",filelist)]
  
  for(file in R_files) {
    url <- paste0("https://raw.githubusercontent.com/", package_source, "master/", file)
    source(url)
  }
}
save(file = "source_github.Rda", source_github)

source_github()

# harjutuse jaoks vajalik:
Omega.ruum <- rolldie(3, nsides = 4, makespace = TRUE)
Omega.ruum <- addrv(Omega.ruum, FUN = sum, invars = c("X1", "X2", "X3"), name = "U")
Omega.ruum <- addrv(Omega.ruum, FUN = max, invars = c("X1", "X2", "X3"), name = "V")
```

*** =sample_code
```{r}
# Muutuja U jaotustabel
U.jaotus <- marginal(Omega.ruum, vars = "U")
U.jaotus

# Muutuja V jaotustabel
V.jaotus <- ________________________________
V.jaotus

# Muutuja U jaotus graafikul
plot(x = U.jaotus$U, y = U.jaotus$probs, xlab = "u", ylab = "P(U = u)", type = "h", col = "blue")

# Muutuja V jaotus fraafikul
________________________________________ # ise!
```

*** =solution
```{r}
# Muutuja U jaotustabel
U.jaotus <- marginal(Omega.ruum, vars = "U")
U.jaotus

# Muutuja V jaotustabel
V.jaotus <- marginal(Omega.ruum, vars = "V")
V.jaotus

# Muutuja U jaotus graafikul
plot(x = U.jaotus$U, y = U.jaotus$probs, xlab = "u", ylab = "P(U = u)", type = "h", col = "blue")

# Muutuja V jaotus fraafikul
plot(x = V.jaotus$V, y = V.jaotus$probs, xlab = "v", ylab = "P(V = v)", type = "h", col = "red") # ise!
```

*** =sct
```{r}

```



--- type:NormalExercise lang:r xp:100 skills:1 key:af3c1cf198
## Binoomjaotus
**Binoomajaotus** on hästi tuntud *diskreetne* jaotus. Selle jaotusega on huvipakkuva sündmuse $A$ realiseerumiste arv lõplikus katseseerias, kus kõik katsed on sõltumatud ning igal katsel antud sündmus võib kas realiseeruda või mitte. Sündmus $A$ realiseerub igas katses võrdse tõenäosusega. Jaotusel on kaks parameetrit: katsete arv $n$ katseseerias ja sündmuse $A$ realiseerumise tõenäosus ühes katses $p = P(A)$.

Binoomajotusega on näiteks kirjade arv, kui visata münti 20 korda ($X\sim Bin(20,\ 0.5)$). Binoomajotusega on seotud `R`-is järgmised funktsioonid:

* `dbinom()`: binoomjaotuse väärtustele vastavad tõenäosused, $P(X = x)$;
* `pbinom()`: kumulatiivsed tõenäosused ehk jaotusfunktsiooni väärtused, $P(X \leq x)$;
* `qbinom()`: kvantiilide väärtused binoomjaotuse korral;
* `rbinom()`: (pseudo)juhuslik(ud) väärtus(ed) binoomjaotusest.

Kasuta `help()` või `?`, et teada saada rohkem nende funktsioonide kasutuse kohta.

*** =instructions
* Oletame, et eelneva statistika põhjal poes, kus müüakse t-särke on teada: klient ostab särgi tõenäosusega 0.3. Poes on hetkel 8 kliente, kes vaatavad ringi. Kliendid omavahel ei suhtle.
* Mis on tõenäosus, et kaks nendest ostavad t-särgi?
* Mis on tõenäosus, et seitse nendest ostavad t-särgi?
* Mis on tõenäosus, et *vähemalt* kaks nendest ostavad t-särgi? Pane tähele, et pead kasutama argumenti `lower.tail`. Sellel argumendil on kaks võimalikku väärtust: kui `TRUE` (vaikimisi), siis leitakse tõenäosust $P(X\leq x)$, kui `FALSE`, siis $P(X>x)$.
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Mis on tõenäosus, et kaks klienti ostab t-särgi ära? P(X = 2)
dbinom(2, size = 8, prob = 0.3)

# Mis on tõenäosus, et seitse klienti ostab t-särgi ära? P(X = 7)


# Mis on tõenäosus, et vähemalt kaks klienti ostab t-särgid ära? P(X => 2)


```

*** =solution
```{r}
# Mis on tõenäosus, et kaks klienti ostab t-särgi ära? P(X = 2)
dbinom(2, size = 8, prob = 0.3)

# Mis on tõenäosus, et seitse klienti ostab t-särgi ära? P(X = 7)
dbinom(7, size = 8, prob = 0.3)

# Mis on tõenäosus, et vähemalt kaks klienti ostab t-särgid ära? P(X => 2)
pbinom(1, size = 8, prob = 0.3, lower.tail = FALSE)

```

*** =sct
```{r}
#LIIVIKA, muuda ingl. keelne msg ära! See harjutus on kopeeritud Kimmolt.


# submission correctness tests

test_output_contains("dbinom(7, size = 8, prob  = 0.3)", incorrect_msg = "Did you calculate the probability of 7 of the customers buying a t-shirt?")

test_output_contains("pbinom(1, size = 8, prob = 0.3, lower.tail=FALSE)", incorrect_msg = "Did you calculate the probability of at least 2 of the customers buying a t-shirt?")

# test if the students code produces an error
test_error()

# Final message the student will see upon completing the exercise
success_msg("Wonderful! Keep going!")

```



--- type:NormalExercise lang:r xp:100 skills:1 key:1491be4b66
## Geomeetriline jaotus
Juhuslik suurus $X$ on **geomeetrilise** jaotusega, kui katseseerias, kus kõik katsed on sõltumatud loetakse katsete arvu kuni sündmuse $A$ esmakordse toimumiseni (kaasa arvatud). Igal katsel saab huvipakkuv sündmus $A$ realiseeruda tõenäosusega $p=P(A)$. See tõenäosus ongi ainsaks jaotuse parameetriks.

Sageli defineeritakse geomeetrilist jaotust ka alternatiivselt: $X$ on katsete arv **enne** esimest toimumist. Just sellist definitsiooni kasutab ka `R`. Analoogiliselt binoomjaotusega on ka geomeetrilisel jaotusel olemas 4 põhifunktsiooni: `dgeom()`, `pgeom()`, `qgeom()`, `rgeom()`. 

Kasuta `help()` või `?` et teada saada rohkem nende funktsioonide kasutuse kohta.


*** =instructions
* Oletame, et eelneva statistika põhjal on teada ühe väravavahi kohta, et ta püüab palli kinni tõenäosusega 0.82.
* Leia tõenäosus, et ta püüab alles kolmanda palli, mis lendab tema värava suunas. Arvestades `R`-i definitsiooni, tuleks leida $P(X = 2)$. 
* Mis on tõenäosus, et ta püüab kinni vaid viienda palli?
* Mis on tõenäosus, et *vähemalt* kaks palli laseb ta väravasse lüüa, enne kui suudab kinni püüda oma esimese palli?


*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Olgu X - ebaõnnestunud katsete arv kuni 1. õnnestunud katseni (pole kaasa arvatud).

# Mis on tõenäosus, et väravavaht suudab kinni püüda vaid kolmandat palli? P(X = 2)
dgeom(2, prob = 0.82)

# Mis on tõenäosus, et väravavaht suudab kinni püüda vaid viiendat palli? P(X = 4)


# Mis on tõenäosus, et *vähemalt* kahte palli ta laseb mööda enne kui suudab 
# kinni püüda esimest oma palli? P(X >= 2) = P(X > 1)


```

*** =solution
```{r}
# Olgu X - ebaõnnestunud katsete arv kuni 1. õnnestunud katseni (pole kaasa arvatud).

# Mis on tõenäosus, et väravavaht suudab kinni püüda vaid kolmandat palli? P(X = 2)
dgeom(2, prob = 0.82)

# Mis on tõenäosus, et väravavaht suudab kinni püüda vaid viiendat palli? P(X = 4)
dgeom(4, prob = 0.82)

# Mis on tõenäosus, et *vähemalt* kahte palli ta laseb mööda enne kui suudab 
# kinni püüda esimest oma palli? P(X >= 2) = P(X > 1)
pgeom(1,  prob = 0.82, lower.tail = FALSE)

```

*** =sct
```{r}

```
