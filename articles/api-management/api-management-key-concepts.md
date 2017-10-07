---
title: "Zarządzanie interfejsami API aaaAzure omówienie i klucz pojęcia | Dokumentacja firmy Microsoft"
description: "Poznaj interfejsy API, produkty, role, grupy i inne ważne pojęcia dotyczące usługi API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a77b24b4632d868afa15bd6cf88060982046cb38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-api-management"></a>Co to jest API Management?
Zarządzanie interfejsami API pomaga organizacjom publikowania interfejsów API tooexternal, partnera i deweloperzy wewnętrznej toounlock hello potencjalne swoich danych i usług. Firm wszędzie są wyszukiwania tooextend operacje jako platforma digital, tworzenie nowych kanałów, znajdowanie nowych klientów i kierowania głębiej interakcji użytkowników z istniejących. Zarządzanie interfejsami API udostępnia hello podstawowe umiejętności tooensure pomyślnie program interfejsu API za pomocą zaangażowania deweloperów, informacje biznesowe, analytics, zabezpieczeń i ochrony.

Obejrzyj powitania po wideo Omówienie usługi Azure API Management i Dowiedz się, jak tooadd zarządzanie interfejsami API toouse wiele tooyour funkcje interfejsu API, łącznie z kontrolą dostępu szybkości ograniczenie, monitorowanie, rejestrowanie zdarzeń i buforowanie odpowiedzi z minimalnym nakładu pracy.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

toouse zarządzanie interfejsami API Administratorzy tworzyć interfejsy API. Każdy interfejs API składa się z co najmniej jedną operację, i każdego interfejsu API można dodać tooone lub więcej produktów. toouse interfejsu API, deweloperzy subskrypcji tooa produktu, który zawiera ten interfejs API, a następnie można wywołać operacji hello interfejsu API, zasad użytkowania tooany podmiotu, które mogą obowiązywać.

Ten temat zawiera przegląd najważniejszych założeń usługi API Management.

