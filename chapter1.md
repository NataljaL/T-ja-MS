---
title       : Sissejuhatus R-i
description : Siin saab tutvuda tarkvaraga R ja teha esimesi samme programmeerimises :) Alustame!



--- type:NormalExercise lang:r xp:100 skills:1 key:ca824b1118
## R kui kalkulaator

R-i võib kasutada kui kalkulaatorit. Toome ära mõned tehtemärgid:

- Liitmine: `+`
- Lahutamine: `-`
- Korrutamine: `*`
- Jagamine: `/`
- Astendamine: `^` või `**`
- Jääk jagamisel: `%%`

ja paar funktsiooni:

- Siinus: `sin()`
- Naturaallogaritm: `log()`
- Arvu jääk jagamisel: `%%`


<!--The ^ operator raises the number to its left to the power of the number to its right: for example 3^2 is 9.
The modulo returns the remainder of the division of the number to the left by the number on its right, for example 5 modulo 3 or 5 %% 3 is 2.
With this knowledge, follow the instructions below to complete the exercise.-->

*** =instructions

- Tee läbi Näited 1 kuni 4, ühe rea täitmiseks R script-is vajuta `Ctrl + Enter`.
- Pane tähele, et sümbol  `#` on kasutatud kommenteeritud ridade eristamiseks.
- Kirjuta Ülesandesse tehe, mis leiaks $$(0.5 \cdot 6) ^3 - 4 $$ ja vajuta 'Submit Answer'.

<br>

Kui tekib küsimus mõne R funktsiooni või märgi kohta, näiteks jäägi kohta, siis kirjuta R konsooli: `?"%%"`.



*** =hint

* Kui sul tekkisid probleemid märgi `^` leidmisega, siis kasuta selle asemel `**`.  
* Kümnendemurru sisestamiseks kasuta punkti: `0.5`. 
 





*** =pre_exercise_code
```{r}
#polegi
```

*** =sample_code
```{r}
# Näide 1. Liitmine. 
3 + 4

# Näide 2. Jagamine.
8 / 2

# Näide 3. Mis on jääk, kui jagada 9 arvuga 2?
9 %% 2

# Näide 4. Pikem avaldis.
7 * (8 + 9) - 10 / 5

#Ülesanne


```

*** =solution
```{r}
# Näide 1. Liitmine. 
3 + 4

# Näide 2. Jagamine.
8 / 2

# Näide 3. Funktsiooni kasutamine.
9 %% 2

# Näide 4. Pikem avaldis.
7 * (8 + 9) - 10 / 5

#Ülesanne
(0.5 * 6)^3 - 4

```

*** =sct
```{r}
test_output_contains("(0.5 * 6)^3 - 4", incorrect_msg = "Vale vastus. Proovi uuesti!")
success_msg("Tubli! Suundu järgmise ülesande juurde.")
```

<--! Järmine harjutus-->


--- type:NormalExercise lang:r xp:100 skills:1 key:3b528fab71
## Muutujad 1

Ka kalkulaatorit kasutades tekib peatselt vajadus meeles pidada arvutuste tulemusi. R-is võivad muutujate nimed sisaldada suuri ja väikesi tähti, numbreid; punkti ja alakriipsu. Erandiks on see, et nimi ei või alata numbri või alakriipsuga. Näiteks saab omistada `x`-le väärtuse 3 järgmiselt: `x <- 3`. 

**Tähtis!** R teeb vahet suurte ja väikeste tähtede vahel. Seega on `x` ja `X` kaks erinevat objekti. Samuti annab `SQRT(2)` veateate, sest ruutjuure leidmise funktsioon on `sqrt()` (väikesed tähed!).


*** =instructions

- Proovi läbi näited 1 ja 2.
- Ülesanne: Loo muutuja `w` väärtusega 3 ning  omista muutujale `z` summa, mille liidetavad on `w` ja 5. Väljasta `z` väärtus ekraanile.


*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Näide 1. Omistame muutjale y väärtuse 2 ja väljastame väärtuse
y <- 2
y

# Näide 2. Kasutame muutujat y arvutuses
y + 5

# Ülesanne


```

*** =solution
```{r}
# Näide 1. Omistame muutjale y väärtuse 2 ja väljastame väärtuse
y <- 2
y

# Näide 2. Kasutame muutujat y arvutuses
y + 5

