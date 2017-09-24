---
title       : Sündmused
description : Mõned kasulikud käsud sündmuste defineerimiseks. Alustame! :)


--- type:NormalExercise lang:r xp:100 skills:1 key:6075a680df
## Sündmuse defineerimine R-is

Lõpliku või loenduva elementaarsündmuste hulga $\Omega$ korral võib sündmuseks *A* nimetada selle hulga $\Omega$ alamhulka. Alamhulga võtmine on `R`-i jaoks ridade valik  $\Omega$-le vastavast tabelist teatud tingimuse järgi. Selliseid võimalusi on palju.

Olgu katseks 3 täringu viskamine. Elementaarsündmuste hulk koosneb: $|\Omega|=6\cdot 6\cdot 6 = 216$ katsetulemusest. 

Proovi järgmised näited läbi ja uuri sündmuste defineerimise võimalusi `R`-is.

*** =instructions
Elementaarsündmuste hulk `Omega` on juba defineeritud. Uuri, millest see koosneb, millised on tabeli `Omega` veergude nimed.
* **Näide 1.** Saame viidata tabeli `Omega` ridadele kasutades rea numbreid. Antud näites mingit tingimust sündmuste *A* ja *B* defineerimiseks ei kasutata.
* **Näide 2.** Olgu sündmuseks $C$ kõik read, kus 1. täringu katsetulemuseks on 2 silma. Käsud muutujate `C1`, `C2` ja `C3` defineerimiseks annavad ühte ja sama sündmust $C$.
* **Näide 3.** Olgu sündmus $D$ kõik read, kus 2. täringu katsetulemuseks on 2 kuni 4 silma. Uuri muutujaid `D1`, `D2` ja `D3`.
* **Näide 4.** Viimaseks on sündmus $E$, mis vastab sellistele katsetulemustele, kus kõigi kolme täringu viske tulemuste summa on suurem kui 16. Muutujad `E1` ja `E2` on vaid mõned võimalused selle sündmuse defineerimiseks.


*** =hint
Kas vajutasid nuppu `Submit Answer`? Antud ülesande eesmärk on demonstreerida võtteid alamhulkade valimiseks tabelist $\Omega$.

*** =pre_exercise_code
```{r}
rolldie <- function (times, nsides = 6, makespace = FALSE){
    temp = list()
    for (i in 1:times) {
        temp[[i]] <- 1:nsides
    }
    res <- expand.grid(temp, KEEP.OUT.ATTRS = FALSE)
    names(res) <- c(paste(rep("X", times), 1:times, sep = ""))
    if (makespace) 
        res$probs <- rep(1, nsides^times)/nsides^times
    return(res)
}

Omega <- rolldie(3) #kõikvõimalike katsetulemuste hulk kolme täringu veeretamisel
```

*** =sample_code
```{r}
Omega #kogu tabel
colnames(Omega) #veergude nimed

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
C3 <- subset(Omega, X1==2) #funktsiooni subset() abil, kuulub paketti prob
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
Omega #kogu tabel
colnames(Omega) #veergude nimed

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
C3 <- subset(Omega, X1==2) #funktsiooni subset() abil, kuulub paketti prob
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
## Ülesanne: neli täringut

Olgu katseks nelja 6-tahulise täringu veeretamine. Huvipakkuvaks sündmuseks $A$ on kõik sellised realisatsioonid, kus silmade summa jagub 20-ga. Millega võrdub sündmuse *A* elementide arv? 

`Omega` on juba defineeritud. Uuri, millest see koosneb. Sündmuse $A$ defineerimist harjutasid eelmises ülesandes. Kindlasti on abiks tehe `a %% b`, mis leiab jäägi arvu `a` jagamisel arvuga `b` ja käsk `nrow(A)`, mille abil saab leida tabeli `A` ridade arvu. 

Harjuta jugelt aknas `R Console`!

*** =instructions

* 4
* 35
* 168
* 1292
* minu vastust pole

*** =hint
Sündmuse $A$ defineerimiseks sobib näiteks järgmine käsk: 

`A <- subset(Omega, (X1+X2+X3+X4) %% 20 == 0)`.

*** =pre_exercise_code
```{r}
rolldie <- function (times, nsides = 6, makespace = FALSE){
    temp = list()
    for (i in 1:times) {
        temp[[i]] <- 1:nsides
    }
    res <- expand.grid(temp, KEEP.OUT.ATTRS = FALSE)
    names(res) <- c(paste(rep("X", times), 1:times, sep = ""))
    if (makespace) 
        res$probs <- rep(1, nsides^times)/nsides^times
    return(res)
}

