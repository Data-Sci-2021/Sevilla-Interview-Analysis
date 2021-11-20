Sevilla Transcription
================
Angela Krak
11/15/2021

## R Markdown

``` r
mypath <- "/Users/angelakrak/Desktop/DataScience/Sevilla-Interview-Analysis/Transcriptions"
setwd(mypath)
##Plz don't set my computer on fire, I just don't know how to set up a relative file path yet! Will figure that out by the next progress report.
text_txt <- readLines(paste("002_Q2.txt", sep= ","), n= -1L)
 text_df <- tibble(line= 1:8, text = text_txt)
 text_df
```

    ## # A tibble: 8 × 2
    ##    line text                                                               
    ##   <int> <chr>                                                              
    ## 1     1 "Opino que cuanto más variedad lingüística haya, hay más calidad. "
    ## 2     2 "Yo creo que todo lo que venga siempre deja. "                     
    ## 3     3 "Influye más cultura, más belleza. "                               
    ## 4     4 "Más engrandece el país. "                                         
    ## 5     5 "Todo lo que sea más idiomas y más. "                              
    ## 6     6 "Yo creo que eso siempre engrandece. "                             
    ## 7     7 "Y la cultura es mejor. "                                          
    ## 8     8 "Cuanto más idiomas y más lenguas habla un país."

``` r
 text_df %>% unnest_tokens(word, text)
```

    ## # A tibble: 56 × 2
    ##     line word       
    ##    <int> <chr>      
    ##  1     1 opino      
    ##  2     1 que        
    ##  3     1 cuanto     
    ##  4     1 más        
    ##  5     1 variedad   
    ##  6     1 lingüística
    ##  7     1 haya       
    ##  8     1 hay        
    ##  9     1 más        
    ## 10     1 calidad    
    ## # … with 46 more rows

``` r
 text_df %>% unnest_tokens(word, text) %>% mutate(Speaker= "002", .after=line)
```

    ## # A tibble: 56 × 3
    ##     line Speaker word       
    ##    <int> <chr>   <chr>      
    ##  1     1 002     opino      
    ##  2     1 002     que        
    ##  3     1 002     cuanto     
    ##  4     1 002     más        
    ##  5     1 002     variedad   
    ##  6     1 002     lingüística
    ##  7     1 002     haya       
    ##  8     1 002     hay        
    ##  9     1 002     más        
    ## 10     1 002     calidad    
    ## # … with 46 more rows

``` r
 ##This worked well for one file, but when I tried to replicate it on the whole set it didn't because I didn't have an argument for "line". So went with a different approach. 
```

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
