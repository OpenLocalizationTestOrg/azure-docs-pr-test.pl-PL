---
title: "szczegółowe omówienie planów usługi aplikacji aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak planów usługi App Service dla pracy w usłudze Azure App Service i korzyści do środowiska zarządzania."
keywords: app service, azure app service, scale, scalable, app service plan, app service cost
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Szczegółowe omówienie planów usługi Azure App Service

Plany usług aplikacji reprezentują hello zbiór toohost fizyczne zasoby używane aplikacje.

Plany usługi App Service definiują następujące elementy:

- Region (zachodnie stany USA, wschodnie stany USA, itp.)
- Liczba skali (jedną, dwie trzy wystąpienia, itp.)
- Rozmiar wystąpienia (mały, Średni, duże)
- Jednostka magazynowa (Bezpłatna, Współdzielona, Podstawowa, Standardowa, Premium)

Sieci Web Apps, Mobile Apps, aplikacje interfejsu API, funkcja aplikacji (lub funkcji), w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) wszystkie działania w planie usługi aplikacji.  Aplikacje w hello tej samej subskrypcji i regionu można udostępniać plan usługi aplikacji. 

Wszystkie aplikacje przypisane tooan **planu usługi aplikacji** udostępnianie zasobów hello zdefiniowana przez nią. Udostępnianie tego zapisuje pieniędzy odnośnie do hostowania wielu aplikacji w ramach jednego planu usługi aplikacji.

Twoje **planu usługi aplikacji** można skalować z **wolne** i **Shared** jednostki SKU zbyt**podstawowe**, **standardowe**, i **Premium** jednostki SKU, umożliwiając dostęp do zasobów toomore i funkcje wzdłuż hello sposób.

Jeśli plan usługi aplikacji jest ustawiona zbyt**podstawowe** SKU lub nowszej, a następnie można kontrolować hello **rozmiar** i skalować liczbę hello maszyn wirtualnych.

Na przykład jeśli plan jest skonfigurowany toouse dwa wystąpienia "małe" w warstwie usług standardowa na powitania, wszystkie aplikacje, które są skojarzone z tym planem uruchamiane na obu wystąpień. Aplikacje mają również funkcje warstwy standardowa usługa toohello dostępu. Wystąpieniach planu, na których działają aplikacje są pełni zarządzany i wysokiej dostępności.

> [!IMPORTANT]
> Witaj **SKU** i **skali** z usługi aplikacji hello plan określa hello kosztów i nie hello liczbę aplikacje znajdujące się w nim.

Ten artykuł opisuje hello właściwości klucza, takie jak warstwy i skali plan usługi aplikacji i sposób ich wchodzić w grę w aplikacji i zarządzania nimi.

## <a name="apps-and-app-service-plans"></a>Aplikacje i planów usługi aplikacji

Aplikacji w usłudze App Service może być skojarzony tylko jeden plan usługi aplikacji w danym momencie.

Aplikacjach i planów są zawarte w **grupy zasobów**. Grupa zasobów służy jako hello cyklu życia granic dla każdego zasobu, który jest w nim. Możesz użyć toomanage grup zasobów wszystkich elementów hello aplikacji.

Ponieważ pojedyncza grupa zasobów może mieć wiele planów usługi aplikacji, możesz przydzielić różnych aplikacji toodifferent zasobów fizycznych.

Na przykład można oddzielić zasobów w środowiskach deweloperów, badanie i produkcji. Posiadanie oddzielnego środowiska produkcyjnego i tworzenie/testowanie oprogramowania pozwala izolować zasobów. W ten sposób obciążenia testowanie nowej wersji aplikacji nie konkurują o hello samo zasobów co aplikacji produkcyjnych, które służy rzeczywistych klientów.

Jeśli masz wiele planów w pojedynczej grupy zasobów można także zdefiniować aplikacji obejmującej regionów geograficznych.

