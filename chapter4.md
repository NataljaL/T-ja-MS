---
title       : Tõenäosus
description : Insert the chapter description here

--- type:NormalExercise lang:r xp:100 skills:1 key:4186379252
## Tõenäosusruum

`R`-i jaoks on tõenäosusruumiks objekt tüüpi `data.frame`, mis sisaldab lõpliku elementaarsündmuste hulga $\Omega$ kõikvõimalike väärtuseid ning tõenäosusi, millega need sündmused võivad realiseeruda. 

Paketis `prob` on olemas eraldi funktsioon tõenäosusruumi loomiseks: 

`probspace(x, probs)`, 

kus `x` on elementaarsündmuste ruum ja `probs` tõenäosuste vektor, mille pikkus on võrdne elementaarsündmuste ruumi elementide arvuga ja mille väärtuste summa on 1.

*** =instructions

* Tee läbi näide 1. Pane tähele, kuidas luuakse tõenäosusruum 6-tahulise täringu visketulemuste jaoks.
* Ülesanne. Loo tõenäosusruum nimega `mynt.ruum`, mis vastab ühe tavalise mündi viske tulemustele. Kasuta funktsiooni `tosscoin()`.

*** =hint
Pane tähele, et sisestad `tosscoin(1)`. Ära unusta kohandada vektorit `p`!

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
# Näide 1. 6-tahulise täringu veeretamise tulemused ja vastav tõenäosusruum.
taring <- rolldie(1)                # elementaarsündmuste ruum 
p <- rep(1/6, times=6)              # tõenäosuste vektor
taring.ruum <- probspace(taring, p) # vastav tõenäosusruum

# Ülesanne. Ühe mündi viskamisele vastav tõenäosusruum


```

*** =solution
```{r}
# Näide 1. 6-tahulise täringu veeretamise tulemused ja vastav tõenäosusruum.
taring <- rolldie(1)                # elementaarsündmuste ruum 
p <- rep(1/6, times=6)              # tõenäosuste vektor
taring.ruum <- probspace(taring, p) # vastav tõenäosusruum

# Ülesanne. Ühe mündi viskamisele vastav tõenäosusruum
mynt <- tosscoin(1)
p <- rep(1/2, times=2)
mynt.ruum <- probspace(mynt, p)


```

*** =sct
```{r}
test_object("mynt.ruum", undefined_msg = NULL, incorrect_msg = "Kas muutsid ka tõenäosuste vektori ära?")

success_msg("Väga hea!")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:201fd41f0e
## Klassikaline tõenäosus 1

Sündmuse $A$ klassikalist tõenäosust leitakse nii, et sellele sündmusele vastavate elementaarsündmuste arve $n\_A$ jagatakse  hulga $\Omega$ elementide arvuga $n\_{\Omega}$,
$$P(A)=\frac{n\_A}{n\_{\Omega}}.$$

**Näide.** Kahe täringu veeretamine. Olgu sündmus $A=$'silmade arvu summa on väiksem kui 5'. Leida $P(A)$.

Teame, et elementaarsündmuste ruum koosneb paaridest $\Omega=\{(1,1), (1,2),...(6,6)\}$, seega $n\_{\Omega}=36$. Sündmusele $A$ vastavad järgmised paarid: $A=\{(1,1), (1,2),(1,3),(2,1),(2,2),(3,1)\}$, ehk $n\_A=6$. Kokku saame, et $P(A)=6/36=1/6$. 

`R`-is sündmuse defineerimine on analoogiline alamhulga valimisega, mis vastab teatud tingimusele. Antud näidet saaks `R`-is lahendada järgmiselt.

*** =instructions

* Hulk $\Omega$ ja vastav tõenäosusruum on juba defineeritud muutuja `Omega` abil. 
* Uuri, kuidas on kasutatud funktsiooni `subset()` sündmuse $A$ defineerimiseks.
* Tõenäosust saab leida kahel viisil: otse valemi järgi või kasutades funktsiooni `Prob(event)`, kus `event` on huvipakkuv sündmus. Pane tähele, et funktsioon `Prob()` töötab vaid siis kui eelnevalt on defineeritud tõenäosusruum, ehk kõikvõimalikud elementaarsündmused vastavate tõenäosustega.
* ÜLESANNE. Defineeri sündmus $B$, mis vastab võrdsele silmade arvule mõlemal täringul ning leia selle tõenäosus funktsiooni `Prob()` abil.

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
# Elementaarsündmuste hulk Omega koos vastavate tõenäosustega
Omega <- rolldie(2, makespace = TRUE)
head(Omega) # 6 esimest rida tabelist Omega

# Sündmus A
A <- subset(Omega, X1 + X2 < 5)
A 

# Sündmuse A tõenäosus valemi abil:
P.A.valem <- nrow(A)/nrow(Omega)
P.A.valem

# Sündmuse A tõenäosus funktsiooni Prob() abil:
P.A.funkts <- Prob(A)
P.A.funkts

#ÜLESANNE:
B <- ___________________
P.B <- _________________
P.B

```

*** =solution
```{r}
# Elementaarsündmuste hulk Omega koos vastavate tõenäosustega
Omega <- rolldie(2, makespace = TRUE)
head(Omega) # 6 esimest rida tabelist Omega

# Sündmus A
A <- subset(Omega, X1 + X2 < 5)
A 

# Sündmuse A tõenäosus valemi abil:
P.A.valem <- nrow(A)/nrow(Omega)
P.A.valem 

# Sündmuse A tõenäosus funktsiooni Prob() abil:
P.A.funkts <- Prob(A)
P.A.funkts

#ÜLESANNE:
B <- subset(Omega, X1 == X2)
P.B <- Prob(B)
P.B

```

*** =sct
```{r}

```

