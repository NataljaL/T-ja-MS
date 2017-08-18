---
title       : Kombinatoorika
description : Kordame kombinatoorikat. Edukat tööd!


--- type:NormalExercise lang:r xp:100 skills:1 key:2cc7965304
## Elementaarsündmuste hulk

Lihtsamaid elementaarsündmuste ruume saab `R`-is defineerida  funktsiooni `c` abil, näiteks

`Omega <- c("kiri", "vapp")`

Tõenäosusteoorias on palju ülesandeid, mis on seotud mündi viskamisega või täringu veeretamisega. Nende jaoks on olemas paketis `prob` vastavad funktsioonid:

`tosscoin(k)` ja `rolldie(k, nsides = n)`, 

kus `k` vastab müntide/täringute arvule ja `n` täringu korral tahkude arvule (6 on vaikeväärtus).

*** =instructions
Pakett `prob` on juba lisatud ja kasutuseks valmis!

1. Defineeri ülesandes 1 elementaarsündmuste hulk `Omega1`, mis vastab klaasi kukkumisele põrandale järgmiste väärtustega: `põhja peale`, `põhi ülespidi` ja `külili` (sisesta väärtused antud järjekorras).
2. Defineeri ülesandes 2 elementaarsündmuste hulk `Omega2`, mis vastab kolme mündi viskamisele funktsiooni `tosscoin()` abil. 
3. Defineeri ülesandes 3 elementaarsündmuste hulk `Omega3`, mis vastab kahe täringu visketulemustele, millel mõlemal on vaid 4 tahku.

*** =hint
* Ülesandes 1 kasuta funktsiooni `c()` nii nagu on see tehtud näites.
* Ülesandes 2 kasuta argumendina arvu `3`.
* Ülesandes 3 kasuta funktsiooni `rolldie()` esimese argumendiga `k = 2` ja teisega `nsides = 4`.

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
# Ülesanne 1. Klaasi kukkumine

Omega1 <- c(___________)

# Ülesanne 2. Kolme mündi viske tulemused

Omega2 <- ________________

# Ülesanne 3. Kahe 4-tahulise täringu viske tulemused

Omega3 <- ________________

```

*** =solution
```{r}
# Ülesanne 1. Klaasi kukkumine

Omega1 <- c("põhja peale", "põhi ülespidi", "külili")

# Ülesanne 2. Kolme mündi viske tulemused

Omega2 <- tosscoin(3)

# Ülesanne 3. Kahe 4-tahulise täringu viske tulemused

Omega3 <- rolldie(2, nsides = 4)


```

*** =sct
```{r}
test_object("Omega1", undefined_msg = NULL, incorrect_msg = "Kontrolli kas muutuja `Omega1` väärtused on samad kui ülesandes antud ja nõutud järjekorras!")
test_object("Omega2", undefined_msg = NULL, incorrect_msg = "Kas kasutasid funktsiooni `tosscoin` ja panid argumendiks `3`?")
test_object("Omega3", undefined_msg = NULL, incorrect_msg = "Kas kasutasid funktsiooni `rolldie` täringute arvuga `2` ja argumendi `nsides` väärtusega `4`?")

success_msg("Hästi tehtud! Suundu järgmise harjutuse juurde!")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:1bfaf7f47c
## Kombinatsioonid

Funktsioon `expand.grid()` võimaldab luua kõikvõimalikest kombinatsioonidest andmetabeli. Funktsiooni sisendiks on elementaarsündmuste vektor või vektorid. Seda funktsiooni on samuti võimalik kasutada elementaarsündmuste hulga defineerimisel.  


*** =instructions

- Proovi läbi näited 1 ja 2.
- Ülesanne: olgu antud kaardipakk järgmiste väärtustega:
`"A", 2, 3, 4, 5, 6, 7, 8, 9, 10, "J", "Q", "K"` ja mastidega
`"poti", "ärtu", "risti", "ruutu"`
Moodustada nendest vektoritest kõikvõimalikud kombinatsioonid. NB! Kasuta esimese argumendina väärtuseid ja teisena masti.


*** =hint

Kasuta vektori moodustamiseks funktsiooni `c()`, näiteks `c("punane", "kollane", "sinine")`.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Näide 1. Kõikvõimalikud kombinatsioonid visates ausat münti kolm korda:
mynt <- c("k", "v")
tulemused1 <- expand.grid(mynt, mynt, mynt)
tulemused1