Na przykład aplikację o wysokiej dostępności w dwóch regionach zawiera co najmniej dwa pakiety, po jednej dla każdego regionu i jeden aplikacji skojarzonej z każdego planu. W takiej sytuacji wszystkie kopie hello aplikacji hello następnie znajdują się w pojedynczej grupy zasobów. Dostępność grupy zasobów z wieloma planami i wielu aplikacji, ułatwia toomanage łatwe, sterowania i Wyświetl kondycję hello aplikacji hello.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>Tworzenie planu usługi App Service lub użyć istniejącego

Podczas tworzenia aplikacji, należy rozważyć utworzenie grupy zasobów. Na powitania drugiej strony, jeśli ta aplikacja jest składnikiem większej aplikacji, utwórz go w grupie zasobów hello przydzielonej do większych aplikację.

Czy aplikacja hello jest całkowicie nowa aplikacja lub część większego, możesz wybrać toouse istniejących toohost planu go lub Utwórz nową. Ta decyzja jest bardziej pytanie pojemności i oczekiwane obciążenia.

Zalecamy Izolowanie aplikacji do nowej usługi aplikacji podczas planowania:

- Aplikacja jest obciążający zasoby.
- Aplikacja ma różne czynniki skalowania z hello innych aplikacji hostowanej w istniejącego planu.
- Aplikacja potrzebuje zasobów w innym regionie geograficznym.

W ten sposób można przydzielić nowego zestawu zasobów dla aplikacji i uzyskać większą kontrolę nad aplikacjami.

## <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