Omega <- rolldie(4, nsides=6) #kõikvõimalike katsetulemuste hulk kolme täringu veeretamisel

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "Kahjuks pole õige vastus."
msg_success <- "Super! Said asjast õigesti aru!"
test_mc(correct = 2, feedback_msgs = c(msg_bad,  msg_success, msg_bad, msg_bad, msg_bad))
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7874b5a8d3
## Sündmuste ühend, ühisosa, vahe, täiend

Sündmuste tehetele vastavad käsud on:

| `R`-i funktsioon    | Tehe         | Tähistus | Definitsioon                       |
|---------------------|--------------|:--------:|------------------------------------|
| `union(A, B)`       | Ühend        |$A \cup B$| *A* või *B* elemendid, või mõlemad     |
| `intersect(A, B)`   | Ühisosa      |$A \cap B$| *A* ja *B* ühised elemendid           |
| `setdiff(A, B)`     | Vahe         |$A\backslash B$    | elemendid *A*-st, mis ei kuulu *B*-sse   |

Täiendi $\bar A$ saamiseks saab kasutada `setdiff(Omega, A)`, kus `Omega` on kõikide elementaarsündmuste hulk.
Argumendid `A`, `B` ja `Omega` peavad olema vektorid.

*** =instructions
Koosnegu $\Omega$ 36-st kaardist, milles on neli masti ja kaardid 6, 7, 8, 9, poiss, emand, kuningas ja äss.
Sündmus *A* on defineeritud kui kõik ärtu masti kaardid ja sündmus *B* kui kaardid numbritega 7, 8 ja 9.

1. Muutujad `Omega`, `A` ja `B` on juba defineeritud. Uuri neid!
* **Ülesanded:**
4. Defineeri sündmus `X`, mis on sündmuste *A* ja *B* ühend.
5. Defineeri sündmus `Y`, mis on sündmuste *A* ja *B* ühisosa.
6. Defineeri sündmus `Z1`, mis vastab tehtele $A\backslash B$.
7. Defineeri sündmus `Z2`, mis vastab tehtele $B\backslash A$. Kas `Z1` ja `Z2` langevad kokku? 
8. Defineeri sündmus `B_taiend`, mis vastab tehtele $\bar B$.

*** =hint
Kasuta tabelis olevad funktsioonid ning argumentideks `A`, `B` või `Omega`. 

*** =pre_exercise_code
```{r}
#Omega loomine
vaartused <- c( 6, 7, 8, 9, 10, "poiss", "emand", "kuningas", "äss")
mastid <- c("poti", "ärtu", "risti", "ruutu")
Omega <- expand.grid(mastid, vaartused)
colnames(Omega) = c("Mast", "Vaartus") # täpitähed nimedes võivad tekitada veateateid


#Sündmuste A ja B defineerimine
A <- subset(Omega, Mast == "ärtu")
B <- subset(Omega, Vaartus %in% 7:9)

#Vektorite moodustamine:
Omega <- paste(Omega$Mast, Omega$Vaartus)
A <- paste(A$Mast, A$Vaartus);  B <- paste(B$Mast, B$Vaartus)
```

*** =sample_code
```{r}
head(Omega)
A
B

# Ülesanne 1. Sündmuste A ja B ühend:
X <- ___________

# Ülesanne 2. Sündmuste A ja B ühisosa:
Y <- ___________

# Ülesanne 3. Sündmsuste A ja B vahe:
Z1 <- ___________ 

# Ülesanne 4. Sündmsute B ja A vahe:
Z2 <- ___________ 

# Ülesanne 5. Sündmuse B täiend:
B_taiend <- ___________ 
```

