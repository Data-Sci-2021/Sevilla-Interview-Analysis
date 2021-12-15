Sevilla\_Transcription
================
Angela Krak
11/15/2021

-   [R Markdown](#r-markdown)

## R Markdown

``` r
mypath <- "/Users/angelakrak/Desktop/DataScience/Sevilla-Interview-Analysis/Transcriptions"
setwd(mypath) 
##Testing method on one file
df <- read.delim("002_Q3.txt", header = FALSE, sep = "\t", dec = ".", encoding = "UTF-8")
head(df)
```

    ##                                                                                           V1
    ## 1                                                                                        Sí.
    ## 2 Galicia, Madrid, Extremadura, Valencia, País Vasco, para partes de Cataluña no, Salamanca.
    ## 3                                                                      Sí, algunas veces sí.
    ## 4                          Hay el resto, partes de España el acento andaluz no se lo millan.
    ## 5                                                                           No lo entienden.
    ## 6                                                                     Creen que es inferior.

``` r
df <- df %>% add_column(fname = "002_Q3.txt")
head(df)
```

    ##                                                                                           V1
    ## 1                                                                                        Sí.
    ## 2 Galicia, Madrid, Extremadura, Valencia, País Vasco, para partes de Cataluña no, Salamanca.
    ## 3                                                                      Sí, algunas veces sí.
    ## 4                          Hay el resto, partes de España el acento andaluz no se lo millan.
    ## 5                                                                           No lo entienden.
    ## 6                                                                     Creen que es inferior.
    ##        fname
    ## 1 002_Q3.txt
    ## 2 002_Q3.txt
    ## 3 002_Q3.txt
    ## 4 002_Q3.txt
    ## 5 002_Q3.txt
    ## 6 002_Q3.txt

``` r
##Works well, let's try the whole set
## Making function for file names
get_df <- function(file) {
    df = read.delim(file, header = FALSE, sep = "\t", dec = ".",encoding = "UTF-8") 
    df["fname"] <- file
    return(df)
}
##Generating a list of file names
flist <- list.files(".", pattern = "*.txt", full.names=TRUE, recursive = TRUE)
flist
```

    ##   [1] "./002_Q1.txt" "./002_Q2.txt" "./002_Q3.txt" "./002_Q4.txt" "./002_Q5.txt"
    ##   [6] "./028_Q1.txt" "./028_Q2.txt" "./028_Q3.txt" "./028_Q4.txt" "./028_Q5.txt"
    ##  [11] "./045_Q1.txt" "./045_Q2.txt" "./045_Q3.txt" "./045_Q4.txt" "./045_Q5.txt"
    ##  [16] "./068_Q1.txt" "./068_Q2.txt" "./068_Q3.txt" "./068_Q4.txt" "./068_Q5.txt"
    ##  [21] "./111_Q1.txt" "./111_Q2.txt" "./111_Q3.txt" "./111_Q4.txt" "./111_Q5.txt"
    ##  [26] "./133_Q1.txt" "./133_Q2.txt" "./133_Q3.txt" "./133_Q4.txt" "./133_Q5.txt"
    ##  [31] "./189_Q1.txt" "./189_Q2.txt" "./189_Q3.txt" "./189_Q4.txt" "./189_Q5.txt"
    ##  [36] "./351_Q1.txt" "./351_Q2.txt" "./351_Q3.txt" "./351_Q4.txt" "./351_Q5.txt"
    ##  [41] "./470_Q1.txt" "./470_Q2.txt" "./470_Q3.txt" "./470_Q4.txt" "./470_Q5.txt"
    ##  [46] "./500_Q1.txt" "./500_Q2.txt" "./500_Q3.txt" "./500_Q4.txt" "./500_Q5.txt"
    ##  [51] "./574_Q1.txt" "./574_Q2.txt" "./574_Q3.txt" "./574_Q4.txt" "./574_Q5.txt"
    ##  [56] "./603_Q1.txt" "./603_Q2.txt" "./603_Q3.txt" "./603_Q4.txt" "./603_Q5.txt"
    ##  [61] "./643_Q1.txt" "./643_Q2.txt" "./643_Q3.txt" "./643_Q4.txt" "./643_Q5.txt"
    ##  [66] "./647_Q1.txt" "./647_Q2.txt" "./647_Q3.txt" "./647_Q4.txt" "./647_Q5.txt"
    ##  [71] "./706_Q1.txt" "./706_Q2.txt" "./706_Q3.txt" "./706_Q4.txt" "./706_Q5.txt"
    ##  [76] "./711_Q1.txt" "./711_Q2.txt" "./711_Q3.txt" "./711_Q4.txt" "./711_Q5.txt"
    ##  [81] "./809_Q1.txt" "./809_Q2.txt" "./809_Q3.txt" "./809_Q4.txt" "./809_Q5.txt"
    ##  [86] "./848_Q1.txt" "./848_Q2.txt" "./848_Q3.txt" "./848_Q4.txt" "./848_Q5.txt"
    ##  [91] "./865_Q1.txt" "./865_Q2.txt" "./865_Q3.txt" "./865_Q4.txt" "./865_Q5.txt"
    ##  [96] "./887_Q1.txt" "./887_Q2.txt" "./887_Q3.txt" "./887_Q4.txt" "./887_Q5.txt"
    ## [101] "./929_Q1.txt" "./929_Q2.txt" "./929_Q3.txt" "./929_Q4.txt" "./929_Q5.txt"
    ## [106] "./957_Q1.txt" "./957_Q2.txt" "./957_Q3.txt" "./957_Q4.txt" "./957_Q5.txt"

``` r
#Looping
master_df = data.frame('V1' = character(), 'fname' = character()) 
for(file in flist) {
    df = get_df(file)
    rbind(master_df, df) -> master_df
}
```

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './002_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './002_Q4.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './028_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './028_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './028_Q4.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './045_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './045_Q5.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './068_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './068_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './068_Q4.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './111_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './111_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './111_Q5.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './133_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './133_Q3.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './133_Q4.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './189_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './189_Q5.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './470_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './500_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './500_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './500_Q4.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './500_Q5.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './574_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './574_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './574_Q5.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './603_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './603_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './603_Q4.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './643_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './647_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './706_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './706_Q3.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './706_Q4.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './706_Q5.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './711_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './711_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './711_Q5.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './809_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './809_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './809_Q4.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './809_Q5.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './848_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './848_Q5.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './865_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './865_Q4.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './887_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './887_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './887_Q3.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './929_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './929_Q2.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './957_Q1.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './957_Q4.txt'

    ## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
    ## incomplete final line found by readTableHeader on './957_Q5.txt'

``` r
head(master_df) 
```

    ##                                                                  V1
    ## 1                                                       De Sevilla.
    ## 2                                                               Sí.
    ## 3 Opino que cuanto más variedad lingüística haya, hay más calidad. 
    ## 4                      Yo creo que todo lo que venga siempre deja. 
    ## 5                                Influye más cultura, más belleza. 
    ## 6                                          Más engrandece el país. 
    ##          fname
    ## 1 ./002_Q1.txt
    ## 2 ./002_Q1.txt
    ## 3 ./002_Q2.txt
    ## 4 ./002_Q2.txt
    ## 5 ./002_Q2.txt
    ## 6 ./002_Q2.txt

``` r
tail(master_df)
```

    ##                                                                                                                                                        V1
    ## 603 Y luego después fuera de España también exagera porque yo he visto por ejemplo películas donde aparecen andaluces y la verdad es que no me gusta, eh?
    ## 604                                                                                                                             Porque lo exageran mucho.
    ## 605                                                                                                                                           Permanecen.
    ## 606                                                                      Yo quiero decir que siempre van a permanecer aunque la gente ahora es más culta.
    ## 607                                                                                                                                 Intenta hablar mejor.
    ## 608                                                                              Pero al mismo tiempo hay como sentirse orgulloso de tu manera de hablar.
    ##            fname
    ## 603 ./957_Q4.txt
    ## 604 ./957_Q4.txt
    ## 605 ./957_Q5.txt
    ## 606 ./957_Q5.txt
    ## 607 ./957_Q5.txt
    ## 608 ./957_Q5.txt

``` r
##rename column to "line"
master_df <- master_df %>%
    rename(line = V1)

##Get participant info
master_df <- master_df %>%
mutate(question = str_extract(fname, "Q\\d"))
##Get question info
master_df <- master_df %>%
mutate(participant = str_extract(fname, "\\d+"))
head(master_df)
```

    ##                                                                line
    ## 1                                                       De Sevilla.
    ## 2                                                               Sí.
    ## 3 Opino que cuanto más variedad lingüística haya, hay más calidad. 
    ## 4                      Yo creo que todo lo que venga siempre deja. 
    ## 5                                Influye más cultura, más belleza. 
    ## 6                                          Más engrandece el país. 
    ##          fname question participant
    ## 1 ./002_Q1.txt       Q1         002
    ## 2 ./002_Q1.txt       Q1         002
    ## 3 ./002_Q2.txt       Q2         002
    ## 4 ./002_Q2.txt       Q2         002
    ## 5 ./002_Q2.txt       Q2         002
    ## 6 ./002_Q2.txt       Q2         002

``` r
tail(master_df)
```

    ##                                                                                                                                                      line
    ## 603 Y luego después fuera de España también exagera porque yo he visto por ejemplo películas donde aparecen andaluces y la verdad es que no me gusta, eh?
    ## 604                                                                                                                             Porque lo exageran mucho.
    ## 605                                                                                                                                           Permanecen.
    ## 606                                                                      Yo quiero decir que siempre van a permanecer aunque la gente ahora es más culta.
    ## 607                                                                                                                                 Intenta hablar mejor.
    ## 608                                                                              Pero al mismo tiempo hay como sentirse orgulloso de tu manera de hablar.
    ##            fname question participant
    ## 603 ./957_Q4.txt       Q4         957
    ## 604 ./957_Q4.txt       Q4         957
    ## 605 ./957_Q5.txt       Q5         957
    ## 606 ./957_Q5.txt       Q5         957
    ## 607 ./957_Q5.txt       Q5         957
    ## 608 ./957_Q5.txt       Q5         957

``` r
##STOP HERE FOR ANALYSIS OF INDIVIDUAL PHRASES, CONTINUE TO SPLIT WORDS

##fix line numbers
master_df <- master_df %>%
   mutate(line.number = row_number()) %>%
  ungroup()

##Unnest tokens
master_df <- master_df %>% 
    unnest_tokens(word, line)

##Reorder column names
##This will be the format that I use for running frequency analyses. 
master_df <- master_df %>% 
    select(word,line.number,fname, participant,question)
head(master_df)
```

    ##      word line.number        fname participant question
    ## 1      de           1 ./002_Q1.txt         002       Q1
    ## 2 sevilla           1 ./002_Q1.txt         002       Q1
    ## 3      sí           2 ./002_Q1.txt         002       Q1
    ## 4   opino           3 ./002_Q2.txt         002       Q2
    ## 5     que           3 ./002_Q2.txt         002       Q2
    ## 6  cuanto           3 ./002_Q2.txt         002       Q2

``` r
tail(master_df)
```

    ##           word line.number        fname participant question
    ## 6182 orgulloso         608 ./957_Q5.txt         957       Q5
    ## 6183        de         608 ./957_Q5.txt         957       Q5
    ## 6184        tu         608 ./957_Q5.txt         957       Q5
    ## 6185    manera         608 ./957_Q5.txt         957       Q5
    ## 6186        de         608 ./957_Q5.txt         957       Q5
    ## 6187    hablar         608 ./957_Q5.txt         957       Q5

``` r
##Frequency Analysis
## load 'stop word' library
library(tm)
##get overall frequency of data with stop words included
## I have to always add head() to avoid calling the whole data set, which cannot be shared
master_df  %>%  count (word, sort= TRUE) %>% head()
```

    ##   word   n
    ## 1  que 335
    ## 2   de 211
    ## 3   no 164
    ## 4   el 155
    ## 5    y 152
    ## 6   sí 147

``` r
##looks like the most frequent are all stop words!
options(repr.plot.width=12, repr.plot.height=8)
##plot overall frequency
master_df %>%
  count(word, sort = TRUE) %>%
  filter(n > 25) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word)) +
  geom_col() +
  labs(y = NULL)
```

![](images/unnamed-chunk-2-1.png)<!-- -->

``` r
##separate data frames into questions
## I could have probably turned this into a function, but decided not to in order to manipulate the filters for each question if necessary. For example, some questions had less tokens, so the frequency filter could be lower. 
##Q1
master_df_Q1 <- master_df %>% 
    select(word,line.number,fname, participant,question) %>%
    filter(question == "Q1")
master_df_Q1  %>%  count (word, sort= TRUE) %>% head()
```

    ##      word  n
    ## 1      de 28
    ## 2 sevilla 28
    ## 3      sí 18
    ## 4 siempre 12
    ## 5 capital 11
    ## 6      he 11

``` r
master_df_Q1 %>%
  count(word, sort = TRUE) %>%
  filter(n > 5) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word)) +
  geom_col() +
  labs(y = NULL)
```

![](images/unnamed-chunk-3-1.png)<!-- -->

``` r
##Q2
master_df_Q2 <- master_df %>% 
    select(word,line.number,fname, participant,question) %>%
    filter(question == "Q2")
master_df_Q2  %>%  count (word, sort= TRUE) %>% head()
```

    ##   word  n
    ## 1  que 75
    ## 2   el 37
    ## 3   es 33
    ## 4    y 29
    ## 5   en 26
    ## 6   de 25

``` r
master_df_Q2 %>%
  count(word, sort = TRUE) %>%
  filter(n > 6) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word)) +
  geom_col() +
  labs(y = NULL)
```

![](images/unnamed-chunk-4-1.png)<!-- -->

``` r
##Q3
master_df_Q3 <- master_df %>% 
    select(word,line.number,fname, participant,question) %>%
    filter(question == "Q3")
master_df_Q3  %>%  count (word, sort= TRUE) %>% head()
```

    ##   word  n
    ## 1  que 87
    ## 2   sí 73
    ## 3   de 48
    ## 4   el 47
    ## 5   en 44
    ## 6    y 42

``` r
master_df_Q3 %>%
  count(word, sort = TRUE) %>%
  filter(n > 8) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word)) +
  geom_col() +
  labs(y = NULL)
```

![](images/unnamed-chunk-5-1.png)<!-- -->

``` r
##Q4
master_df_Q4 <- master_df %>% 
    select(word,line.number,fname, participant,question) %>%
    filter(question == "Q4")
master_df_Q4  %>%  count (word, sort= TRUE) %>% head()
```

    ##   word  n
    ## 1  que 73
    ## 2   no 57
    ## 3   de 52
    ## 4   en 34
    ## 5    y 32
    ## 6   es 31

``` r
master_df_Q4 %>%
  count(word, sort = TRUE) %>%
  filter(n > 7) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word)) +
  geom_col() +
  labs(y = NULL)
```

![](images/unnamed-chunk-6-1.png)<!-- -->

``` r
##Q5
master_df_Q5 <- master_df %>% 
    select(word,line.number,fname, participant,question) %>%
    filter(question == "Q5")
master_df_Q5  %>%  count (word, sort= TRUE) %>% head()
```

    ##   word  n
    ## 1  que 98
    ## 2   de 58
    ## 3   no 47
    ## 4    y 45
    ## 5   el 41
    ## 6 creo 29

``` r
master_df_Q5 %>%
  count(word, sort = TRUE) %>%
  filter(n > 7) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word)) +
  geom_col() +
  labs(y = NULL)
```

![](images/unnamed-chunk-7-1.png)<!-- -->

``` r
##Look at Spanish stop words list
list(stopwords(kind = "es"))
```

    ## [[1]]
    ##   [1] "de"           "la"           "que"          "el"           "en"          
    ##   [6] "y"            "a"            "los"          "del"          "se"          
    ##  [11] "las"          "por"          "un"           "para"         "con"         
    ##  [16] "no"           "una"          "su"           "al"           "lo"          
    ##  [21] "como"         "más"          "pero"         "sus"          "le"          
    ##  [26] "ya"           "o"            "este"         "sí"           "porque"      
    ##  [31] "esta"         "entre"        "cuando"       "muy"          "sin"         
    ##  [36] "sobre"        "también"      "me"           "hasta"        "hay"         
    ##  [41] "donde"        "quien"        "desde"        "todo"         "nos"         
    ##  [46] "durante"      "todos"        "uno"          "les"          "ni"          
    ##  [51] "contra"       "otros"        "ese"          "eso"          "ante"        
    ##  [56] "ellos"        "e"            "esto"         "mí"           "antes"       
    ##  [61] "algunos"      "qué"          "unos"         "yo"           "otro"        
    ##  [66] "otras"        "otra"         "él"           "tanto"        "esa"         
    ##  [71] "estos"        "mucho"        "quienes"      "nada"         "muchos"      
    ##  [76] "cual"         "poco"         "ella"         "estar"        "estas"       
    ##  [81] "algunas"      "algo"         "nosotros"     "mi"           "mis"         
    ##  [86] "tú"           "te"           "ti"           "tu"           "tus"         
    ##  [91] "ellas"        "nosotras"     "vosotros"     "vosotras"     "os"          
    ##  [96] "mío"          "mía"          "míos"         "mías"         "tuyo"        
    ## [101] "tuya"         "tuyos"        "tuyas"        "suyo"         "suya"        
    ## [106] "suyos"        "suyas"        "nuestro"      "nuestra"      "nuestros"    
    ## [111] "nuestras"     "vuestro"      "vuestra"      "vuestros"     "vuestras"    
    ## [116] "esos"         "esas"         "estoy"        "estás"        "está"        
    ## [121] "estamos"      "estáis"       "están"        "esté"         "estés"       
    ## [126] "estemos"      "estéis"       "estén"        "estaré"       "estarás"     
    ## [131] "estará"       "estaremos"    "estaréis"     "estarán"      "estaría"     
    ## [136] "estarías"     "estaríamos"   "estaríais"    "estarían"     "estaba"      
    ## [141] "estabas"      "estábamos"    "estabais"     "estaban"      "estuve"      
    ## [146] "estuviste"    "estuvo"       "estuvimos"    "estuvisteis"  "estuvieron"  
    ## [151] "estuviera"    "estuvieras"   "estuviéramos" "estuvierais"  "estuvieran"  
    ## [156] "estuviese"    "estuvieses"   "estuviésemos" "estuvieseis"  "estuviesen"  
    ## [161] "estando"      "estado"       "estada"       "estados"      "estadas"     
    ## [166] "estad"        "he"           "has"          "ha"           "hemos"       
    ## [171] "habéis"       "han"          "haya"         "hayas"        "hayamos"     
    ## [176] "hayáis"       "hayan"        "habré"        "habrás"       "habrá"       
    ## [181] "habremos"     "habréis"      "habrán"       "habría"       "habrías"     
    ## [186] "habríamos"    "habríais"     "habrían"      "había"        "habías"      
    ## [191] "habíamos"     "habíais"      "habían"       "hube"         "hubiste"     
    ## [196] "hubo"         "hubimos"      "hubisteis"    "hubieron"     "hubiera"     
    ## [201] "hubieras"     "hubiéramos"   "hubierais"    "hubieran"     "hubiese"     
    ## [206] "hubieses"     "hubiésemos"   "hubieseis"    "hubiesen"     "habiendo"    
    ## [211] "habido"       "habida"       "habidos"      "habidas"      "soy"         
    ## [216] "eres"         "es"           "somos"        "sois"         "son"         
    ## [221] "sea"          "seas"         "seamos"       "seáis"        "sean"        
    ## [226] "seré"         "serás"        "será"         "seremos"      "seréis"      
    ## [231] "serán"        "sería"        "serías"       "seríamos"     "seríais"     
    ## [236] "serían"       "era"          "eras"         "éramos"       "erais"       
    ## [241] "eran"         "fui"          "fuiste"       "fue"          "fuimos"      
    ## [246] "fuisteis"     "fueron"       "fuera"        "fueras"       "fuéramos"    
    ## [251] "fuerais"      "fueran"       "fuese"        "fueses"       "fuésemos"    
    ## [256] "fueseis"      "fuesen"       "siendo"       "sido"         "tengo"       
    ## [261] "tienes"       "tiene"        "tenemos"      "tenéis"       "tienen"      
    ## [266] "tenga"        "tengas"       "tengamos"     "tengáis"      "tengan"      
    ## [271] "tendré"       "tendrás"      "tendrá"       "tendremos"    "tendréis"    
    ## [276] "tendrán"      "tendría"      "tendrías"     "tendríamos"   "tendríais"   
    ## [281] "tendrían"     "tenía"        "tenías"       "teníamos"     "teníais"     
    ## [286] "tenían"       "tuve"         "tuviste"      "tuvo"         "tuvimos"     
    ## [291] "tuvisteis"    "tuvieron"     "tuviera"      "tuvieras"     "tuviéramos"  
    ## [296] "tuvierais"    "tuvieran"     "tuviese"      "tuvieses"     "tuviésemos"  
    ## [301] "tuvieseis"    "tuviesen"     "teniendo"     "tenido"       "tenida"      
    ## [306] "tenidos"      "tenidas"      "tened"

``` r
##Make list for stop words
custom_stop_words <- bind_rows(stop_words, tibble(word = tm::stopwords("spanish"),
                                          lexicon = "custom"))
##Add more stop words
word <- c("entonces", "pues", "si", "bueno", "así", "bien", "cada", "risa", "toda", "mucho", "mucha", "va", "van", "muchas", "además", "eh", "da", "sé", "casi", "todas")
lexicon <- rep("custom", times=length(word))
new_stop_words <- data.frame(word, lexicon)
names(new_stop_words) <- c("word", "lexicon")
custom_stop_words <-bind_rows(custom_stop_words, new_stop_words)

##Remove stop words from master_df and save to master_df_nostop
master_df_nostop <- master_df %>%
  anti_join(custom_stop_words %>% 
              filter(lexicon=="custom"))
```

    ## Joining, by = "word"

``` r
##Get frequency for overall data frame
master_df_nostop  %>%  count (word, sort= TRUE) %>% head()
```

    ##      word  n
    ## 1  acento 66
    ## 2 andaluz 61
    ## 3    creo 58
    ## 4 siempre 53
    ## 5  españa 33
    ## 6   gente 29

``` r
##Plot overall frequency results for nostop
master_df_nostop %>%
  count(word, sort = TRUE) %>%
  filter(n > 10) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word)) +
  geom_col(color="black") +
  labs(y = NULL) +
  theme(text= element_text(size=12))
```

![](images/unnamed-chunk-10-1.png)<!-- -->

``` r
##Separate data frames from nostop 
##Q1
master_df_Q1_nostop <- master_df_nostop %>% 
    select(word,line.number,fname, participant,question) %>%
    filter(question == "Q1")
master_df_Q1_nostop  %>%  count (word, sort= TRUE) %>% head()
```

    ##      word  n
    ## 1 sevilla 28
    ## 2 siempre 12
    ## 3 capital 11
    ## 4  vivido  8
    ## 5    aquí  6
    ## 6    años  5

``` r
master_df_Q1_nostop %>%
  count(word, sort = TRUE) %>%
  filter(n > 2) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word)) +
  geom_col() +
  labs(y = NULL)
```

![](images/unnamed-chunk-11-1.png)<!-- -->

``` r
##Separate data frames from nostop 
##Q2
master_df_Q2_nostop <- master_df_nostop %>% 
    select(word,line.number,fname, participant,question) %>%
    filter(question == "Q2")
master_df_Q2_nostop  %>%  count (word, sort= TRUE) %>% head()
```

    ##        word  n
    ## 1  variedad 19
    ## 2      creo 12
    ## 3   catalán  9
    ## 4 dialectos  9
    ## 5   idiomas  9
    ## 6    lengua  8

``` r
master_df_Q2_nostop %>%
  count(word, sort = TRUE) %>%
  filter(n > 4) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word, fill=word)) +
  geom_col(color="black") +
  labs(y = NULL) +
  theme(text= element_text(size=12))
```

![](images/unnamed-chunk-12-1.png)<!-- -->

``` r
##Separate data frames from nostop 
##Q3
master_df_Q3_nostop <- master_df_nostop %>% 
    select(word,line.number,fname, participant,question) %>%
    filter(question == "Q3")
master_df_Q3_nostop  %>%  count (word, sort= TRUE) %>% head()
```

    ##      word  n
    ## 1  acento 20
    ## 2  españa 18
    ## 3  madrid 16
    ## 4 andaluz 13
    ## 5 siempre 13
    ## 6 galicia 12

``` r
master_df_Q3_nostop %>%
  count(word, sort = TRUE) %>%
  filter(n > 4) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word, fill=word)) +
  geom_col(color="black") +
  labs(y = NULL) +
  theme(text= element_text(size=12))
```

![](images/unnamed-chunk-13-1.png)<!-- -->

``` r
##Separate data frames from nostop 
##Q4
master_df_Q4_nostop <- master_df_nostop %>% 
    select(word,line.number,fname, participant,question) %>%
    filter(question == "Q4")
master_df_Q4_nostop  %>%  count (word, sort= TRUE) %>% head()
```

    ##             word  n
    ## 1        andaluz 28
    ## 2         acento 24
    ## 3        siempre 14
    ## 4      películas 13
    ## 5           creo 12
    ## 6 representación 12

``` r
master_df_Q4_nostop %>%
  count(word, sort = TRUE) %>%
  filter(n > 4) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word, fill=word)) +
  geom_col(color="black") +
  labs(y = NULL) +
  theme(text= element_text(size=12))
```

![](images/unnamed-chunk-14-1.png)<!-- -->

``` r
##Separate data frames from nostop 
##Q5
master_df_Q5_nostop <- master_df_nostop %>% 
    select(word,line.number,fname, participant,question) %>%
    filter(question == "Q5")
master_df_Q5_nostop  %>%  count (word, sort= TRUE) %>% head()
```

    ##         word  n
    ## 1       creo 29
    ## 2     acento 20
    ## 3    andaluz 15
    ## 4  cambiando 13
    ## 5      gente 10
    ## 6 permanecen  9

``` r
master_df_Q5_nostop %>%
  count(word, sort = TRUE) %>%
  filter(n > 4) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(n, word, fill=word)) +
  geom_col(color="black") +
  labs(y = NULL) +
  theme(text= element_text(size=12))
```

![](images/unnamed-chunk-15-1.png)<!-- -->

``` r
library(wordcloud)
```

    ## Loading required package: RColorBrewer

``` r
library(dplyr)
master_df_nostop %>%
  count(word, sort = TRUE) %>%
  dplyr::filter(n > 8 & word != "master_df_nostop") %>%
  with(wordcloud::wordcloud(words = word, 
                            freq = n, 
                            max.words = 300,
                            random.order = FALSE,
                            rot.per = 0.3,
                            colors = brewer.pal(8,"Dark2")))
```

![](images/unnamed-chunk-16-1.png)<!-- -->

``` r
sessionInfo()
```

    ## R version 4.1.1 (2021-08-10)
    ## Platform: x86_64-apple-darwin17.0 (64-bit)
    ## Running under: macOS Mojave 10.14.5
    ## 
    ## Matrix products: default
    ## BLAS:   /Library/Frameworks/R.framework/Versions/4.1/Resources/lib/libRblas.0.dylib
    ## LAPACK: /Library/Frameworks/R.framework/Versions/4.1/Resources/lib/libRlapack.dylib
    ## 
    ## locale:
    ## [1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8
    ## 
    ## attached base packages:
    ## [1] stats     graphics  grDevices utils     datasets  methods   base     
    ## 
    ## other attached packages:
    ##  [1] wordcloud_2.6      RColorBrewer_1.1-2 tm_0.7-8           NLP_0.2-1         
    ##  [5] forcats_0.5.1      stringr_1.4.0      dplyr_1.0.7        purrr_0.3.4       
    ##  [9] readr_2.0.2        tidyr_1.1.3        tibble_3.1.4       ggplot2_3.3.5     
    ## [13] tidyverse_1.3.1    tidytext_0.3.2    
    ## 
    ## loaded via a namespace (and not attached):
    ##  [1] Rcpp_1.0.7        lubridate_1.7.10  lattice_0.20-45   assertthat_0.2.1 
    ##  [5] digest_0.6.27     utf8_1.2.2        slam_0.1-48       R6_2.5.1         
    ##  [9] cellranger_1.1.0  backports_1.2.1   reprex_2.0.1      evaluate_0.14    
    ## [13] highr_0.9         httr_1.4.2        pillar_1.6.2      rlang_0.4.11     
    ## [17] readxl_1.3.1      rstudioapi_0.13   Matrix_1.3-4      rmarkdown_2.10   
    ## [21] labeling_0.4.2    munsell_0.5.0     broom_0.7.9       compiler_4.1.1   
    ## [25] janeaustenr_0.1.5 modelr_0.1.8      xfun_0.25         pkgconfig_2.0.3  
    ## [29] htmltools_0.5.2   tidyselect_1.1.1  fansi_0.5.0       crayon_1.4.1     
    ## [33] tzdb_0.1.2        dbplyr_2.1.1      withr_2.4.2       SnowballC_0.7.0  
    ## [37] grid_4.1.1        jsonlite_1.7.2    gtable_0.3.0      lifecycle_1.0.0  
    ## [41] DBI_1.1.1         magrittr_2.0.1    scales_1.1.1      tokenizers_0.2.1 
    ## [45] cli_3.0.1         stringi_1.7.4     farver_2.1.0      fs_1.5.0         
    ## [49] xml2_1.3.2        ellipsis_0.3.2    generics_0.1.0    vctrs_0.3.8      
    ## [53] tools_4.1.1       glue_1.4.2        hms_1.1.0         parallel_4.1.1   
    ## [57] fastmap_1.1.0     yaml_2.2.1        colorspace_2.0-2  rvest_1.0.1      
    ## [61] knitr_1.33        haven_2.4.3
