---
title: aaaWhat jest Machine Learning na platformie Azure? | Microsoft Docs
description: "Wyjaśnia podstawowe pojęcia dotyczące uczenia w chmurze hello maszynowego opisuje go w celu wykorzystania i definiuje terminy dotyczące uczenia maszynowego."
keywords: "co to jest uczenie maszynowe, terminy dotyczące uczenia maszynowego, predykcyjna, co to jest analiza predykcyjna, terminy dotyczące uczenia maszynowego"
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: eaee083e-eaa1-4408-838b-93e51423d159
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: cgronlun
ms.openlocfilehash: 4cd9ad0a0fd9c573e78f28603bb9bf7b361d3faa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomachine-learning-in-hello-azure-cloud"></a>Wprowadzenie tooMachine Learning w hello Azure w chmurze

## <a name="what-is-machine-learning"></a>Co to jest uczenie maszynowe?
Machine learning to technika analizy danych, która umożliwia komputerom toouse istniejących danych tooforecast przyszłych zachowań, rezultatów i trendów. Za pomocą techniki uczenia maszynowego komputery uczą się bez ich jawnego programowania. 

Uczenie maszynowe jest uznawane za podkategorię sztucznej inteligencji. Dzięki prognozom lub przewidywaniom uzyskiwanym za pomocą uczenia maszynowego aplikacje i urządzenia są bardziej inteligentne. Podczas zakupów w Internecie uczenie maszynowe wspomaga proces rekomendowania innych produktów, które mogą się spodobać kupującemu, na podstawie dotychczasowych zakupów. W przypadku płacenia karty kredytowej uczenie maszynowe porównuje bazy danych tooa transakcji hello transakcji, co ułatwia wykrywanie oszustw. Twoje odkurzacz robot vacuums pokoju, uczenie maszynowe wspomaga on zdecydować, czy zadanie hello jest wykonywane.

Krótki przegląd, spróbuj seria filmów hello [nauki danych dla początkujących](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md). Nie używając żargonu ani matematyki, seria Przetwarzanie danych dla początkujących przedstawia uczenie maszynowe i prowadzi Cię krok po kroku przez prosty model predykcyjny.

## <a name="what-is-machine-learning-in-hello-microsoft-azure-cloud"></a>Co to jest Machine Learning w hello chmury Microsoft Azure?

![Co to jest uczenie maszynowe? Podstawowy przepływ pracy toooperationalize predykcyjnej analizy w usłudze Azure Machine Learning.](./media/machine-learning-what-is-machine-learning/machine-learning-service-parts-and-workflow.png)

Azure Machine Learning to usługa analizy predykcyjnej w chmurze, dzięki którym możliwe tooquickly tworzenie i wdrażanie modeli predykcyjnych jako rozwiązań analitycznych.

Można pracować z gotowych do użycia biblioteki algorytmów, użyj ich modeli toocreate komputera podłączonego do Internetu i szybko wdrażać rozwiązania predykcyjne. Rozpocznij od gotowych do użycia przykłady i rozwiązania w hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).

Usługa Azure Machine Learning nie tylko udostępnia narzędzia do analizy predykcyjnej toomodel, ale również zapewnia pełni zarządzaną usługę można użyć toodeploy modeli predykcyjnych jako gotowe do użycia usług sieci web.

## <a name="what-is-predictive-analytics"></a>Co to jest analiza predykcyjna?
Analiza predykcyjna wykorzystuje formuły matematyczne wywołuje algorytmów analizowanie historyczne lub bieżące dane tooidentify trendy i w kolejności tooforecast przyszłych zdarzeń.

## <a name="tools-toobuild-complete-machine-learning-solutions-in-hello-cloud"></a>Narzędzia toobuild pełną rozwiązań do uczenia maszynowego w chmurze hello
Usługa Azure Machine Learning zawiera wszystko, co potrzebne toocreate kompletnych rozwiązań analizy predykcyjnej w chmurze hello, od dużej biblioteki algorytmów, tooa studio przeznaczone do budowania modeli, toodeploy łatwy sposób tooan model jako usługę sieci web. Szybko twórz, testuj i operacjonalizuj modele predykcyjne oraz zarządzaj nimi.

