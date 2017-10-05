---
title: "(przestarzałe) Analiza przetrwania przy użyciu usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7d4066d5f15a39c428d8035257c4841f9b3cc775
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-survival-analysis"></a>(przestarzałe) Surwiwalowy analizy

> [!NOTE]
> Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

W wielu scenariuszach główny wynik oceny to czas na zdarzenie zainteresowań. Innymi słowy zapytania "wystąpieniu tego zdarzenia zostanie?" monitu. Jako przykłady, należy wziąć pod uwagę sytuacji, gdy dane w tym artykule opisano czas (dni, lat, przebieg itp.) do zdarzenia zainteresowań (relapse choroby, stopień Praca odebrane, konsola hamulca awarii) występuje. Każde wystąpienie w danych reprezentuje określonego obiektu (pacjenta, gdy uczniowie, car, itp.).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) odpowiedzi na pytanie "jakie jest prawdopodobieństwo, że zdarzenie odsetek zostanie przeprowadzona przez czas n dla obiekt x?" Zapewniając modelu analizy przetrwania tej usługi sieci web umożliwia użytkownikom dostarczania danych do nauczenia modelu i przetestować go. Motywu głównego doświadczenia jest model długość czasu, jaki upłynął, dopóki nie wystąpi zdarzenie zainteresowań. 

> Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale celem usługi sieci web jest również służyć jako przykład sposobu użycia usługi Azure Machine Learning do tworzenia usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. Usługi sieci web może następnie opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w całym świecie bez ustawień infrastruktury przez autora usługi sieci web.  
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
W poniższej tabeli przedstawiono schemat danych wejściowych usługi sieci web. Sześć części informacje są wymagane jako dane wejściowe: uczenie danych, testowanie, wymiaru czasu zainteresowań, indeks "czas", indeks wymiaru "event" i typy zmiennych (ciągłe lub współczynnik). Dane szkoleniowe odpowiada na ciąg, gdzie wiersze są oddzielone przecinkami, a kolumny oddzielonych średnikami. Liczba elementów danych jest elastyczny. Wszystkie elementy w ciąg wejściowy musi być liczbą. W danych szkoleniowych wymiaru "czas" oznacza, że liczba jednostek czasu (dni, lat, przebieg itp.), jaki upłynął od punkt początkowy badania (pacjenta odbieranie narkotyków traktowania programów, badanie Praca początkowy dla użytkowników domowych, samochodu rozpoczyna się zmiennych, itp.) do zdarzenia zainteresowań (pacjenta wracając do użycia narkotyków, uczniów uzyskania stopnia praca, car o awarii hamulca konsoli itp.) występuje. Wymiar "event" wskazuje, czy zdarzenie odsetek na końcu badania. Wartość "zdarzenia = 1" oznacza, że odsetek zdarzenie o godzinie określonej w wymiarze "czas"; "zdarzenie = 0" oznacza, że nie przeprowadzono zdarzenia odsetek czasu wskazanych w wymiarze "czas".

* trainingdata — ciąg znaków. Wiersze są oddzielone przecinkami, a kolumny oddzielonych średnikami. Każdy wiersz zawiera wymiaru "czas", "event" wymiaru i zmienne predykcyjne.
* testingdata — jeden wiersz danych zawierający zmienne predykcyjne dla danego obiektu.
* time_of_interest - n odsetek czas, który upłynął.
* index_time — indeks kolumny wymiaru "czas" (począwszy od 1).
* index_event — indeks kolumny wymiaru "event" (począwszy od 1).
* variable_types — ciąg znaków średnikami jako separatorów w nim. 0 reprezentuje ciągłe, zmiennych i 1 oznacza współczynnik zmiennych.

Dane wyjściowe to prawdopodobieństwo zdarzenia występujące w określonym czasie. 

> Ta usługa hostowana w portalu Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

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




Interpretacja tego testu ma następującą składnię. Zakładając, że celem danych jest modelować czas, który upłynął do powrotu do użycia narkotyków dla pacjentów, którzy otrzymali jeden z dwóch traktowania programów. Dane wyjściowe odczytów usługi sieci web: pacjentów trwa 35 lat, o poprzednim leku traktowania 2 godziny, biorąc program traktowania długo lokalną i z użyciem zarówno heroiny, jak i kokainy, wracając do użycia narkotyków prawdopodobieństwo 95.64% dzień 500.

## <a name="creation-of-web-service"></a>Tworzenie usługi sieci web
> Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning. Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml). Poniżej przedstawiono zrzut ekranu doświadczenia utworzony kod przykład i usługi sieci web dla każdego z modułów w ramach eksperymentu.
> 
> 

Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona i dwa [wykonanie skryptu języka R] [ execute-r-script] moduły są pobierane na obszar roboczy. Schemat danych został utworzony przy użyciu prostego [wykonanie skryptu języka R][execute-r-script], który definiuje schemat danych wejściowych dla usługi sieci web. Ten moduł jest następnie łączony drugi [wykonanie skryptu języka R] [ execute-r-script] moduł, który główne pracy. Ten moduł jest wstępnego przetwarzania danych, konstruowania modelu i prognoz. W kroku wstępnego przetwarzania danych danych wejściowych reprezentowany przez ciąg jest przekształcać i konwertowana do ramki danych. W kroku tworzenia modelu pakietów zewnętrznych R "survival_2.37 7.zip" najpierw zainstalowano przeprowadzania analizy przeżycia. Następnie funkcja "coxph" jest wykonywana po zadań przetwarzania danych serii. Szczegóły funkcji "coxph" przetrwania analizy mogą być odczytywane z dokumentacji R. W kroku prognozowania testowania wystąpienia jest dostarczany do trenowanego modelu przy użyciu funkcji "surfit", i krzywej przetrwania dla tego wystąpienia testowania jest tworzony jako zmienną "krzywej". Na koniec są uzyskiwane prawdopodobieństwo czasu zainteresowań. 

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

    maml.mapOutputPort("sampleInput"); #send data to output port

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

    # Prepare to build model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct the execution string
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

    # Fit a Cox proportional hazards model and get the predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find the event occurrence probability
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

    #Pull out results to send to web service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a>Ograniczenia
Ta usługa sieci web może zająć tylko wartości liczbowe jako zmienne funkcji (kolumny). Kolumna "event" może być tylko wartość 0 lub 1. Kolumna "time" musi być dodatnią liczbą całkowitą.

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

