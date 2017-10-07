---
title: "portal usługi sieci Web systemu Azure Machine Learning hello aaaUse | Dokumentacja firmy Microsoft"
description: "Obszary robocze uczenia maszynowego tooAzure dostępu, zarządzania i wdrażania i zarządzania nimi usług sieci web interfejsu API uczenia Maszynowego"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a>Zarządzanie usługą sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello
Można zarządzać za pomocą portalu usługi sieci Web Microsoft Azure Machine Learning hello usługi Machine Learning nowy i klasycznych sieci Web. Ponieważ usługi nowej sieci Web i usług sieci Web klasycznego są oparte na różnych technologii podstawowej, masz możliwości zarządzania nieco inne dla każdego z nich.

W portalu usługi sieci Web usługi Machine Learning hello można:

* Monitorowanie, jak usługa sieci web hello jest używany.
* Skonfiguruj opis hello, aktualizacja hello kluczy hello sieci web usługi (tylko nowy), aktualizacja Twojego magazynu konta klucza (tylko nowy), Włącz rejestrowanie i włączyć lub wyłączyć przykładowych danych.
* Usunąć hello usługi sieci web.
* Tworzenie, delete lub update rozliczeń planów (tylko nowy).
* Dodawanie i usuwanie punktów końcowych (tylko klasyczne)

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a>Usługi sieci web na podstawie uprawnień toomanage nowego Menedżera zasobów

Nowe usługi sieci web są wdrażane jako zasobów platformy Azure. Tak musisz mieć hello toodeploy odpowiednie uprawnienia i zarządzanie nowych usług sieci web.  toodeploy lub zarządzać nowych usług sieci web musi być przypisany współautora lub roli administratora usługi sieci web hello toowhich subskrypcji hello jest wdrażana. Jeśli zaprosić inną maszynę tooa użytkownika obszaru roboczego uczenia, należy je przypisać rolę współautora lub administrator tooa na powitania subskrypcji przed wdrożeniem lub zarządzania usługami sieci web. 

Jeśli użytkownik hello nie ma hello Popraw uprawnienia tooaccess zasobów w portalu usługi sieci Web systemu Azure Machine Learning hello, otrzymają hello następujący błąd podczas próby toodeploy usługi sieci web:

*Wdrażanie usługi sieci Web nie powiodło się. To konto nie ma wystarczających toohello dostępu subskrypcji Azure, która zawiera hello obszaru roboczego. W kolejności toodeploy tooAzure usługi sieci Web, powitalne muszą być tego samego konta zaproszenie toohello obszaru roboczego i być toohello dostępu do danej subskrypcji Azure zawiera hello obszaru roboczego.*

Aby uzyskać więcej informacji na temat tworzenia obszaru roboczego, zobacz [tworzenie i udostępnianie obszaru roboczego uczenia maszynowego Azure](machine-learning-create-workspace.md).

Aby uzyskać więcej informacji o ustawianiu uprawnień dostępu, zobacz [Wyświetl przypisania dostępu dla użytkowników i grup w portalu Azure - publicznej wersji zapoznawczej hello](../active-directory/role-based-access-control-manage-assignments.md).


## <a name="manage-new-web-services"></a>Zarządzanie usługami nowej sieci Web
toomanage usług nowej sieci Web:

