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
Omega

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
Omega

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