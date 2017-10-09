---
title: AAA(deprecated) regresji liniowej Multivariate - Azure | Dokumentacja firmy Microsoft
description: "(przestarzałe) Regresja liniowa wielu zmiennych"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
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
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="52a95-103">(przestarzałe) Regresja liniowa wielu zmiennych</span><span class="sxs-lookup"><span data-stu-id="52a95-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="52a95-104">Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="52a95-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="52a95-105">Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="52a95-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="52a95-106">Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="52a95-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="52a95-107">Załóżmy, że masz zestawu danych i jak tooquickly czy prognozowania zależnych od zmiennej (y) dla poszczególnych osób (i), w oparciu o zmienne niezależne.</span><span class="sxs-lookup"><span data-stu-id="52a95-107">Suppose you have a dataset and would like tooquickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="52a95-108">Regresja liniowa jest popularnych techniki statystyczne używane dla takich prognoz.</span><span class="sxs-lookup"><span data-stu-id="52a95-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="52a95-109">W tym miejscu hello zależnych od zmiennej y zakłada, że toobe wartości ciągłej.</span><span class="sxs-lookup"><span data-stu-id="52a95-109">Here hello dependent variable y is assumed toobe a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="52a95-110">Prosty scenariusz może być, gdzie analitykowi hello próbuje wagi hello toopredict osoby (y), w oparciu o ich wysokość (x).</span><span class="sxs-lookup"><span data-stu-id="52a95-110">A simple scenario could be where hello researcher is trying toopredict hello weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="52a95-111">Bardziej zaawansowanym scenariuszu można gdzie analitykowi hello zawiera dodatkowe informacje dotyczące poszczególnych (takich jak wagi, płci, wyścigu) hello i próbuje wagi hello toopredict hello osoby.</span><span class="sxs-lookup"><span data-stu-id="52a95-111">A more advanced scenario could be where hello researcher has additional information for hello individual (such as weight, gender, race) and attempts toopredict hello weight of hello individual.</span></span> <span data-ttu-id="52a95-112">To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) mieści się hello danych toohello modelu regresji liniowej i dane wyjściowe hello przewidywane wartości (y) dla każdego z uwagi hello hello danych.</span><span class="sxs-lookup"><span data-stu-id="52a95-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits hello linear regression model toohello data and outputs hello predicted value (y) for each of hello observations in hello data.</span></span>

> <span data-ttu-id="52a95-113">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="52a95-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="52a95-114">Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="52a95-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="52a95-115">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="52a95-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="52a95-116">usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="52a95-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="52a95-117">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="52a95-117">Consumption of web service</span></span>
<span data-ttu-id="52a95-118">Ta hello zapewnia usługi sieci web przewidzieć wartości hello zależnych od zmiennej opartej na zmienne niezależne hello wszystkie hello uwag.</span><span class="sxs-lookup"><span data-stu-id="52a95-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="52a95-119">Usługa sieci web Hello oczekuje hello użytkownika końcowego tooinput dane jako ciąg, gdzie wiersze są oddzielone przecinkami (,), a kolumny oddzielonych średnikami (;).</span><span class="sxs-lookup"><span data-stu-id="52a95-119">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="52a95-120">Usługa sieci web Hello oczekuje 1 wiersz w czasie i oczekuje hello pierwszej kolumny toobe hello zależnych od zmiennej.</span><span class="sxs-lookup"><span data-stu-id="52a95-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="52a95-121">Przykład zestawu danych może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="52a95-121">An example dataset could look like this:</span></span>

![Dane przykładowe][1]

<span data-ttu-id="52a95-123">Uwagi bez zależnych od zmiennej można wprowadzić jako "Brak" y.</span><span class="sxs-lookup"><span data-stu-id="52a95-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="52a95-124">Witaj danych wejściowych dla hello powyżej zestawu danych czy powitania po ciągu: "10 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1 NA; 3 i 4".</span><span class="sxs-lookup"><span data-stu-id="52a95-124">hello data input for hello above dataset would be hello following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="52a95-125">Witaj output hello przewidywane wartości dla poszczególnych wierszy hello opiera się na powitania zmienne niezależne.</span><span class="sxs-lookup"><span data-stu-id="52a95-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="52a95-126">Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="52a95-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="52a95-127">Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="52a95-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="52a95-128">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="52a95-128">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="52a95-129">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="52a95-129">Creation of web service</span></span>
> <span data-ttu-id="52a95-130">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="52a95-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="52a95-131">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="52a95-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="52a95-132">Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="52a95-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="52a95-133">Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona i dwa [wykonanie skryptu języka R] [ execute-r-script] moduły są pobierane na powitania obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="52a95-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="52a95-134">Ta usługa sieci web uruchamia eksperymentu uczenia maszynowego Azure przy użyciu podstawowego skrypt języka R.</span><span class="sxs-lookup"><span data-stu-id="52a95-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="52a95-135">Istnieją 2 części toothis eksperymentu: definicja schematu i szkolenia modelu + oceniania.</span><span class="sxs-lookup"><span data-stu-id="52a95-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="52a95-136">Moduł pierwszy Hello definiuje strukturę hello oczekiwano hello wejściowy zestaw danych, gdzie hello pierwszej zmiennej jest hello zależnych od zmiennej, a pozostałe zmienne hello są niezależne.</span><span class="sxs-lookup"><span data-stu-id="52a95-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="52a95-137">Drugi moduł Hello pasuje model regresji liniowej ogólnego hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="52a95-137">hello second module fits a generic linear regression model for hello input data.</span></span>  

![Przepływ eksperymentu][3]

#### <a name="module-1"></a><span data-ttu-id="52a95-139">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="52a95-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="52a95-140">Definicja schematu</span><span class="sxs-lookup"><span data-stu-id="52a95-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="52a95-141">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="52a95-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="52a95-142">LM modelowania</span><span class="sxs-lookup"><span data-stu-id="52a95-142">LM modeling</span></span>
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a><span data-ttu-id="52a95-143">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="52a95-143">Limitations</span></span>
<span data-ttu-id="52a95-144">Jest bardzo prosty przykład wielu usług sieci web regresji liniowej.</span><span class="sxs-lookup"><span data-stu-id="52a95-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="52a95-145">Jak wynika z powyższych hello przykładowy kod, nie błąd Przechwytywanie jest zaimplementowana i usługi hello przyjęto założenie, że wszystko jest ciągłe zmiennej (nie podzielone na kategorie funkcji dozwolone), jako hello usługi tylko dane wejściowe wartości liczbowe w czasie hello hello tworzenia tej sieci Web Usługa.</span><span class="sxs-lookup"><span data-stu-id="52a95-145">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="52a95-146">Ponadto usługa hello obsługuje obecnie rozmiar ograniczoną ilość danych, powodu toohello charakter żądanie/odpowiedź usługi sieci web hello połączeń i hello fakt, że hello modelu jest nadaje się zawsze nosi nazwę usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="52a95-146">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="52a95-147">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="52a95-147">FAQ</span></span>
<span data-ttu-id="52a95-148">Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="52a95-148">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

