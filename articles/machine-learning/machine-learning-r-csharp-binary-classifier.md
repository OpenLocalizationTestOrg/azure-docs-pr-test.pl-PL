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
# <a name="deprecated-binary-classifier"></a>(przestarzałe) Klasyfikator binarne

> [!NOTE]
> Witaj Microsoft DataMarket została wycofana i ten interfejs API jest przestarzały. 
> 
> Możesz znaleźć wiele interfejsów API i przydatne przykład eksperymenty w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Załóżmy, że masz zestawu danych i chcesz toopredict binarne zależnych od zmiennej opartej na zmienne niezależne hello. "Regresja logistyczna" jest popularnych techniki statystyczne używane dla takich prognoz. W tym miejscu hello zależnych od zmiennej jest binary lub dichotomous, a p jest prawdopodobieństwo hello obecności cechy hello zainteresowań. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Prosty scenariusz może być, gdzie analitykowi próbuje toopredict czy potencjalnego uczniów jest prawdopodobnie tooaccept university tooa oferta wprowadzenia na podstawie informacji (GPA w szkole, dochód rodziny, znajdują się stan, płci). wyniki przewidywane Hello jest prawdopodobieństwo hello hello student potencjalnego akceptowanie hello wprowadzenia oferty. To [usługi sieci web](https://datamarket.azure.com/dataset/aml_labs/log_regression) mieści się hello Regresja logistyczna modelu toohello danych i dane wyjściowe hello wartość prawdopodobieństwa (y) dla każdego z uwagi hello hello danych.  

> Ta usługa sieci web może być używana przez użytkowników — potencjalnie za pomocą aplikacji mobilnej, za pośrednictwem witryny sieci Web lub nawet na komputerze lokalnym, na przykład. Ale hello hello usługi sieci web służy również tooserve, na przykład jak usługi Azure Machine Learning można toocreate używanych usług sieci web na podstawie kodu języka R. Przy użyciu kilku wierszy kodu języka R i kliknięcia przycisku w usłudze Azure Machine Learning Studio eksperyment można tworzyć z kodem R i opublikowane jako usługę sieci web. usługi sieci web Hello można następnie toohello opublikowane w portalu Azure Marketplace i używane przez użytkowników i urządzeń w Witaj świecie bez ustawień infrastruktury przez autora hello hello usługi sieci web.  
> 
> 

## <a name="consumption-of-web-service"></a>Użycie usługi sieci web
Ta hello zapewnia usługi sieci web przewidzieć wartości hello zależnych od zmiennej opartej na zmienne niezależne hello wszystkie hello uwag. Usługa sieci web Hello oczekuje hello użytkownika końcowego tooinput dane jako ciąg, gdzie wiersze są oddzielone przecinkami (,), a kolumny oddzielonych średnikami (;). Usługa sieci web Hello oczekuje 1 wiersz w czasie i oczekuje hello pierwszej kolumny toobe hello zależnych od zmiennej. Przykład zestawu danych może wyglądać następująco:

![Dane przykładowe][1]

Uwagi bez zależnych od zmiennej można wprowadzić jako "Brak" y. Witaj danych wejściowych dla hello powyżej zestawu danych czy powitania po ciągu: "1 5 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, NA; 3; 4". Witaj output hello przewidywane wartości dla poszczególnych wierszy hello opiera się na powitania zmienne niezależne. 

> Ta usługa hostowana na hello Azure Marketplace jest usługi OData; te można wywoływać za pomocą metody POST lub GET. 
> 
> 

Istnieje wiele sposobów używania usługi hello w zautomatyzowany sposób (przykładową aplikację jest [tutaj](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).

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

Za pomocą w usłudze Azure Machine Learning nowy pusty eksperyment została utworzona i dwa [wykonanie skryptu języka R] [ execute-r-script] modułów pobierane na powitania obszaru roboczego. Ta usługa sieci web uruchamia eksperymentu uczenia maszynowego Azure przy użyciu podstawowego skrypt języka R. Istnieją 2 części toothis eksperymentu: definicja schematu i szkolenia modelu + oceniania. Moduł pierwszy Hello definiuje strukturę hello oczekiwano hello wejściowy zestaw danych, gdzie hello pierwszej zmiennej jest hello zależnych od zmiennej, a pozostałe zmienne hello są niezależne. Drugi moduł Hello pasuje do ogólnego Regresja logistyczna model hello danych wejściowych.    

![Przepływ eksperymentu][2]

#### <a name="module-1"></a>Moduł 1:
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a>Moduł 2:
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


## <a name="limitations"></a>Ograniczenia
Jest bardzo prosty przykład usługi sieci web klasyfikacji binarnej. Jak wynika z powyższych hello przykładowy kod, nie błąd Przechwytywanie jest zaimplementowana i usługi hello przyjęto założenie, że wszystko jest zmienną binary/ciągłego (nie podzielone na kategorie funkcji dozwolone), jako hello usługi tylko dane wejściowe wartości liczbowe w czasie hello hello tworzenia tego Usługa sieci Web. Ponadto usługa hello obsługuje obecnie rozmiar ograniczoną ilość danych, powodu toohello charakter żądanie/odpowiedź usługi sieci web hello połączeń i hello fakt, że hello modelu jest nadaje się zawsze nosi nazwę usługi sieci web hello. 

## <a name="faq"></a>Często zadawane pytania
Często zadawane pytania dotyczące wykorzystania hello usługi sieci web lub toohello publikowania portalu Azure Marketplace, zobacz [tutaj](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