# Ülesanne
w <- 3
z <- w + 5
z

```

*** =sct
```{r}
test_object(c("w", "z"), undefined_msg = "Kontrolli muutujate nimesid, kas Sul on defineeritud muutujad `w` ja `z`?", incorrect_msg = "Kontrolli mõlema muutuja väärtust!")
test_output_contains("8", incorrect_msg = "Vale vastus. Proovi uuesti!")
success_msg("Hästi tehtud!")
```



    
--- type:NormalExercise lang:r xp:100 skills:1 key:72c5e1fdd6
## Muutujad 2
Muutujad võivad olla ka tekstilised. Näiteks `x <- "Tere maailm!"` omistab muutujale `x` väärtuseks teksti `Tere maailm!`.
Tekstiväärtustega arvutustehteid teha ei saa, küll aga saab tekste omavahel ühendada funktsiooni `paste()` abil.



*** =instructions
- Proovi läbi näited 1 ja 2.
- Täida ka näite 3 käsud ja vaata, millise veateate annab R. Kas saad aru milles on viga?
- Ülesanne: paranda näite 3 koodi nii, et liitmisel tuleks vastuseks arv ning punast veateadet ei ilmuks.


*** =hint
Veendu, et oled muutnud koodi nii, et muutujale `poisse` omistatakse arvuline väärtus `3`: `poisse <- 3` ning muutujale `tydrukuid` arvuline väärtus 2: `tydrukuid <- 2`. 


*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Näide 1: omistame muutujale `x` väärtuseks  teksti "Tere maailm!" ja väljastame selle
x <- "Tere maailm!"
x

# Näide 2: tekstide ühendamine, eri võimalusi
poisse <- "kolm"
tydrukuid <- "2"
paste(poisse, "ja", tydrukuid)
paste(poisse, tydrukuid)
paste(poisse, tydrukuid, sep = "")

# Näide 3: tekste ei saa liita, tulemuseks on veateade.
poisse <- "kolm"
tydrukuid <- "2"
lapsi <- poisse + tydrukuid
```

*** =solution
```{r}
# Näide 1: omistame muutujale `x` väärtuseks  teksti "Tere maailm!" ja väljastame selle
x <- "Tere maailm!"
x

# Näide 2: tekstide ühendamine, eri võimalusi
poisse <- "kolm"
tydrukuid <- "2"
paste(poisse, "ja", tydrukuid)
paste(poisse, tydrukuid)
paste(poisse, tydrukuid, sep = "")

# Näide 3: tekste ei saa liita, tulemuseks on veateade.
poisse <- 3
tydrukuid <- 2
lapsi <- poisse + tydrukuid
```

*** =sct
```{r}
test_object("poisse", incorrect_msg = "Kontrolli, kas omistad muutujale `poisse` arvu 3.")
test_object("tydrukuid", incorrect_msg = "Kontrolli, kas omistad muutujale `tydrukuid` arvu 2.")
#test_output_contains("poisse + tydrukuid",
#                     incorrect_msg = "Konrolli, kas väljastad laste arvu muutuja `lapsi` abil?")
msg <- "Kas kasutasid omistmiskäsku `lapsi <- poisse + tydrukuid`?"
test_object("lapsi", undefined_msg = msg, incorrect_msg = msg)
success_msg("Nice one! The great advantage of doing calculations with variables is reusability. If you just change `my_apples` to equal 12 instead of 5 and rerun the script, `my_fruit` will automatically update as well. Continue to the next exercise.")
#test_object("poisse", undefined_msg = "Kontrolli muutujate nimesid, kas Sul defineeritud arvuline muutuja `poisse`?", incorrect_msg = "Kontrolli kas muutuja `poisse`  on arvuline.")
#test_object("tydrukuid", undefined_msg = "Kontrolli muutujate nimesid, kas Sul defineeritud arvuline muutuja `tydrukuid`?", incorrect_msg = "Kontrolli kas muutuja `tydrukuid`  on arvuline.")
#test_object( "lapsi", undefined_msg = "Kontrolli muutujate nimesid, kas Sul defineeritud arvuline muutuja `lapsi`?", incorrect_msg = "Vale vastus")
#test_output_contains("lapsi", incorrect_msg = "Vale vastus. Proovi uuesti!")
#success_msg("Hästi tehtud!")
```






