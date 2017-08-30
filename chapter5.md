---
title       : Diskreetsed jaotused
description : Insert the chapter description here



--- type:NormalExercise lang:r xp:100 skills:1 key:c288cce688
## Juhuslik suurus (1a)

Juhuslik suurus $X$ on defineeritud kui funktsioon  $X:\Omega \to R$, mis seab igale elementaarsündmusele $w \in \Omega$ vastavusse täpselt ühe väärtuse $X(\omega)=x$ reaalarvude hulgast $R$. Näiteks, viskame münti 2 korda ja juhuslikuks suuruseks on *saadud vappide arv*. Sel juhul sisaldab $\Omega$ paare $(v,k), (k,v), (v,v), (k,k)$ ja juhuslik suurus $X$ võib saada väärtuseks 0, 1 või 2.

Paketis `prob` on olemas funktsioon `addrv()` (ingl. lühendatud *Add Random Variable*), mille abil on lihtne luua juhuslikku suurust olemasoleva tõenäosusruumi baasil. See aga omakorda tähendab, et eelnevalt peab looma elementaarsündmuste hulga $\Omega$ koos vastavate tõenäosustega. Uuri, kuidas on see tehtud järgneva näite abil.

**Näide.** Veeretatakse kolme neljatahulist täringut korraga ning juhuslikuks suuruseks $U$ on *veeretamisel saadud silmade arvude summa* ja $V$ on *saadud maksmimaalne tulemus*. Vaatame, kuidas saab neid defineerida `R`-is.

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
head(Omega.ruum)

# Alternatiivne võimalus U jaoks (muutuja nimi olgu U1, sest U on juba olemas):
Omega.ruum <- addrv(Omega.ruum, FUN = sum, invars = c("X1", "X2", "X3"), name = "U1")

# Täienda käsk nii, et see looks juh. suuruse V (maksimaalne silmade arv ühel veeretamisel)
Omega.ruum <- addrv(Omega.ruum, FUN = max, invars = c("X1", "X2", "X3"), name = "V")
```

*** =sct
```{r}
test_function("rolldie", args = c("nsides", "makespace"),incorrect_msg=c("Kas määrasid argumendile `nsides` väärtuse 4?", "Kas määrasid argumendile `makespace` loogilise väärtuse `TRUE`?"))
test_function("addrv", index=1, eval=FALSE)
test_function("addrv",args=c("space", "FUN", "invars"), index=2, eval=FALSE)
test_function("addrv",args=c("space", "FUN", "invars"), incorrect_msg=c("Kas määrasid argumendile `space` väärtuse `Omega.ruum`?", 
                   "Kas määrasid argumendile `FUN` funktsiooni `max`?", "Kas määrasid argumendile `invars` muutujate vektori elementidega `X1, X2, X3`?"), index=3, , eval=TRUE)
success_msg("Nice job!")
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



