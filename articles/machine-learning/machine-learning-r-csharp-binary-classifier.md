---
title: AAA(deprecated) binarne klasyfikatora - Azure | Dokumentacja firmy Microsoft
description: "(przestarzałe) Klasyfikator binarne"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="d4abc-103">(przestarzałe) Klasyfikator binarne</span><span class="sxs-lookup"><span data-stu-id="d4abc-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="d4abc-104">Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="d4abc-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="d4abc-105">Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="d4abc-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="d4abc-106">Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d4abc-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="d4abc-107">Załóżmy, że masz zestawu danych i chcesz toopredict binarne zależnych od zmiennej opartej na zmienne niezależne hello.</span><span class="sxs-lookup"><span data-stu-id="d4abc-107">Suppose you have a dataset and would like toopredict a binary dependent variable based on hello independent variables.</span></span> <span data-ttu-id="d4abc-108">"Regresja logistyczna" jest popularnych techniki statystyczne używane dla takich prognoz.</span><span class="sxs-lookup"><span data-stu-id="d4abc-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="d4abc-109">W tym miejscu hello zależnych od zmiennej jest binary lub dichotomous, a p jest prawdopodobieństwo hello obecności cechy hello zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="d4abc-109">Here hello dependent variable is binary or dichotomous, and p is hello probability of presence of hello characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="d4abc-110">Prosty scenariusz może być, gdzie analitykowi próbuje toopredict czy potencjalnego uczniów jest prawdopodobnie tooaccept university tooa oferta wprowadzenia na podstawie informacji (GPA w szkole, dochód rodziny, znajdują się stan, płci).</span><span class="sxs-lookup"><span data-stu-id="d4abc-110">A simple scenario could be where a researcher is trying toopredict whether a prospective student is likely tooaccept an admission offer tooa university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="d4abc-111">wyniki przewidywane Hello jest prawdopodobieństwo hello hello student potencjalnego akceptowanie hello wprowadzenia oferty.</span><span class="sxs-lookup"><span data-stu-id="d4abc-111">hello predicted outcome is hello probability of hello prospective student accepting hello admission offer.</span></span> <span data-ttu-id="d4abc-112">To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/log_regression) mieści się hello Regresja logistyczna modelu toohello danych i dane wyjściowe hello wartość prawdopodobieństwa (y) dla każdego z uwagi hello hello danych.</span><span class="sxs-lookup"><span data-stu-id="d4abc-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits hello logistic regression model toohello data and outputs hello probability value (y) for each of hello observations in hello data.</span></span>  

> <span data-ttu-id="d4abc-113">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="d4abc-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="d4abc-114">Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="d4abc-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="d4abc-115">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="d4abc-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="d4abc-116">usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="d4abc-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="d4abc-117">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="d4abc-117">Consumption of web service</span></span>
<span data-ttu-id="d4abc-118">Ta hello zapewnia usługi sieci web przewidzieć wartości hello zależnych od zmiennej opartej na zmienne niezależne hello wszystkie hello uwag.</span><span class="sxs-lookup"><span data-stu-id="d4abc-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="d4abc-119">Usługa sieci web Hello oczekuje hello użytkownika końcowego tooinput dane jako ciąg, gdzie wiersze są oddzielone przecinkami (,), a kolumny oddzielonych średnikami (;).</span><span class="sxs-lookup"><span data-stu-id="d4abc-119">hello web service expects hello end user tooinput data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="d4abc-120">Usługa sieci web Hello oczekuje 1 wiersz w czasie i oczekuje hello pierwszej kolumny toobe hello zależnych od zmiennej.</span><span class="sxs-lookup"><span data-stu-id="d4abc-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="d4abc-121">Przykład zestawu danych może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="d4abc-121">An example dataset could look like this:</span></span>

![Dane przykładowe][1]

<span data-ttu-id="d4abc-123">Uwagi bez zależnych od zmiennej można wprowadzić jako "Brak" y.</span><span class="sxs-lookup"><span data-stu-id="d4abc-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="d4abc-124">Witaj danych wejściowych dla hello powyżej zestawu danych czy powitania po ciągu: "1 5 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, NA; 3; 4".</span><span class="sxs-lookup"><span data-stu-id="d4abc-124">hello data input for hello above dataset would be hello following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="d4abc-125">Witaj output hello przewidywane wartości dla poszczególnych wierszy hello opiera się na powitania zmienne niezależne.</span><span class="sxs-lookup"><span data-stu-id="d4abc-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="d4abc-126">Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="d4abc-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="d4abc-127">Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d4abc-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="d4abc-128">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="d4abc-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
           public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
        byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
        return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
        var input = new Input() { value = TextBox1.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
        var httpClient = new HttpClient();

        httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
        httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

        var response = httpClient.PostAsync(acitionUri, new StringContent(json));
        var result = response.Result.Content;
        var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="d4abc-129">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="d4abc-129">Creation of web service</span></span>
> <span data-ttu-id="d4abc-130">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d4abc-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="d4abc-131">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="d4abc-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="d4abc-132">Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="d4abc-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="d4abc-133">Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona i dwa [wykonanie skryptu języka R] [ execute-r-script] modułów pobierane na powitania obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="d4abc-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="d4abc-134">Ta usługa sieci web uruchamia eksperymentu uczenia maszynowego Azure przy użyciu podstawowego skrypt języka R.</span><span class="sxs-lookup"><span data-stu-id="d4abc-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="d4abc-135">Istnieją 2 części toothis eksperymentu: definicja schematu i szkolenia modelu + oceniania.</span><span class="sxs-lookup"><span data-stu-id="d4abc-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="d4abc-136">Moduł pierwszy Hello definiuje strukturę hello oczekiwano hello wejściowy zestaw danych, gdzie hello pierwszej zmiennej jest hello zależnych od zmiennej, a pozostałe zmienne hello są niezależne.</span><span class="sxs-lookup"><span data-stu-id="d4abc-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="d4abc-137">Drugi moduł Hello pasuje do ogólnego Regresja logistyczna model hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="d4abc-137">hello second module fits a generic logistic regression model for hello input data.</span></span>    

![Przepływ eksperymentu][2]

#### <a name="module-1"></a><span data-ttu-id="d4abc-139">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="d4abc-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="d4abc-140">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="d4abc-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="d4abc-141">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="d4abc-141">Limitations</span></span>
<span data-ttu-id="d4abc-142">Jest bardzo prosty przykład usługi sieci web klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="d4abc-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="d4abc-143">Jak wynika z powyższych hello przykładowy kod, nie błąd Przechwytywanie jest zaimplementowana i usługi hello przyjęto założenie, że wszystko jest zmienną binary/ciągłego (nie podzielone na kategorie funkcji dozwolone), jako hello usługi tylko dane wejściowe wartości liczbowe w czasie hello hello tworzenia tego Usługa sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d4abc-143">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a binary/continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="d4abc-144">Ponadto usługa hello obsługuje obecnie rozmiar ograniczoną ilość danych, powodu toohello charakter żądanie/odpowiedź usługi sieci web hello połączeń i hello fakt, że hello modelu jest nadaje się zawsze nosi nazwę usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="d4abc-144">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="d4abc-145">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="d4abc-145">FAQ</span></span>
<span data-ttu-id="d4abc-146">Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d4abc-146">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