> [!TIP]
> Jeśli masz środowisko usługi aplikacji, można przejrzeć hello dokumentacji określonych tooApp środowiska usługi tutaj: [Utwórz plan usługi aplikacji w środowisku usługi aplikacji](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

Można utworzyć pusty plan usługi aplikacji, z hello środowisko przeglądania planu usługi aplikacji lub w ramach tworzenia aplikacji.

W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność**, a następnie wybierz **aplikacji sieci Web** lub innego typu aplikacji usługi aplikacji.

![Tworzenie aplikacji w hello portalu Azure.][createWebApp]

Można następnie wybrać lub utworzyć hello planu usługi App Service dla nowej aplikacji hello.

 ![Tworzenie planu usługi aplikacji.][createASP]

Kliknij toocreate plan usługi aplikacji **[+] Utwórz nowy**, hello typu **planu usługi aplikacji** nazwy, a następnie wybierz odpowiedni **lokalizacji**. Kliknij przycisk **warstwa cenowa**, a następnie wybierz odpowiednią warstwę cenową dla usługi hello. Wybierz **Wyświetl wszystkie** tooview więcej cennik opcje, takie jak **wolne** i **Shared**. Po wybraniu warstwy cenowej powitania kliknij hello **wybierz** przycisku.

## <a name="move-an-app-tooa-different-app-service-plan"></a>Przenoszenie aplikacji tooa inny plan usługi aplikacji

Można przenosić aplikacji tooa inny plan usługi aplikacji hello [portalu Azure](https://portal.azure.com). Aplikacje można przenosić między planami tak długo, jak plany hello znajdują się w hello tej samej grupie zasobów i region geograficzny.

toomove plan tooanother aplikacji:

- Przejdź toohello aplikacji, które mają toomove.
- W hello **Menu**, wyszukaj hello **planu usługi App Service** sekcji.
- Wybierz **planu usługi aplikacji zmiany** toostart hello procesu.

**Zmień plan usługi aplikacji** hello otwiera **planu usługi aplikacji** selektora. W tym momencie można wybrać istniejący plan toomove tej aplikacji do.

> [!IMPORTANT]
> Wybierz plan usługi aplikacji Hello interfejsu użytkownika są filtrowane według hello następujące kryteria:
> - Istnieje w ramach hello same grupy zasobów
> - Istnieje w hello sam Region geograficzny
> - Istnieje w ramach hello sam przestrzeni sieci Web
>
> Przestrzeni sieci Web jest konstrukcją logiczną, w ramach usługi aplikacji, który definiuje grupę zasobów serwera. Region geograficzny (na przykład zachodnie stany USA) zawiera wiele Webspaces w kolejności tooallocate klientów korzystających z usługi aplikacji. Obecnie zasobów usługi aplikacji nie są toobe można przenosić między Webspaces.
>

![Selektor planu usługi aplikacji.][change]

Każdy plan ma własną warstwy cenowej. Umożliwia przenoszenie lokacji z warstwy standardowej tooa warstwę bezpłatna, na przykład wszystkie aplikacje przypisane tooit toouse hello funkcje i zasoby hello warstwy standardowa.

## <a name="clone-an-app-tooa-different-app-service-plan"></a>Klonowanie aplikacji tooa inny plan usługi aplikacji

Jeśli chcesz toomove hello aplikacji tooa innym regionie, co alternatywa to aplikacji klonowania. Klonowanie tworzy kopię aplikacji w nowy lub istniejący plan usługi aplikacji w dowolnym regionie.

Można znaleźć **aplikacji w klonowania** w hello **narzędzi programistycznych** część hello menu.

> [!IMPORTANT]
> Klonowanie ma pewne ograniczenia, które możesz przeczytać temat na [klonowania aplikacji usługi aplikacji Azure przy użyciu portalu Azure](../app-service-web/app-service-web-app-cloning-portal.md).

## <a name="scale-an-app-service-plan"></a>Skalowanie planu usługi aplikacji

Istnieją trzy sposoby tooscale plan:

- **Zmiany planu hello do warstwy cenowej**. Planu w warstwie podstawowa hello może być przekonwertowany tooStandard i wszystkie aplikacje przypisane tooit toouse funkcje hello hello warstwy standardowa.
- **Zmień rozmiar wystąpienia planu hello**. Na przykład planu w warstwie podstawowa hello korzystającej z małej wystąpień może być zmienione toouse dużych wystąpień. Wszystkie aplikacje, które są skojarzone z tym planem teraz można używać hello dodatkową pamięć i zasoby Procesora, które hello większych oferty rozmiar wystąpienia.
- **Zmiana liczby wystąpień w planie hello**. Na przykład standardowy plan, który jest skalowana w poziomie toothree wystąpień może być skalowana too10 wystąpień. Premium plan można skalować w poziomie too20 wystąpień (tooavailability podmiotu). Wszystkie aplikacje, które są skojarzone z tym planem teraz można używać hello dodatkową pamięć i zasoby Procesora, które hello większych oferty liczba wystąpień.

Możesz zmienić hello cennik rozmiar warstwy i wystąpienia, klikając hello **Skaluj w górę** elementu w obszarze Ustawienia aplikacji hello lub hello planu usługi aplikacji. Zmiany zastosować toohello planu usługi aplikacji i wpływają na wszystkie aplikacje, które obsługuje.

 ![Ustaw wartości tooscale zapasowej aplikacji.][pricingtier]

## <a name="app-service-plan-cleanup"></a>Oczyszczanie planu usługi aplikacji

> [!IMPORTANT]
> **Planów usługi App Service** nie toothem aplikacji skojarzonych z nadal spowodować naliczenie opłat, ponieważ nadal wydajności obliczeniowej hello tooreserve, która ma.

tooavoid nieoczekiwany opłat, po usunięciu aplikacji ostatniego hello hostowanej w planie usługi aplikacji hello wynikowy pusta planu usługi aplikacji są także usuwane.

## <a name="summary"></a>Podsumowanie

Plany usług aplikacji reprezentują zestaw funkcji i możliwości, które można udostępniać między swoimi aplikacjami. Planów usługi App Service zapewnia hello elastyczność tooallocate określonych aplikacji tooa zestawu zasobów i dalszą optymalizację z wykorzystania zasobów platformy Azure. W ten sposób Jeśli chcesz toosave pieniądze na środowisku do testowania, można udostępnić plan wielu aplikacjom. Można również zmaksymalizować przepustowość dla środowiska produkcyjnego skalując w wielu regionach i planów.

## <a name="whats-changed"></a>Co zostało zmienione

- Przewodnik toohello zmian z tooApp witryn sieci Web Service, zobacz: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