--- type:NormalExercise lang:r xp:100 skills:1 key:b021441630
## Vektorid 1

- Üksikuid arve või tekstiväärtusi saab kokku panna vektoriks funktsiooni `c()` (*combine*) abil. 
- Veel võimalusi vektorite moodustamiseks:
    * `1:5                 # arvujada 1, 2, 3, 4, 5`
    * `rep(1:5, times = 2)     # vektorit elementidega 1, 2, 3, 4, 5 korrata 2 korda`
    * `seq(2, 8, by = 2)   # arvujada sammuga 2: 2, 4, 6, 8`


*** =instructions
- Tee läbi näited 1 kuni 3.
- Ülesanne 1. Kasutades operaatorit `:` moodusta vektor nimega `jada1`, mille elemendid on `5, 4, 3, 2, 1`. Väljasta tulemus ekraanile.
- Ülesanne 2. Kasutades funkstiooni `rep` moodusta vektor nimega `jada2`, mille elemendid on `"Ruhnu", "Kihnu", "Ruhnu", "Kihnu", "Ruhnu", "Kihnu"`. Väljasta tulemus ekraanile.


*** =hint
- Kasuta teises ülesandes funktsiooni `rep` esimese argumendina vektorit  `c("Ruhnu", "Kihnu")`.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Näide 1: Moodustame 2 vektorit, millest ühes on kirjas temperatuurid (20.01.2010 kell 10), teises jaamad, kus need on mõõdetud :
temp <- c(-6.2, -12.9, -13.0, -15.4, -16.1, -16.9, -17.0, -19.6, -19.9)
jaam <- c("Ruhnu", "Kihnu", "Pakri", "Tallinn", "Pärnu", "Kunda", "Kuusiku", "Võru", "Jõgeva")            # NB! Kui jutumärgid unustada, otsib R vastava nimega objekte!

# Näide 2: Väljastame tulemused 
temp; jaam

# Näide 3:  Tehted tehakse läbi kõigi vektori elementidega. Teisendame celsiuse skaalalt fahrenheiti skaalale
Fahrenheit <- temp*9/5+32
Fahrenheit 

# Ülesanne 1. Asenda alakriipsud õigete väärtustega
jada1 <- __:__
jada1

# Ülesanne 2.  Asenda alakriipsud vajalike suurustega
jada2 <- rep(c(_____,_____), times = __)
jada2

```

*** =solution
```{r}
# Näide 1: Moodustame 2 vektorit, millest ühes on kirjas temperatuurid (20.01.2010 kell 10), teises jaamad, kus need on mõõdetud :
temp <- c(-6.2, -12.9, -13.0, -15.4, -16.1, -16.9, -17.0, -19.6, -19.9)
jaam <- c("Ruhnu", "Kihnu", "Pakri", "Tallinn", "Pärnu", "Kunda", "Kuusiku", "Võru", "Jõgeva")            # NB! Kui jutumärgid unustada, otsib R vastava nimega objekte!

# Näide 2: Väljastame tulemused 
temp; jaam

# Näide 3:  Tehted tehakse läbi kõigi vektori elementidega. Teisendame celsiuse skaalalt fahrenheiti skaalale
Fahrenheit <- temp*9/5+32
Fahrenheit 

# Ülesanne 1. Asenda alakriipsud õigete väärtustega
jada1 <- 5:1
jada1

# Ülesanne 2.  Asenda alakriipsud vajalike suurustega
jada2 <- rep(c("Ruhnu", "Kihnu"), times = 3)
jada2
```

*** =sct
```{r}
ex() %>% check_operator(":") %>% check_result(msg = "Viga, kasutatud pole :") %>% check_equal()
test_function("rep", args = c("x", "times"))
success_msg("Tubli!")
#test_student_typed("jada1 <- 5:1", fixed = TRUE, "Viga")