# Näide 2. Korraga visatakse ausat münti ja ausat täringut. Kõikvõimalikud kombinatsioonid:
mynt <- c("k", "v")
taring <- 1:6
tulemused2 <- expand.grid(mynt,taring)
tulemused2

# Ülesanne
vaartused <- _______________
mastid <- ________________

tulemused3 <- ______________ 

```

*** =solution
```{r}
# Näide 1. Omistame muutjale y väärtuse 2 ja väljastame väärtuse
# Näide 1. Kõikvõimalikud kombinatsioonid visates ausat münti kolm korda:
mynt <- c("k", "v")
tulemused1 <- expand.grid(mynt, mynt, mynt)
tulemused1

# Näide 2. Korraga visatakse ausat münti ja ausat täringut. Kõikvõimalikud kombinatsioonid:
mynt <- c("k", "v")
taring <- 1:6
tulemused2 <- expand.grid(mynt,taring)
tulemused2

# Ülesanne
vaartused <- c("A", 2, 3, 4, 5, 6, 7, 8, 9, 10, "J", "Q", "K")
mastid <- c("poti", "ärtu", "risti", "ruutu")

tulemused3 <- expand.grid(vaartused, mastid)

```

*** =sct
```{r}
test_object("vaartused",  incorrect_msg = "Kas sisestatud väärtused ja nende järjekord vektoris `vaartused` vastab ülesandes antule? ")
test_object("mastid",  incorrect_msg = "Kas sisestatud väärtused ja nende järjekord vektoris `mastid` vastab ülesandes antule? ")

test_student_typed("tulemused3 <- expand.grid(vaartused, mastid)", not_typed_msg =  "Kas kasutasid õiget funktsiooni? Kas argumendid on õiges järjekorras?")

