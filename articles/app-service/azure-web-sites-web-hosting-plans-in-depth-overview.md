---
title: "Szczegółowe omówienie planów usługi aplikacji Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f97be571d104e3cc1c6ee732886fa7133ba0dc83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Szczegółowe omówienie planów usługi Azure App Service

Plany usług aplikacji reprezentują kolekcji zasobów fizycznych używana do hostowania aplikacji.

Plany usługi App Service definiują następujące elementy:

- Region (zachodnie stany USA, wschodnie stany USA, itp.)
- Liczba skali (jedną, dwie trzy wystąpienia, itp.)
- Rozmiar wystąpienia (mały, Średni, duże)
- Jednostka magazynowa (Bezpłatna, Współdzielona, Podstawowa, Standardowa, Premium)

Sieci Web Apps, Mobile Apps, aplikacje interfejsu API, funkcja aplikacji (lub funkcji), w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) wszystkie działania w planie usługi aplikacji.  Aplikacje w tej samej subskrypcji i regionu można udostępnić plan usługi aplikacji. 

Wszystkie aplikacje przypisane do **planu usługi aplikacji** udostępnianie zasobów zdefiniowana przez nią. Udostępnianie tego zapisuje pieniędzy odnośnie do hostowania wielu aplikacji w ramach jednego planu usługi aplikacji.

**Plan usługi App Service** może być jednostką magazynową typu **Bezpłatna**, **Współdzielona**, **Podstawowa**, **Standardowa** lub **Premium**, zapewniając dostęp do odpowiedniej liczby zasobów i funkcji.

Jeśli ustawiono planu usługi aplikacji **podstawowe** SKU lub nowszej, a następnie można kontrolować **rozmiar** i skalowanie liczby maszyn wirtualnych.

Na przykład jeśli plan jest skonfigurowany do używania dwóch wystąpień "małe" w warstwie usług standardowa, wszystkie aplikacje, które są skojarzone z tym planem uruchamiane na obu wystąpień. Aplikacje mają także dostęp do funkcji warstwy standardowa usługi. Wystąpieniach planu, na których działają aplikacje są pełni zarządzany i wysokiej dostępności.

> [!IMPORTANT]
> Ustawienia **Jednostka magazynowa** i **Skala** planu usługi App Service określają koszt i liczbę hostowanych w nim aplikacji.

Ten artykuł opisuje klucza cechy, takie jak warstwy i skali, plan usługi aplikacji i sposób ich wchodzić w grę w aplikacji i zarządzania nimi.

## <a name="apps-and-app-service-plans"></a>Aplikacje i planów usługi aplikacji

Aplikacji w usłudze App Service może być skojarzony tylko jeden plan usługi aplikacji w danym momencie.

Aplikacjach i planów są zawarte w **grupy zasobów**. Grupa zasobów służy jako granica cyklu życia dla każdego zasobu, który jest w nim. Grupy zasobów można użyć do zarządzania ze sobą wszystkie elementy aplikacji.

Ponieważ pojedyncza grupa zasobów może mieć wiele planów usługi aplikacji, możesz przydzielić różnych aplikacji do różnych zasobów fizycznych.

Na przykład można oddzielić zasobów w środowiskach deweloperów, badanie i produkcji. Posiadanie oddzielnego środowiska produkcyjnego i tworzenie/testowanie oprogramowania pozwala izolować zasobów. W ten sposób obciążenia testowanie nowej wersji aplikacji nie konkurują o tych samych zasobów co aplikacji produkcyjnych, które służy rzeczywistych klientów.

Jeśli masz wiele planów w pojedynczej grupy zasobów można także zdefiniować aplikacji obejmującej regionów geograficznych.

