---
title: "aaaManage obszaru roboczego usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Obszary robocze uczenia maszynowego tooAzure dostępu, zarządzania i wdrażania i zarządzania nimi usług sieci web interfejsu API uczenia Maszynowego"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a>Zarządzanie obszarem roboczym usługi Azure Machine Learning

> [!NOTE]
> Dla informacji o zarządzaniu usług sieci Web w portalu usługi sieci Web usługi Machine Learning hello, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md).
> 
> 

Możesz zarządzać obszary robocze uczenia maszynowego, albo hello portalu Azure lub hello klasycznego portalu Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a>Użyj hello portalu Azure

toomanage obszaru roboczego w hello portalu Azure:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/) przy użyciu konta administratora subskrypcji platformy Azure.
2. W polu wyszukiwania hello u góry strony hello hello, wprowadź "komputera learning obszary robocze", a następnie wybierz **obszarów roboczych Machine Learning**.
3. Kliknij obszar roboczy hello ma toomanage.

Oprócz informacji zarządzania standardowych zasobów toohello i dostępne opcje, można:

- Widok **właściwości** — ta strona zawiera informacje dotyczące hello obszaru roboczego i zasobów, a można zmienić hello subskrypcji i grupy zasobów, połączony z tym obszarem roboczym.
- **Ponownej synchronizacji magazynu kluczy** -hello obszar roboczy obsługuje konto magazynu toohello kluczy. Jeśli konto magazynu hello zmiany kluczy, a następnie kliknięcie **ponownej synchronizacji kluczy** toosynchronize hello kluczy do obszaru roboczego hello.

portal usługi sieci Web usługi Machine Learning hello jest używany przez usługi sieci web hello toomanage skojarzony z tym obszarem roboczym. Zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md) pełne informacje.

> [!NOTE]
> toodeploy lub zarządzać nowych usług sieci web musi być przypisany współautora lub roli administratora usługi sieci web hello toowhich subskrypcji hello jest wdrażana. Jeśli zaprosić inną maszynę tooa użytkownika obszaru roboczego uczenia, należy je przypisać rolę współautora lub administrator tooa na powitania subskrypcji przed wdrożeniem lub zarządzania usługami sieci web. 
> 
>Aby uzyskać więcej informacji o ustawianiu uprawnień dostępu, zobacz [Wyświetl przypisania dostępu dla użytkowników i grup w portalu Azure - publicznej wersji zapoznawczej hello](../active-directory/role-based-access-control-manage-assignments.md).

## <a name="use-hello-azure-classic-portal"></a>Witaj Użyj klasycznego portalu Azure

Hello klasycznego portalu Azure można zarządzać do uczenia maszynowego obszarów roboczych:

* Monitorowanie, sposobu używania hello obszaru roboczego
* Konfigurowanie hello tooallow obszaru roboczego lub odmowa dostępu
* Zarządzanie usługami sieci Web utworzona w obszarze roboczym hello
* Usuwanie obszaru roboczego hello

Ponadto hello karty Pulpit nawigacyjny zawiera omówienie użycie obszaru roboczego i szybkiego dostępu informacji obszaru roboczego.  

> [!TIP]
> W usłudze Azure Machine Learning Studio na powitania **usług sieci WEB** karcie, można dodać, zaktualizować lub usunąć usługi Machine Learning w sieci Web.
> 
> 

toomanage obszaru roboczego w hello klasycznego portalu Azure:

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) konta przy użyciu platformy Microsoft Azure — należy użyć konta hello, skojarzoną z hello subskrypcji platformy Azure.
2. Witaj Panel usługi Microsoft Azure, kliknij przycisk **UCZENIA MASZYNOWEGO**.
3. Kliknij obszar roboczy hello ma toomanage.

Strona obszaru roboczego Hello zawiera trzy karty:

* **Pulpit NAWIGACYJNY** — pozwala tooview użycia obszaru roboczego i informacji
* **Konfiguruj** — pozwala toomanage dostępu toohello roboczym
* **USŁUGI sieci WEB** — pozwala toomanage usług sieci Web, które zostały opublikowane z tego obszaru roboczego

### <a name="toomonitor-how-hello-workspace-is-being-used"></a>toomonitor sposobu używania hello obszaru roboczego
Kliknij przycisk hello **pulpitu NAWIGACYJNEGO** kartę.

Z poziomu pulpitu nawigacyjnego hello możesz wyświetlić ogólne użycie obszaru roboczego i uzyskać szybkiego dostępu informacji obszaru roboczego.

* Witaj **OBLICZENIOWE** wykres zawiera zasoby obliczeniowe hello używany przez hello obszaru roboczego. Można zmienić toodisplay widoku hello względną lub bezwzględną wartości, a przedział czasu hello wyświetlane na wykresie hello można zmienić.
* **Przegląd wykorzystania** Wyświetla magazynu Azure używany przez hello obszaru roboczego.
* **Szybkiego dostępu** zawiera podsumowanie informacji obszaru roboczego i przydatne łącza.

