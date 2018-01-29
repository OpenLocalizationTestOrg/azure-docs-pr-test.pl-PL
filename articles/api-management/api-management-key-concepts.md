---
title: "Przegląd i kluczowe pojęcia usługi Azure API Management | Microsoft Docs"
description: "Poznaj interfejsy API, produkty, role, grupy i inne ważne pojęcia dotyczące usługi API Management."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 11/15/2017
ms.author: apimpm
ms.custom: mvc
ms.openlocfilehash: 727be96828b9217f89214722f474abfc220b0b3c
ms.sourcegitcommit: 1fbaa2ccda2fb826c74755d42a31835d9d30e05f
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/22/2018
---
# <a name="what-is-api-management"></a>Co to jest API Management?

Usługa API Management (APIM) pomaga organizacjom publikować interfejsy API dla deweloperów zewnętrznych, partnerskich i wewnętrznych, aby w pełni wykorzystać potencjał danych i usług. Firmy na całym świecie dążą do rozszerzenia operacji w postaci platformy cyfrowej, tworząc nowe kanały, znajdując nowych klientów i nakłaniając obecnych do głębszego zaangażowania. Usługa API Management zapewnia podstawowe możliwości, które pozwalają na pomyślne programowanie interfejsów API przez zaangażowanych deweloperów, a także udostępnia wgląd w kwestie biznesowe, analizy, zabezpieczenia i ochronę. Usługa Azure API Management umożliwia użycie dowolnego oprogramowania zaplecza i uruchomienie opartego na nim, w pełni funkcjonalnego programu interfejsu API.

Obejrzyj poniższy film przedstawiający przegląd usługi Azure API Management i dowiedz się, jak używać usługi API Management, aby przy minimalnym nakładzie pracy dodać do interfejsu API wiele funkcji obejmujących kontrolę dostępu, ograniczanie liczby wywołań, monitorowanie, rejestrowanie zdarzeń i buforowanie odpowiedzi.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

Ten temat zawiera omówienie typowych scenariuszy dotyczących usługi APIM.  Omówiono w nim też krótko główne składniki systemu usługi APIM. W dalszej części tematu bardziej szczegółowo omówiono poszczególne składniki.

## <a name="overview"></a>Omówienie

Aby użyć usługi API Management, administratorzy tworzą interfejsy API. Każdy interfejs API składa się z co najmniej jednej operacji i można go dodać do co najmniej jednego produktu. Aby użyć interfejsu API, deweloperzy subskrybują produkt, który zawiera ten interfejs API, a następnie wywołują operację interfejsu API, która podlega obowiązującym dla niej zasadom użycia. Typowe scenariusze obejmują:

* **Zabezpieczanie infrastruktury mobilnej** przez uzyskanie dostępu bramowego z kluczami interfejsu API, zapobieganie atakom DOS przy użyciu ograniczania przepływności lub korzystanie z zaawansowanych zasad zabezpieczeń, takich jak sprawdzanie poprawności tokenu JWT.
* **Włączanie ekosystemów partnerów niezależnych dostawców oprogramowania** dzięki oferowaniu szybkiego dołączania partnerów za pośrednictwem portalu dla deweloperów i tworzeniu fasady interfejsu API w celu oddzielenia od wewnętrznych implementacji, które nie są dojrzałe do użycia przez partnera.
* **Uruchamianie wewnętrznego programu interfejsu API** dzięki oferowaniu organizacji scentralizowanej lokalizacji w celu komunikowania dostępności oraz ostatnich zmian wprowadzonych do interfejsów API, uzyskania dostępu bramowego za pomocą kont organizacyjnych, a wszystko to na podstawie zabezpieczonego kanału między bramą interfejsu API a zapleczem.

System składa się z następujących składników:

* **Brama interfejsu API** to punkt końcowy, który ma następujące zastosowania:
  
  * Przyjmowanie wywołań API i kierowanie ich do zaplecza.
  * Weryfikowanie kluczy interfejsu API, tokenów JWT, certyfikatów i innych poświadczeń.
  * Wymuszanie przydziałów użycia i ograniczeń liczby wywołań.
  * Przekształcanie interfejsu API na bieżąco, bez modyfikacji kodu.
  * Buforowanie odpowiedzi zaplecza w skonfigurowanym miejscu.
  * Rejestrowanie w dzienniku metadanych wywołań w celu analizy.
* **Portal wydawcy** to interfejs administracyjny, w którym konfiguruje się program interfejsu API. Jego zastosowania to:
  
  * Definiowanie lub importowanie schematu interfejsu API.
  * Tworzenie pakietów interfejsów API do produktów.
  * Konfigurowanie zasad, takich jak przydziały lub przekształcenia w interfejsach API.
  * Uzyskiwanie szczegółowych informacji analitycznych.
  * Zarządzanie użytkownikami.
