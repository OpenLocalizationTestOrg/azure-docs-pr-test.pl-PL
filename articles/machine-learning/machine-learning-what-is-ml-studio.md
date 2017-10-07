---
title: aaaWhat jest Azure Machine Learning Studio? | Microsoft Docs
description: "Omówienie usługi Azure ML Studio, narzędzia obsługiwanego metodą „przeciągnij i upuść” przeznaczonego do szybkiego budowania modeli z gotowej do użycia biblioteki algorytmów i modułów."
keywords: azure machine learning, azure ml, ml studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a>Co to jest usługa Azure Machine Learning Studio?
Microsoft Azure Machine Learning Studio to narzędzie współpracy, przeciągnij i upuść służy toobuild, testowania i wdrażania rozwiązań analizy predykcyjnej na podstawie danych. Usługa Machine Learning Studio publikuje modele jako usługi sieci Web, które mogą być łatwo używane w niestandardowych aplikacjach albo narzędziach do analiz biznesowych, takich jak program Excel.

Usługa Machine Learning Studio to połączenie analiz danych, analiz predykcyjnych, zasobów w chmurze oraz samych danych.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a>Witaj interaktywny obszar roboczy usługi Machine Learning Studio
toodevelop modelu analizy predykcyjnej zwykle używane są dane z jednego lub więcej źródeł, przekształcania i analizować te dane przy użyciu różnych manipulowania danymi i funkcji statystycznych, a wygenerować zestaw wyników. Tworzenie modelu w ten sposób jest procesem iteracyjnym. Podczas modyfikowania hello różnych funkcji i ich parametry, wyniki stają się zbieżne aż do uzyskania czy masz wyuczonego, skutecznego modelu.

**Azure Machine Learning Studio** zapewnia interaktywny, wizualny obszar roboczy tooeasily tworzenia, testowania i wykonywanie kolejnych iteracji modelu analizy predykcyjnej. Możesz przeciągać i upuszczać ***zestawów danych*** i analiza ***modułów*** na kanwę interaktywne, łącząc je razem tooform ***eksperymentu***, który jest uruchamiany w uczeniu maszynowym Studio. tooiterate projektu modelu, Edytuj hello eksperymentu, Zapisz kopię w razie potrzeby i uruchom go ponownie. Jeśli wszystko jest gotowe, możesz przekształcić Twojej ***eksperyment uczenia*** tooa ***eksperyment predykcyjny***, a następnie opublikować go jako ***usługi sieci web*** tak, aby uzyskiwał modelu inne osoby.

Nie jest wymagane żadne programowanie — wystarczy tylko wizualne łączenie zestawów danych i moduły tooconstruct modelu analizy predykcyjnej.

