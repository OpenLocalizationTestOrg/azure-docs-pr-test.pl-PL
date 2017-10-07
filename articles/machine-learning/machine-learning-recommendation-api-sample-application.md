---
title: operacje aaaCommon w hello Machine Learning API zalecenia | Dokumentacja firmy Microsoft
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
redirect_document_id: True
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>Przewodnik po przykładowej aplikacji interfejsu API zaleceń
> [!NOTE]
> Należy rozpocząć za pomocą hello usługi kognitywnych zalecenia dotyczące interfejsu API, zamiast tej wersji. Hello kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną wszystkie hello nowe funkcje. Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.
> Dowiedz się więcej o [toohello Migrowanie nową usługę kognitywnych](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>Przeznaczenie
Ten dokument zawiera hello użycie hello Azure Learning zalecenia dotyczące maszyny interfejsu API za pomocą [Przykładowa aplikacja](https://code.msdn.microsoft.com/Recommendations-144df403).

Ta aplikacja nie jest zamierzone tooinclude pełnej funkcjonalności nie używa hello wszystkich interfejsów API. Pokazuje niektóre typowe tooperform operacji, należy najpierw tooplay z hello usługi Machine Learning zalecenia. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a>Wprowadzenie tooMachine Learning zalecenia usługi
Zalecenia za pośrednictwem usługi Machine Learning zalecenie hello są włączone podczas konstruowania modelu zalecenie oparte na powitania następujące dane:

* Repozytorium elementów hello ma toorecommend, znany również jako katalog
* Dane reprezentujące użycia hello elementów na użytkownika lub sesję (to może być uzyskane wraz z upływem czasu za pomocą pozyskiwania danych, nie jako część hello przykładowej aplikacji)

Po utworzeniu modelu zalecenie umożliwia toopredict elementy, które mogą być zainteresowani użytkownika, zgodnie z tooa wybiera użytkownika hello zbiór elementów (lub jeden element).

tooenable hello poprzednim scenariuszu, wykonaj następujące hello w hello usługi Machine Learning zalecenia:

* Tworzenie modelu: jest to logiczne kontener, który zawiera dane hello (katalogu i użycia) i hello modeli prognozowania. Każdy kontener modelu jest identyfikowany za pomocą unikatowego Identyfikatora zaalokowano podczas jego tworzenia. Ten identyfikator jest nazywane hello identyfikator modelu i jest używany przez większość hello interfejsów API. 
* Przekaż toocatalog: po utworzeniu kontenera modelu można skojarzyć tooit wykazu.

**Uwaga**: Tworzenie modelu i przekazać katalogu tooa zazwyczaj są realizowane raz dla hello modelu w cyklu życia.

* Przekaż użycia: spowoduje to dodanie kontenerem modelu toohello danych użycia.
* Tworzenie modelu zalecenie: po wystarczającej ilości danych, można tworzyć hello zalecenie modelu. Ta operacja używa hello top uczenia maszynowego algorytmów toocreate modelu zalecenia. Każdej kompilacji jest skojarzony z unikatowego identyfikatora. Tookeep rekord ten identyfikator jest konieczne, ponieważ jest on wymagany do działania funkcji hello niektórych interfejsów API.
* Proces konstruowania hello monitora: kompilacja modelu zalecenie jest operacja asynchroniczna, i może potrwać od kilku godzin tooseveral minut, w zależności od hello ilości danych (katalog i użycia) i hello parametry kompilacji. W związku z tym należy toomonitor hello kompilacji. Model zalecenie jest tworzony tylko wtedy, gdy jego skojarzony kompilacja zostaje ukończona pomyślnie.
* (Opcjonalnie) Wybierz kompilacji modelu active zalecenie: ten krok tylko jest to konieczne, jeśli masz więcej niż jednego modelu zalecenie wbudowane z kontenerem modelu. Żadnych zaleceń tooget żądania bez wskazujący modelu active zalecenie hello jest automatycznie przekierowane przez kompilację active toohello domyślne hello systemu. 

**Uwaga**: model active zalecenie jest gotowy w środowisku produkcyjnym i jest zbudowany dla obciążeń produkcyjnych. To różni się od modelu zalecenie nieaktywnego pozostaje w środowisku przypominającej testu (nazywane również przemieszczania).

* Uzyskaj zalecenia: po modelu zalecenie, możesz wyzwolić zalecenia dotyczące pojedynczego elementu lub listy elementów, które można wybrać. 

Pobierz zalecenia wywoła zazwyczaj w okresie czasu. W tym okresie czasu można przekierowywać toohello danych użycia systemu zalecenie uczenia maszynowego, który dodaje ten kontener danych toohello określonego modelu. Jeśli masz za mało danych użycia, można utworzyć nowy model zalecenie uwzględniająca hello użycie dodatkowych danych. 

## <a name="prerequisites"></a>Wymagania wstępne
* Visual Studio 2013 lub nowszy
* Dostęp do Internetu 
* Subskrypcja toohello zalecenia dotyczące interfejsu API (https://datamarket.azure.com/dataset/amla/recommendations).

## <a name="azure-machine-learning-sample-app-solution"></a>Azure Machine Learning przykładowe rozwiązanie aplikacji
To rozwiązanie zawiera kod źródłowy hello, przykładowe zastosowanie pliku wykazu i dyrektywy toodownload hello pakiety, które są wymagane dla kompilacji.

## <a name="hello-apis-used"></a>interfejsy API używane Hello
Aplikacja Hello korzysta uczenia maszynowego zalecenie funkcji za pośrednictwem podzbioru dostępnych interfejsach API. Witaj, które przedstawiono w następujących interfejsów API w aplikacji hello:

* Tworzenie modelu: tworzenie toohold kontenerem logicznym modeli danych i zalecenia. Model jest identyfikowane przez nazwę i nie można utworzyć więcej niż jednego modelu z hello tej samej nazwy.
* Przekaż plik katalogu: Użyj tooupload wykazu danych.
* Przekaż plik użycia: Użyj tooupload danych użycia.
* Wyzwalanie kompilacji: Użyj toocreate modelu zalecenia.
* Monitorować wykonywania kompilacji: Użyj toomonitor hello Stan kompilacji modelu zalecenia.
* Wybierz model wbudowanych zalecenie: tooindicate które toouse modelu zalecenie domyślnie używają kontenera modelu. Ten krok jest konieczne tylko wtedy, gdy masz więcej niż jednego modelu zalecenie i chcesz tooactivate nieaktywnego kompilacji jako hello active zalecenie modelu.
* Pobierz zalecenia: Użyj tooretrieve zalecanych elementów według tooa pojedynczy element lub zbiór elementów. 

Pełny opis hello interfejsów API Zobacz hello Microsoft Azure Marketplace w dokumentacji. 

**Uwaga**: model może mieć kilka kompilacji w czasie (nie jednocześnie). Każda Kompilacja została utworzona z hello, tej samej lub zaktualizowane katalogu i dane użycia dodatkowych.

## <a name="common-pitfalls"></a>Typowych problemów
* Należy tooprovide swoją nazwę użytkownika i aplikacji przykładowej hello toorun klucza podstawowego konta Microsoft Azure Marketplace.
* Uruchomione Przykładowa aplikacja hello kolejno zakończy się niepowodzeniem. Przepływ aplikacji Hello obejmuje tworzenie, przekazywanie, tworzenie hello monitora i pobieranie zalecenia ze wstępnie zdefiniowanych modelu; w związku z tym nie będzie na wykonanie kolejnych Jeśli nie zmienisz nazwę modelu hello między wywołań.
* Zalecenia mogą zwracać bez danych. Hello Przykładowa aplikacja korzysta z bardzo mały plik wykazu i użycia. W związku z tym niektóre elementy z katalogu hello nie odniesie zalecanych elementów.

## <a name="disclaimer"></a>Zrzeczenie odpowiedzialności
Witaj przykładowej aplikacji nie jest zamierzone toobe uruchamiane w środowisku produkcyjnym. Hello danych w katalogu hello jest bardzo mała i nie będzie on zawierał modelu zalecenie łatwy do rozpoznania. Witaj, dane są dostarczane jako pokaz. 