1. Zaloguj się toohello [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portalu za pomocą konta Microsoft Azure — Użyj hello konta, z którym skojarzony jest hello subskrypcji platformy Azure.
2. Polecenie hello menu **usług sieci Web**.

Spowoduje to wyświetlenie listy wdrożonych usług sieci Web dla Twojej subskrypcji. 

toomanage usługi sieci Web, kliknij opcję usługi sieci Web. Strony usługi sieci Web hello można:

* Kliknij przycisk toomanage usługi sieci web hello go.
* Kliknij przycisk hello rozliczeń planowanie dla tooupdate usługi sieci web hello go.
* Usuwanie usługi sieci web.
* Skopiuj usługi sieci web i wdróż je tooanother regionu.

Po kliknięciu usługi sieci web otwiera stronę Szybki Start usługi sieci web hello. Strona Szybki Start usługi sieci web Hello ma dwie opcje menu, które pozwalają toomanage usługi sieci web:

* **Pulpit NAWIGACYJNY** — umożliwia użycie usługi sieci Web tooview.
* **Konfiguruj** — umożliwia tooadd tekst opisowy, klucz hello aktualizacji hello konta magazynu skojarzone z hello usługi sieci Web i włączyć lub wyłączyć przykładowych danych.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Monitorowanie, jak usługa sieci web hello jest używany
Kliknij przycisk hello **pulpitu NAWIGACYJNEGO** kartę.

Z poziomu pulpitu nawigacyjnego hello można wyświetlić ogólne użycie usługi sieci Web w danym okresie czasu. Możesz wybrać tooview okresu hello z menu rozwijanego okresu hello w prawym górnym rogu hello hello użycia wykresów. pulpit nawigacyjny Hello zawiera hello następujących informacji:

* **Żądań w czasie** wykres krok hello liczba żądań za pośrednictwem hello w wybranym okresie. Może pomóc ustalić, czy występują wzrostów użycia.
* **Żądanie-odpowiedź żądań** Wyświetla hello łączna liczba wywołań żądań i odpowiedzi usługi hello odebrał za pośrednictwem hello wybrany okres czasu i ile z nich nie powiodło się.
* **Średni czas obliczeniowe żądanie-odpowiedź** wyświetla średni czas hello potrzebne tooexecute hello odebranych żądań.
* **Partie żądania** Wyświetla hello łączna liczba żądań wsadowych hello usługi odebrał w wybranym okresie hello i ile z nich nie powiodło się.
* **Średni czas oczekiwania zadania** wyświetla średni czas hello potrzebne tooexecute hello odebranych żądań.
* **Błędy** Wyświetla hello łączna liczba błędów, które wystąpiły w usłudze sieci web toohello wywołania.
* **Koszty usługi** Wyświetla hello opłat za hello plan rozliczeniowy skojarzonych z usługą hello.

### <a name="configuring-hello-web-service"></a>Konfigurowanie usługi sieci web hello
Kliknij przycisk hello **Konfiguruj** opcji menu.

Można aktualizować hello następujące właściwości:

* **Opis elementu** pozwala tooenter opis hello usługi sieci Web.
* **Tytuł** pozwala tooenter tytuł hello usługi sieci Web
* **Klucze** pozwala toorotate klucze interfejsu API podstawowe i pomocnicze.
* **Klucz konta magazynu** pozwala tooupdate hello klucza dla konta magazynu hello skojarzone z hello zmiany w usługi sieci Web. 
* **Włącz przykładowe dane** pozwala tooprovide przykładowych danych służy tootest hello żądań i odpowiedzi usługi. Jeśli utworzono hello usługi sieci web w usłudze Machine Learning Studio hello przykładowych danych jest pobierana z danych hello sieci używanych tootrain modelu. Jeśli utworzono usługi hello programowo, hello dane są pobierane z hello przykładowe dane podane jako część pakietu hello JSON.

### <a name="managing-billing-plans"></a>Zarządzanie planami rozliczeń
Kliknij przycisk hello **plany** opcji menu ze strony Szybki Start usługi sieci web hello. Możesz również kliknąć hello planu powiązanego z określonych toomanage usługi sieci Web, która.

* **Nowe** pozwala toocreate nowy plan.
* **Dodaj lub usuń Plan wystąpienia** pozwala zbyt "skalowanie" istniejące pojemności tooadd planu.
* **Uaktualnianie i obniżanie wersji** pozwala zbyt "skalowanie w górę" istniejące pojemności tooadd planu.
* **Usuń** pozwala toodelete planu.

Kliknij przycisk tooview planu jego pulpitu nawigacyjnego. pulpit nawigacyjny Hello umożliwia użycie migawki lub plan przez wybrany czas. tooselect hello tooview okres czasu, kliknij przycisk hello **okres** listy rozwijanej w prawym górnym rogu hello pulpitu nawigacyjnego. 

pulpit nawigacyjny planu Hello zapewnia hello następujących informacji:

* **Opis planu** zawiera informacje o hello kosztów i wydajności związanych z programem hello.
* **Planowanie użycia** Wyświetla hello liczbę transakcji i godziny obliczeniowe, które została obciążona przed hello planu.
* **Usługi sieci Web** Wyświetla hello liczbę usług sieci Web, które korzystają z tego planu.
* **Wywołania przez usługi sieci Web z góry** Wyświetla usług sieci Web pierwszych czterech hello wykonywania wywołań, które są powiązane z hello planu.
* **Usługi sieci Web z góry za obliczeniowe godz** Wyświetla usług sieci Web pierwszych czterech hello są używane zasoby obliczeniowe, które są powiązane z planu hello.

## <a name="manage-classic-web-services"></a>Zarządzanie usługami sieci Web klasycznego
> [!NOTE]
> Hello procedury w tej sekcji są toomanaging odpowiednich usług sieci web klasycznego portalu usługi sieci Web systemu Azure Machine Learning hello. Informacje na temat zarządzania klasycznych sieci Web usług za pośrednictwem hello Machine Learning Studio i hello Azure klasycznym portalu, zobacz [Zarządzanie obszarem roboczym usługi Azure Machine Learning](machine-learning-manage-workspace.md).
> 
> 

toomanage usług sieci Web klasycznego:

1. Zaloguj się toohello [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portalu za pomocą konta Microsoft Azure — Użyj hello konta, z którym skojarzony jest hello subskrypcji platformy Azure.
2. Polecenie hello menu **klasycznym usługi sieci Web**.

toomanage klasycznym usługi sieci Web, kliknij przycisk **klasycznym usługi sieci Web**. Strony usługi sieci Web klasycznego hello można:

* Kliknij przycisk punkty końcowe skojarzone hello tooview hello sieci web usługi.
* Usuwanie usługi sieci web.

Jeśli zarządzasz usługi sieci Web klasycznego zarządzasz każdego z punktów końcowych hello oddzielnie. Po kliknięciu usługi sieci web na stronie sieci Web usług hello otwiera hello listę punktów końcowych skojarzonych z usługą hello. 

Na stronie punkt końcowy usługi sieci Web klasycznego hello można dodawać i usuwać punktów końcowych w usłudze hello. Aby uzyskać więcej informacji dotyczących dodawania punktów końcowych, zobacz [tworzenie punktów końcowych](machine-learning-create-endpoint.md).

Kliknij jeden z tooopen punkty końcowe hello hello strony Szybki Start usługi sieci web. Na stronie szybkiego startu hello istnieją dwie opcje menu, które pozwalają toomanage usługi sieci web:

* **Pulpit NAWIGACYJNY** — umożliwia użycie usługi sieci Web tooview.
* **Konfiguruj** — pozwala tooadd tekst opisowy, Włącz błąd Logowanie i wylogowywanie klucz hello aktualizacji, hello konta magazynu skojarzone z hello usługi sieci Web i włączanie i wyłączanie przykładowych danych.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Monitorowanie, jak usługa sieci web hello jest używany
Kliknij przycisk hello **pulpitu NAWIGACYJNEGO** kartę.

Z poziomu pulpitu nawigacyjnego hello można wyświetlić ogólne użycie usługi sieci Web w danym okresie czasu. Możesz wybrać tooview okresu hello z menu rozwijanego okresu hello w prawym górnym rogu hello hello użycia wykresów. pulpit nawigacyjny Hello zawiera hello następujących informacji:

* **Żądań w czasie** wykres krok hello liczba żądań za pośrednictwem hello w wybranym okresie. Może pomóc ustalić, czy występują wzrostów użycia.
* **Żądanie-odpowiedź żądań** Wyświetla hello łączna liczba wywołań żądań i odpowiedzi usługi hello odebrał za pośrednictwem hello wybrany okres czasu i ile z nich nie powiodło się.
* **Średni czas obliczeniowe żądanie-odpowiedź** wyświetla średni czas hello potrzebne tooexecute hello odebranych żądań.
* **Partie żądania** Wyświetla hello łączna liczba żądań wsadowych hello usługi odebrał w wybranym okresie hello i ile z nich nie powiodło się.
* **Średni czas oczekiwania zadania** wyświetla średni czas hello potrzebne tooexecute hello odebranych żądań.
* **Błędy** Wyświetla hello łączna liczba błędów, które wystąpiły w usłudze sieci web toohello wywołania.
* **Koszty usługi** Wyświetla hello opłat za hello plan rozliczeniowy skojarzonych z usługą hello.

### <a name="configuring-hello-web-service"></a>Konfigurowanie usługi sieci web hello
Kliknij przycisk hello **Konfiguruj** opcji menu.

Można aktualizować hello następujące właściwości:

* **Opis elementu** pozwala tooenter opis hello usługi sieci Web. Opis jest polem wymaganym.
* **Rejestrowanie** pozwala błąd tooenable lub Wyłącz rejestrowanie hello w punkcie końcowym. Aby uzyskać więcej informacji, zobacz Włącz [rejestrowania dla usług sieci web uczenie maszynowe](machine-learning-web-services-logging.md).
* **Włącz przykładowe dane** pozwala tooprovide przykładowych danych służy tootest hello żądań i odpowiedzi usługi. Jeśli utworzono hello usługi sieci web w usłudze Machine Learning Studio hello przykładowych danych jest pobierana z danych hello sieci używanych tootrain modelu. Jeśli utworzono usługi hello programowo, hello dane są pobierane z hello przykładowe dane podane jako część pakietu hello JSON.

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a>Udziel lub zawiesić dostęp tooWeb usługi dla użytkowników w portalu hello
Przy użyciu hello klasycznego portalu Azure, można akceptować lub odrzucać dostępu toospecific użytkowników.

### <a name="access-for-users-of-new-web-services"></a>Dostęp dla użytkowników usługi nowej sieci Web
tooenable innych toowork użytkowników z usług sieci Web w portalu usługi sieci Web systemu Azure Machine Learning hello, należy dodać je jako co Administratorzy w Twojej subskrypcji platformy Azure.

Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) konta przy użyciu platformy Microsoft Azure — należy użyć konta hello, skojarzoną z hello subskrypcji platformy Azure.

1. W okienku nawigacji powitania kliknij **ustawienia**, następnie kliknij przycisk **Administratorzy**.
2. U dołu hello hello, kliknij przycisk **Dodaj**. 
3. W powitalne okno dialogowe Dodaj A WSPÓŁADMINISTRATOREM wpisz adres e-mail osoby hello ma tooadd jako administratora współpracującego i hello następnie wybierz subskrypcję, która ma hello tooaccess współadministratorem hello.
4. Kliknij pozycję **Zapisz**.

### <a name="access-for-users-of-classic-web-services"></a>Dostęp dla użytkowników z usług sieci Web klasycznego
toomanage obszaru roboczego:

Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) konta przy użyciu platformy Microsoft Azure — należy użyć konta hello, skojarzoną z hello subskrypcji platformy Azure.

