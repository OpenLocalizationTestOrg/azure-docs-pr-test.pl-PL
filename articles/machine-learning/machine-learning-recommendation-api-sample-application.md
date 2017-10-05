---
title: Typowe operacje w Machine Learning zalecenia API | Dokumentacja firmy Microsoft
description: "Azure ML zalecenie przykładowej aplikacji"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 8d8efa93e820f4a745ed93c0f4d13b2438dfa1eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>Przewodnik po przykładowej aplikacji interfejsu API zaleceń
> [!NOTE]
> Należy rozpocząć korzystanie z usługi kognitywnych interfejsu API zalecenia zamiast tej wersji. Kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną nowe funkcje. Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.
> Dowiedz się więcej o [migracji do nowej usługi kognitywnych](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>Przeznaczenie
Ten dokument zawiera użycia usługi Azure Machine Learning zalecenia API za pomocą [Przykładowa aplikacja](https://code.msdn.microsoft.com/Recommendations-144df403).

Ta aplikacja nie jest przeznaczona do obejmują pełnej funkcjonalności ani jest korzystanie z interfejsów API. Jednak przedstawia niektórych typowych operacji do wykonania, jeśli chcesz najpierw odtworzyć w usłudze Machine Learning zalecenie. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-to-machine-learning-recommendation-service"></a>Wprowadzenie do usługi Machine Learning zalecenia
Zalecenia za pomocą usługi Machine Learning zalecenia są włączone podczas konstruowania modelu zalecenia na podstawie następujących danych:

* Repozytorium elementów chcesz zaleca znanej także jako katalog
* Dane reprezentujące użycie elementów na użytkownika lub sesję (to może być uzyskane wraz z upływem czasu za pomocą pozyskiwania danych, nie jako część przykładowej aplikacji)

Po utworzeniu modelu zalecenie można go do prognozowania elementy, które użytkownik może być zainteresowani, na podstawie zestawu elementów (lub jeden element) użytkownik wybiera.

Aby włączyć w poprzednim scenariuszu, wykonaj następujące czynności w usłudze Machine Learning zalecenia:

* Tworzenie modelu: jest to logiczne kontener, który zawiera dane (katalogu i użycia) i modele prognozowania. Każdy kontener modelu jest identyfikowany za pomocą unikatowego Identyfikatora zaalokowano podczas jego tworzenia. Ten identyfikator jest nazywane identyfikator modelu i jest używany przez większość interfejsów API. 
* Przekazywanie do katalogu: po utworzeniu kontenera modelu można skojarzyć do niego wykaz.

**Uwaga**: Tworzenie modelu i przekazać do wykazu zazwyczaj są realizowane raz dla cyklu życia modelu.

* Przekaż użycia: dane użycia to dodaje do kontenera modelu.
* Tworzenie modelu zalecenie: po wystarczającej ilości danych, można utworzyć modelu zalecenia. Tej operacji używa top algorytmów uczenia maszynowego w celu utworzenia modelu zalecenie. Każdej kompilacji jest skojarzony z unikatowego identyfikatora. Należy zachować rekord ten identyfikator, ponieważ jest on wymagany dla funkcji niektórych interfejsów API.
* Monitorowanie procesu tworzenia: kompilacja modelu zalecenie jest operacja asynchroniczna, i może potrwać od kilku minut do kilku godzin, zależnie od ilości danych (katalog i użycia) i parametry kompilacji. W związku z tym należy monitorować kompilacji. Model zalecenie jest tworzony tylko wtedy, gdy jego skojarzony kompilacja zostaje ukończona pomyślnie.
* (Opcjonalnie) Wybierz kompilacji modelu active zalecenie: ten krok tylko jest to konieczne, jeśli masz więcej niż jednego modelu zalecenie wbudowane z kontenerem modelu. Wszelkie uzyskać zalecenia bez wskazujący modelu active zalecenie kierowane jest żądanie automatycznie przez system kompilacji active domyślne. 

**Uwaga**: model active zalecenie jest gotowy w środowisku produkcyjnym i jest zbudowany dla obciążeń produkcyjnych. To różni się od modelu zalecenie nieaktywnego pozostaje w środowisku przypominającej testu (nazywane również przemieszczania).

* Uzyskaj zalecenia: po modelu zalecenie, możesz wyzwolić zalecenia dotyczące pojedynczego elementu lub listy elementów, które można wybrać. 

Pobierz zalecenia wywoła zazwyczaj w okresie czasu. W tym okresie czasu można przekierować danych użycia do systemu zalecenie uczenia maszynowego, który dodaje te dane do kontenera określonego modelu. Jeśli masz za mało danych użycia, można utworzyć nowego modelu zalecenie, który zawiera dane dodatkowe obciążenie. 

## <a name="prerequisites"></a>Wymagania wstępne
* Visual Studio 2013 lub nowszy
* Dostęp do Internetu 
* Subskrypcja zalecenia dotyczące interfejsu API (https://datamarket.azure.com/dataset/amla/recommendations).

## <a name="azure-machine-learning-sample-app-solution"></a>Azure Machine Learning przykładowe rozwiązanie aplikacji
To rozwiązanie zawiera kod źródłowy, przykładowe zastosowanie, plik wykazu i dyrektywy, aby pobrać pakiety, które są wymagane do kompilacji.

## <a name="the-apis-used"></a>Interfejsy API używane
Aplikacja używa funkcji zalecenie uczenia maszynowego za pośrednictwem podzbioru dostępnych interfejsach API. Przedstawiono w następujących interfejsów API w aplikacji:

* Tworzenie modelu: utworzyć kontener do przechowywania danych i zaleceń modelami logiczny. Model jest identyfikowane przez nazwę, a nie można utworzyć więcej niż jeden model o tej samej nazwie.
* Przekaż plik katalogu: Użyj, aby przekazać dane wykazu.
* Przekaż plik użycia: umożliwia przekazywanie danych użycia.
* Wyzwalanie kompilacji: do utworzenia modelu zalecenia.
* Monitorować wykonywania kompilacji: służy do monitorowania stanu kompilacji modelu zalecenia.
* Wybierz model wbudowanych zalecenie: służy do wskazywania model zalecenie, który ma być używany domyślnie dla kontenera modelu. Ten krok jest konieczne tylko wtedy, gdy masz więcej niż jednego modelu zalecenia i chcesz aktywować usługę kompilacji nieaktywnego jako model active zalecenia.
* Pobierz zalecenia: służy do pobierania elementów zalecane zgodnie z danym pojedynczy element lub zbiór elementów. 

Pełny opis interfejsów API zapoznaj się z dokumentacją systemu Microsoft Azure Marketplace. 

**Uwaga**: model może mieć kilka kompilacji w czasie (nie jednocześnie). Każda Kompilacja została utworzona z takie same lub zaktualizowane katalogu i dane użycia dodatkowych.

## <a name="common-pitfalls"></a>Typowych problemów
* Należy podać nazwę użytkownika i klucz podstawowy konta Microsoft Azure Marketplace do uruchomienia aplikacji przykładowej.
* Uruchamianie przykładowej aplikacji po kolei zakończy się niepowodzeniem. Przepływ aplikacji obejmuje tworzenie, przekazywanie, tworzenie monitora i pobieranie zalecenia ze wstępnie zdefiniowanych modelu; w związku z tym nie będzie na wykonanie kolejnych Jeśli nie zmienisz nazwę modelu między wywołań.
* Zalecenia mogą zwracać bez danych. Przykładowa aplikacja korzysta z bardzo mały plik wykazu i użycia. W związku z tym niektóre elementy z katalogu nie odniesie zalecanych elementów.

## <a name="disclaimer"></a>Zrzeczenie odpowiedzialności
Przykładowa aplikacja nie jest przeznaczona do uruchamiania w środowisku produkcyjnym. Dane dostarczone w katalogu jest bardzo mała i nie będzie on zawierał modelu zalecenie łatwy do rozpoznania. Dane są dostarczane jako pokaz. 

