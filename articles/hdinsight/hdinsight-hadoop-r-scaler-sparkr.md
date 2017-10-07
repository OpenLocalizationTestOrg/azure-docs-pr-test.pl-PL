---
title: "aaaUse ScaleR i SparkR z usługą Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj ScaleR i SparkR z serwerem R i HDInsight"
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a>Łączenie ScaleR i SparkR w usłudze HDInsight

W tym artykule opisano, jak toopredict lotu opóźnienia przyjęcia przy użyciu **ScaleR** Regresja logistyczna model danych w locie opóźnienia i pogody połączony z **SparkR**. Ten scenariusz pokazuje możliwości hello ScaleR do manipulowania danymi na Spark używane z programem Microsoft R Server w celu wykonania analizy. Witaj kombinację tych technologii umożliwia tooapply hello najnowsze możliwości przetwarzania rozproszonego.

Mimo że oba pakiety uruchomione na aparat wykonywania platformy Spark w Hadoop, jest blokowane udostępnianie, ponieważ wymagają one każdego własnych odpowiednich sesji Spark danych w pamięci. Dopóki ten problem został rozwiązany w nadchodzącej wersji serwera R, obejście hello jest toomaintain nienakładający Spark sesji i tooexchange danych za pośrednictwem plików pośrednich. instrukcje Hello pokazują, że te wymagania są proste tooachieve.

Używamy przykład tutaj początkowo udostępniony w rozmawiać na Strata 2016 Mario Inchiosa i Roni Burd, który jest również dostępny za pośrednictwem hello webinar [tworzenie skalowalnych platformy nauki danych z R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). przykład Witaj używa SparkR toojoin hello dobrze znane airlines przyjęcia opóźnienie zestawu danych z danymi pogody na lotniskach wyjścia i przyjęcia. danych Hello przyłączony jest następnie używany jako model Regresja logistyczna ScaleR tooa wejściowych do przewidywania transmitowane przyjęcia opóźnienia.

Witaj kodu, możemy wskazówki pierwotnie sformatowano platformy R Server działającej w Spark w klaster usługi HDInsight w systemie Azure. Ale koncepcji hello mieszania hello stosowania SparkR i ScaleR w jednym skrypcie również jest prawidłowy w kontekście hello środowiska lokalnego. W następujących hello możemy zakładają poziom pośredni wiedzy hello R oraz R [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) biblioteki R Server. Wprowadzeniu użycie [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) podczas tego scenariusza.

## <a name="hello-airline-and-weather-datasets"></a>Witaj lotniczych i pogody zbiory danych

Witaj **AirOnTime08to12CSV** airlines publiczny zestaw danych zawiera informacje na temat transmitowane przyjęcia i szczegóły wyjścia dla wszystkich lotach komercyjnych w USA, hello z tooDecember 1987 października 2012. Jest to dużego zestawu danych: Całkowita liczba są prawie 150 miliony rekordów. Jest tylko mniej niż 4 GB, rozpakowane. Jest ona dostępna z hello [archiwa dla instytucji rządowych USA](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236). Ułatwia, jest dostępny jako plik zip (AirOnTimeCSV.zip) zawierający zestaw 303 oddzielnych miesięczne plików CSV, z hello [Analytics obrotów repozytorium zestawu danych](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)

