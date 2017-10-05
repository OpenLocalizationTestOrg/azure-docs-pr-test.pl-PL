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
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="bee66-103">(przestarzałe) Surwiwalowy analizy</span><span class="sxs-lookup"><span data-stu-id="bee66-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="bee66-104">Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="bee66-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="bee66-105">Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="bee66-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="bee66-106">Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="bee66-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="bee66-107">W wielu scenariuszach główny wynik oceny to czas na zdarzenie zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="bee66-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span></span> <span data-ttu-id="bee66-108">Innymi słowy zapytania "wystąpieniu tego zdarzenia zostanie?"</span><span class="sxs-lookup"><span data-stu-id="bee66-108">In other words, the question “when this event will occur?”</span></span> <span data-ttu-id="bee66-109">monitu.</span><span class="sxs-lookup"><span data-stu-id="bee66-109">is asked.</span></span> <span data-ttu-id="bee66-110">Jako przykłady, należy wziąć pod uwagę sytuacji, gdy dane w tym artykule opisano czas (dni, lat, przebieg itp.) do zdarzenia zainteresowań (relapse choroby, stopień Praca odebrane, konsola hamulca awarii) występuje.</span><span class="sxs-lookup"><span data-stu-id="bee66-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="bee66-111">Każde wystąpienie w danych reprezentuje określonego obiektu (pacjenta, gdy uczniowie, car, itp.).</span><span class="sxs-lookup"><span data-stu-id="bee66-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="bee66-112">To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) odpowiedzi na pytanie "jakie jest prawdopodobieństwo, że zdarzenie odsetek zostanie przeprowadzona przez czas n dla obiekt x?"</span><span class="sxs-lookup"><span data-stu-id="bee66-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="bee66-113">Zapewniając modelu analizy przetrwania tej usługi sieci web umożliwia użytkownikom dostarczania danych do nauczenia modelu i przetestować go.</span><span class="sxs-lookup"><span data-stu-id="bee66-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span></span> <span data-ttu-id="bee66-114">Motywu głównego doświadczenia jest model długość czasu, jaki upłynął, dopóki nie wystąpi zdarzenie zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="bee66-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span></span> 

> <span data-ttu-id="bee66-115">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="bee66-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="bee66-116">Ale celem usługi sieci web jest również służyć jako przykład sposobu użycia usługi Azure Machine Learning do tworzenia usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="bee66-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="bee66-117">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="bee66-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="bee66-118">Usługi sieci web może następnie opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w całym świecie bez ustawień infrastruktury przez autora usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="bee66-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="bee66-119">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="bee66-119">Consumption of web service</span></span>
<span data-ttu-id="bee66-120">W poniższej tabeli przedstawiono schemat danych wejściowych usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="bee66-120">The input data schema of the web service is shown in the following table.</span></span> <span data-ttu-id="bee66-121">Sześć części informacje są wymagane jako dane wejściowe: uczenie danych, testowanie, wymiaru czasu zainteresowań, indeks "czas", indeks wymiaru "event" i typy zmiennych (ciągłe lub współczynnik).</span><span class="sxs-lookup"><span data-stu-id="bee66-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span></span> <span data-ttu-id="bee66-122">Dane szkoleniowe odpowiada na ciąg, gdzie wiersze są oddzielone przecinkami, a kolumny oddzielonych średnikami.</span><span class="sxs-lookup"><span data-stu-id="bee66-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span></span> <span data-ttu-id="bee66-123">Liczba elementów danych jest elastyczny.</span><span class="sxs-lookup"><span data-stu-id="bee66-123">The number of features of the data is flexible.</span></span> <span data-ttu-id="bee66-124">Wszystkie elementy w ciąg wejściowy musi być liczbą.</span><span class="sxs-lookup"><span data-stu-id="bee66-124">All the elements in the input string must be numeric.</span></span> <span data-ttu-id="bee66-125">W danych szkoleniowych wymiaru "czas" oznacza, że liczba jednostek czasu (dni, lat, przebieg itp.), jaki upłynął od punkt początkowy badania (pacjenta odbieranie narkotyków traktowania programów, badanie Praca początkowy dla użytkowników domowych, samochodu rozpoczyna się zmiennych, itp.) do zdarzenia zainteresowań (pacjenta wracając do użycia narkotyków, uczniów uzyskania stopnia praca, car o awarii hamulca konsoli itp.) występuje.</span><span class="sxs-lookup"><span data-stu-id="bee66-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="bee66-126">Wymiar "event" wskazuje, czy zdarzenie odsetek na końcu badania.</span><span class="sxs-lookup"><span data-stu-id="bee66-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span></span> <span data-ttu-id="bee66-127">Wartość "zdarzenia = 1" oznacza, że odsetek zdarzenie o godzinie określonej w wymiarze "czas"; "zdarzenie = 0" oznacza, że nie przeprowadzono zdarzenia odsetek czasu wskazanych w wymiarze "czas".</span><span class="sxs-lookup"><span data-stu-id="bee66-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span></span>