*** =solution
```{r}
head(Omega)
A
B

# Ülesanne 1. Sündmuste A ja B ühend:
X <- union(A, B)

# Ülesanne 2. Sündmuste A ja B ühisosa:
Y <- intersect(A, B)

# Ülesanne 3. Sündmsuste A ja B vahe:
Z1 <- setdiff(A, B) 

# Ülesanne 4. Sündmsute B ja A vahe:
Z2 <- setdiff(B, A) 

# Ülesanne 5. Sündmuse B täiend:
B_taiend <- setdiff(Omega, B) 
```

*** =sct
```{r}
test_object("X", undefined_msg = NULL, incorrect_msg = "Kas kasutasid funktsiooni `union` ja argumentideks `A` ning `B`?")
test_object("Y", undefined_msg = NULL, incorrect_msg = "Kas kasutasid funktsiooni `intersect` ja argumentideks `A` ning `B`?")
test_object("Z1", undefined_msg = NULL, incorrect_msg = "Kas kasutasid funktsiooni `setdiff` ja esimeseks argumendiks panid `A`?")
test_object("Z2", undefined_msg = NULL, incorrect_msg = "Kas kasutasid funktsiooni `setdiff` ja esimeseks argumendiks panid `B`?")
test_object("B_taiend", undefined_msg = NULL, incorrect_msg = "Täiendi saamiseks kasuta funktsiooni `setdiff` koos esimese argumendiga `Omega` ja teisega `B`.")

success_msg("Sa said sellega hakkama! Suurepärane!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:c5c1237bb4
## Arvu ära arvamine
Saadud teadmisi nüüd saad rakendada järgmise ülesande juures. 

Kristjan mõtles ühe kolmekohalise arvu. Kas arvad ära? Oma mõeldud arvu kohta ütleb Kristjan nii:

1. see on paarisarv
2. arv ei jagu 4-ga, kuid jagub kas 91 või 90-ga
3. numbrite summa selles arvus on suurem kui 11, kuid väiksem või võrdne 15-ga

Arvame ära Kristjani mõeldud arvu sündmuste ja tehete abil!

*** =instructions
* Elementaarsündmuste hulk $\Omega$ koosneb kõikidest kolmekohalistest arvudest, `R`-is `100:999.` Omista neid muutujale `Omega`.
* Tingimusi, mida mõeldud arv rahuldab, sisestame sündmustena. Läheb vaja sajaliste (`X100`), kümneliste (`X10`) ja üheliste (`X1`) numbreid. Uuri, kuidas on need defineeritud.
* Olgu sündmus $A$ paarisarv. Paarisarvu saame, kui arvu jagamisel 2-ga on jäägiks 0. Vastav sündmus on `R`-is juba defineeritud. Kirjuta analoogiliselt sündmused `B1`, `B2` ja `B3`, mis on defineeritud järgmiselt:
    - `B1`: arv ei jagu 4-ga;
    - `B2`: arv jagub 90-ga;
    - `B3`: arv jagub 91-ga.
* Kristjani 2. väide on sel juhul sündmuste tehete kaudu: $B = B1 \cap (B2\cup B3)$. Defineeri see sündmus R-is, kasutades funktsiooni `union()` ja `intersect()`. 
* Olgu sündmus `C1`: numbrite summa on suurem kui 11. See sündmus on juba defineeritud. Kirjuta analoogiline käsk sündmuse `C2` jaoks: numbrite summa on väiksem või võrdne 15-ga.
* Olgu sündmus $C = C1\cap C2$. Defineeri see `R`-is.
* Kristjani mõeldud arvu saab esitada nüüd kui $Arv = (A \cap B) \cap C$. Täienda muutuja `Arv` funktsioonidega ning saad Kristjani arvu kätte!

*** =hint
* Sündmuste tehete defineerimiseks on abiks eelmise harjutuses kasutatud käskude tabel.
* Sümbol `!=` vastab väljendile "ei võrdu". 

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
Omega <- _______             # elementaarsündmuste hulk
X100 <- Omega%/%100          # sajalised
X10 <- (Omega-X100*100)%/%10 # kümnelised
X1 <- Omega-X100*100-X10*10  # ühelised

A <- subset(Omega, Omega %% 2 == 0)    # paarisarv

B1 <- ______________________________   # arv ei jagu 4-ga 
B2 <- ______________________________   # arv jagub 90-ga
B3 <- ______________________________   # arv jagub 91-ga
B <- ________(B1, ______(B2, B3))

C1 <- subset(Omega, X100+X10+X1 > 11)  # numbrite summa > 11
C2 <- ______________________________   # numbrite summa <= 15
C <- _____________________

Arv <- ____________(____________(A,B),  C)
Arv

```

