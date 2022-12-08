***Лабораторна робота № 3. Зчитування даних з WEB.***
```
install.packages('rvest')
library(rvest)
my_data <- read_html("http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature")

rankData_html <- html_nodes(my_data,'.text-primary')
rankData <- html_text(rankData_html)
rankData<-as.numeric(rankData)

titleData_html <- html_nodes(my_data,'.lister-item-header a')
titleData <- html_text(titleData_html)

runtimeData_html <- html_nodes(my_data,'.text-muted .runtime')
runtimeData <- html_text(runtimeData_html)
runtimeData<-gsub(" min","",runtimeData)
runtimeData<-as.numeric(runtimeData)

my_movies <- data.frame(Rank = rankData, Title = titleData, Runtime = runtimeData, stringsAsFactors = FALSE )
```

**Виведіть перші 6 назв фільмів дата фрейму.**
```
head(my_movies$Title, 6)
```
```
[1] "Воно"                         "Пастка"                       "Той, хто біжить по лезу 2049"
[4] "Вітряна ріка"                 "Дюнкерк"                      "Найвеличніший шоумен"    
```
**Виведіть всі назви фільмів с тривалістю більше 120 хв.**
```
my_movies[my_movies$Runtime > 120, ]$Title
```
```
 [1] "Воно"                                     "Той, хто біжить по лезу 2049"            
 [3] "Назви мене своїм ім'ям"                   "Джон Вік 2"                              
 [5] "Мати!"                                    "Kingsman: Золоте кільце"                 
 [7] "Форма води"                               "Вартові Галактики 2"                     
 [9] "Красуня і Чудовисько"                     "Вбивство священного оленя"               
[11] "Квадрат"                                  "Тор: Раґнарок"                           
[13] "Пірати Карибського моря: Помста Салазара" "Диво-жінка"                              
[15] "Людина-павук: Повернення додому"          "Логан: Росомаха"                         
[17] "Зоряні війни: Епізод 8 - Останні Джедаї"  "Roman J. Israel, Esq."                   
[19] "Гра Моллі"                                "Темні часи"                              
[21] "Чужий: Заповіт"                           "Валеріан і місто тисячі планет"          
[23] "Метелик"                                  "Примарна нитка"                          
[25] "Король Артур: Легенда меча"               "Трансформери: Останній лицар"            
[27] "Saban's Могутні рейнджери"                "Вороги"                                  
[29] "Форсаж 8"                                 "Сім сестер"                              
[31] "Постріл в безодню"                        "The Glass Castle"                        
[33] "Вогнеборці"                               "Війна за планету мавп"         
```                     
**Скільки фільмів мають тривалість менше 100 хв.**
```
length(my_movies[my_movies$Runtime < 100, ]$Title)
```
```
[1] 14
```
