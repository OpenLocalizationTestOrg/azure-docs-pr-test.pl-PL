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
# <a name="deprecated-multivariate-linear-regression"></a>(przestarzałe) Regresja liniowa wielu zmiennych

> [!NOTE]
> Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Załóżmy, że masz zestawu danych i jak tooquickly czy prognozowania zależnych od zmiennej (y) dla poszczególnych osób (i), w oparciu o zmienne niezależne. Regresja liniowa jest popularnych techniki statystyczne używane dla takich prognoz. W tym miejscu hello zależnych od zmiennej y zakłada, że toobe wartości ciągłej.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Prosty scenariusz może być, gdzie analitykowi hello próbuje wagi hello toopredict osoby (y), w oparciu o ich wysokość (x). Bardziej zaawansowanym scenariuszu można gdzie analitykowi hello zawiera dodatkowe informacje dotyczące poszczególnych (takich jak wagi, płci, wyścigu) hello i próbuje wagi hello toopredict hello osoby. To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) mieści się hello danych toohello modelu regresji liniowej i dane wyjściowe hello przewidywane wartości (y) dla każdego z uwagi hello hello danych.

> Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.  
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
Ta hello zapewnia usługi sieci web przewidzieć wartości hello zależnych od zmiennej opartej na zmienne niezależne hello wszystkie hello uwag. Usługa sieci web Hello oczekuje hello użytkownika końcowego tooinput dane jako ciąg, gdzie wiersze są oddzielone przecinkami (,), a kolumny oddzielonych średnikami (;). Usługa sieci web Hello oczekuje 1 wiersz w czasie i oczekuje hello pierwszej kolumny toobe hello zależnych od zmiennej. Przykład zestawu danych może wyglądać następująco:

![Dane przykładowe][1]

Uwagi bez zależnych od zmiennej można wprowadzić jako "Brak" y. Witaj danych wejściowych dla hello powyżej zestawu danych czy powitania po ciągu: "10 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1 NA; 3 i 4". Witaj output hello przewidywane wartości dla poszczególnych wierszy hello opiera się na powitania zmienne niezależne. 

> Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Rozpoczynanie korzystania z usług sieci web kod C#:
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




## <a name="creation-of-web-service"></a>Tworzenie usługi sieci web
> Ta usługa sieci web został utworzony przy użyciu usługi Azure Machine Learning. Bezpłatna wersja próbna, a także wprowadzające filmy wideo dotyczące tworzenia eksperymenty i [publikowania usług sieci web](machine-learning-publish-a-machine-learning-web-service.md), można znaleźć pod adresem [azure.com/ml](http://azure.com/ml). Poniżej przedstawiono zrzut ekranu hello eksperymentu, utworzona hello kod przykład i usługi sieci web dla każdego z modułów hello w ramach eksperymentu hello.
> 
> 

Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona i dwa [wykonanie skryptu języka R] [ execute-r-script] moduły są pobierane na powitania obszaru roboczego. Ta usługa sieci web uruchamia eksperymentu uczenia maszynowego Azure przy użyciu podstawowego skrypt języka R. Istnieją 2 części toothis eksperymentu: definicja schematu i szkolenia modelu + oceniania. Moduł pierwszy Hello definiuje strukturę hello oczekiwano hello wejściowy zestaw danych, gdzie hello pierwszej zmiennej jest hello zależnych od zmiennej, a pozostałe zmienne hello są niezależne. Drugi moduł Hello pasuje model regresji liniowej ogólnego hello danych wejściowych.  

![Przepływ eksperymentu][3]

#### <a name="module-1"></a>Moduł 1:
#### <a name="schema-definition"></a>Definicja schematu
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a>Moduł 2:
#### <a name="lm-modeling"></a>LM modelowania
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

## <a name="limitations"></a>Ograniczenia
Jest bardzo prosty przykład wielu usług sieci web regresji liniowej. Jak wynika z powyższych hello przykładowy kod, nie błąd Przechwytywanie jest zaimplementowana i usługi hello przyjęto założenie, że wszystko jest ciągłe zmiennej (nie podzielone na kategorie funkcji dozwolone), jako hello usługi tylko dane wejściowe wartości liczbowe w czasie hello hello tworzenia tej sieci Web Usługa. Ponadto usługa hello obsługuje obecnie rozmiar ograniczoną ilość danych, powodu toohello charakter żądanie/odpowiedź usługi sieci web hello połączeń i hello fakt, że hello modelu jest nadaje się zawsze nosi nazwę usługi sieci web hello. 

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