toosee hello skutki pogody w locie opóźnień, musimy również hello pogody danych w każdej lotniskach hello. Te dane mogą być pobierane jako pliki zip w formie raw, przez miesiąc, od hello [National Oceanu i administrowanie atmosferycznych repozytorium](http://www.ncdc.noaa.gov/orders/qclcd/). Dla celów hello w tym przykładzie firma Microsoft pogody ściągania z maja 2007 — grudzień 2012 i użyć hello co godzinę pliki danych w ramach każdy 68 zips miesięczne hello. plików zip miesięcznych Hello również zawierać mapowania (YYYYMMstation.txt) między hello pogody stacji identyfikator (WBAN), lotnisku hello jest skojarzony z (CallSign) i hello przesunięcia strefy czasowej na lotnisku w formacie UTC (strefa czasowa). Wszystkie te informacje jest potrzebne podczas sprzęgania z danymi opóźnienie i pogody linii lotniczych hello.

## <a name="setting-up-hello-spark-environment"></a>Konfigurowanie środowiska Spark hello

pierwszym krokiem Hello jest tooset hello Spark środowiska. Zaczniemy wskazując toohello katalog, który zawiera katalogi naszych danych wejściowych, tworzenia kontekstu obliczeń Spark i tworzenie funkcji rejestrowania, rejestrowanie informacyjny toohello konsoli:

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

Następnie dodamy ścieżki wyszukiwania toohello "Spark_Home" dla pakietów języka R, aby możemy użyć SparkR i zainicjować sesję SparkR:

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a>Przygotowywanie danych pogody hello

tooprepare hello pogody danych, możemy podzestawu go kolumn toohello potrzebne do modelowania: 

- "Widoczność"
- "DryBulbCelsius"
- "DewPointCelsius"
- "RelativeHumidity"
- "Prędkość wiatru"
- "Wysokościomierza"

Następnie możemy dodać kod lotnisku skojarzony z hello pogody stacji i konwertowanie miar hello z tooUTC czasu lokalnego.

Zaczniemy przez utworzenie pliku toomap hello pogody (WBAN) informacje o tooan lotnisku kod stacji. Firma Microsoft może uzyskać korelacji ten od pliku mapowania hello dołączonego hello pogody danych. Przez mapowanie hello *CallSign* (na przykład LAX) pola w pliku danych pogody hello zbyt*pochodzenia* hello linii lotniczych danych. Jednak firma Microsoft tak się stało toohave innego mapowania dostępnych mapujący *WBAN* za*AirportID* (na przykład 12892 dla LAX) i obejmuje *strefy czasowej* który zapisano tooa Plik CSV o nazwie "wban do lotnisku id-tz. CSV", które możemy użyć. Na przykład:

| AirportID | WBAN | Strefa czasowa
|-----------|------|---------
| 10685 | 54831 | -6
| 14871 | 24232 | -8
| .. | .. | ..

pliki Hello następującego kodu odczyty każdego hello co godzinę pogody nieprzetworzone dane podzestawy toohello kolumny możemy muszą, scala plik mapowania stacji pogody hello, dostosowuje hello daty i godziny z tooUTC pomiarów i następnie zapisuje nowej wersji pliku hello:

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a>Importowanie hello lotniczych i pogody danych tooSpark DataFrames

Teraz używamy hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) tooimport hello pogodą i linii lotniczych danych tooSpark DataFrames funkcji. Tej funkcji, takich jak wiele innych metod Spark, są wykonywane w trybie opóźnienia, co oznacza, że są umieszczone w kolejce do wykonania, ale nie zostanie wykonane do czasu.

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a>Czyszczenie danych i przekształcania

Następnie przejdziemy porządkowanie danych linii lotniczych hello zaimportowane możemy toorename kolumn. Firma Microsoft tylko Zachowaj zmienne hello potrzebne i zaokrąglona godziny zaplanowanego wyjścia dół toohello najbliższej godziny tooenable scalanie z najnowszych danych pogody hello przy wyjściu:

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

Teraz wykonywać podobne operacji na danych pogody hello:

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a>Łączenie danych pogodą i linii lotniczych hello

Używamy teraz hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) funkcji toodo lewe sprzężenie zewnętrzne hello lotniczych i pogody danych przez wyjścia AirportID i datetime. sprzężenie zewnętrzne Hello pozwala nam tooretain rejestruje wszystkie dane linii lotniczych hello nawet, jeśli nie ma pasującego pogody danych. Następujące sprzężenia hello możemy Usuń zbędne kolumny i zmiana nazwy hello przechowywane kolumn tooremove hello przychodzące DataFrame prefiks wprowadzone przez hello sprzężenia.

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

