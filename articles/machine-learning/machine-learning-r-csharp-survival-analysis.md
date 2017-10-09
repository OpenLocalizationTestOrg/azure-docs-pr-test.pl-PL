---
title: "AAA(deprecated) przetrwania analizy przy użyciu usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Prawdopodobieństwo wystąpienia zdarzenia analizy przetrwania"
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a>(przestarzałe) Surwiwalowy analizy

> [!NOTE]
> Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

W wielu scenariuszach hello główny wynik oceny jest zdarzenie tooan czasu hello zainteresowań. Innymi słowy hello pytanie "wystąpieniu tego zdarzenia zostanie?" monitu. Jako przykłady, należy wziąć pod uwagę sytuacji, w którym hello danych opisuje hello Upłynęło czasu (dni, lat, przebieg itp.) do momentu hello zdarzenie zainteresowań (relapse choroby, stopień Praca odebrane, konsola hamulca awarii). Każde wystąpienie w danych hello reprezentuje określonego obiektu (pacjenta, gdy uczniowie, car, itp.).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) odpowiedzi na pytanie hello "co to jest hello prawdopodobieństwo, że hello zdarzeń odsetek nastąpi przez czas n dla obiekt x?" Zapewniając modelu analizy przetrwania tej usługi sieci web umożliwia użytkownikom toosupply danych tootrain hello modelu i przetestować go. Hello motywu głównego doświadczenia hello jest toomodel hello hello Upłynęło czasu do czasu wystąpienia zdarzeń hello zainteresowań. 

> Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.  
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
Schemat danych wejściowych Hello hello usługi sieci web jest wyświetlana w hello w poniższej tabeli. Sześć części informacje są wymagane jako dane wejściowe hello: dane szkoleniowe, danych testowych, czas odsetek, indeks wymiaru "time" hello, indeks hello wymiaru "event" i typy zmiennych hello (ciągłe lub współczynnik). dane szkoleniowe Hello jest reprezentowane na ciąg, gdzie wierszy hello są oddzielone przecinkami, a kolumny hello są oddzielone średnikami. Witaj liczbę funkcji danych hello jest elastyczny. Wszystkie elementy hello hello ciąg wejściowy musi być liczbą. W danych szkoleniowych hello wymiaru czasu"hello" oznacza, że hello liczbę jednostek czasu (dni, lat, przebieg itp.), jaki upłynął od hello punkt początkowy hello badanie (pacjenta odbieranie narkotyków traktowania programów, badanie Praca początkowy dla użytkowników domowych, samochodu uruchamianie toobe sterowane, itp.) do czasu uruchomienia hello zdarzeń zainteresowań (pacjenta hello zwracanie toodrug użycia, hello uczniów uzyskania hello Praca stopień, car hello o awarii konsoli hamulca, itp.). Wymiar "event" Hello wskazuje, czy zdarzeń hello zainteresowania na końcu hello badania hello. Wartość "zdarzenia = 1" oznacza, że hello zdarzeń odsetek występuje w momencie hello wskazywanym przez wymiar "czas" hello; "zdarzenie = 0" oznacza, że hello zdarzeń odsetek nie przeprowadzono czasu hello wskazywanym przez wymiar "czas" hello.

* trainingdata — ciąg znaków. Wiersze są oddzielone przecinkami, a kolumny oddzielonych średnikami. Każdy wiersz zawiera wymiaru "czas", "event" wymiaru i zmienne predykcyjne.
* testingdata — jeden wiersz danych zawierający zmienne predykcyjne dla danego obiektu.
* time_of_interest — czas hello n zainteresowań.
* index_time — indeks kolumny hello wymiaru "czas" hello (począwszy od 1).
* index_event — indeks kolumny hello wymiaru "event" hello (począwszy od 1).
* variable_types — ciąg znaków średnikami jako separatorów w nim. 0 reprezentuje ciągłe, zmiennych i 1 oznacza współczynnik zmiennych.

dane wyjściowe Hello jest prawdopodobieństwo hello zdarzenia występujące w określonym czasie. 

> Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Rozpoczynanie korzystania z usług sieci web kod C#:
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




Interpretacja Hello tego testu ma następującą składnię. Przy założeniu celem hello hello danych jest toomodel hello Upłynęło czasu do czasu hello zwrócił użycia toodrug pacjentów hello, którzy otrzymali jednego z programów traktowania hello dwa. Witaj dane wyjściowe odczytów usługi sieci web hello: pacjentów trwa 35 lat, o poprzednim leku traktowania 2 godziny, biorąc program długo rezydentnej traktowania hello, i z użyciem zarówno heroiny, jak i kokainy, prawdopodobieństwo hello przekazujących użycia narkotyków toohello 95.64% dzień 500.

## <a name="creation-of-web-service"></a>Tworzenie usługi sieci web
> Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning. Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml). Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.
> 
> 

Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona i dwa [wykonanie skryptu języka R] [ execute-r-script] moduły są pobierane na powitania obszaru roboczego. Witaj schemat danych została utworzona przy użyciu prostego [wykonanie skryptu języka R][execute-r-script], który definiuje schemat danych wejściowych hello hello usługi sieci web. Ten moduł jest następnie drugi połączone toohello [wykonanie skryptu języka R] [ execute-r-script] moduł, który główne pracy. Ten moduł jest wstępnego przetwarzania danych, konstruowania modelu i prognoz. Hello danych wejściowych reprezentowany przez ciąg hello krok wstępnego przetwarzania danych, jest przekształcać i konwertowana do ramki danych. W kroku tworzenia modelu hello pakietów zewnętrznych R "survival_2.37 7.zip" najpierw jest zainstalowany na przeprowadzanie analizy przeżycia. Następnie funkcja "coxph" hello jest wykonywana po zadań przetwarzania danych serii. Szczegóły Hello funkcji "coxph" hello przetrwania analizy mogą być odczytywane z dokumentacji hello R. W kroku prognozowania hello testowania wystąpienia jest dostarczany do hello uczonego modelu z funkcją "surfit" hello, i hello krzywej przetrwania dla tego wystąpienia testowania jest tworzony jako zmienną "krzywej". Na koniec są uzyskiwane prawdopodobieństwo hello czasu hello zainteresowań. 

### <a name="experiment-flow"></a>Przepływ eksperymentu:
![Przepływ eksperymentu][1]

#### <a name="module-1"></a>Moduł 1:
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a>Moduł 2:
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a>Ograniczenia
Ta usługa sieci web może zająć tylko wartości liczbowe jako zmienne funkcji (kolumny). Kolumna "event" Hello może trwać tylko wartości 0 lub 1. Kolumna "time" Hello musi toobe dodatnią liczbą całkowitą.

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

