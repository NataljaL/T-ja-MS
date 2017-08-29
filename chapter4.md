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
mynt <- ___________      
p <- ____________
mynt.ruum <- _______________

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
test_object("mynt", undefined_msg = NULL, incorrect_msg = "Mündi viskele vastav sündmuste ruum `mynt` on defineeritud valesti!")
test_object("p", undefined_msg = NULL, incorrect_msg = "Vektor `p` peab sisaldama kahte võrdset elementi 0.5!")
test_object("mynt.ruum", undefined_msg = NULL, incorrect_msg = "Viga muutujas `mynt.ruum`!")

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
Võrdne arv silmi mõlemal täringul on `R`-is tingimus `X1 == X2`. Ülejäänud on analoogiline näitega.

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
test_object("B", undefined_msg = NULL, incorrect_msg = "Valesti defineeritud sündmus `B`! Kasuta funktsiooni `subset` ja tingimust `X1 == X2`!")
test_student_typed("P.B <- Prob(B)", not_typed_msg =  "Viga tõenäosuse leidmisel! Kas kasutasid `Prob(B)`?")

success_msg("Suurepärane! Suundu järgmise harjutuse juurde!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:ebb7291a12
## Klassikaline tõenäosus 2

Väikeste näidete korral (nagu oli kahe täringu viske korral) ei vaja me sageli arvutit tõenäosuste leidmiseks. Elus võib aga ette tulla olukordi, kus teisiti on raske hakkama saada. 

Eelmises harjutuses rakendasime funktsiooni `Prob()` juba eelnevalt defineeritud sündmuse korral. Seda saab kasutada ka teisiti: `Prob(x, event)`, kus `x` on elementaarsündmuste ruum $\Omega$ koos tõenäosustega ja `event` on huvipakkuvale sündmusele vastav loogiline tingimus. 

Uuri näidet ja tee ülesanded läbi!

**Näide.** Miku rahakotis on 9 ühe-eurost münti ja 7 kahe-eurost, ülejäänud on sendid: 6 kahekümne-sendist ja 3 viiekümne-sendist. Kommipakk maksab poes 2 EUR ja 60 senti. Miku rahakott on väike ja ebamugav ning ta võtab sealt kaks münti-senti pimesi. Mis on tõenäosus, et saadud rahaga saab ta kommipaki eest maksta (st et müntide summa on vähemalt 2 EUR ja 60 senti)? Lahendame `R`-is.

*** =instructions
* Esmalt tuleb defineerida elementaarsündmuste hulk koos tõenäosustega, mis vastab kahe mündi-sendi võtmisele tagasipanekuta 25-st mündist-sendist. Sellele vastab muutuja `Omega`. Antud ülesanne on lahendatud eristades kõike münte ja sente (ka sama väärtusega), ehk järjestustega.
* Leiame tõenäsosuse, et saadud müntide-sentide summa on vähemalt 2,60. 
* **Ülesanne.** Eelmises ülesandes leida tõenäosus, et juhuslikult võetud kaks münti-senti on sama väärtusega.

*** =hint
Tuleta meelde, et võrdusmärgi sisestamiseks tingimuse ritta tuleks kasutada topelt võrdusmärki `==`, näiteks `A == B`.

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
# Elementaarsündmuste hulk koos tõenäosustega:
Myndid <- rep(c(1,2,0.2,0.5), c(9,7,6,3)) #Miku rahakott
Omega <- urnsamples(Myndid, size = 2, replace = FALSE, ordered = TRUE) # kombinatsioonid 25-st 2 kaupa, kus järjestus on oleuline
Omega <- probspace(Omega) #lisab tõenäosusi

# Tõenäosus, et juhuslikult võetud 2 mündi summa on vähemalt 2,60.
Tn <- Prob(Omega, X1 + X2 >= 2.6)
Tn

# ÜLESANNE. Samast rahakotist juhuslikult võetud kaks münti on sama väärtusega.
Tn1 <- 
Tn1
```

*** =solution
```{r}
# Elementaarsündmuste hulk koos tõenäosustega:
Myndid <- rep(c(1,2,0.2,0.5), c(9,7,6,3)) #Miku rahakott
Omega <- urnsamples(Myndid, size = 2, replace = FALSE, ordered = TRUE) # kombinatsioonid 25-st 2 kaupa, kus järjestus on oleuline
Omega <- probspace(Omega) #lisab tõenäosusi

# Tõenäosus, et juhuslikult võetud 2 mündi summa on vähemalt 2,60.
Tn <- Prob(Omega, X1 + X2 >= 2.6)
Tn

# ÜLESANNE. Samast rahakotist juhuslikult võetud kaks münti on sama väärtusega.
Tn1 <- Prob(Omega, X1 == X2)
Tn1
```

*** =sct
```{r}
test_object("Tn1", undefined_msg = NULL, incorrect_msg = "Muutuja Tn1 on defineeritud valesti. Proovi veel!")

success_msg("Lahe! Oskad nii hästi `R`-i!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:cbf176cd0c
## Kahe sündmuse ühendi tõenäosus

Üldiselt, kui $A$ ja $B$ on kaks suvalist sündmust, siis nende ühendi (summa) tõenäosuse leidmiseks kasutatakse järgmist valemit:
$$P(A\cup B)=P(A) + P(B) - P(A\cap B).$$

Juhul, kui sündmused $A$ ja $B$ on üksteist välistavad (ei saa toimuda koos), siis $P(A\cap B)= 0$ ja $P(A\cup B)= P(A)+ P(B)$.

Kaardipakist, kus on 52 kaarti mastidega ärtu, ruutu, risti ja poti tõmmatakse juhuslikult üks kaart. Leida tõenäosus, et tõmmatud kaart on kas ärtu masti või suvalist masti pilt (poiss, emand, kuningas või äss).

*** =instructions
* Kaardipakile vastav sündmuste ruum nimega `kaardid.ruum` on juba loodud. Vaata aknas `R Console` selle muutuja väärtused.
* Omista muutujale `A` kõik ärtu masti kaardid ja analoogiliselt muutujale `B` kõik pildid. Kontrolli muutujate väärtused aknas `R Console`!
* Leia sündmuste `A` ja `B` tõenäosused eraldi. Ning ka nende koostoimumise tõenäosus.
* Vastus on leitud muutujas `A.yhend.B.tn`.
* Analoogilise vastuse saab ka teisiti. Uuri!
* ÜLESANNE: leida eelmises ülesandes, et tõmmatud kaart on kas musta masti või numbriga 7, 8 või 9. Lõplikku vastust omista muutujale `yl.tn`.

*** =hint
Ülesande lahendamiseks defineeri esmalt uued vajalikud sündmused ning seejärel kasuta näiteks funktsiooni `Prob(union(___ ,____))`.

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

vaartused <- c("A", 2, 3, 4, 5, 6, 7, 8, 9, 10, "J", "Q", "K")
mastid <- c("poti", "artu", "risti", "ruutu")
pakk <- expand.grid(vaartused, mastid)
colnames(pakk) <- c("vaartused", "mastid")

p <- rep(1/52, times=52)
kaardid.ruum <- probspace(pakk, p)
```

*** =sample_code
```{r}
A <- subset(kaardid.ruum, mastid=="artu")
B <- subset(kaardid.ruum, vaartused %in% c("J", "Q", "K", "A"))

A.tn <- Prob(A); B.tn <- Prob(B); AB.tn <- Prob(intersect(A,B))

A.yhend.B.tn <- A.tn + B.tn - AB.tn

# Alternatiivne viis vastuse saamiseks:
Prob(union(A, B))

#Ülesanne:

yl.tn <- ___________________
```

*** =solution
```{r}
A <- subset(kaardid.ruum, mastid=="artu")
B <- subset(kaardid.ruum, vaartused %in% c("J", "Q", "K", "A"))

A.tn <- Prob(A); B.tn <- Prob(B); AB.tn <- Prob(intersect(A,B))

A.yhend.B.tn <- A.tn + B.tn - AB.tn

# Alternatiivne viis vastuse saamiseks:
Prob(union(A, B))

#Ülesanne:
C <- subset(kaardid.ruum, mastid %in% c("risti", "poti"))
D <- subset(kaardid.ruum, vaartused %in% c(7,8,9))
yl.tn <- Prob(union(C,D))

```

*** =sct
```{r}
test_object("yl.tn", undefined_msg = NULL, incorrect_msg = "Vatus pole õige. Proovi veelkord!")
success_msg("Suurepärane! Kasuta `R`-i ka edaspidi oma töös :) ")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:3c0bf3ee30
## Tinglik tõenäosus
Sündmuse $A$ tõenäosust tingimusel, et sündmus $B$ on toimunud nimetatakse **tinglikukus tõenäosuseks** ja leitakse järgmiselt: 

$$P(A|B)=\frac{P(A\cap B)}{P(B)},\mbox{ kus } P(B)>0.$$

**Näide.** Veeretatakse kahte täringut korraga. Kõikide elementaarsündmuste hulk on paarid $\Omega=\{(1,1), (1,2),...,(6,6)\}$. 

Olgu sündmus $A=$'võrdne silmade arv mõlemal täringul' ja $B=$'silmade arvude summa on vähemalt 8'. 

Leida $P(A|B)$ (tõenäosus saada võrdne arv silmi tingmusel, et silmade arvude summa on vähemalt 8) ja $P(B|A)$ (tõenäosus saada summaks vähemalt 8 tingimusel, et mõlemal täringul on sama arv silmi). 

Joonisel on ristiga märgitud sündmusele $A$ vastavad tulemused ja ringiga need, mis vastavad sündmusele $B$. Selle abil on lihtne veenduda, et 

$$P(A|B)=\frac{P(A\cap B)}{P(B)}=\frac{3/36}{15/36}= \frac{1}{5} \mbox{ ja } P(B|A)=\frac{3/36}{6/36}=\frac{1}{2}.$$

Lahendame ka `R`- i abil.

*** =instructions

* Hulk $\Omega$, mis vastab kahe täringu veeretamisele, on defineeritud muutuja `Omega` abil. Uuri, millest see koosneb!
* Sündmus `A` on defineeritud. Defineeri analoogiliselt ka sündmus `B`.
* Leida $P(A|B)$ valemi järgi täiendades vastavat käsku funktsiooniga `intersect()`.
* Tõenäosust $P(A|B)$ saab leida ka teisiti. Vastav käsk on juba olemas. Kirjuta analoogiline käsk ka sündmuse $B|A$ tõenäosuse leidmiseks. Kas vastused langevad eespool leituga?
 
*** =hint
* Kasuta tingimust `X1 + X2 >= 8` sündmuse `B` defineerimisel.
* Tingliku tõenäosuse leidmisel valemi järgi lugejaks on `Prob(intersect(A,B))`.

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

#Joonis ülesande jaoks:
plot(1:6, 1:6,bty='n',pch='',ylab='1. vise',xlab='', xaxt = 'n', 
ylim=rev(range(c(6.5,0.5))), xlim=c(0.5,6.5))

axis(3, xaxp=c(1, 6, 5))
mtext("2. vise", 1)

grid(nx =NULL, ny = NULL, col = "lightgray", lty = "dotted")

points(1:6,1:6, pch=4, cex=2)
points(2:6, rep(6,5), pch=1, cex=3)
points(3:6, rep(5,4), pch=1, cex=3)
points(4:6, rep(4,3), pch=1, cex=3)
points(5:6, rep(3,2), pch=1, cex=3)
points(6, 2, pch=1, cex=3)

vaartused <- c("A", 2, 3, 4, 5, 6, 7, 8, 9, 10, "J", "Q", "K")
mastid <- c("poti", "artu", "risti", "ruutu")
pakk <- expand.grid(vaartused, mastid)
colnames(pakk) <- c("vaartused", "mastid")

p <- rep(1/52, times=52)
kaardid.ruum <- probspace(pakk, p)
```

*** =sample_code
```{r}
# Elemntaarsündmuste hulga Omega loomine
Omega <- rolldie(2, makespace = TRUE) #kahe täringu veeretamisele vastav tõenäosusruum
head(Omega) #esimest 6 rida tabelist Omega

# Sündmuste A ja B defineerimine
A <- subset(Omega, X1 == X2)
B <- subset(Omega, ________) # ISE! Silmade summa on vähemalt 8

# Tinglik tõenäosus valemi järgi:
Prob(________)/Prob(B)

# Tinglike tõenäosuste leidmine alternatiivselt: 
Prob(A, given = B)
Prob(B, _________) #ISE!
```

*** =solution
```{r}
# Elemntaarsündmuste hulga Omega loomine
Omega <- rolldie(2, makespace = TRUE) #kahe täringu veeretamisele vastav tõenäosusruum
head(Omega) #esimest 6 rida tabelist Omega

# Sündmuste A ja B defineerimine
A <- subset(Omega, X1 == X2)
B <- subset(Omega, X1+X2 >= 8) # ISE! Silmade summa on vähemalt 8

# Tinglik tõenäosus valemi järgi:
Prob(intersect(A,B))/Prob(B)

# Tinglike tõenäosuste leidmine alternatiivselt: 
Prob(A, given = B)
Prob(B, given = A) #ISE!
```

*** =sct
```{r}
test_object("B", undefined_msg = NULL, incorrect_msg = "Kontrolli, kas defineerisid sündmuse `B` õigesti!")
test_student_typed("Prob(intersect(A,B))/Prob(B)", not_typed_msg = "Kas kirjutasid `intersect(A,B)`?")
#test_output_contains("Prob(intersect(A,B))/Prob(B)", incorrect_msg = "Kas kasutasid funktsiooni `intersect(A, B)` tingliku tõenäosuse valemis lugeja leidmiseks?")
test_output_contains("Prob(B, given = A)", incorrect_msg = "Viga. Kas defineerisid sündmuse `B` õigesti?")
```