1. Witaj Panel usługi Microsoft Azure, kliknij przycisk **UCZENIA MASZYNOWEGO**.
2. Kliknij obszar roboczy hello ma toomanage.
3. Kliknij przycisk hello **Konfiguruj** kartę.

Na karcie Konfiguracja hello, można wstrzymać obszaru roboczego uczenia maszynowego toohello dostępu, klikając **ODMÓW**. Użytkownicy będą już mogli tooopen hello roboczym w usłudze Machine Learning Studio. toorestore dostępu, kliknij przycisk **Zezwalaj**.

Użytkownicy toospecific:

toomanage dodatkowych kont mających roboczym toohello dostępu w usłudze Machine Learning Studio, kliknij przycisk **logowania tooML Studio** w hello **pulpitu NAWIGACYJNEGO** kartę. Spowoduje to otwarcie hello obszaru roboczego usługi Machine Learning Studio. W tym miejscu, kliknij przycisk hello **ustawienia** kartę, a następnie **użytkowników**. Możesz kliknąć **ZAPROSIĆ użytkowników więcej** toogive użytkowników dostępu toohello obszaru roboczego, lub wybierz użytkownika i kliknij przycisk **Usuń**.

> [!NOTE]
> Witaj **logowania tooML Studio** łącze powoduje otwarcie przy użyciu hello Account Microsoft użytkownik jest już zarejestrowany w usłudze Machine Learning Studio. Witaj Account Microsoft toosign jest używany w toohello klasycznego portalu Azure toocreate obszaru roboczego nie ma automatycznie tooopen uprawnienia tego obszaru roboczego. tooopen obszaru roboczego, musisz zarejestrować się w toohello Account Microsoft został zdefiniowany jako hello właściciela obszaru roboczego hello, lub należy tooreceive zaproszenia od hello właściciela toojoin hello roboczym.
> 
> 