success_msg("Tubli! Võta kommi!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:05f6e26773
## Valik tagasipanekuga ja tagasipanekuta
Sageli on ülesanded seotud valikutega mingist hulgast (näiteks urnist). Valikud võivad olla kas tagasipanekuga (võtame juhuslikult ühe kuuli urnist, fikseerime selle tulemuse ning paneme kõrvale; seejärel võtame järgmise kuuli jne) või tagasipanekuga (peale tulemuse fikseerimist paname kuuli tagasi urni). Mõnikord on valikute juures tähtis ka võtmise järjekord (näiteks, esimesena on võetud musta värvi kuul, teisena punane, kolmandana sinine jne).

Erinevaid valikuid saab teostada funktsiooni `urnsamples(x, size, replace, ordered)` abil, mis kuulub paketti `prob`. Argumentide seletused ja võimalikud väärtused on järgmised:

* `x` -- väärtuste vektor, millest toimub valik (väärtused kõik peavad olema erinevad!)
* `size` -- valitavate objektide arv
* `replace` -- kas tagasipanekuga (`=TRUE`) või tagasipanekuta (`=FALSE`) valik
* `ordered` -- kas valitavate objektide järjestus on tähtis (`=TRUE`) või mitte (`=FALSE`)

*** =instructions

* Proovi läbi näited 1-4, kus urnist kuulidega 1, 2 ja 3 võetakse 2 kuuli.
* Ülesanne: koosnegu urn viiest kuulist tähtedega `"a"` kuni `"e"` (funktsioon `letters[]` on abiks!), muutuja nimeks olgu `urn1`. Urnist võetakse 3 kuuli tagasipanekuta, kusjuures võtmise järjekord on oluline. Millised on võimalikud katsetulemused? Omista need muutujale `tulemus`.

*** =hint
* Funktsioon `letters` deineerib vektorina tähestikku, millest tuleks võtta 5 esimest tähte käsuga `1:5`.


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
#Näide 1. Kaks kuuli urnist tagasipanekuTA, järjestus POLE oluline
urn <- 1:3
a <- urnsamples(urn, size = 2, replace = FALSE, ordered = FALSE)
a

#Näide 2. Kaks kuuli urnist tagasipanekuGA, järjestus POLE oluline
b <- urnsamples(urn, size = 2, replace = TRUE, ordered = FALSE)
b

#Näide 3. Kaks kuuli urnist tagasipanekuTA, järjestus ON oluline
c <- urnsamples(urn, size = 2, replace = FALSE, ordered = TRUE)
c

#Näide 4. Kaks kuuli urnist tagasipanekuGA, järjestus ON oluline
d <- urnsamples(urn, size = 2, replace = TRUE, ordered = TRUE)
d

#Ülesanne. Kolm kuuli viiest tagasipanekuta, järjestus on oluline.
urn1 <- ________________________
tulemus <- ___________________________
```

*** =solution
```{r}
#Näide 1. Kaks kuuli urnist tagasipanekuTA, järjestus POLE oluline
urn <- 1:3
a <- urnsamples(urn, size = 2, replace = FALSE, ordered = FALSE)
a

#Näide 2. Kaks kuuli urnist tagasipanekuGA, järjestus POLE oluline
b <- urnsamples(urn, size = 2, replace = TRUE, ordered = FALSE)
b

#Näide 3. Kaks kuuli urnist tagasipanekuTA, järjestus ON oluline
c <- urnsamples(urn, size = 2, replace = FALSE, ordered = TRUE)
c

#Näide 4. Kaks kuuli urnist tagasipanekuGA, järjestus ON oluline
d <- urnsamples(urn, size = 2, replace = TRUE, ordered = TRUE)
d

#Ülesanne. Kolm kuuli viiest tagasipanekuta, järjestus on oluline.
urn1 <- letters[1:5]
tulemus <- urnsamples(urn1, size = 3, replace = FALSE, ordered = TRUE)

```

*** =sct
```{r}
#test_object("tulemus",  incorrect_msg = "Kas kasutasud funktsiooni `urnsamples` argumentidega `replace = FALSE` ja `ordered = TRUE`?")

test_function("urnsamples",
              args = c("x", "size", "replace", "ordered"), index = 5,
              eval = TRUE,
              eq_condition = "equivalent",
              not_called_msg = c("Nõutud funktsiooni pole kasutatud!", "2", "3", "4"),
              args_not_specified_msg = c("Mõni nõutud argument on puudu.", "vale2", "vale3", "vale4"),
              incorrect_msg = c("viga1", "viga2", "viga3", "viga4"))
              
              
#test_output_contains(tulemus, incorrect_msg = "Jälle mingi viga, tulemus pole sama")

success_msg("Tubli! Võta kommi!")




```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:651f739370
## Ülesanne 1 (värvipliiatsid)

Karbis on 15 erinevat värvipliiatsit. Juhuslikult võetakse sealt 4 ja antakse Liisale joonistamiseks. Mitu erinevat varianti on selle nelja pliiatsi valimiseks? Pliiatsite järjestus pole Liisa jaoks oluline. 

NB! Kaks funktsiooni võivad osutuda kasulikuks  ridade arvu leidmisel tabelis: `dim()` ja `nrow()`.

*** =instructions

- 32760
- 3060
- 1365
- 50625

*** =hint

Kasuta funktsiooni `urnsamples()`

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

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "Mõtle veel!"
msg_success <- "Just nii!"
test_mc(correct = 3, feedback_msgs = c(msg_bad,msg_bad, msg_success, msg_bad))
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:2f502adc67
## Ülesanne 2 (arvude koostamine)

Mitu erinevat 6-kohalist arvu on võimalik koostada numbritest 0, 1, 3, 5, 7 ja 9?

NB! Arvud, mis algavad 0-ga (nt 051397) ei sobi, kuna sel juhul saame 5-kohalise arvu (51397).
*** =instructions

- 336
- 720
- 600
- 43531

*** =hint
Leia kõigepealt järjestuste arvu kuuest kuue kaupa ja lahuta sellest maha järjestuste arvu viiest viie kaupa.

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

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "Proovi veel!"
msg_success <- "Väga tubli!"
test_mc(correct = 4, feedback_msgs = c(msg_bad,msg_bad,  msg_bad, msg_success))
```




--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:e40ebad664
## Ülesanne 3 (sport)
Toomas tegeleb aktiivselt spordiga, kusjuures 4 päeval nädalas ta sõidab rattaga, 2 päeval nädalas käib jõusaalis ja 1 päeva nädalas ta puhkab. Mitu erinevaid nädalaplaane on võimalik tal selle põhjal koostada?

Vihje: kasuta funktsiooni `urnsamples` ja edasi rakenda funktsiooni `unique()` unikaalsete ridade saamiseks. Ära unusta kasutada funktsiooni `nrow()` ridade arvu saamiseks tabelis. 


*** =instructions

* 105
* 203
* 5040
* minu vastust pole pakutud

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

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "See tulemus pole küll õige"
msg_success <- "Suurepärane!"
test_mc(correct = 1, feedback_msgs = c( msg_success, msg_bad,msg_bad,  msg_bad))
```