* **Portal dla deweloperów** służy jako główna witryna internetowa dla deweloperów, która umożliwia im:
  
  * Czytanie dokumentacji interfejsu API.
  * Wypróbowanie interfejsu API za pośrednictwem interakcyjnej konsoli.
  * Tworzenie konta i subskrybowanie, aby uzyskać klucze interfejsu API.
  * Zyskanie dostępu do analiz własnego użycia.

Aby uzyskać więcej informacji, zobacz oficjalny dokument PDF [Cloud-based API Management: Harnessing the Power of APIs](http://j.mp/ms-apim-whitepaper) (Oparta na chmurze usługa API Management: wykorzystanie możliwości interfejsów API). Ten wprowadzający oficjalny dokument dotyczący usługi API Management opracowany przez firmę CITO Research obejmuje następujące tematy: 
 
 * Typowe wymagania i wyzwania związane z interfejsem API
 * Rozdzielanie interfejsów API i prezentowanie fasad
 * Szybkie rozpoczęcie pracy przez deweloperów
 * Zabezpieczanie dostępu
 * Analizy i metryki
 * Uzyskiwanie kontroli i wglądu dzięki platformie usługi API Management
 * Porównanie rozwiązań w chmurze i rozwiązań lokalnych
 * Usługa Azure API Management
 
## <a name="apis"> </a>Interfejsy API i operacje
Interfejsy API są podstawą wystąpienia usługi API Management. Każdy interfejs API reprezentuje zestaw operacji dostępnych dla deweloperów. Każdy interfejs API zawiera odwołanie do usługi zaplecza, która implementuje interfejs API, oraz mapę odwzorowań operacji interfejsu API na operacje zaimplementowane w usłudze zaplecza. Operacje usługi API Management są wysoce konfigurowalne, pozwalają na kontrolę mapowania adresu URL, parametrów zapytania i ścieżki, zawartości żądania i odpowiedzi oraz buforowanie odpowiedzi operacji. Ograniczenia liczby wywołań, przydziały i zasady ograniczeń adresów IP mogą być implementowane zarówno na poziomie interfejsu API, jak i na poziomie poszczególnych operacji.

Aby uzyskać więcej informacji, zobacz [How to create APIs][How to create APIs] (Jak utworzyć interfejsy API) i [How to add operations to an API][How to add operations to an API] (Jak dodać operacje do interfejsu API).

## <a name="products"> </a> Produkty
Produkty stanowią sposób udostępniania interfejsów API deweloperom. Produkty w usłudze API Management mają co najmniej jeden interfejs API oraz skonfigurowany tytuł, opis i warunki użytkowania. Produkty mogą być **otwarte** lub **chronione**. Produkty chronione trzeba subskrybować przed użyciem, a produkty otwarte mogą być używane bez subskrypcji. Kiedy produkt jest gotowy do użycia przez deweloperów, można go opublikować. Po opublikowaniu produktu deweloperzy mogą go wyświetlać (a w przypadku produktów chronionych również subskrybować). Zatwierdzenie subskrypcji jest konfigurowane na poziomie produktu i może wymagać zatwierdzenia przez administratora lub odbywać się automatycznie.

Grupy służą do zarządzania widocznością produktów dla deweloperów. Widoczność produktów jest przydzielana według grup, a deweloperzy mogą wyświetlać i subskrybować produkty, które są widoczne dla grup, do których należą. 

## <a name="groups"> </a> Grupy
Grupy służą do zarządzania widocznością produktów dla deweloperów. Usługa API Management ma następujące niezmienne grupy systemowe:

* **Administratorzy** — do tej grupy należą administratorzy subskrypcji platformy Azure. Administratorzy zarządzają wystąpieniami usługi API Management, tworząc interfejsy API, operacje i produkty, które są używane przez deweloperów.
* **Deweloperzy** — do tej grupy należą uwierzytelnieni użytkownicy portalu dla deweloperów. Deweloperzy to klienci, którzy tworzą aplikacje przy użyciu interfejsów API. Deweloperzy otrzymują dostęp do portalu dla deweloperów i tworzą aplikacje, które wywołują operacje interfejsów API.
* **Goście** — do tej grupy należą nieuwierzytelnieni użytkownicy portalu dla deweloperów, tacy jak potencjalni klienci odwiedzający portal dla deweloperów wystąpienia usługi API Management. Mogą mieć przyznany pewien zakres dostępu tylko do odczytu, czyli np. możliwość wyświetlania interfejsów API, ale nie ich wywoływania.

Oprócz tych grup systemowych administratorzy mogą tworzyć niestandardowe grupy lub [wykorzystać zewnętrzne grupy w skojarzonych dzierżawach usługi Azure Active Directory](api-management-howto-aad.md). Niestandardowe i zewnętrzne grupy mogą być używane razem z grupami systemowymi, zapewniając deweloperom widoczność produktów interfejsu API i dostęp do nich. Można na przykład utworzyć jedną grupę niestandardową dla deweloperów powiązanych z konkretną organizacją partnera i zezwolić im na dostęp do interfejsów API z produktów zawierających tylko odpowiednie interfejsy API. Użytkownik może należeć do więcej niż jednej grupy.

Aby uzyskać więcej informacji, zobacz [How to create and use groups][How to create and use groups] (Jak utworzyć grupy i używać ich).

## <a name="developers"> </a> Deweloperzy
Deweloperzy reprezentują konta użytkowników w wystąpieniu usługi API Management. Konta deweloperów mogą być tworzone lub dołączane na zaproszenie administratorów. Ponadto deweloperzy mogą się zarejestrować w [Portalu dla deweloperów][Developer portal]. Każdy deweloper jest członkiem jednej lub wielu grup i może subskrybować produkty, które mają przyznaną widoczność w tych grupach.

Kiedy deweloperzy subskrybują produkt, otrzymują klucz podstawowy i pomocniczy produktu. Ten klucz jest używany podczas wywołań interfejsów API produktu.

Aby uzyskać więcej informacji, zobacz [How to create or invite developers][How to create or invite developers] (Jak utworzyć i zaprosić deweloperów) i [How to associate groups with developers][How to associate groups with developers] (Jak skojarzyć grupy z deweloperami).

## <a name="policies"> </a> Zasady
Zasady są zaawansowaną możliwością usługi API Management, która pozwala wydawcy zmieniać zachowanie interfejsu API za pomocą konfiguracji. Zasady to zbiór instrukcji, które są wykonywane sekwencyjnie podczas żądania lub odpowiedzi interfejsu API. Popularne instrukcje obejmują konwersję z formatu XML na format JSON i ograniczanie liczby wywołań, aby zmniejszyć liczbę wywołań przychodzących od dewelopera. Ponadto dostępnych jest wiele innych zasad.

Wyrażenia zasad mogą służyć jako wartości atrybutów lub wartości tekstowe w dowolnej z zasad usługi API Management, o ile w zasadach nie określono inaczej. Niektóre zasady, np. [Przepływ sterowania](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) i [Ustawianie zmiennej](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable), są oparte na wyrażeniach zasad. Aby uzyskać więcej informacji, zobacz tematy [Advanced policies](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies) (Zaawansowane zasady) i [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) (Wyrażenia zasad).


Pełna lista zasad usługi API Management znajduje się w artykule [Policy reference][Policy reference] (Dokumentacja zasad). Aby uzyskać więcej informacji na temat korzystania z zasad i konfigurowania ich, zobacz [API Management policies][API Management policies] (Zasady usługi API Management). Samouczek dotyczący tworzenia produktu z zasadami dotyczącymi ograniczania liczby wywołań i przydziałów znajduje się w artykule [Jak utworzyć i skonfigurować zaawansowane ustawienia produktów][How create and configure advanced product settings].


## <a name="developer-portal"> </a> Portal dla deweloperów
Portal dla deweloperów jest miejscem, gdzie deweloperzy mogą poznawać interfejsy API, wyświetlać i wywoływać operacje oraz subskrybować produkty. Potencjalni klienci mogą odwiedzić portal dla deweloperów, wyświetlić interfejsy API i operacje oraz zarejestrować się. Adres URL do portalu dla deweloperów znajduje się na pulpicie nawigacyjnym w witrynie Azure Portal danego wystąpienia usługi API Management.

Wygląd swojego portalu dla deweloperów możesz dostosować, dodając niestandardową zawartość, dostosowując style i dodając znak marki.

## <a name="api-management-and-the-api-economy"></a>Usługa API Management i ekonomia interfejsów API

Aby dowiedzieć się więcej na temat usługi API Management, obejrzyj następującą prezentację z konferencji Microsoft Ignite 2017.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/Microsoft-Ignite-Orlando-2017/BRK2186/player]
> 
> 

## <a name="next-steps"></a>Następne kroki

Wykonaj procedury przedstawione w następującym przewodniku Szybki Start i zacznij korzystać z usługi Azure API Management:

> [!div class="nextstepaction"]
> [Tworzenie wystąpienia usługi Azure API Management](get-started-create-service-instance.md)

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How to create APIs]: api-management-howto-create-apis.md
[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: transform-api.md
[How to create or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: get-started-create-service-instance.md




