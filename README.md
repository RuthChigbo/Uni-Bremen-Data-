# Uni-Bremen-Data-
another attempt
         
         ## R Markdown
         
         This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.
         
         When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:
           
           ```{r cars}
         summary(cars)
         ```
         
         ## Including Plots
         
         You can also embed plots, for example:
           
           ```{r pressure, echo=FALSE}
         plot(pressure)
         ```
         
         Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
         
         #importing data
         ```{r}
         temp <- read.csv("Data/data_OBS_DEU_PT1H_T2M.csv")
         
         my.tp <- data.table(tp)
         
         ppt <- read.csv("Data/data_OBS_DEU_PT1H_RR.csv")
         
         my.ppt <- data.table(ppt)
         
         wd <- read.csv("Data/data_OBS_DEU_PT1H_F.csv")
         
         my.wd <- data.table(wd)
         
         cloud <- read.csv("Data/data_OBS_DEU_PT1H_N.csv")
         
         my.cloud <- data.table(cloud)
         
         rh <- read.csv("Data/data_OBS_DEU_PT1H_RF.csv")
         
         my.rh <- data.table(rh)
         
         glbr <- read.csv("Data/data_OBS_DEU_PT10M_RAD-G.csv")
         
         my.gr <- data.table(glbr)
         
         sun <- read.csv("Data/data_OBS_DEU_PT1H_SD.csv")
         
         my.sun <- data.table(sun)
         
         
         ```
         # changing times stamp to date time
         
         ```{r}
         temp <- read.csv("Data/data_OBS_DEU_PT1H_T2M.csv")
         
         my.tp <- data.table(temp)
         
         my.tp[,Zeitstempel:=as.POSIXct(Zeitstempel, format = "%Y-%m-%dT%H:%M:%S")]
         
         my.tp.list <- split(
           my.tp,
           rep(1:668, each = 1000)
         )
         library(ggplot2)
         
         my.tp <- as.data.frame.matrix(my.wd)
         
         my.tp <- data.frame(wd)
         
         
         ggplot(my.tp.list$`1`, aes(x=Zeitstempel, y=Wert))+
           geom_point()
         ```
         
         
         ```{r}
         
         my.wd <- data.table(wd)
         
         my.wd[,Zeitstempel:=as.POSIXct(Zeitstempel, format = "%Y-%m-%dT%H:%M:%S")]
         
         my.wd.list <- split(
           my.wd,
           rep(1:668, each = 1000)
         )
         library(ggplot2)
         
         my.wd <- as.data.frame.matrix(my.wd)
         
         my.wd <- data.frame(wd)
         
         ggplot(my.wd.list$`1`, aes(x=Zeitstempel, y=Wert))+
           geom_point()
         
         
         ```
         
         
         ```{r}
         my.cloud <- data.table(cloud)
         
         my.cloud[,Zeitstempel:=as.POSIXct(Zeitstempel, format = "%Y-%m-%dT%H:%M:%S")]
         
         my.cloud.list <- split(
           data_OBS_DEU_PT1H_N,
           rep(1:668, each = 1000)
         )
         library(ggplot2)
         
         my.cloud <- as.data.frame.matrix(my.wd)
         
         my.cloud <- data.frame(cloud)
         
         ggplot(my.cloud.list$'1', aes(x=Zeitstempel, y=Wert))+
           geom_point()
         labs(title="cloud of metadata",caption="Energy analysis")
         ```
      
         ```{r}
         rh <- read.csv("Data/data_OBS_DEU_PT1H_RF.csv")
         
         my.rh <- data.table(rh)
         my.rh[,Zeitstempel:=as.POSIXct(Zeitstempel, format = "%Y-%m-%dT%H:%M:%S")]
         
         my.rh.list<- split(
           data_OBS_DEU_PT1H_RF,
           rep(1:668, each = 1000)
         )
         
         my.rh <- data.frame(rh)
         
         ggplot(my.rh.list$'1', aes(x=Zeitstempel, y=Wert))+
           geom_point()
         
         ```
         
      
         ```{r}
         ppt <- read.csv("Data/data_OBS_DEU_PT1H_RF.csv")
         
         my.ppt <- data.table(ppt)
         
         my.ppt[,Zeitstempel:=as.POSIXct(Zeitstempel, format = "%Y-%m-%dT%H:%M:%S")]
         
         my.ppt.list <- split(
           data_OBS_DEU_PT1H_RR,
           rep(1:668, each = 1000)
         )
         
         my.ppt <- data.frame(ppt)
         
         ggplot(my.ppt.list$'1', aes(x=Zeitstempel, y=Wert))+
           geom_point()
         ```
         
    
         ```{r}
         sun <- read.csv("Data/data_OBS_DEU_PT1H_SD.csv")
         
         my.sun <- data.table(sun)
         
         my.sun[,Zeitstempel:=as.POSIXct(Zeitstempel, format = "%Y-%m-%dT%H:%M:%S")]
         
         my.sun.list <- split(
           my.sun,
           rep(1:668, each = 1000)
         )
         
         my.sun <- data.frame(sun)
         
         ggplot(my.sun.list$'1', aes(x=Zeitstempel, y=Wert))+
           geom_point()
         ```
         
       
         ```{r}
         gr <- read.csv("Data/data_OBS_DEU_PT10M_RAD-G.csv")
         
         my.gr <- data.table(gr)
         
         my.gr[,Zeitstempel:=as.POSIXct(Zeitstempel, format = "%Y-%m-%dT%H:%M:%S")]
         
         my.gr.list <- split(
           my.gr,
           rep(1:668, each = 1000)
         )
         
         my.gr <- data.frame(gr)
         
         gr_plot <- function(grl){
           ggplot(my.gr.list$'1', aes(x=Zeitstempel, y=Wert))+
             geom_point()
         }
         ````
         
         # deleting  unused column in the dataframe
      #first trial
         # removing unused coloumn in all the elements of the list
         ```{r}
         lapply(my.cloud.list, function(x) x[, c("Zeitstempel", "Wert")])
         lapply(my.ppt.list, function(x) x[, c("Zeitstempel", "Wert")])
         lapply(my.wd.list, function(x) x[, c("Zeitstempel", "Wert")])
         lapply(my.sun.list, function(x) x[, c("Zeitstempel", "Wert")])
         lapply(my.tp.list, function(x) x[, c("Zeitstempel", "Wert")])
         lapply(my.gr.list, function(x) x[, c("Zeitstempel", "Wert")])
         lapply(my.rh.list, function(x) x[, c("Zeitstempel", "Wert")])
         
         ```
         #second trial
         #removing the unused column in the choosen list
         #cloud
         ```{r}
         
         my.cloud.list$`1` <- subset(my.cloud.list$`1`, select = -Qualitaet_Byte)
         print(my.cloud.list$`1`)
         
         my.cloud.list$`1` <- subset(my.cloud.list$`1`, select = -Qualitaet_Niveau)
         print(my.cloud.list$`1`)
         
         my.cloud.list$`1` <- subset(my.cloud.list$`1`, select = -SDO_ID)
         print(my.cloud.list$`1`)
         
         my.cloud.list$`1` <- subset(my.cloud.list$`1`, select = -X)
         print(my.cloud.list$`1`)
         
         my.cloud.list$`1` <- subset(my.cloud.list$`1`, select = -Produkt_Code)
         print(my.cloud.list$`1`)
         ```
         #ppt
         ```{r}
         my.ppt.list$`1` <- subset(my.ppt.list$`1`, select = -Qualitaet_Byte)
         print(my.ppt.list$`1`)
         
         my.ppt.list$`1` <- subset(my.ppt.list$`1`, select = -Qualitaet_Niveau)
         print(my.ppt.list$`1`)
         
         my.ppt.list$`1` <- subset(my.ppt.list$`1`, select = -SDO_ID)
         print(my.ppt.list$`1`)
         
         my.ppt.list$`1` <- subset(my.ppt.list$`1`, select = -X)
         print(my.ppt.list$`1`)
         
         my.ppt.list$`1` <- subset(my.ppt.list$`1`, select = -Produkt_Code)
         print(my.ppt.list$`1`)
         ```
         #sun
         ```{r}
         my.sun.list$`1` <- subset(my.sun.list$`1`, select = -Qualitaet_Byte)
         print(my.sun.list$`1`)
         
         my.sun.list$`1` <- subset(my.sun.list$`1`, select = -Qualitaet_Niveau)
         print(my.cloud.list$`1`)
         
         my.sun.list$`1` <- subset(my.sun.list$`1`, select = -SDO_ID)
         print(my.sun.list$`1`)
         
         my.sun.list$`1` <- subset(my.sun.list$`1`, select = -X)
         print(my.sun.list$`1`)
         
         my.sun.list$`1` <- subset(my.sun.list$`1`, select = +Produkt_Code)
         print(my.sun.list$`1`)
         ```
         #gr
         ```{r}
         my.gr.list$`1` <- subset(my.gr.list$`1`, select = -Qualitaet_Byte)
         print(my.gr.list$`1`)
         
         my.gr.list$`1` <- subset(my.gr.list$`1`, select = -Qualitaet_Niveau)
         print(my.gr.list$`1`)
         
         my.gr.list$`1` <- subset(my.gr.list$`1`, select = -SDO_ID)
         print(my.gr.list$`1`)
         
         my.gr.list$`1` <- subset(my.gr.list$`1`, select = -X)
         print(my.gr.list$`1`)
         
         my.gr.list$`1` <- subset(my.gr.list$`1`, select = -Produkt_Code)
         print(my.gr.list$`1`)
         ```
         #rh
         ```{r}
         my.rh.list$`1` <- subset(my.rh.list$`1`, select = -Qualitaet_Byte)
         print(my.rh.list$`1`)
         
         my.rh.list$`1` <- subset(my.rh.list$`1`, select = -Qualitaet_Niveau)
         print(my.rh.list$`1`)
         
         my.rh.list$`1` <- subset(my.rh.list$`1`, select = -SDO_ID)
         print(my.rh.list$`1`)
         
         my.rh.list$`1` <- subset(my.rh.list$`1`, select = -X)
         print(my.rh.list$`1`)
         
         my.rh.list$`1` <- subset(my.rh.list$`1`, select = -Produkt_Code)
         print(my.rh.list$`1`)
         ```
         #wd
         ```{r}
         my.wd.list$`1` <- subset(my.wd.list$`1`, select = -Qualitaet_Byte)
         print(my.wd.list$`1`)
         
         my.wd.list$`1` <- subset(my.wd.list$`1`, select = -Qualitaet_Niveau)
         print(my.wd.list$`1`)
         
         my.wd.list$`1` <- subset(my.wd.list$`1`, select = -SDO_ID)
         print(my.wd.list$`1`)
         
         my.wd.list$`1` <- subset(my.wd.list$`1`, select = -X)
         print(my.wd.list$`1`)
         
         my.wd.list$`1` <- subset(my.wd.list$`1`, select = -Produkt_Code)
         print(my.wd.list$`1`)
         ```
         #tp
         ```{r}
         my.tp.list$`1` <- subset(my.tp.list$`1`, select = -Qualitaet_Byte)
         print(my.tp.list$`1`)
         
         my.tp.list$`1` <- subset(my.tp.list$`1`, select = -Qualitaet_Niveau)
         print(my.tp.list$`1`)
         
         my.tp.list$`1` <- subset(my.tp.list$`1`, select = -SDO_ID)
         print(my.tp.list$`1`)
         
         my.tp.list$`1` <- subset(my.tp.list$`1`, select = -X)
         print(my.tp.list$`1`)
         my.tp.list$`1` <- subset(my.tp.list$`1`, select = -Produkt_Code)
         print(my.tp.list$`1`)
         ```
         #ploting all the data together
         1. you have to merge the data together 
         2. plot all 
         sepracting with different colours 
        
         ```{r}
         rbind(my.cloud.list$`1`,my.rh.list$`1`, my.ppt.list$`1`, my.sun.list$`1`, my.gr.list$`1`, my.wd.list$`1`, my.tp.list$`1`)
        
         meta.data <- rbind(my.cloud.list$`1`, my.gr.list$`1`, my.ppt.list$`1`, my.rh.list$`1`, my.sun.list$`1`, my.tp.list$`1`, my.wd.list$`1`)
         
         ```
         #join the data together
         ```{r}
         
         mate.data2 <- rbind(my.ppt.list$`1` %>% mutate(Type = "ppt"), my.rh.list$`1` %>% mutate(Type = "rh"), my.cloud.list$`1` %>% mutate(Type = "cloud"), my.gr.list$`1` %>% mutate(Type ="gr" ), my.wd.list$`1` %>% mutate(Type = "wd"), my.sun.list$`1` %>% mutate(Type = "sun"), my.tp.list$`1` %>% mutate(Type = "tp"))
         
         mate.data2 %>% 
           ggplot(aes(Zeitstempel, Wert, color = Type)) +
           geom_point()+ 
           geom_line(size =1, linejoin= "round")
         labs(X="1-Zeitstempel",
              y="Wert")+
           scale_color_manual(name=NULL,
                              breaks = c("climate data"))
         
         
         
         #i also tried combining the data
         cbind(my.ppt.list$`1` %>% mutate(Type = "ppt"), my.rh.list$`1` %>% mutate(Type = "rh"), my.cloud.list$`1` %>% mutate(Type = "cloud"), my.gr.list$`1` %>% mutate(Type ="gr" ), my.wd.list$`1` %>% mutate(Type = "wd"), my.sun.list$`1` %>% mutate(Type = "sun"), my.tp.list$`1` %>% mutate(Type = "tp"))
        
         ```{r}
         mate_all<- merge(my.cloud.list$`1`,my.rh.list$`1`,by="Zeitstempel")
         print(mate_all)
         
         
         mate_all2 <- merge(my.wd.list$'1',my.gr.list$`1`,by="Zeitstempel")
         
         print(mate_all2)
         
         mate_all3 <- merge(as.data.frame (my.gr.list$`1`),as.data.frame(my.sun.list$`1`),by="Zeitstempel")
         mate_all3[is.na(mate_all3)] <- 0
         View(mate_all3)
         
         print(mate_all3)
         
         cbind(my.cloud.list$'1', my.rh.list$`1`, my.ppt.list$`1`, my.sun.list$`1`, my.gr.list$`1`, my.wd.list$`1`, my.tp.list$`1`)
         rbind(my.cloud.list$'1', my.rh.list$`1`, my.ppt.list$`1`, my.sun.list$`1`, my.gr.list$`1`, my.wd.list$`1`, my.tp.list$`1` by = "Zeitstempel") 
         
         merge(my.wd.list$`1`, my.gr.list$`1`, by.x = "Zeitstempel", by.y = "Wert")
         
         
         mate.data_2 <- merge(my.ppt.list$`1` %>% mutate(Type = "ppt"), my.rh.list$`1` %>% mutate(Type = "rh"))
         print(mate.data_2)
         ```
      
         
         