### <a name="machine-learning-studio-create-predictive-models"></a>Usługa Machine Learning Studio: tworzenie modeli predykcyjnych
W usłudze [Machine Learning Studio](machine-learning-what-is-ml-studio.md) możesz szybko tworzyć modele predykcyjne, przeciągając, upuszczając i łącząc moduły. Możesz eksperymentować z różnymi kombinacjami, a [próby nic nie kosztują](https://studio.azureml.net/?selectAccess=true&o=2).

* W witrynie [Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md) możesz wypróbować rozwiązania analityczne stworzone przez innych użytkowników lub dodać swoje własne. Publikuj pytania lub komentarze dotyczące eksperymentów Wspólnoty toohello lub udostępnić tooexperiments łącza w sieciach społecznościowych, takich jak LinkedIn i Twitter.

  ![Wypróbuj eksperymenty predykcyjne lub publikuj swoje w witrynie Azure Cortana Intelligence Gallery](./media/machine-learning-what-is-machine-learning/machine-learning-cortana-intelligence-gallery.png)
* Skorzystaj z obszernej biblioteki z [algorytmów uczenia maszynowego i modułów](https://msdn.microsoft.com/library/azure/f5c746fd-dcea-4929-ba50-2a79c4c067d7) w usłudze Machine Learning Studio toojump-start modeli predykcyjnych. Wybieraj rozwiązania spośród przykładowych eksperymentów, pakietów dla języków R i Python oraz najlepszych w swojej klasie algorytmów z produktów Microsoft, takich jak Xbox i Bing. Rozszerzaj moduły Studia o własne skrypty w językach [R](machine-learning-extend-your-experiment-with-r.md) i [Python](machine-learning-execute-python-scripts.md).

  ![Co to jest analiza predykcyjna: przykład eksperymentu analizy predykcyjnej w usłudze Azure Machine Learning Studio](./media/machine-learning-what-is-machine-learning/azure-machine-learning-studio-predictive-score-experiment.png)

### <a name="operationalize-predictive-analytics-solutions-by-publishing-your-own"></a>Operacjonalizowanie rozwiązań analizy predykcyjnej, publikując własne
Witaj następujące samouczki wyjaśniają, jak toooperationalize modelami analizy predykcyjnej:

 * [Wdrażaj usługi sieci Web](machine-learning-publish-a-machine-learning-web-service.md)
 * [Ponownie ucz modele za pośrednictwem interfejsów API](machine-learning-retrain-models-programmatically.md)
 * [Zarządzaj punktami końcowymi usług sieci Web](machine-learning-create-endpoint.md)
 * [Skaluj usługę sieci Web](machine-learning-scaling-webservice.md)
 * [Korzystaj z usług sieci Web](machine-learning-consume-web-services.md)

## <a name="key-machine-learning-terms-and-concepts"></a>Kluczowe terminy i pojęcia dotyczące uczenia maszynowego
Terminy dotyczące uczenia maszynowego mogą być mylące. Poniżej znajdują się definicje toohelp kluczowe terminy użytkownik. Komentarze służą następujące tootell nas o inny termin, który ma zdefiniowane.

### <a name="data-exploration-descriptive-analytics-and-predictive-analytics"></a>Eksploracja danych, analiza opisowa i analiza predykcyjna

**Eksploracja danych** hello proces zbierania informacji o dużych i często nieustrukturyzowanych zestawach danych w kolejności właściwości toofind potrzeby ukierunkowanej analizy.

**Wyszukiwanie danych** odwołuje się tooautomated Eksploracja danych.

**Analiza opisowa** jest hello proces analizowania zestawu danych w kolejności toosummarize, co się stało. Większość Hello analizy biznesowe — takie jak raporty ze sprzedaży, metryki sieci web i analizy sieci społecznościowych — są opisowy.

**Analizy predykcyjnej** hello proces tworzenia modeli z danych historycznych lub bieżących w kolejności tooforecast przyszłych rezultatów.

### <a name="supervised-and-unsupervised-learning"></a>Uczenie nadzorowane i nienadzorowane
 **Uczenia nadzorowanego** algorytmy są uczone z użyciem danych oznaczonych — innymi słowy, danych złożonych z przykładów żądanych odpowiedzi hello. Na przykład model, który identyfikuje użycie karty kredytowej w celu oszustwa, może być uczony z użyciem zestawu danych zawierającego oznaczone etykietą punkty danych dotyczące znanych oszustw i poprawnego użycia karty. Większość uczenia maszynowego jest nadzorowana.

 **Uczenie nienadzorowane** jest używany w przypadku danych bez oznaczeń, a celem hello jest toofind relacji w danych hello. Na przykład można toofind grup demograficznych klientów o podobnych nawykach zakupowych.

### <a name="model-training-and-evaluation"></a>Uczenie i ewaluacja modelu
Model uczenia maszynowego to Abstrakcja pytania hello próbujesz tooanswer lub hello wynik ma toopredict. Modele są uczone i ewaluowane na podstawie istniejących danych.

#### <a name="training-data"></a>Dane szkoleniowe
Podczas uczenia modelu danych, możesz użyć znanego zestawu danych i dostosowania toohello model oparty na powitania danych właściwości tooget hello najdokładniejszych odpowiedzi. W usłudze Azure Machine Learning model jest budowany na podstawie modułu algorytmu, który przetwarza dane szkoleniowe i moduły funkcjonalne, takie jak moduł oceny.

Jeśli model wykrywania oszustw jest uczony w trybie uczenia nadzorowanego, użyj zestawu transakcji, które są oznaczone jako oszustwa lub prawidłowe transakcje. Podzielić losowo, zestaw danych i użyj modelu hello tootrain części i tootest części lub ocena hello modelu.

#### <a name="evaluation-data"></a>Dane do ewaluacji
Po uzyskaniu nauczonego modelu należy obliczyć hello modelu przy użyciu hello pozostałe dane testowe. Używasz danych, które znasz już wyniki hello, dzięki czemu można stwierdzić, czy model przewiduje dokładnie.

## <a name="other-common-machine-learning-terms"></a>Inne typowe terminy dotyczące uczenia maszynowego
* **Algorytm**: autonomiczny zestaw reguł używany toosolve problemów poprzez przetwarzania danych, matematyczne lub rozsądkiem automatycznych.
* **wykrywanie anomalii**: model, który oznacza flagami nietypowe zdarzenia lub wartości, ułatwiając znalezienie problemów. Na przykład wykrywanie oszustw dotyczących karty kredytowej polega na wyszukiwaniu nietypowych zakupów.
* **dane podzielone na kategorie**: dane uporządkowane według kategorii, które mogą zostać podzielone na grupy. Na przykład zestaw danych podzielonych na kategorie dotyczący samochodów może określać rok produkcji, markę, model i cenę.
* **klasyfikacja**: model organizacji punktów danych w kategorie na podstawie zestawu danych, dla którego grupy kategorii są już znane.
* **Inżynieria**: hello proces wyodrębniania lub wybierania cech związanych danych tooa w kolejności tooenhance hello zestawu danych i poprawienia wyników. Na przykład dane dotyczące opłat lotniczych można wzbogacić o dni tygodnia hello i dni wolnych. Zobacz [Feature selection and engineering in Azure Machine Learning](machine-learning-feature-selection-and-engineering.md) (Wybór i inżynieria cech w usłudze Azure Machine Learning).
* **Moduł**: element funkcjonalny w modelu usługi Machine Learning Studio, takich jak moduł danych wprowadź hello, który umożliwia wprowadzanie i edycję niewielkich zestawów danych. Algorytm również jest typem modułu w usłudze Machine Learning Studio.
* **model**: uczenia nadzorowanego model jest iloczyn hello obejmuje dane szkoleniowe, moduł algorytmu i moduły funkcjonalne, takich jak moduł Score Model eksperymentu uczenia maszynowego.
* **dane liczbowe**: dane, które mają znaczenie jako pomiary (dane ciągłe) lub liczniki (dane dyskretne). Nazywana także tooas *danymi ilościowymi*.
* **partycja**: hello — metoda, za pomocą którego dzielenia danych na próbki. Aby uzyskać więcej informacji, zobacz [Partition and Sample](https://msdn.microsoft.com/library/azure/dn905960.aspx) (Partycja i próbka).
* **przewidywanie**: prognoza wartości z modelu uczenia maszynowego. Może być również wyświetlany hello termin "wynik przewidywany." Jednak wyniki przewidywane nie są hello ostatecznymi danymi wynikowymi modelu. Ocena modelu hello następuje hello wynik.
* **Regresja**: model do przewidywania wartości w oparciu o zmienne niezależne, na przykład przewidywanie ceny samochodu hello oparte na jego marki i roku produkcji.
* **wynik**: wartość przewidziana wygenerowana z nauczony model klasyfikacji lub regresji, przy użyciu hello [modułu Score Model](https://msdn.microsoft.com/library/azure/dn905995.aspx) w usłudze Machine Learning Studio. Modele klasyfikacji zwracają również wynik dla hello prawdopodobieństwo hello przewidzieć wartość. Po wygenerowaniu wyniku z modelu można ocenić dokładność hello modelu przy użyciu hello [modułu Evaluate Model](https://msdn.microsoft.com/library/azure/dn905915.aspx).
* **Przykładowe**: część zestawu danych przeznaczone toobe przedstawiciel hello całego. Przykłady można wybierane losowo lub na podstawie konkretnych cech zestawu danych hello.

## <a name="next-steps"></a>Następne kroki
Można dowiedzieć się hello podstaw analizy predykcyjnej i uczenia przy użyciu maszynowego [samouczek krok po kroku](machine-learning-create-experiment.md) oraz [rozwijając przykłady](machine-learning-sample-experiments.md).  

<!-- Module References -->
[learning-with-counts]: https://msdn.microsoft.com/library/azure/81c457af-f5c0-4b2d-922c-fdef2274413c/