* <span data-ttu-id="bee66-128">trainingdata — ciąg znaków.</span><span class="sxs-lookup"><span data-stu-id="bee66-128">trainingdata - A character string.</span></span> <span data-ttu-id="bee66-129">Wiersze są oddzielone przecinkami, a kolumny oddzielonych średnikami.</span><span class="sxs-lookup"><span data-stu-id="bee66-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="bee66-130">Każdy wiersz zawiera wymiaru "czas", "event" wymiaru i zmienne predykcyjne.</span><span class="sxs-lookup"><span data-stu-id="bee66-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="bee66-131">testingdata — jeden wiersz danych zawierający zmienne predykcyjne dla danego obiektu.</span><span class="sxs-lookup"><span data-stu-id="bee66-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="bee66-132">time_of_interest - n odsetek czas, który upłynął.</span><span class="sxs-lookup"><span data-stu-id="bee66-132">time_of_interest - The elapsed time of interest n.</span></span>
* <span data-ttu-id="bee66-133">index_time — indeks kolumny wymiaru "czas" (począwszy od 1).</span><span class="sxs-lookup"><span data-stu-id="bee66-133">index_time - The column index of the “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="bee66-134">index_event — indeks kolumny wymiaru "event" (począwszy od 1).</span><span class="sxs-lookup"><span data-stu-id="bee66-134">index_event - The column index of the “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="bee66-135">variable_types — ciąg znaków średnikami jako separatorów w nim.</span><span class="sxs-lookup"><span data-stu-id="bee66-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="bee66-136">0 reprezentuje ciągłe, zmiennych i 1 oznacza współczynnik zmiennych.</span><span class="sxs-lookup"><span data-stu-id="bee66-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="bee66-137">Dane wyjściowe to prawdopodobieństwo zdarzenia występujące w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="bee66-137">The output is the probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="bee66-138">Ta usługa hostowana w portalu Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="bee66-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="bee66-139">Istnieje wiele sposobów używania usługi w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="bee66-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="bee66-140">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="bee66-140">Starting C# code for web service consumption:</span></span>
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