*** =solution
```{r}
Omega <- 100:999             # elementaarsündmuste hulk
X100 <- Omega%/%100          # sajalised
X10 <- (Omega-X100*100)%/%10 # kümnelised
X1 <- Omega-X100*100-X10*10  # ühelised

A <- subset(Omega, Omega %% 2 == 0)    # paarisarv

B1 <- subset(Omega, Omega %% 4 != 0)   # arv ei jagu 4-ga 
B2 <- subset(Omega, Omega %% 90 == 0)  # arv jagub 90-ga
B3 <- subset(Omega, Omega %% 91 == 0)  # arv jagub 91-ga
B <- intersect(B1, union(B2, B3))

C1 <- subset(Omega, X100+X10+X1 > 11)  # numbrite summa > 11
C2 <- subset(Omega, X100+X10+X1 <= 15) # numbrite summa <= 15
C <- intersect(C1, C2)

Arv <- intersect(intersect(A,B),  C)
Arv

```

*** =sct
```{r}
test_object("Omega", undefined_msg = NULL, incorrect_msg = "`Onmega` defineerimisel kasuta näiteks `100:999`")
test_object("B1", undefined_msg = NULL, incorrect_msg = "Defineeri `B1` sarnaselt muutujaga `A`! Kasuta `!=` defineerimaks seda, et arv ei jagu 4-ga!")
test_object("B2", undefined_msg = NULL, incorrect_msg = "Defineeri `B2` analoogiliselt muutujaga `A`! Kasuta `90` `2`-asemel.")
test_object("B3", undefined_msg = NULL, incorrect_msg = "Defineeri `B3` analoogiliselt muutujaga `A`! Kasuta `91` `2`-asemel.")

test_object("B", undefined_msg = NULL, incorrect_msg = "Kas kasutasid käsu `intersect` ühe argumendina funktsioon `union(B2, B3)`?")

test_object("C2", undefined_msg = NULL, incorrect_msg = "Defineeri `C2` analoogiliselt muutujaga `C1`! Kasuta märki `<=`.")
test_object("C", undefined_msg = NULL, incorrect_msg = "Kas kasutasid käsku `intersect(C1, C2)`?")

test_object("Arv", undefined_msg = NULL, incorrect_msg = "Kas kasutasid funktsiooni `intersect`, mille üheks argumendiks on samuti funktsioon `intersect`?")

success_msg("Suurepärane! R on igal pool abiks!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:201fd41f0e
## Klassikaline tõenäosus (1)

Tuletame meelde, et sündmuse $A$ klassikaline tõenäosus on defineeritud järgmise suhte abil:
$$P(A)=\frac{|A|}{|{\Omega}|}.$$

**Näide.** Kahe täringu veeretamine. Olgu sündmus $A=$'silmade arvu summa on väiksem kui 5'. Leida sündmuse *A* tõenäosus.

Teame, et elementaarsündmuste ruum $\Omega$ koosneb paaridest (1,1), (1,2) kuni (6,6) , ehk kokku 36 elementaarsündmust. 

Sündmusele *A* vastavad järgmised paarid: (1,1), (1,2),(1,3),(2,1),(2,2) ja (3,1), ehk kokku 6 sobivat elementaarsündmust. Vastuseks saame 
$$P(A)=6/36=1/6.$$ 

`R`-is sündmuse defineerimine on analoogiline alamhulga valimisega, mis vastab teatud tingimusele. Antud näidet saaks `R`-is lahendada järgmiselt.

*** =instructions

* Uuri, kuidas on defineeritud elementaarsündmuste hulk `Omega`.
* Uuri, kuidas on kasutatud funktsiooni `subset()` sündmuse *A* defineerimiseks.
* Sündmuse *A* tõenäosus on leitud otse valemi järgi.
* **Ülesanne.** Defineeri sündmus *B*, mis vastab võrdsele silmade arvule mõlemal täringul ning leia selle tõenäosus.

*** =hint
Võrdne arv silmi mõlemal täringul on `R`-is tingimus `Taring1 == Taring2`. Ülejäänud on analoogiline näitega.

*** =pre_exercise_code
```{r}
taring <- 1:6                       # elementaarsündmuste ruum 
p <- rep(1/6, times=6)              # tõenäosuste vektor
taring.ruum <- cbind(taring, p) 
```

*** =sample_code
```{r}
# Kahe täringu veeretamisele vastav elementaarsündmuste hulk Omega:
Omega <- expand.grid(1:6, 1:6)
colnames(Omega) <- c("Taring1", "Taring2")
head(Omega) # 6 esimest rida tabelist Omega

