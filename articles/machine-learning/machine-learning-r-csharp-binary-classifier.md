---
title: "(przestarzałe) Klasyfikator Binary - Azure | Dokumentacja firmy Microsoft"
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
redirect_document_id: TRUE
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="8e92e-103">(przestarzałe) Klasyfikator binarne</span><span class="sxs-lookup"><span data-stu-id="8e92e-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="8e92e-104">Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="8e92e-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="8e92e-105">Możesz znaleźć wiele eksperymenty przykład przydatne i interfejsów API w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="8e92e-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="8e92e-106">Aby uzyskać więcej informacji o galerii, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="8e92e-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="8e92e-107">Załóżmy, że masz zestawu danych i chcesz przewidzieć binarne zależnych od zmiennej opartej na zmienne niezależne.</span><span class="sxs-lookup"><span data-stu-id="8e92e-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span></span> <span data-ttu-id="8e92e-108">"Regresja logistyczna" jest popularnych techniki statystyczne używane dla takich prognoz.</span><span class="sxs-lookup"><span data-stu-id="8e92e-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="8e92e-109">Oto zmienną zależną binary lub dichotomous i p jest prawdopodobieństwo występowania cech odsetek.</span><span class="sxs-lookup"><span data-stu-id="8e92e-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="8e92e-110">Prosty scenariusz może być, gdzie analitykowi próbuje przewidzieć czy potencjalnego uczniów jest może zaakceptować ofertę wprowadzenia uniwersytetu na podstawie informacji (GPA w szkole, dochód rodziny, znajdują się stan, płci).</span><span class="sxs-lookup"><span data-stu-id="8e92e-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="8e92e-111">Wyniki przewidywane jest prawdopodobieństwo potencjalnego student akceptowanie oferta wprowadzenia.</span><span class="sxs-lookup"><span data-stu-id="8e92e-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span></span> <span data-ttu-id="8e92e-112">To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/log_regression) pasuje Regresja logistyczna modelu do danych i wyświetla wartość prawdopodobieństwa (y) dla każdego uwag w danych.</span><span class="sxs-lookup"><span data-stu-id="8e92e-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span></span>  

> <span data-ttu-id="8e92e-113">Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład.</span><span class="sxs-lookup"><span data-stu-id="8e92e-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="8e92e-114">Ale celem usługi sieci web jest również służyć jako przykład sposobu użycia usługi Azure Machine Learning do tworzenia usług sieci web na podstawie kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="8e92e-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="8e92e-115">Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e92e-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="8e92e-116">Usługi sieci web może następnie opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w całym świecie bez ustawień infrastruktury przez autora usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e92e-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="8e92e-117">Użycie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="8e92e-117">Consumption of web service</span></span>
<span data-ttu-id="8e92e-118">Ta usługa sieci web zapewnia przewidywane wartości zmiennej zależnej na podstawie zmiennych niezależne od wszystkich obserwacji.</span><span class="sxs-lookup"><span data-stu-id="8e92e-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="8e92e-119">Usługa sieci web oczekuje użytkownikom na wprowadzanie danych jako ciąg, gdzie wiersze są oddzielone przecinkami (,), a kolumny oddzielonych średnikami (;).</span><span class="sxs-lookup"><span data-stu-id="8e92e-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="8e92e-120">Usługa sieci web oczekuje 1 wiersz w czasie i oczekuje pierwszej kolumny jako zmienną zależną.</span><span class="sxs-lookup"><span data-stu-id="8e92e-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="8e92e-121">Przykład zestawu danych może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="8e92e-121">An example dataset could look like this:</span></span>

![Dane przykładowe][1]

<span data-ttu-id="8e92e-123">Uwagi bez zależnych od zmiennej można wprowadzić jako "Brak" y.</span><span class="sxs-lookup"><span data-stu-id="8e92e-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="8e92e-124">Dane wejściowe dla powyższych zestawu danych może być następujący ciąg: "1 5 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, NA; 3; 4".</span><span class="sxs-lookup"><span data-stu-id="8e92e-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="8e92e-125">Dane wyjściowe są przewidzianej wartości dla wszystkich wierszy, w oparciu o zmienne niezależne.</span><span class="sxs-lookup"><span data-stu-id="8e92e-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="8e92e-126">Ta usługa hostowana w portalu Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET.</span><span class="sxs-lookup"><span data-stu-id="8e92e-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="8e92e-127">Istnieje wiele sposobów używania usługi w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="8e92e-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="8e92e-128">Rozpoczynanie korzystania z usług sieci web kod C#:</span><span class="sxs-lookup"><span data-stu-id="8e92e-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="8e92e-129">Tworzenie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="8e92e-129">Creation of web service</span></span>
> <span data-ttu-id="8e92e-130">Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8e92e-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="8e92e-131">Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="8e92e-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="8e92e-132">Poniżej przedstawiono zrzut ekranu doświadczenia utworzony kod przykład i usługi sieci web dla każdego z modułów w ramach eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="8e92e-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="8e92e-133">Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona i dwa [wykonanie skryptu języka R] [ execute-r-script] modułów pobierane na obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="8e92e-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="8e92e-134">Ta usługa sieci web uruchamia eksperymentu uczenia maszynowego Azure przy użyciu podstawowego skrypt języka R.</span><span class="sxs-lookup"><span data-stu-id="8e92e-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="8e92e-135">Istnieją 2 części do tego eksperymentu: definicja schematu i szkolenia modelu + oceniania.</span><span class="sxs-lookup"><span data-stu-id="8e92e-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="8e92e-136">Pierwszy modułu definiuje oczekiwanej struktury wejściowego zestawu danych, gdzie pierwszej zmiennej jest zmienną zależną, a pozostałe zmienne są niezależne.</span><span class="sxs-lookup"><span data-stu-id="8e92e-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="8e92e-137">Drugi moduł pasuje do ogólnego Regresja logistyczna modelu dla danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="8e92e-137">The second module fits a generic logistic regression model for the input data.</span></span>    

![Przepływ eksperymentu][2]

#### <a name="module-1"></a><span data-ttu-id="8e92e-139">Moduł 1:</span><span class="sxs-lookup"><span data-stu-id="8e92e-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="8e92e-140">Moduł 2:</span><span class="sxs-lookup"><span data-stu-id="8e92e-140">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="8e92e-141">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="8e92e-141">Limitations</span></span>
<span data-ttu-id="8e92e-142">Jest bardzo prosty przykład usługi sieci web klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="8e92e-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="8e92e-143">Jak wynika z przykładowy kod powyżej, nie błąd Przechwytywanie jest zaimplementowany i usługa przyjęto założenie, że wszystko jest zmienną binary/ciągłego (nie podzielone na kategorie funkcji dozwolone), jako usługa tylko dane wejściowe wartości liczbowe w momencie utworzenia tej usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e92e-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="8e92e-144">Ponadto usługi obecnie obsługuje rozmiar ograniczoną ilość danych właściwym charakter żądanie/odpowiedź wywołania usługi sieci web i fakt, że modelu jest nadaje się zawsze, gdy zostanie wywołana przez usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e92e-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="8e92e-145">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="8e92e-145">FAQ</span></span>
<span data-ttu-id="8e92e-146">Często zadawane pytania dotyczące wykorzystania usługi sieci web i publikowanie w portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="8e92e-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