> [!TIP]
> toodownload i Drukuj diagram, który zawiera omówienie funkcji hello usługi Machine Learning Studio, zobacz [diagram przeglądowy możliwości usługi Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
> 
> 

![Diagram usługi Azure ML Studio: tworzenie eksperymentów, odczytywanie danych z wielu źródeł, zapis ocenianych danych, zapis modeli.][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a>Wprowadzenie do usługi Machine Learning Studio
Po przejściu [Machine Learning Studio](https://studio.azureml.net) Zobacz hello **Home** strony. Z tego miejsca można wyświetlać dokumenty, materiały wideo i seminaria internetowe, a także znajdować wartościowe zasoby.

Witaj w lewym górnym menu ![Menu](media/machine-learning-what-is-ml-studio/menu.png) a zostanie wyświetlonych kilka opcji.

### <a name="cortana-intelligence"></a>Cortana Intelligence
Kliknij przycisk **Cortana Intelligence** i spowoduje przekierowanie strony głównej toohello hello [pakietu Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite). Hello pakietu Cortana Intelligence Suite jest w pełni zarządzana danych big data oraz zaawansowane analytics suite tootransform danych do inteligentnego akcji. Zobacz stronę główną Suite hello pełną dokumentację, łącznie z wątków klienta.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Dostępne są dwie opcje w tym miejscu **Home**, strona hello, którym został uruchomiony, i **Studio**.

Kliknij przycisk **Studio** i spowoduje przekierowanie toohello **Azure Machine Learning Studio**. Najpierw zostanie zapytany toosign za pomocą konta Microsoft lub konta służbowego. Po zalogowaniu zobaczysz hello następujące karty po lewej stronie powitania:

* **PROJECTS** (Projekty) — kolekcje eksperymentów, zestawów danych, notesów i innych zasobów reprezentujących pojedynczy projekt
* **EXPERIMENTS** (Eksperymenty) — eksperymenty, które zostały utworzone i uruchomione lub zapisane jako wersje robocze
* **WEB SERVICES** (Usługi sieci Web) — usługi sieci Web, które zostały wdrożone z eksperymentów
* **NOTEBOOKS** (Notesy) — utworzone notesy Jupyter
* **DATASETS** (Zestawy danych) — zestawy danych, które zostały przekazane do Studia
* **TRAINED MODELS** (Nauczone modele) — modele nauczone w eksperymentach i zapisane w Studio
* **USTAWIENIA** — zbiór ustawień, można użyć tooconfigure zasobów oraz Twojego konta.

### <a name="gallery"></a>Galeria
Kliknij przycisk **galerii** i spowoduje przekierowanie toohello  **[Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)**. Hello Galeria jest miejscem, w którym społeczność programistów i analityków danych udostępniać rozwiązania utworzone przy użyciu składników pakietu Cortana Intelligence Suite hello.

Aby uzyskać więcej informacji na temat hello galerii, zobacz [udziału i odnajdywanie rozwiązań w hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

## <a name="components-of-an-experiment"></a>Składniki eksperymentu
Eksperyment składa się z zestawów danych, które zapewniają modułów tooanalytical danych, które można połączyć ze sobą tooconstruct modelu analizy predykcyjnej. Prawidłowy eksperyment ma następujące cechy:

* Witaj obejmuje co najmniej jeden zestaw danych i jeden moduł
* Zestawy danych mogą być połączone tylko toomodules
* Moduły mogą być zestawami tooeither połączonych danych lub inne moduły
* Wszystkie porty wejściowe modułów muszą mieć określone dane toohello połączenia przepływu
* Konieczne jest ustawienie wszystkich wymaganych parametrów dla każdego modułu

Eksperymenty można tworzyć od podstaw albo przy użyciu przykładowego eksperymentu jako szablonu. Aby uzyskać więcej informacji, zobacz [przykład kopii experiments toocreate nowe uczeniem maszynowym](machine-learning-sample-experiments.md).

Przykład tworzenia prostego eksperymentu zawiera temat [Tworzenie prostego eksperymentu w usłudze Azure Machine Learning Studio](machine-learning-create-experiment.md).

Bardziej szczegółowy przewodnik tworzenia rozwiązania analizy predykcyjnej zawiera temat [Tworzenie rozwiązania predykcyjnego za pomocą usługi Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="datasets"></a>Zestawy danych
Zestaw danych jest danych, który został przekazany tooMachine Learning Studio, dzięki czemu można w hello modelowania procesu. Szereg przykładowych zestawów danych są dołączone do usługi Machine Learning Studio dla tooexperiment z, a dodatkowe zestawy danych w razie potrzeby możesz przekazać. Oto przykładowe zestawy danych dostępne w Studio:

* **MPG data for various automobiles** (Dane MPG dotyczące różnych samochodów) — wartości przebiegu w milach na galon paliwa (MPG) dla samochodów zidentyfikowanych na podstawie liczby cylindrów, mocy itp.
* **Breast cancer data** (Dane dot. raka piersi) — dane z diagnoz raka piersi.
* **Forest fires data** (Dane dot. pożarów lasów) — rozmiary pożarów lasów w północno-wschodniej Portugalii.

Podczas tworzenia eksperymentu można wybierać z hello listę dostępnych zestawów danych czy toohello pozostałych hello kanwy.

Aby uzyskać listę przykładowych zestawów danych w usłudze Machine Learning Studio, zobacz [korzystanie z zestawów danych przykładowych hello w usłudze Azure Machine Learning Studio](machine-learning-use-sample-datasets.md).

### <a name="modules"></a>Moduły
Moduł jest algorytmem, który można wykonać na danych. Machine Learning Studio zawiera szereg modułów od danych wejściowych funkcji tootraining, ocenę i sprawdzania poprawności procesów. Oto przykładowe dołączone moduły:

* [Konwertuj tooARFF] [ convert-to-arff] -Format pliku Konwertuje zestaw danych .NET serializacji tooAttribute relacji (ARFF).
* [Compute Elementary Statistics][elementary-statistics] (Obliczanie statystyk podstawowych) — oblicza podstawowe statystyki, takie jak średnia, odchylenie standardowe itp.
* [Linear Regression][linear-regression] (Regresja liniowa) — tworzy model regresji liniowej online na podstawie spadku gradientu.
* [Score Model][score-model] (Ocena modelu) — ocenia nauczony model klasyfikacji lub regresji.

Podczas tworzenia eksperymentu można wybierać z hello listy modułów, dostępny się, że toohello pozostałych hello kanwy.  

Moduł może zawierać zestaw parametrów, których można używać wewnętrzne algorytmy modułu hello tooconfigure. Po wybraniu modułu na kanwie hello parametry modułu hello są wyświetlane w hello **właściwości** toohello okienko rogu hello kanwy. Można zmodyfikować parametry hello w tym okienku tootune modelu.

Aby uzyskać pomoc w nawigowaniu hello dużej biblioteki algorytmów uczenia maszynowego, zobacz [jak Microsoft Azure Machine Learning algorytmów toochoose](machine-learning-algorithm-choice.md).

## <a name="deploying-a-predictive-analytics-web-service"></a>Wdrażanie usługi sieci Web analizy predykcyjnej
Gdy model analizy predykcyjnej jest gotowy, można go wdrożyć jako usługę sieci Web bezpośrednio z usługi Machine Learning Studio. Dodatkowe szczegóły dotyczące tego procesu zawiera temat [Wdrażanie usługi sieci Web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