# Sündmus A
A <- subset(Omega, Taring1 + Taring2 < 5)
A 

# Sündmuse A tõenäosus:
P.A.valem <- nrow(A)/nrow(Omega)
P.A.valem

#ÜLESANNE:
B <- ___________________
P.B <- _________________
P.B

```

*** =solution
```{r}
# Kahe täringu veeretamisele vastav elementaarsündmuste hulk Omega:
Omega <- expand.grid(1:6, 1:6)
colnames(Omega) <- c("Taring1", "Taring2")
head(Omega) # 6 esimest rida tabelist Omega

# Sündmus A
A <- subset(Omega, Taring1 + Taring2 < 5)
A 

# Sündmuse A tõenäosus:
P.A.valem <- nrow(A)/nrow(Omega)
P.A.valem 

#ÜLESANNE:
B <- subset(Omega, Taring1 == Taring2)
P.B <- nrow(B)/nrow(Omega)
P.B

```

*** =sct
```{r}
test_object("B", undefined_msg = NULL, incorrect_msg = "Valesti defineeritud sündmus `B`! Kasuta funktsiooni `subset` ja tingimust `Taring1 == Taring2`!")
test_student_typed("P.B <- nrow(B)/nrow(Omega)", not_typed_msg =  "Viga tõenäosuse P(B) leidmisel! Kas kasutasid `nrow(B)/nrow(Omega)`?")

