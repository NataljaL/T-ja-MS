---
title       : Sündmused
description : Mõned kasulikud käsud sündmuste defineerimiseks. Alustame! :)

--- type:NormalExercise lang:r xp:100 skills:1 key:6075a680df
## Sündmuse lihtsustatud definitsioon

Lõpliku või loenduva elementaarsündmuste hulga $\Omega$ korral võib sündmuseks $A$ nimetada selle hulga $\Omega$ alamhulka. Alamhulga võtmine on `R`-i jaoks lihtsalt ridade valik elementaarsündmuste tabelist, mis vastab teatud tingimusele. Selliseid võimalusi on palju.

Olgu katseks 3 täringu viskamine. Elementaarsündmuste hulk koosneb: $|\Omega|=6\cdot 6\cdot 6 = 216$ katsetulemusest. 

Proovi järgmised näited läbi ja uuri, kuidas on võimalik sündmust defineerida `R`-is.

*** =instructions

* **Näide 1.** Saame viidata tabeli `Omega` ridadele kasutades rea numbreid. Antud näites mingit tingimust sündmuste $A$ ja $B$ defineerimiseks ei kasutata.
* **Näide 2.** Olgu sündmuseks $C$ kõik read, kus 1. täringu katsetulemuseks on 2 silma. Käsud muutujate `C1`, `C2` ja `C3` defineerimiseks annavad ühte ja sama sündmust $C$.
* **Näide 3.** Olgu sündmus $D$ kõik read, kus 2. täringu katsetulemuseks on 2 kuni 4 silma. Uuri muutujaid `D1`, `D2` ja `D3`.
* **Näide 4.** Viimaseks on sündmus $E$, mis vastab sellistelekatsetuöemustele, kus kõigi kolme täringu viske tulemuste summa on suurem kui 16. Muutujad `E1` ja `E2` on vaid mõned võimalused selle sündmuse defineerimiseks.


*** =hint

Kas vajutasid nuppu `Submit Answer`?

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
Omega <- rolldie(3) #kõikvõimalike katsetulemuste hulk kolme täringu veeretamisel

# Näide 1. Alamhulga võtmine ridade numbrite järgi:
A <- Omega[1:3,] #1. kuni 3. rida kaasaarvatud
A
B <- Omega[c(2,4,6),] #2., 4. ja 6. rida
B

# Näide 2. Esimese täringu katsetulemuseks on 2 silma. Järgmised käsud viivad sama tulemuseni:
C1 <- Omega[Omega$X1==2,] #veeru nime järgi
C1
C2 <- Omega[Omega[,1]==2,] #veeru järjekorra numbri järgi
C2
C3 <- subset(Omega, X1==2) #funktsiooni subset() abil
C3

# Näide 3. Teise täringu katsetulemuseks on 2 kuni 4 silma. Võimalusi on jällegi mitmeid:
D1 <- Omega[Omega$X2 %in% 2:4,] #ära unusta koma (soovime siiski kõiki veerge Omegast)
D1
D2 <- Omega[Omega$X2>=2 & Omega$X2<=4,] #märk & vastab tingimusele AND 
D2
D3 <- subset(Omega, X2 %in% 2:4)
D3

# Näide 4. Tulemuste summa on suurem kui 16. Mõned võimalused:
E1 <- subset(Omega, X1 + X2 + X3 > 16)
E1
E2 <- Omega[Omega$X1 + Omega$X2 + Omega$X3 > 16,]
E2
```

*** =solution
```{r}
Omega <- rolldie(3) #kõikvõimalike katsetulemuste hulk kolme täringu veeretamisel

# Näide 1. Alamhulga võtmine ridade numbrite järgi:
A <- Omega[1:3,] #1. kuni 3. rida kaasaarvatud
A
B <- Omega[c(2,4,6),] #2., 4. ja 6. rida
B

# Näide 2. Esimese täringu katsetulemuseks on 2 silma. Järgmised käsud viivad sama tulemuseni:
C1 <- Omega[Omega$X1==2,] #veeru nime järgi
C1
C2 <- Omega[Omega[,1]==2,] #veeru järjekorra numbri järgi
C2
C3 <- subset(Omega, X1==2) #funktsiooni subset() abil
C3

# Näide 3. Teise täringu katsetulemuseks on 2 kuni 4 silma. Võimalusi on jällegi mitmeid:
D1 <- Omega[Omega$X2 %in% 2:4,] #ära unusta koma (soovime siiski kõiki veerge Omegast)
D1
D2 <- Omega[Omega$X2>=2 & Omega$X2<=4,] #märk & vastab tingimusele AND 
D2
D3 <- subset(Omega, X2 %in% 2:4)
D3

# Näide 4. Tulemuste summa on suurem kui 16. Mõned võimalused:
E1 <- subset(Omega, X1 + X2 + X3 > 16)
E1
E2 <- Omega[Omega$X1 + Omega$X2 + Omega$X3 > 16,]
E2
```

*** =sct
```{r}
success_msg("Lahe! Suundu järgmise harjutuse juurde!")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:b60b137d4b
## Ülesanne. Neli täringut

Olgu katseks nelja 6-tahulise täringu veeretamine. Huvipakkuvaks sündmuseks $A$ on kõik sellised realisatsioonid, kus silmade summa jagub 20-ga. Millega võrdub $|A|$ ehk sündmuse $A$ elementaarsündmuste arv?

Abiks on tehe `a %% b`, mis leiab jäägi arvu `a` jagamisel arvuga `b`. 

*** =instructions

* 1292
* 4
* 35
* minu vastust pole

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

msg_bad <- "Kahjuks pole õige vastus."
msg_success <- "Super!"
test_mc(correct = 3, feedback_msgs = c(msg_bad,msg_bad,  msg_success,  msg_bad))
```


