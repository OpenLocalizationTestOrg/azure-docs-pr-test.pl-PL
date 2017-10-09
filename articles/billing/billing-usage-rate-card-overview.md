---
title: "aaaAzure rozliczeń interfejsów API | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat użycia rozliczenia Azure i RateCard interfejsów API, które są używane tooprovide wgląd w informacje zużycia zasobów platformy Azure i trendów."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/18/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: b3214996cc3279f76fdc7f0dbd2059c3ae7bb15c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-billing-apis-tooprogrammatically-get-insight-into-your-azure-usage"></a>Użyj interfejsów API usługi Azure rozliczeń tooprogrammatically uzyskiwanie wglądu w wykorzystanie sieci platformy Azure
Za pomocą interfejsów API usługi Azure rozliczeń toopull danych użycia i zasobów do narzędziami analizy danych preferowany. Hello użycia zasobów platformy Azure i interfejsów API RateCard może pomóc dokładnie przewidzieć i zarządzanie nimi kosztów. Witaj interfejsy API są zaimplementowane jako dostawca zasobów i część hello interfejsów API udostępnianych przez hello Azure Resource Manager.  

## <a name="azure-invoice-download-api-preview"></a>Interfejs API pobierania faktury Azure (wersja zapoznawcza)
Raz hello [opcjonalnych zostało ukończone](billing-manage-access.md#opt-in), faktury pobierania za pomocą wersji zapoznawczej hello [API faktury](/rest/api/billing). Funkcje Hello:

* **Azure kontroli dostępu opartej na rolach** — Konfigurowanie dostępu zasad na powitania [portalu Azure](https://portal.azure.com) lub za pomocą [poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview) toospecify użytkowników lub aplikacji, które mogą uzyskać dostęp dane użycia toohello subskrypcji. Obiekty wywołujące należy użyć standardowego tokeny usługi Azure Active Directory do uwierzytelniania. Dodaj hello wywołującego tooeither hello czytnika rozliczeń, czytelnika, właścicielem lub współautorem roli tooget toohello dane użycia dostępu dla określonej subskrypcji platformy Azure.
* **Data filtrowanie** -Użyj hello `$filter` tooget parametru wszystkie faktury hello w odwrotnej kolejności chronologicznej przez hello faktury Data zakończenia okresu. 

> [!NOTE]
> Ta funkcja jest w pierwszej wersji zapoznawczej i może być zmiany niezgodne toobackward podmiotu. Obecnie nie jest dostępne dla niektórych subskrypcji oferty (EA, dostawcy usług Kryptograficznych, AIO nieobsługiwane) i platformy Azure w Niemczech.

## <a name="azure-resource-usage-api-preview"></a>Użycie zasobów platformy Azure, interfejsu API (wersja zapoznawcza)
Użyj hello Azure [API użycia zasobów](https://msdn.microsoft.com/library/azure/mt219003) tooget danych szacowany wykorzystania platformy Azure. obejmuje Hello interfejsu API:

* **Azure kontroli dostępu opartej na rolach** — Konfigurowanie dostępu zasad na powitania [portalu Azure](https://portal.azure.com) lub za pomocą [poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview) toospecify użytkowników lub aplikacji, które mogą uzyskać dostęp dane użycia toohello subskrypcji. Obiekty wywołujące należy użyć standardowego tokeny usługi Azure Active Directory do uwierzytelniania. Dodaj hello wywołującego tooeither hello czytnika rozliczeń, czytelnika, właścicielem lub współautorem roli tooget toohello dane użycia dostępu dla określonej subskrypcji platformy Azure.
* **Co godzinę lub agregacje codzienne** — wywołań można określić, czy chcą ich danych użycia usługi Azure co godzinę pakiety w ramach Agreement lub pakiety codziennie w ramach Agreement. Domyślnie Hello jest codziennie.
* **Wystąpienie metadanych (w tym tagi zasobów)** — Pobierz szczegóły na poziomie wystąpienia takich jak hello identyfikatora uri zasobu w pełni kwalifikowana (/subscriptions/ {identyfikator subskrypcji} /..), hello informacji o grupie zasobów i tagi zasobów. Te metadane pomaga w sposób niejednoznaczny i programowo przydzielenie użycia tagów hello, przypadków użycia, takich jak między ładowania.
* **Metadane zasobu** — szczegóły zasobów, takie jak nazwa licznika hello, kategoria licznika podkategorii miernika, jednostki i region zapewniają wywołującego hello lepiej zrozumieć co został wykorzystany. Naszym celem jest również terminologii metadanych zasobów tooalign hello portalu Azure, Azure użycia woluminów CSV, EA CSV, rozliczeń i inne środowiska publicznych toolet korelowania danych na środowiska.
* **Użycia dla wszystkich oferują typy** — danych użycia jest dostępna dla wszystkich oferują typy jak płatność za rzeczywiste użycie, MSDN, zobowiązania pieniężnego, środki pieniężne i atrybutów Rozszerzonych.

## <a name="azure-resource-ratecard-api-preview"></a>RateCard zasobów platformy Azure, interfejsu API (wersja zapoznawcza)
Użyj hello [interfejsu API usługi Azure Resource RateCard](https://msdn.microsoft.com/library/azure/mt219005) tooget hello listę dostępnych zasobów platformy Azure i szacowany informacje o cenach dla każdego. obejmuje Hello interfejsu API:

* **Azure kontroli dostępu opartej na rolach** — Konfigurowanie zasad dostępu na powitania [portalu Azure](https://portal.azure.com) lub za pomocą [poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview) toospecify użytkowników lub aplikacji, które mogą uzyskać dostęp toohello RateCard danych. Obiekty wywołujące należy użyć standardowego tokeny usługi Azure Active Directory do uwierzytelniania. Dodaj hello wywołującego tooeither hello czytnika, właścicielem lub współautorem roli tooget toohello dane użycia dostępu dla określonej subskrypcji platformy Azure.
* **(Nie obsługiwany EA) oferuje obsługę płatność za rzeczywiste użycie, MSDN, zobowiązań i środki pieniężne** — ten interfejs API zawiera informacje o szybkości poziomu oferty Azure.  obiekt wywołujący Hello tego interfejsu API musi upłynąć w szczegóły zasobu tooget hello oferta informacji i szybkości. Jesteśmy stawki EA tooprovide aktualnie nie, ponieważ EA oferty zostały dostosowane stawki dla rejestracji. 

## <a name="scenarios"></a>Scenariusze
Oto niektóre scenariusze hello, które są możliwe z kombinacją hello hello użycia i hello RateCard interfejsów API:

* **Azure spędzają w miesiącu hello** -miesiącach hello spędzają na użycie hello kombinację hello użycia i interfejsów API RateCard tooget lepsze wgląd w chmurze. Można analizować hello co godzinę i oszacowania zasobników codziennego użycia i opłat.
* **Konfigurowanie alertów** — hello użycia i hello tooget RateCard interfejsów API Szacowane użycie w chmurze i opłat, skonfigurować alerty oparte na zasobach lub pieniężne na podstawie.
* **Przewidywanie rachunku** — Get szacowane zużycie i w chmurze spędzają i zastosować machine learning toopredict algorytmy faktury jakie hello byłoby na końcu hello hello cyklu rozliczeniowym.
* **Wstępne zużycia koszt analizy** — Użyj toopredict RateCard API hello ile rachunku byłby przez użycie oczekiwanej w przypadku przenoszenia tooAzure Twojego obciążeń. Jeśli masz istniejące obciążenia w innych chmur lub chmur prywatnych, możesz mapować użycie z hello Azure stawki tooget spędzają lepiej oszacować platformy Azure. Dzięki temu szacowania hello toopivot możliwości oferty i porównaj oraz kontrast między typami inną ofertę hello poza płatność za rzeczywiste użycie, takie jak zobowiązań i środki pieniężne. Witaj interfejsu API umożliwia także hello możliwości toosee koszt różnice według regionu i pozwala toodo toohelp analizy warunkowej kosztów, wprowadzeniu decyzji dotyczących wdrożenia.
* **Analizy warunkowej** -
  
  * Można określić, czy jest ono więcej obciążeń ekonomicznego toorun w innym regionie lub w innej konfiguracji hello zasobów platformy Azure. Zasobów platformy Azure, które koszty mogą się różnić oparte na powitania region platformy Azure, którego używasz.
  * Można również określić, czy innego typu oferty Azure zapewnia większą szybkość na zasobów platformy Azure.
  
## <a name="partner-solutions"></a>Rozwiązania partnerskie
[Microsoft Azure użycia i Cloudyn Włącz interfejsy API RateCard tooProvide ITFM dla klientów](billing-usage-rate-card-partner-solution-cloudyn.md) opisano środowisko integracji hello oferowanych przez partnera interfejsu API Azure rozliczeń [Cloudyn](https://www.cloudyn.com/microsoft-azure/). Ten artykuł zawiera informacje o ich środowiska i zawiera wideo przedstawia sposób użycia Cloudyn i hello interfejsów API usługi Azure rozliczeń tooget wgląd w dane dotyczące wykorzystania platformy Azure danych.

[Cruiser i rozliczeń integracji interfejsu API programu Microsoft Azure w chmurze](billing-usage-rate-card-partner-solution-cloudcruiser.md) w tym artykule opisano sposób [Express Cruiser chmury Azure pakietu](http://www.cloudcruiser.com/partners/microsoft/) współpracuje bezpośrednio z portalu Windows Azure Pack (map) hello. Bezproblemowo można zarządzać zarówno hello operacyjne i finansowe aspektów hello Microsoft Azure prywatne lub hostowanej chmurze publicznej za pomocą interfejsu użytkownika.   

## <a name="next-steps"></a>Następne kroki
* Wyewidencjonuj hello przykłady kodu w witrynie GitHub:
  * [Przykładowy kod faktury interfejsu API](https://go.microsoft.com/fwlink/?linkid=845124)

  * [Przykładowy kod użycia interfejsu API](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [Przykładowy kod RateCard interfejsu API](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* Zobacz toolearn więcej informacji na temat usługi Azure Resource Manager hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). 

* Aby uzyskać więcej informacji na powitania pakiet narzędzi spędzają na potrzeby toohelp zawierają opis chmury, zobacz artykuł Gartner hello [rynku przewodnik dla narzędzi IT zarządzanie finansowe (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

