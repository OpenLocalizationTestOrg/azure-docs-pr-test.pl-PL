---
title: "Jak korzystać z usługi sieci Web Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Po wdrożeniu usługi uczenia maszynowego, usługę sieci Web RESTFul, który ma zostać udostępnione mogą być używane jako usługa w czasie rzeczywistym żądanie odpowiedź lub jako usługę wykonywania wsadowego."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: eec9f637b4b2306ab4a888dbd5ef5b9a021bcac5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-consume-an-azure-machine-learning-web-service"></a>Jak korzystać z usługi Azure Machine Learning w sieci Web

Po wdrożenia usługi Azure Machine Learning model predykcyjny jako usługę sieci Web, można użyć interfejsu API REST przesyła dane do pobrania prognoz. Możesz wysłać dane w czasie rzeczywistym lub w trybie wsadowym.

Można znaleźć więcej informacji na temat sposobu tworzenia i wdrażania usługi Machine Learning w sieci Web przy użyciu usługi Machine Learning Studio, w tym miejscu:

* Samouczek dotyczący sposobu tworzenia eksperymentu w usłudze Machine Learning Studio, zobacz [Tworzenie pierwszego eksperymentu](machine-learning-create-experiment.md).
* Aby uzyskać więcej informacji na temat wdrażania usługi sieci Web, zobacz [wdrażania usługi Machine Learning Web](machine-learning-publish-a-machine-learning-web-service.md).
* Aby uzyskać więcej informacji na temat usługi Machine Learning, odwiedź [Centrum dokumentacji uczenia maszynowego](https://azure.microsoft.com/documentation/services/machine-learning/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Omówienie
W usłudze Azure Machine Learning w sieci Web aplikacji zewnętrznej komunikuje się z modelem oceniania uczenia maszynowego przepływu pracy w czasie rzeczywistym. Wywołanie usługi Machine Learning Web zwraca wyniki prognozowania do aplikacji zewnętrznej. Aby wywołać usługi Machine Learning w sieci Web, należy przekazać klucz interfejsu API, który jest tworzony podczas wdrażania prognozowania. Usługa Machine Learning w sieci Web jest oparta na REST, wybór popularnych Architektura programowania projektów sieci Web.

Usługa Azure Machine Learning udostępnia dwa typy usług:

* Odpowiedź na żądania usługi (RR) — krótki czas oczekiwania, wysoce skalowalna usługa, która zapewnia interfejs do modeli bezstanowych, utworzeniu i wdrożeniu z Machine Learning Studio.
* Usługa partia zadań wykonywania (BES) — asynchronicznego usługi tego wyniki w partii rekordów danych.

Aby uzyskać więcej informacji na temat usługi Machine Learning w sieci Web, zobacz [wdrażania usługi Machine Learning Web](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Pobierz klucz autoryzacji usługi Azure Machine Learning
Podczas wdrażania eksperymentu klucze interfejsu API są generowane przez usługę sieci Web. Klucze można pobrać z kilku lokalizacjach.

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a>W portalu usługi sieci Web Microsoft Azure Machine Learning
Zaloguj się do [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net) portalu.

Aby pobrać klucz interfejsu API usługi sieci Web uczenie nowe maszyny:

1. W portalu usługi sieci Web systemu Azure Machine Learning kliknij **usług sieci Web** menu u góry.
2. Kliknij usługę sieci Web, dla których chcesz pobrać klucza.
3. W górnym menu, kliknij przycisk **Consume**.
4. Skopiuj i Zapisz **klucz podstawowy**.

Aby pobrać klucz interfejsu API usługi klasycznego Machine Learning w sieci Web:

1. W portalu usługi sieci Web systemu Azure Machine Learning kliknij **usług sieci Web klasycznego** menu u góry.
2. Kliknij usługę sieci Web, z którym pracujesz.
3. Kliknij punkt końcowy, dla którego chcesz pobrać klucza.
4. W górnym menu, kliknij przycisk **Consume**.
5. Skopiuj i Zapisz **klucz podstawowy**.

### <a name="classic-web-service"></a>Klasycznym usługi sieci Web
 Można również pobierać klucza dla usługi sieci Web klasycznego z usługi Machine Learning Studio lub klasycznego portalu Azure.

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. W usłudze Machine Learning Studio, kliknij przycisk **usług sieci WEB** po lewej stronie.
2. Kliknij usługę sieci Web. **Klucz interfejsu API** znajduje się na **pulpitu NAWIGACYJNEGO** kartę.

#### <a name="azure-classic-portal"></a>klasyczny portal Azure
1. Kliknij przycisk **UCZENIA MASZYNOWEGO** po lewej stronie.
2. Kliknij obszar roboczy, w którym znajduje się usługa sieci Web.
3. Kliknij przycisk **usług sieci WEB**.
4. Kliknij usługę sieci Web.
5. Kliknij punkt końcowy. "Klucz interfejsu API" jest wyłączony w prawej dolnej.

## <a id="connect"></a>Połączyć się z usługą Machine Learning w sieci Web
Można nawiązać połączenia z usługą Machine Learning w sieci Web przy użyciu języka programowania, która obsługuje żądania HTTP i odpowiedzi. Przykłady można wyświetlić w języku C#, Python i R ze strony pomocy usługi Machine Learning w sieci Web.

**Maszyny pomocy Learning API** Machine Learning API pomocy jest tworzona podczas wdrażania usługi sieci Web. Zobacz [uczenie maszynowe Azure wskazówki — wdrażanie usługi sieci Web](machine-learning-walkthrough-5-publish-web-service.md).
Pomoc Machine Learning API zawiera szczegółowe informacje o prognozowania usługi sieci Web.

1. Kliknij usługę sieci Web, z którym pracujesz.
2. Kliknij punkt końcowy, dla którego chcesz wyświetlić strona pomocy interfejsu API.
3. W górnym menu, kliknij przycisk **Consume**.
4. Kliknij przycisk **strona pomocy interfejsu API** w obszarze żądanie-odpowiedź lub wykonywania wsadowego usługi punktów końcowych.

**Do widoku interfejsu API uczenia maszynowego Pomoc dla usługi sieci Web nowy**

W Azure Machine Learning Portal usługi sieci Web:

1. Kliknij przycisk **usług sieci WEB** w górnym menu.
2. Kliknij usługę sieci Web, dla których chcesz pobrać klucza.

Kliknij przycisk **Consume** można pobrać identyfikatorów URI dla żądania Reposonse i usługi wykonywania wsadowego i przykładowy kod w języku C#, R i Python.

Kliknij przycisk **interfejsu API programu Swagger** można pobrać struktury Swagger interfejsy API wywoływanych z podany identyfikator URI na podstawie dokumentacji.

### <a name="c-sample"></a>Przykład C#
Aby połączyć się z usługą Machine Learning w sieci Web, należy użyć **HttpClient** przekazywanie ScoreData. ScoreData zawiera FeatureVector, n wymiarowej wektor liczbowe funkcje reprezentuje ScoreData. Uwierzytelnianie usługi Machine Learning przy użyciu klucza interfejsu API.

Aby połączyć się z usługą Machine Learning w sieci Web, **Microsoft.AspNet.WebApi.Client** musi być zainstalowany pakiet NuGet.

**Instalowania Microsoft.AspNet.WebApi.Client NuGet w programie Visual Studio**

1. Publikowanie pobierania zestawu danych z UCI: 2 dla dorosłych klasy dataset usługi sieci Web.
2. Kliknij pozycję **Narzędzia** > **Menedżer pakietów NuGet** > **Konsola menedżera pakietów**.
3. Wybierz **Microsoft.AspNet.WebApi.Client Install-Package**.

**Aby uruchomić przykładowy kod**

1. Publikowanie "przykład 1: pobrać zestaw danych z UCI: osoba dorosła 2 klasy dataset" eksperymentu, część pobieranie próbek uczenia maszynowego.
2. Przypisz apiKey przy użyciu klucza z usługi sieci Web. Zobacz **Pobierz klucz autoryzacji usługi Azure Machine Learning** powyżej.
3. Przypisz serviceUri o identyfikatorze URI żądania.

### <a name="python-sample"></a>Przykładowe Python
Aby połączyć się z usługą Machine Learning w sieci Web, należy użyć **urllib2** przekazywanie ScoreData biblioteki. ScoreData zawiera FeatureVector, n wymiarowej wektor liczbowe funkcje reprezentuje ScoreData. Uwierzytelnianie usługi Machine Learning przy użyciu klucza interfejsu API.

**Aby uruchomić przykładowy kod**

1. Wdrażanie "przykład 1: pobrać zestaw danych z UCI: osoba dorosła 2 klasy dataset" eksperymentu, część pobieranie próbek uczenia maszynowego.
2. Przypisz apiKey przy użyciu klucza z usługi sieci Web. Zobacz **Pobierz klucz autoryzacji usługi Azure Machine Learning** na początku części tego artykułu.
3. Przypisz serviceUri o identyfikatorze URI żądania.

