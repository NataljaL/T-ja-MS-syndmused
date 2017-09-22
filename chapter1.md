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

*** =instructions
Koosnegu $\Omega$ 36-st kaardist, milles on neli masti ja kaardid 6, 7, 8, 9, poiss, emand, kuningas ja äss.
Sündmus *A* on defineeritud kui kõik ärtu masti kaardid ja sündmus *B* kui kaardid numbritega 7, 8 ja 9.

1. Defineerida sündmus `X`, mis on sündmuste *A* ja *B* ühend.
2. Defineerida sündmus `Y`, mis on sündmuste *A* ja *B* ühisosa.
3. Defineerida sündmus `Z1`, mis vastab tehtele $A\backslash B$.
4. Defineerida sündmus `Z2`, mis vastab tehtele $B\backslash A$. Kas `Z1` ja `Z2` langevad kokku? 
5. Defineerida sündmus `B_taiend`, mis vastab tehtele $\bar B$.

*** =hint
Kasuta tabelis olevad funktsioonid ning argumentideks `A`, `B` või `Omega`. 

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
#Omega loomine
vaartused <- c( 6, 7, 8, 9, 10, "J", "Q", "K", "Ä")
mastid <- c("poti", "ärtu", "risti", "ruutu")
Omega <- expand.grid(vaartused, mastid)
colnames(Omega) = c("Vaartus", "Mast") # täpitähed nimedes võivad tekitada veateateid
Omega

#Sündmuste A ja B defineerimine
A <- subset(Omega, Mast == "ärtu")
B <- subset(Omega, Vaartus %in% 7:9)

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
#Omega loomine
vaartused <- c( 6, 7, 8, 9, 10, "J", "Q", "K", "Ä")
mastid <- c("poti", "ärtu", "risti", "ruutu")
Omega <- expand.grid(vaartused, mastid)
colnames(Omega) = c("Vaartus", "Mast") # täpitähed nimedes võivad tekitada veateateid
Omega

#Sündmuste A ja B defineerimine
A <- subset(Omega, Mast == "ärtu")
B <- subset(Omega, Vaartus %in% 7:9)

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
test_object("B_taiend", undefined_msg = NULL, incorrect_msg = "Täiendi saamiseks kasuta funktsiooni `setdiff` koos esimese aergumendiga `Omega`")

success_msg("Sa said sellega hakkama! Super!")
```