Na przykład aplikację o wysokiej dostępności w dwóch regionach zawiera co najmniej dwa pakiety, po jednej dla każdego regionu i jeden aplikacji skojarzonej z każdego planu. W takiej sytuacji wszystkie kopie aplikacji następnie znajdują się w pojedynczej grupy zasobów. Grupy zasobów z wieloma planami i wiele aplikacji o ułatwia zarządzanie, sterowanie i wyświetlić informacje o kondycji aplikacji.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>Tworzenie planu usługi App Service lub użyć istniejącego

Podczas tworzenia aplikacji, należy rozważyć utworzenie grupy zasobów. Z drugiej strony Jeśli ta aplikacja jest składnikiem większej aplikacji, utwórz je w grupie zasobów przydzielonej dla danego zastosowania większej.

Czy aplikacja jest całkowicie nowa aplikacja lub część większego, można użyć istniejącego planu hostingu lub Utwórz nową. Ta decyzja jest bardziej pytanie pojemności i oczekiwane obciążenia.

Zalecamy Izolowanie aplikacji do nowej usługi aplikacji podczas planowania:

- Aplikacja jest obciążający zasoby.
- Aplikacja ma różne czynniki skalowania z innych aplikacji hostowanej w istniejącego planu.
- Aplikacja potrzebuje zasobów w innym regionie geograficznym.

W ten sposób można przydzielić nowego zestawu zasobów dla aplikacji i uzyskać większą kontrolę nad aplikacjami.

## <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

