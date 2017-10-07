---
title: "Usługa Azure Search w portalu hello aaaCreate | Dokumentacja firmy Microsoft"
description: "Udostępnić usługi Azure Search w portalu hello."
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a>Tworzenie usługi Azure Search w portalu hello

W tym artykule opisano, jak toocreate lub świadczenia usługi Azure Search w portalu hello. Aby uzyskać instrukcje programu PowerShell, zobacz [zarządzania usługi Azure Search przy użyciu programu PowerShell](search-manage-powershell.md).

## <a name="subscribe-free-or-paid"></a>Subskrypcja (wolne lub płatną)

[Załóż bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) i użyj tootry bezpłatnych środków limit płatnej usług platformy Azure. Po wyczerpaniu kredytu, Zachowaj konto hello i kontynuować toouse wolnego usług platformy Azure, takich jak witryny sieci Web. Karta kredytowa nigdy nie jest obciążona, chyba że jawnie zmienić ustawienia i poproś toobe obciążona.

Alternatywnie [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Subskrypcję MSDN otrzymasz kredyt, co miesiąc, w której można skorzystać w celu płatnych usług Azure. 

## <a name="find-azure-search"></a>Znajdź wyszukiwanie Azure
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Kliknij znak ("+") plus hello hello górnym lewym rogu.
3. Wybierz **sieci Web i mobilność** > **wyszukiwanie Azure**.

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a>Usługa hello nazwa i adres URL punktu końcowego

Nazwa usługi jest częścią hello końcowy adres URL, względem którego są wydawane wywołań interfejsu API. Wpisz nazwę usługi w hello **adres URL** pola. 

Wymagania dotyczące nazw usługi:
   * 2 do 60 znaków
   * małe litery, cyfry i łączniki ("-")
   * nie dash ("-") jako hello najpierw 2 znaki lub ostatni pojedynczy znak
   * nie następujących po sobie kresek ("--")

## <a name="select-a-subscription"></a>Wybierz subskrypcję
Jeśli masz więcej niż jedną subskrypcję, wybierz jedną z usług magazynu danych lub pliku. Usługa wyszukiwanie Azure można Autowykrywanie magazynu tabel Azure i obiektów Blob, bazy danych SQL i bazy danych Azure rozwiązania Cosmos indeksowania za pośrednictwem *indeksatory*, ale tylko w przypadku usług w hello tej samej subskrypcji.

## <a name="select-a-resource-group"></a>Wybierz grupę zasobów
Grupa zasobów to zbiór usług platformy Azure i zasoby używane razem. Na przykład, jeśli używasz usługi Azure Search tooindex bazy danych SQL, obie te usługi powinny być częścią hello tej samej grupie zasobów.

> [!TIP]
> Usunięcie grupy zasobów powoduje usunięcie usług hello w niej. Prototyp projektów przy użyciu wielu usług, wprowadzenie wszystkich z nich hello tej samej grupie zasobów ułatwia oczyszczania po zakończeniu hello projektu. 

## <a name="select-a-hosting-location"></a>Wybierz lokalizację hostingu 
Jak usługa Azure usługi Azure Search może być hostowana w centrach danych wokół hello world. Należy pamiętać, że [ceny może się różnić](https://azure.microsoft.com/pricing/details/search/) według ich położenia.

## <a name="select-a-pricing-tier-sku"></a>Wybierz warstwę cenową (SKU)
[Usługa Azure Search jest dostępne w wielu warstw cenowych](https://azure.microsoft.com/pricing/details/search/): wolnego, podstawowa lub standardowa. Każda warstwa ma własną [pojemności i limity](search-limits-quotas-capacity.md). Zobacz [wybierz warstwę cenową lub jednostki SKU](search-sku-tier.md) orientacji.

W tym przewodniku Wybraliśmy warstwy standardowa hello naszej usługi.

## <a name="create-your-service"></a>Tworzenie usługi

Należy pamiętać, toopin pulpitu nawigacyjnego toohello usługi łatwy dostęp przy każdym logowaniu.

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a>Skalowanie usługi
Może upłynąć kilka minut toocreate usługi (15 minut lub dłużej w zależności od warstwy hello). Po zainicjowaniu obsługi usługi, to można go skalować toomeet potrzeb. Ponieważ wybrano warstwy standardowa powitania dla usługi Azure Search w dwóch wymiarów można skalować usługi: repliki i partycji. Czy wybierze hello warstwy Basic, można dodać tylko repliki. Jeśli elastycznie bezpłatnej usługi hello, skalowanie jest niedostępne.

***Partycje*** Zezwalaj toostore usługi, a wyszukiwanie za pomocą więcej dokumentów.

***Repliki*** Zezwalaj toohandle Twojego usługi większych obciążeń zapytań wyszukiwania.

> [!Important]
> Usługa musi mieć [2 replik do umowy SLA tylko do odczytu i 3 repliki do odczytu/zapisu SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

1. Przejdź tooyour bloku usługi wyszukiwania w hello portalu Azure.
2. Wybierz w okienku nawigacji po lewej hello **ustawienia** > **skali**.
3. Użyj hello slidebar tooadd repliki lub partycji.

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> Każda warstwa ma inną [limity](search-limits-quotas-capacity.md) hello całkowitej liczby jednostek wyszukiwania dozwolonych w jednej usługi (replik * partycje = Suma jednostek wyszukiwania).

## <a name="when-tooadd-a-second-service"></a>Gdy tooadd drugi usługi

Duże większość klientów używać tylko jednej usługi zainicjowana dla warstwy, która zapewnia hello [prawym przyciskiem myszy salda środków](search-sku-tier.md). Jedna usługa może obsługiwać wiele indeksów, toohello podmiotu [maksymalnych wybrania warstwy hello](search-capacity-planning.md), każdy indeks odizolowane od siebie. W usłudze Azure Search żądań może jedynie być indeksem ukierunkowanej tooone, minimalizując szansy hello pobierania przypadkowym lub zamierzone danych z innych indeksy w hello sama usługa.

Mimo że większość klientów używają tylko jedną usługę, nadmiarowości usługi może być konieczne, jeśli wymagań operacyjnych Uwzględnij hello następujące elementy:

+ Odzyskiwanie po awarii (awarii centrum danych). Usługa Azure Search nie zapewnia błyskawiczne trybu failover w przypadku hello awarii. Aby uzyskać wskazówki i zalecenia, zobacz [usługi administracyjnej](search-manage.md).
+ Badaniu modelowania wielodostępność stwierdził, że dodatkowe usługi jest hello optymalne projektu. Aby uzyskać więcej informacji, zobacz [projektu dla wielu dzierżawców](search-modeling-multitenant-saas-applications.md).
+ Globalny wdrożonej aplikacji może wymagać wystąpienia usługi Azure Search wiele regionów opóźnienia toominimize aplikacji międzynarodowych ruchu.

> [!NOTE]
> W usłudze Azure Search nie może też oddzielić obciążeń indeksowania i wykonywanie zapytania; w związku z tym nigdy nie spowodowałoby utworzenie wielu usług dla obciążeń rozdzielone. Indeks jest zawsze wykonać zapytania w usłudze hello w którym został utworzony (nie można utworzyć indeksu w jedną usługę i skopiuj go tooanother).
>

Drugi usługi nie jest wymagane w celu zapewnienia wysokiej dostępności. Wysoka dostępność dla zapytania jest osiągana, gdy używasz 2 lub więcej replik w hello tę samą usługę. Repliki są aktualizacje sekwencyjnych, co oznacza, że co najmniej jeden działa podczas aktualizacji usługi jest wdrażana. Aby uzyskać więcej informacji o dostępności, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

## <a name="next-steps"></a>Następne kroki
Po zainicjowaniu obsługi administracyjnej usługi Azure Search, wszystko jest gotowe za[zdefiniuj indeks](search-what-is-an-index.md) , można przekazać i wyszukiwać dane.

Usługa hello tooaccess z kodu lub skryptu, podaj adres URL hello (*nazwa usługi*. search.windows.net) i klucz. Klucze administratora przyznają dostęp; klucze zapytań przyznać dostęp tylko do odczytu. Zobacz [jak toouse wyszukiwanie Azure .NET](search-howto-dotnet-sdk.md) tooget uruchomiona.

Zobacz [kompilacji i tworzenie zapytań względem indeksu pierwszego](search-get-started-portal.md) zawiera krótki samouczek oparte na portalu.