success_msg("Suurepärane! Suundu järgmise harjutuse juurde!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:ebb7291a12
## Klassikaline tõenäosus (2)

Väikeste näidete korral (nagu oli kahe täringu viske korral) ei vaja me sageli arvutit tõenäosuste leidmiseks. Elus võib aga ette tulla olukordi, kus teisiti on raske hakkama saada. 

Siin on veel üks näide, millele järgneb ülesanne.

**Näide.** Miku rahakotis on 9 ühe-eurost münti ja 7 kahe-eurost, ülejäänud mündid on sendid: 6 kahekümne-sendist ja 3 viiekümne-sendist.

Kommipakk maksab poes 2 EUR ja 60 senti. Miku rahakott on väike ja ebamugav ning ta võtab sealt kaks münti pimesi. Mis on tõenäosus, et saadud rahaga saab ta kommipaki eest maksta (st et müntide summa on vähemalt 2 EUR ja 60 senti)? 

Lahendame `R`-is.

*** =instructions
* Elementaarsündmuste hulk `Omega` on defineeritud, see vastab kahe mündi võtmisele tagasipanekuta 25-st mündist. Kõik mündid on selles hulgas eristatavad (ka sama väärtusega).
* Olgu *A* sündmus, et kahe mündi summa on vähemalt 2,60. Vaata, kuidas on see defineeritud.
* Sündmuse *A* tõenäosus on seejärel arvutatud klassikalise valemi järgi. Uuri muutujat `P_A`.
* **Ülesanne.** Eelmises ülesandes leida tõenäosus (`P_B`), et juhuslikult võetud kaks münti on sama väärtusega (`B`).

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
Omega <- urnsamples(Myndid, size = 2, replace = FALSE, ordered = TRUE) # kombinatsioonid 25-st 2 kaupa, kus järjestus on oluline
colnames(Omega)=c("Mynt1", "Mynt2")

#Sündmus A:
A <- subset(Omega, Mynt1+Mynt2>=2.6)

# Tõenäosus, et juhuslikult võetud 2 mündi summa on vähemalt 2,60.
P_A <- nrow(A)/nrow(Omega)

# ÜLESANNE. Samast rahakotist juhuslikult võetud kaks münti on sama väärtusega.
B <- 
P_B <- 
P_B
```

*** =solution
```{r}
# Elementaarsündmuste hulk koos tõenäosustega:
Myndid <- rep(c(1,2,0.2,0.5), c(9,7,6,3)) #Miku rahakott
Omega <- urnsamples(Myndid, size = 2, replace = FALSE, ordered = TRUE) # kombinatsioonid 25-st 2 kaupa, kus järjestus on oluline
colnames(Omega)=c("Mynt1", "Mynt2")

#Sündmus A:
A <- subset(Omega, Mynt1+Mynt2>=2.6)

# Tõenäosus, et juhuslikult võetud 2 mündi summa on vähemalt 2,60.
P_A <- nrow(A)/nrow(Omega)

# ÜLESANNE. Samast rahakotist juhuslikult võetud kaks münti on sama väärtusega.
B <- subset(Omega, Mynt1==Mynt2)
P_B <- nrow(B)/nrow(Omega)
P_B
```

*** =sct
```{r}
test_object("B", undefined_msg = NULL, incorrect_msg = "Muutuja B on defineeritud valesti. Kas kasutasid tingimust `Mynt1==Mynt2`?")
test_object("P_B", undefined_msg = NULL, incorrect_msg = "Tõenäosuse P_B väärtus pole õige.")

success_msg("Lahe! Oskad nii hästi `R`-i!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:cbf176cd0c
## Kahe sündmuse ühendi tõenäosus

Üldiselt, kui *A* ja *B* on kaks suvalist sündmust, siis nende ühendi (summa) tõenäosuse leidmiseks kasutatakse järgmist valemit:
$$P(A\cup B)=P(A) + P(B) - P(A\cap B).$$

Varem uurisime näidet, kus $\Omega$ koosnes 36-st kaardist, milles on neli masti ja kaardid 6, 7, 8, 9, poiss, emand, kuningas ja äss.
Sündmus *A* oli defineeritud kui kõik ärtu masti kaardid ja sündmus *B* kui kaardid numbritega 7, 8 ja 9.

*** =instructions
* Kaardipakile vastav `Omega`  on juba loodud. Vaata aknas `R Console` selle väärtuseid.
* Uuri, kuidas on defineeritud muutujad `A` ja `B`
* Funktsiooni `intersect` argumentideks võivad olla vaid vektorid, seega tabelite `A` ja `B` väärtustest tuleks moodustada vektoreid. Abiks on funktsioon `paste`. Uuri!
* Leiame sündmuste `A` ja `B` tõenäosused eraldi ning ka nende koostoimumise tõenäosuse (muutuja `AB.tn`). Funktsioon `length` leiab elementide arvu vektoris.
* Edasi saab juba leida $P(A\cap B)$ otse valemist, vt muutujat `A.yhend.B.tn`.
* Analoogilise vastuse saab ka teisiti. Uuri!
* **Ülesanne:** leida eelmises ülesandes, et tõmmatud kaart on kas musta masti (sündmus `C`) või numbritega 6, 7 (sündmus `D`). Lõplikku vastust omista muutujale `yl.tn`.

*** =hint
Ülesande lahendamiseks defineeri esmalt uued vajalikud sündmused ning seejärel kasuta näiteks funktsiooni `length(union(___ ,____))/36`.

*** =pre_exercise_code
```{r}
#Omega loomine
vaartused <- c( 6, 7, 8, 9, 10, "poiss", "emand", "kuningas", "äss")
mastid <- c("poti", "ärtu", "risti", "ruutu")
Omega <- expand.grid(mastid, vaartused)
colnames(Omega) = c("Mast", "Vaartus") # täpitähed nimedes võivad tekitada veateateid
```

*** =sample_code
```{r}
#Sündmuste A ja B defineerimine:
A <- subset(Omega, mastid=="ärtu")
B <- subset(Omega, vaartused %in% c(7,8,9))

#Vektorite moodustamine tabelitest:
A <- paste(A$Mast, A$Vaartus);
B <- paste(B$Mast, B$Vaartus)

# P(A U B) leidmine valemi järgi:
A.tn <- length(A)/36; B.tn <- length(B)/36; AB.tn <- length(intersect(A,B))/36
A.yhend.B.tn <- A.tn + B.tn - AB.tn
A.yhend.B.tn

#Alternatiivne viis vastuse saamiseks:
length(union(A, B))/36

#Ülesanne:
C <- 
D <- 
C <- paste(C$Mast, C$Vaartus)
D <- paste(D$Mast, D$Vaartus)
yl.tn <- ___________________
```

*** =solution
```{r}
#Sündmuste A ja B defineerimine:
A <- subset(Omega, mastid=="ärtu")
B <- subset(Omega, vaartused %in% c(7,8,9))

#Vektorite moodustamine tabelitest:
A <- paste(A$Mast, A$Vaartus);
B <- paste(B$Mast, B$Vaartus)

# P(A U B) leidmine valemi järgi:
A.tn <- length(A)/36; B.tn <- length(B)/36; AB.tn <- length(intersect(A,B))/36
A.yhend.B.tn <- A.tn + B.tn - AB.tn
A.yhend.B.tn

#Alternatiivne viis vastuse saamiseks:
length(union(A, B))/36

#Ülesanne:
C <- subset(Omega, Mast %in% c("risti", "poti"))
D <- subset(Omega, Vaartus %in% 6:7)
C <- paste(C$Mast, C$Vaartus)
D <- paste(D$Mast, D$Vaartus)
yl.tn <- length(union(C,D))/36
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
* Kirjuta analoogiline käsk ka sündmuse $B|A$ tõenäosuse leidmiseks. Kas `tn1` ja `tn2` langevad kokku?
 
*** =hint
* Kasuta tingimust `X1 + X2 >= 8` sündmuse `B` defineerimisel.
* Tingliku tõenäosuse leidmisel valemi järgi lugejaks on `length(intersect(A,B))`.

*** =pre_exercise_code
```{r}

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

Omega <- expand.grid(1:6, 1:6)
```


*** =sample_code
```{r}
# Sündmuste A ja B defineerimine
A <- subset(Omega, X1 == X2)
B <- subset(Omega, ________) # ISE! Silmade summa on vähemalt 8

# Vektorite moodustamine sündmustest A ja B:
A <- paste(A$X1, A$X2)
B <- paste(B$X1, B$X2)

# Tinglik tõenäosus valemi järgi:
tn1 <- length(________)/lenght(B) # P(A|B)
tn2 <-  _______________________   # P(B|A)
```

*** =solution
```{r}
# Sündmuste A ja B defineerimine
A <- subset(Omega, X1 == X2)
B <- subset(Omega, X1+X2>=8) # ISE! Silmade summa on vähemalt 8

# Vektorite moodustamine sündmustest A ja B:
A <- paste(A$X1, A$X2)
B <- paste(B$X1, B$X2)

# Tinglik tõenäosus valemi järgi:
tn1 <- length(intersect(A,B))/lenght(B)  # P(A|B)
tn2 <- length(intersect(A,B))/lenght(A)  # P(B|A)
 
```

*** =sct
```{r}
test_object("B", undefined_msg = NULL, incorrect_msg = "Kontrolli, kas defineerisid sündmuse `B` õigesti!")
test_object("tn1", undefined_msg = NULL, incorrect_msg = "Kontrolli, kas lugejas on `length(intersect(A,B))`?")
test_object("tn2", undefined_msg = NULL, incorrect_msg = "Kontrolli muutujat `tn2` veel kord. Kas nimetajas on `length(A)`?")
success_msg("Tubli! Tinglik tõenäosus on nüüd ka selge! ")
```