> [!NOTE]
> Aby uzyskać więcej informacji, zobacz hello [oparte na chmurze zarządzanie interfejsami API: wykorzystanie hello zasilania interfejsów API](http://j.mp/ms-apim-whitepaper) oficjalny dokument PDF. Ten wprowadzający oficjalny dokument dotyczący usługi API Management opracowany przez firmę CITO Research obejmuje następujące tematy: 
> 
> * Typowe wymagania i wyzwania związane z interfejsem API
> * Rozdzielanie interfejsów API i prezentowanie fasad
> * Szybkie rozpoczęcie pracy przez deweloperów
> * Zabezpieczanie dostępu
> * Analizy i metryki
> * Uzyskiwanie kontroli i wglądu dzięki platformie usługi API Management
> * Porównanie rozwiązań w chmurze i rozwiązań lokalnych
> * Usługa Azure API Management
> 
> 

## <a name="apis"> </a>Interfejsy API i operacje
Interfejsy API są foundation hello wystąpienia usługi Zarządzanie interfejsami API. Każdy interfejs API reprezentuje zestaw toodevelopers dostępne operacje. Każdy interfejs API zawiera usługi zaplecza toohello odwołania, który implementuje interfejs API hello, oraz jego operacji mapowanie toohello działania wykonywane przez usługę wewnętrzną hello. Operacje usługi API Management są wysoce konfigurowalne, pozwalają na kontrolę mapowania adresu URL, parametrów zapytania i ścieżki, zawartości żądania i odpowiedzi oraz buforowanie odpowiedzi operacji. Limit szybkości, przydziały i zasady ograniczeń IP można również implementowana na poziomie poszczególnych działań lub hello interfejsu API.

Aby uzyskać więcej informacji, zobacz [jak toocreate interfejsów API] [ How toocreate APIs] i [jak tooadd tooan operacje interfejsu API][How tooadd operations tooan API].

## <a name="products"> </a> Produkty
Produkty są jak interfejsy API są udostępniane toodevelopers. Produkty w usłudze API Management mają co najmniej jeden interfejs API oraz skonfigurowany tytuł, opis i warunki użytkowania. Produkty mogą być **otwarte** lub **chronione**. Produkty chronione muszą być subskrybowanego toobefore mogą być używane, otwartej produktów może być używany bez subskrypcji. Kiedy produkt jest gotowy do użycia przez deweloperów, można go opublikować. Po jest publikowany, można wyświetlić (i w hello przypadku produktów chronionych subskrybuje) przez deweloperów. Zatwierdzenie subskrypcji jest skonfigurowana na poziomie produktu hello i można wymagają zatwierdzenia przez administratora lub można automatycznie zatwierdzone.

Grupy są używane toomanage widoczność hello toodevelopers produktów. Produkty Udziel toogroups widoczność i deweloperzy mogą wyświetlać i subskrybować toohello produktów, które są widoczne toohello grup, w których one należą. 

Aby uzyskać więcej informacji, zobacz [jak toocreate i opublikuj produktu] [ How toocreate and publish a product] i hello następujących wideo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <a name="groups"> </a> Grupy
Grupy są używane toomanage widoczność hello toodevelopers produktów. Zarządzanie interfejsami API ma hello następujące grupy systemu niezmienialny.

* **Administratorzy** — do tej grupy należą administratorzy subskrypcji platformy Azure. Administratorzy Zarządzanie wystąpieniami usługi Zarządzanie interfejsami API, tworzenie hello interfejsów API, operacje i produktów, które są używane przez deweloperów.
* **Deweloperzy** — do tej grupy należą uwierzytelnieni użytkownicy portalu dla deweloperów. Deweloperzy są hello klientów, którzy tworzyć aplikacje przy użyciu swoje interfejsy API. Deweloperzy otrzymują dostęp do portalu dla deweloperów toohello i tworzenia aplikacji wywołujących hello operacje interfejsu API.
* **Goście** -nieuwierzytelnionych użytkowników portalu deweloperów, na przykład potencjalni klienci odwiedzający hello portalu dla deweloperów programu spadek wystąpienia interfejsu API zarządzania do tej grupy. Może zostać przydzielony niektórych dostęp tylko do odczytu, takich jak tooview możliwości hello interfejsów API, ale nie połączeń telefonicznych z nimi.

Dodanie toothese systemu grup, Administratorzy mogą tworzyć niestandardowe grupy lub [korzystać z zewnętrznej grupy w skojarzonych dzierżaw usługi Azure Active Directory](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group). Niestandardowe zewnętrznych grup można używać razem grup systemu w zapewniając wgląd w deweloperzy i uzyskują dostęp do tooAPI produktów. Na przykład można utworzyć jedną grupę niestandardowych dla deweloperów powiązane z konkretną organizacji partnera i zezwolić im dostępu toohello interfejsy API z produktu, zawierający tylko odpowiednich interfejsów API. Użytkownik może należeć do więcej niż jednej grupy.

Aby uzyskać więcej informacji, zobacz [jak toocreate i używania grup][How toocreate and use groups].

## <a name="developers"> </a> Deweloperzy
Deweloperzy reprezentują hello kont użytkowników w wystąpieniu usługi Zarządzanie interfejsami API. Deweloperzy mogą być tworzone lub zaproszenie toojoin przez administratorów lub można założyć z hello [portalu dla deweloperów][Developer portal]. Każdy deweloper jest członkiem co najmniej jedną grupę, a może mieć subskrypcji toohello produktów, które przyznać widoczność toothose grup.

Deweloperzy subskrypcji produktu tooa otrzymują klucza podstawowego i pomocniczego hello hello produktu. Ten klucz jest używany podczas wykonywania wywołań do interfejsów API hello produktu.

Aby uzyskać więcej informacji, zobacz [jak deweloperzy toocreate lub zaproszenia] [ How toocreate or invite developers] i [jak tooassociate grup z deweloperami][How tooassociate groups with developers].

## <a name="policies"> </a> Zasady
Zasady są zaawansowanych możliwości zarządzania interfejsu API, które umożliwia zachowanie hello toochange hello interfejsu API za pomocą konfiguracji hello wydawcy. Zasady są zbiór instrukcji, które są wykonywane sekwencyjnie na powitania żądania lub odpowiedzi interfejsu API. Popularne instrukcje zawierają Konwersja formatu od szybkości tooJSON i wywołanie XML ograniczanie toorestrict hello ilość przychodzących od dewelopera i wiele innych zasad są dostępne.

Wyrażenie zasad może służyć jako wartości atrybutu lub tekst w żadnym z zasad interfejsu API zarządzania hello, chyba że zasady hello Określa, w przeciwnym razie wartość. Niektóre zasady, takie jak hello [sterowania przepływem](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) i [zmiennej zestaw](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) zasady są oparte na wyrażeniach zasad. Aby uzyskać więcej informacji, zobacz [zaawansowane zasady](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx), i hello Obejrzyj klip wideo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

Pełna lista zasad usługi API Management znajduje się w artykule [Policy reference][Policy reference] (Dokumentacja zasad). Aby uzyskać więcej informacji na temat korzystania z zasad i konfigurowania ich, zobacz [API Management policies][API Management policies] (Zasady usługi API Management). Samouczek dotyczący tworzenia produktu z zasadami dotyczącymi ograniczania liczby wywołań i przydziałów znajduje się w artykule [Jak utworzyć i skonfigurować zaawansowane ustawienia produktów][How create and configure advanced product settings]. Aby uzyskać demonstrację Zobacz powitania po wideo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="developer-portal"> </a> Portal dla deweloperów
portalu dla deweloperów Hello jest gdzie deweloperzy mogą więcej informacji na temat interfejsów API, widok i wywołania operacji oraz subskrybować tooproducts. Potencjalni klienci mogą odwiedzać hello portalu dla deweloperów, Wyświetlanie interfejsów API i operacje i zarejestruj. adres URL Hello swojego portalu dla deweloperów znajduje się na pulpicie nawigacyjnym hello w hello portalu klasycznego Azure dla swojego wystąpienia usługi Zarządzanie interfejsami API.

Hello wyglądu i działania portalu deweloperów można dostosować, dodając niestandardowe zawartości, Dostosowywanie stylów i dodawanie znakowanie.

## <a name="api-management-and-hello-api-economy"></a>Zarządzanie interfejsami API i hello gospodarka interfejsu API
więcej informacji na temat interfejsu API zarządzania, obejrzyj hello poniższych prezentacja z konferencji hello Microsoft Ignite 2015 toolearn.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How toocreate APIs]: api-management-howto-create-apis.md
[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How toocreate or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