W podobny sposób możemy przyłączyć hello pogodą i linii lotniczych danych na podstawie przyjęcia AirportID i daty/godziny:

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a>Zapisz wyniki tooCSV dla programu exchange z ScaleR

Na tym kończy się sprzężenia hello potrzebujemy toodo z SparkR. Możemy zapisać dane hello z hello końcowego Spark DataFrame "joinedDF5" tooa CSV dla tooScaleR wejściowych, a następnie zamknij wychodzących sesji SparkR hello. Poinformuj nas jawnie SparkR toosave hello CSV wynikowe w 80 osobnych partycji tooenable wystarczające równoległości w przetwarzaniu ScaleR:

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a>Importuj tooXDF do użycia przez ScaleR

Firma Microsoft można użyć pliku CSV hello dołączonego do linii lotniczych i pogody danych jako — dotyczy modelowania za pośrednictwem źródła danych ScaleR tekstu. Ale możemy ją tooXDF najpierw zaimportować, ponieważ jest bardziej wydajne, uruchamiając wiele operacji na powitania zestawu danych:

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a>Podział danych szkoleniowych i testów

Możemy użyć toosplit rxDataStep hello 2012 dane do testowania i Zachowaj rest hello szkolenia:

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a>Nauczenia i przetestowania modelu regresji logistyczna

Teraz możemy gotowe toobuild modelu. toosee hello wpływ danych pogody opóźnienia w Godzina nadejścia hello, używamy procedury Regresja logistyczna firmy ScaleR. Ten element służy toomodel czy przyjęcia opóźnieniem większym niż 15 minut ma wpływ pogody hello na lotniskach wyjścia i przyjęcia hello:

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

Teraz zobaczmy, jak ją na powitania dane testowe niektórych prognoz i patrzeć ROC i AUC.

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a>Ocenianie w innym miejscu

Możemy również użyć modelu hello oceniania danych na innej platformie. Jej zapisania pliku RDS tooan i transferując i importowanie RDS tego miejsca docelowego oceniania środowisku, na przykład usług SQL Server R. Jest ważne tooensure, poziomy współczynnik hello toobe danych hello oceniane zgodne te, na które hello model został utworzony. Czy dopasowanie można osiągnąć wyodrębniając i zapisywania informacji o kolumnie hello skojarzonych z hello modelowania danych za pomocą jego ScaleR `rxCreateColInfo()` funkcji, a następnie zastosowanie tego źródła danych wejściowych kolumny informacji toohello do przewidywania. W następujących hello możemy zapisać kilka wierszy hello zestawu danych testowych i Wyodrębnij i Użyj informacji o kolumnie powitania od tego przykładu w skrypcie prognozowania hello:

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a>Podsumowanie

W tym artykule firma Microsoft już pokazuje, jak jest toocombine możliwe użycie SparkR do manipulowania danymi z ScaleR do tworzenia modelu w Hadoop, Spark. Ten scenariusz wymaga Obsługa osobne sesje Spark, tylko z jedną sesję w czasie i wymiany danych za pośrednictwem plików CSV. Chociaż bezpośrednia, ten proces powinna być łatwiejsze w nadchodzącej wersji R Server, gdy SparkR ScaleR można współużytkować sesji Spark i dlatego udostępnianie Spark DataFrames.

## <a name="next-steps-and-more-information"></a>Następne kroki i dodatkowe informacje

- Aby uzyskać więcej informacji na Użyj R Server w Spark, zobacz hello [przewodnik wprowadzenie w witrynie MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)

- Ogólne informacje na temat R Server, zobacz hello [wprowadzenie R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) artykułu.

- Aby uzyskać informacje na serwerze R w usłudze HDInsight, zobacz [R Server w usłudze Azure HDInsight omówienie](hdinsight-hadoop-r-server-overview.md) i [R Server w usłudze Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).

Aby uzyskać więcej informacji na użycie SparkR zobacz:

- [Apache SparkR dokumentu](https://spark.apache.org/docs/2.1.0/sparkr.html)

- [Omówienie SparkR](https://docs.databricks.com/spark/latest/sparkr/overview.html) z Databricks