> [!NOTE]
> Witaj **logowania tooML Studio** łącze powoduje otwarcie przy użyciu hello Account Microsoft użytkownik jest już zarejestrowany w usłudze Machine Learning Studio. Witaj Account Microsoft toosign jest używany w toohello klasycznego portalu Azure toocreate obszaru roboczego nie ma automatycznie tooopen uprawnienia tego obszaru roboczego. tooopen obszaru roboczego, musisz zarejestrować się w toohello Account Microsoft został zdefiniowany jako hello właściciela obszaru roboczego hello, lub należy tooreceive zaproszenia od hello właściciela toojoin hello roboczym.
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a>toogrant lub zawiesić dostęp dla użytkowników
Kliknij przycisk hello **Konfiguruj** kartę.

Karta Konfiguracja hello można:

* Wstrzymaj obszaru roboczego uczenia maszynowego toohello dostępu, klikając przycisk ODMÓW. Użytkownicy będą już mogli tooopen hello roboczym w usłudze Machine Learning Studio. toorestore dostępu, kliknij przycisk Zezwalaj.

toomanage dodatkowych kont mających roboczym toohello dostępu w usłudze Machine Learning Studio, kliknij przycisk **logowania tooML Studio** w hello **pulpitu NAWIGACYJNEGO** kartę (patrz Uwaga poprzedzających hello dotyczące  **Sign-in tooML Studio**). Spowoduje to otwarcie hello obszaru roboczego usługi Machine Learning Studio. W tym miejscu, kliknij przycisk hello **ustawienia** kartę, a następnie **użytkowników**. Możesz kliknąć **ZAPROSIĆ użytkowników więcej** toogive użytkowników dostępu toohello obszaru roboczego, lub wybierz użytkownika i kliknij przycisk **Usuń**.

### <a name="toomanage-web-services-in-this-workspace"></a>usługi sieci web toomanage w tym obszarze roboczym
Kliknij przycisk hello **usług sieci WEB** kartę.

Spowoduje to wyświetlenie listy publikowane z tym obszarem roboczym usługi sieci web.
toomanage usługi sieci web, kliknij nazwę hello tooopen listy hello hello strony usługi sieci Web.

Usługi sieci Web może mieć co najmniej jeden zdefiniowanych punktów końcowych.

* Można zdefiniować więcej punktów końcowych w punkcie końcowym Dodawanie toohello "Default". tooadd hello punktu końcowego, kliknij przycisk **zarządzanie punktami końcowymi** u dołu hello hello pulpitu nawigacyjnego tooopen hello usługi sieci Web systemu Azure Machine Learning portalu.
* toodelete punktu końcowego (nie można usunąć punktu końcowego hello "Default"), kliknij pole wyboru hello na początku hello hello wiersza punktu końcowego, a następnie kliknij przycisk **usunąć**. Spowoduje to usunięcie punktu końcowego hello z hello usługi sieci Web.
  
  > [!NOTE]
  > Jeśli aplikacja używa punkt końcowy usługi sieci web powitania po usunięciu punktu końcowego hello, aplikacji hello zostanie wyświetlony błąd hello następnym próbuje tooaccess hello usługi.
  > 
  > 

Kliknij nazwę hello tooopen punkt końcowy usługi sieci Web go. 

Z poziomu pulpitu nawigacyjnego hello można wyświetlić ogólne użycie usługi sieci Web w danym okresie czasu. Możesz wybrać tooview okresu hello z menu rozwijanego okresu hello w prawym górnym rogu hello hello użycia wykresów. pulpit nawigacyjny Hello zawiera hello następujących informacji:

* **Żądań w czasie** wykres krok hello liczba żądań za pośrednictwem hello w wybranym okresie. Może pomóc ustalić, czy występują wzrostów użycia.
* **Żądanie-odpowiedź żądań** Wyświetla hello łączna liczba wywołań żądań i odpowiedzi usługi hello odebrał za pośrednictwem hello wybrany okres czasu i ile z nich nie powiodło się.
* **Średni czas obliczeniowe żądanie-odpowiedź** wyświetla średni czas hello potrzebne tooexecute hello odebranych żądań.
* **Partie żądania** Wyświetla hello łączna liczba żądań wsadowych hello usługi odebrał w wybranym okresie hello i ile z nich nie powiodło się.
* **Średni czas oczekiwania zadania** wyświetla średni czas hello potrzebne tooexecute hello odebranych żądań.
* **Błędy** Wyświetla hello łączna liczba błędów, które wystąpiły w usłudze sieci web toohello wywołania.
* **Koszty usługi** Wyświetla hello opłat za hello plan rozliczeniowy skojarzonych z usługą hello.

Na stronie Konfiguruj hello można zaktualizować hello następujące właściwości:

* **Opis elementu** pozwala tooenter opis hello usługi sieci Web. Opis jest polem wymaganym.
* **Rejestrowanie** pozwala błąd tooenable lub Wyłącz rejestrowanie hello w punkcie końcowym. Aby uzyskać więcej informacji, zobacz Włącz [rejestrowania dla usług sieci web uczenie maszynowe](machine-learning-web-services-logging.md).
* **Włącz przykładowe dane** pozwala tooprovide przykładowych danych służy tootest hello żądań i odpowiedzi usługi. Jeśli utworzono hello usługi sieci web w usłudze Machine Learning Studio hello przykładowych danych jest pobierana z danych hello sieci używanych tootrain modelu. Jeśli utworzono usługi hello programowo, hello dane są pobierane z hello przykładowe dane podane jako część pakietu hello JSON.

