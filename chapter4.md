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
Pane tähele, et sisestad `tosscoin(1)`. Sündmuste ruumi defineerimiseks tuleb lisada ka tõenäosuste vektor täpselt nii nagu see on näites tehtud.

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