> [!TIP]
> Jeśli masz środowisko usługi aplikacji zapoznanie się z dokumentacją specyficzną dla środowiska usługi App Service w tym miejscu: [Utwórz plan usługi aplikacji w środowisku usługi aplikacji](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

Środowisko przeglądania planu usługi aplikacji lub w ramach tworzenia aplikacji, można utworzyć pusty plan usługi aplikacji.

W [portalu Azure](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność**, a następnie wybierz **aplikacji sieci Web** lub innego typu aplikacji usługi aplikacji.

![Utwórz aplikację w portalu Azure.][createWebApp]

Możesz wybrać lub utworzyć plan usługi App Service dla nowej aplikacji.

 ![Tworzenie planu usługi aplikacji.][createASP]

Aby utworzyć plan usługi aplikacji, kliknij przycisk **[+] Tworzenie nowych**, typ **planu usługi aplikacji** nazwy, a następnie wybierz odpowiedni **lokalizacji**. Kliknij przycisk **warstwa cenowa**, a następnie wybierz odpowiednią warstwę cenową dla usługi. Wybierz **Wyświetl wszystkie** do widoku więcej cennik opcje, takie jak **wolne** i **Shared**. Po wybraniu warstwy cenowej kliknij **wybierz** przycisku.

## <a name="move-an-app-to-a-different-app-service-plan"></a>Przenieś aplikację do innego planu usługi aplikacji

Aplikację można przenieść do innego planu usługi aplikacji w [portalu Azure](https://portal.azure.com). Aplikacje można przenosić między planami tak długo, jak plany znajdują się w tej samej grupie zasobów i region geograficzny.

Aby przenieść aplikację do innego planu:

- Przejdź do aplikacji, którą chcesz przenieść.
- W **Menu**, wyszukaj **planu usługi App Service** sekcji.
- Wybierz **planu usługi aplikacji zmiany** do rozpoczęcia procesu.

**Zmień plan usługi aplikacji** otwiera **planu usługi aplikacji** selektora. W tym momencie można wybrać istniejący plan można przenieść tej aplikacji do.

> [!IMPORTANT]
> Wybierz plan usługi aplikacji interfejsu użytkownika są filtrowane według następujących kryteriów:
> - Istnieje w tej samej grupie zasobów
> - Istnieje w tym samym regionie geograficznym
> - Istnieje w tej samej przestrzeni sieci Web
>
> Przestrzeni sieci Web jest konstrukcją logiczną, w ramach usługi aplikacji, który definiuje grupę zasobów serwera. Region geograficzny (na przykład zachodnie stany USA) zawiera wiele Webspaces Aby przydzielić klientów korzystających z usługi aplikacji. Obecnie zasobów usługi aplikacji — nie można przenieść między Webspaces.
>

![Selektor planu usługi aplikacji.][change]

Każdy plan ma własną warstwy cenowej. Na przykład przejście lokacji z warstwę bezpłatna do warstwy standardowa, włącza wszystkie aplikacje przypisane do korzystania z funkcji i zasoby warstwy standardowa.

## <a name="clone-an-app-to-a-different-app-service-plan"></a>Klonowanie aplikację do innego planu usługi aplikacji

Jeśli chcesz przenieść aplikację w innym regionie, co alternatywa to aplikacji klonowania. Klonowanie tworzy kopię aplikacji w nowy lub istniejący plan usługi aplikacji w dowolnym regionie.

Można znaleźć **aplikacji w klonowania** w **narzędzi programistycznych** części menu.

> [!IMPORTANT]
> Klonowanie ma pewne ograniczenia, które możesz przeczytać temat na [klonowania aplikacji usługi aplikacji Azure przy użyciu portalu Azure](../app-service-web/app-service-web-app-cloning-portal.md).

## <a name="scale-an-app-service-plan"></a>Skalowanie planu usługi aplikacji

Istnieją trzy sposoby skalowanie planu:

- **Zmień plan na warstwie cenowej**. Standard, a wszystkie aplikacje przypisane do niej można użyć funkcji warstwy standardowa można przekonwertować planu w warstwie podstawowej.
- **Zmień rozmiar wystąpienia planu**. Na przykład można zmienić planu w warstwie podstawowa korzystającej z małej wystąpień do użycia dużych wystąpień. Wszystkie aplikacje, które są skojarzone z tym planem teraz można użyć dodatkowych pamięć i zasoby Procesora, które oferuje większy rozmiar wystąpienia.
- **Zmień liczbę wystąpień planu**. Na przykład standardowy plan, który jest skalowana w poziomie do trzech przypadkach mogą być skalowane do 10 wystąpień. Premium plan można skalować w poziomie do 20 wystąpień (pod warunkiem dostępności). Wszystkie aplikacje, które są skojarzone z tym planem teraz służy dodatkową pamięć i zasoby Procesora, które oferuje większej liczby wystąpień.

Cenową rozmiar warstwy i wystąpienia można zmienić, klikając **Skaluj w górę** elementu w obszarze ustawień aplikacji lub plan usługi aplikacji. Zmiany dotyczą plan usługi aplikacji i wpływają na wszystkie aplikacje, które obsługuje.

 ![Ustaw wartości, aby skalować aplikację.][pricingtier]

## <a name="app-service-plan-cleanup"></a>Oczyszczanie planu usługi aplikacji

> [!IMPORTANT]
> **Planów usługi App Service** , która ma żadnych aplikacji powiązanych z nimi nadal spowodować naliczenie opłat, ponieważ nadal zarezerwować wydajności obliczeniowej.

Aby uniknąć nieoczekiwanego opłat, po usunięciu ostatniej aplikacji hostowanej w planie usługi aplikacji, wynikowy pusty plan usługi aplikacji są także usuwane.

## <a name="summary"></a>Podsumowanie

Plany usług aplikacji reprezentują zestaw funkcji i możliwości, które można udostępniać między swoimi aplikacjami. Planów usługi aplikacji umożliwiają elastyczne do przydzielenie danej aplikacji do zestawu zasobów i dalszą optymalizację z wykorzystania zasobów platformy Azure. Ten sposób, jeśli chcesz oszczędzić pieniądze na środowisku do testowania, można udostępnić plan wielu aplikacjom. Można również zmaksymalizować przepustowość dla środowiska produkcyjnego skalując w wielu regionach i planów.

## <a name="whats-changed"></a>Co zostało zmienione

- Przewodnik dotyczący zmiany z witryn sieci Web w usłudze App Service, zobacz: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
