---
title       : Insert the chapter title here
description : Insert the chapter description here
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

---
## A really bad movie

```yaml
type: MultipleChoiceExercise
lang: r
xp: 50
skills: 1
key: 91ccbcadd2
key: 9b56ae1ea3
```

Have a look at the plot that showed up in the viewer to the right. Which type of movie has the worst rating assigned to it?

`@instructions`
- Adventure
- Action
- Animation
- Comedy

`@hint`
Have a look at the plot. Which color does the point with the lowest rating have?

`@pre_exercise_code`
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

movies <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")

library(ggplot2)

ggplot(movies, aes(x = runtime, y = rating, col = genre)) + geom_point()
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be a very bad action movie in the dataset."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```

---
## More movies

```yaml
type: NormalExercise
lang: r
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 9e33769fcc
skills: 1
key: fee2e36d4f

A dataset with a selection of movies, `movie_selection`, is available in the workspace.

`@instructions`
- Check out the structure of `movie_selection`.
- Select movies with a rating of 5 or higher. Assign the result to `good_movies`.
- Use `plot()` to  plot `good_movies$Run` on the x-axis, `good_movies$Rating` on the y-axis and set `col` to `good_movies$Genre`.

`@hint`
- Use `str()` for the first instruction.
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`.

`@pre_exercise_code`
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code
load(url("https://s3.amazonaws.com/assets.datacamp.com/course/teach/movies.RData"))
movie_selection <- Movies[Movies$Genre %in% c("action", "animated", "comedy"), c("Genre", "Rating", "Run")]

# Clean up the environment
rm(Movies)
```

`@sample_code`
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection


# Select movies that have a rating of 5 or higher: good_movies


# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre

```

`@solution`
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```




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


```

*** =sample_code
```{r}
Omega <- rolldie(3) #kõikvõimalike katsetulemuste hulk kolme täringu veeretamisel
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
Omega <- rolldie(3) #kõikvõimalike katsetulemuste hulk kolme täringu veeretamisel
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