<span data-ttu-id="bee66-141">Interpretacja tego testu ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="bee66-141">The interpretation of this test is as follows.</span></span> <span data-ttu-id="bee66-142">Zakładając, że celem danych jest modelować czas, który upłynął do powrotu do użycia narkotyków dla pacjentów, którzy otrzymali jeden z dwóch traktowania programów.</span><span class="sxs-lookup"><span data-stu-id="bee66-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span></span> <span data-ttu-id="bee66-143">Dane wyjściowe odczytów usługi sieci web: pacjentów trwa 35 lat, o poprzednim leku traktowania 2 godziny, biorąc program traktowania długo lokalną i z użyciem zarówno heroiny, jak i kokainy, wracając do użycia narkotyków prawdopodobieństwo 95.64% dzień 500.</span><span class="sxs-lookup"><span data-stu-id="bee66-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="bee66-144">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="bee66-144">Creation of web service</span></span>
> <span data-ttu-id="bee66-145">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bee66-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="bee66-146">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="bee66-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="bee66-147">Poniżej przedstawiono zrzut ekranu doświadczenia utworzony kod przykład i usługi sieci web dla każdego z modułów w ramach eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="bee66-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="bee66-148">Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona i dwa [wykonanie skryptu języka R] [ execute-r-script] moduły są pobierane na obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="bee66-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="bee66-149">Schemat danych został utworzony przy użyciu prostego [wykonanie skryptu języka R][execute-r-script], który definiuje schemat danych wejściowych dla usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="bee66-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span></span> <span data-ttu-id="bee66-150">Ten moduł jest następnie łączony drugi [wykonanie skryptu języka R] [ execute-r-script] moduł, który główne pracy.</span><span class="sxs-lookup"><span data-stu-id="bee66-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="bee66-151">Ten moduł jest wstępnego przetwarzania danych, konstruowania modelu i prognoz.</span><span class="sxs-lookup"><span data-stu-id="bee66-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="bee66-152">W kroku wstępnego przetwarzania danych danych wejściowych reprezentowany przez ciąg jest przekształcać i konwertowana do ramki danych.</span><span class="sxs-lookup"><span data-stu-id="bee66-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="bee66-153">W kroku tworzenia modelu pakietów zewnętrznych R "survival_2.37 7.zip" najpierw zainstalowano przeprowadzania analizy przeżycia.</span><span class="sxs-lookup"><span data-stu-id="bee66-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="bee66-154">Następnie funkcja "coxph" jest wykonywana po zadań przetwarzania danych serii.</span><span class="sxs-lookup"><span data-stu-id="bee66-154">Then the “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="bee66-155">Szczegóły funkcji "coxph" przetrwania analizy mogą być odczytywane z dokumentacji R.</span><span class="sxs-lookup"><span data-stu-id="bee66-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span></span> <span data-ttu-id="bee66-156">W kroku prognozowania testowania wystąpienia jest dostarczany do trenowanego modelu przy użyciu funkcji "surfit", i krzywej przetrwania dla tego wystąpienia testowania jest tworzony jako zmienną "krzywej".</span><span class="sxs-lookup"><span data-stu-id="bee66-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="bee66-157">Na koniec są uzyskiwane prawdopodobieństwo czasu zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="bee66-157">Finally, the probability of the time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="bee66-158">Przepływ eksperymentu:</span><span class="sxs-lookup"><span data-stu-id="bee66-158">Experiment flow:</span></span>
![Przepływ eksperymentu][1]

#### <a name="module-1"></a><span data-ttu-id="bee66-160">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="bee66-160">Module 1:</span></span>
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

#### <a name="module-2"></a><span data-ttu-id="bee66-161">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="bee66-161">Module 2:</span></span>
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




## <a name="limitations"></a><span data-ttu-id="bee66-162">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="bee66-162">Limitations</span></span>
<span data-ttu-id="bee66-163">Ta usługa sieci web może zająć tylko wartości liczbowe jako zmienne funkcji (kolumny).</span><span class="sxs-lookup"><span data-stu-id="bee66-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="bee66-164">Kolumna "event" może być tylko wartość 0 lub 1.</span><span class="sxs-lookup"><span data-stu-id="bee66-164">The “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="bee66-165">Kolumna "time" musi być dodatnią liczbą całkowitą.</span><span class="sxs-lookup"><span data-stu-id="bee66-165">The “time” column needs to be a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="bee66-166">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="bee66-166">FAQ</span></span>
<span data-ttu-id="bee66-167">Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="bee66-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