```




--- type:NormalExercise lang:r xp:100 skills:1 key:7d4f13d4f0
## Vektorid 2

Väga sageli on tarvis vektorist kätte saada meile hetkel vajalikku alamosa. Vaatame paari võimalust vektorist elementide välja noppimiseks. 




*** =instructions
 - Tee  näited 1 kuni 3  ükshaaval läbi ja uuri tulemust.
 - Ülesanne: vali välja jaamad, kus temperatuur on olnud -17 või alla selle. Kasuta tingimuse kirjapanekul märki $\leq$.

*** =hint
- Märgi $\leq$ moodustamiseks kombineeri `<` ja `=` märke:  `<=`.

*** =pre_exercise_code
```{r}
temp <- c(-6.2, -12.9, -13.0, -15.4, -16.1, -16.9, -17.0, -19.6, -19.9)
jaam <- c("Ruhnu", "Kihnu", "Pakri", "Tallinn", "Pärnu", "Kunda", "Kuusiku", "Võru", "Jõgeva")          
```

*** =sample_code
```{r}
# Näide 1
temp[ 1 ] # vektori esimene element
temp[ -1 ] # vektori kõik elemendid va esimene
temp[ c(1, 5, 9) ] # vektori esimene, viies ja üheksas element

# Näide 2. Tulemuseks tõeväärtustega vektorid 
temp < -15 # Kontrollime millised temperatuurid jäävad alla -15 kraadi. 
jaam == "Tallinn"  # Mitmes jaam on Tallinn?

# Näide 3. Tingimustele vastavate elementide väljavalimine
jaam[ temp < -15 ] # valime välja need  jaamad, kus temperatuur on alla -15
temp[jaam == "Tallinn"]  # valime välja Tallinnale vastava temperatuuri

# Ülesanne: asenda alakriipsud õige käsuga
vastus <- ________
vastus
```

*** =solution
```{r}
# Näide 1
temp[ 1 ] # vektori esimene element
temp[ -1 ] # vektori kõik elemendid va esimene
temp[ c(1, 5, 9) ] # vektori esimene, viies ja üheksas element

# Näide 2. Tulemuseks tõeväärtustega vektorid 
temp < -15 # Kontrollime millised temperatuurid jäävad alla -15 kraadi. 
jaam == "Tallinn"  # Mitmes jaam on Tallinn?

# Näide 3. Tingimustele vastavate elementide väljavalimine
jaam[ temp < -15 ] # valime välja need  jaamad, kus temperatuur on alla -15
temp[jaam == "Tallinn"]  # valime välja Tallinnale vastava temperatuuri

# Ülesanne: asenda alakriipsud õige käsuga
vastus <- jaam[temp <= -17]
vastus
```

*** =sct
```{r}
ex() %>% check_operator("<=") %>% check_result(msg = "Viga, kasutatud pole <=") %>% check_equal()
success_msg("Tubli töö!")
#test_student_typed("jada1 <- 5:1", fixed = TRUE, "Viga")

```



--- type:MultipleChoiceExercise lang:r xp:100 skills:1 key:a1ac08c1e6
## Test 1. Küsimus 1.

Muutja `k` väärtuseks on `"kuusteist"` ja muutuja `m` väärtuseks on `4`. Millega võrdub `n <- k + m` väärtus? 

*** =instructions

- `"kakskümmend"`
- `20`
- tuleb veateade `Viga! Proovi veel!`
- tuleb veateade `Error: non-numeric argument to binary operator`

*** =hint

Vaata veelkord harjutust **Muutujad 2**.

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "See pole õige vastus!"
msg_success <- "Täpselt! R ütleb, et proovid teha liitmistehet tekstiga."
test_mc(correct = 4, feedback_msgs = c(msg_bad,  msg_bad, msg_bad, msg_success))
```


--- type:MultipleChoiceExercise lang:r xp:100 skills:1 key:191cdeba71
## Test 1. Küsimus 2.

Loo vektor `esimene` elementidega 21-st kuni 60-ni sammuga 3 (vektori pikkus peab olema 14 elementi) ja teine vektor nimega `teine`, mille väärtused on `8, 9, 8, 9, 8, 9, 8, 9, 8, 9, 8, 9, 8, 9` . 
Vektorile `tulemus` omista väärtuseks nende vektorite vahe.

Millised vektori `tulemus` elemendid jaguvad 5-ga täpselt?


*** =instructions


- 2., 5. ja 12. element
- Kõik elemendid jaguvad 5-ga
- Ükski ei jagu
- 3. ja 6. element

*** =hint

Vaata veelkord harjutusi **R kui kalkulaator** (jäägi leidmine) ja **Muutujad 2** (vektorite moodustamine).

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "See pole õige vastus!"
msg_success <- "Täpselt nii!"
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad,  msg_bad, msg_bad))
```

