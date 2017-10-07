---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących kontroli dostępu | Dokumentacja firmy Microsoft"
description: "Obejmuje hello tożsamości i identyfikowania wymagań dostępu do zasobów dla użytkowników w środowisku hybrydowym."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a>Określić wymagania dotyczące rozwiązania z tożsamością hybrydową kontroli dostępu
Projektując organizacji mogą również wykorzystać tooreview tej możliwości ich rozwiązania z tożsamością hybrydową dostępu wymagania dotyczące zasobów hello, że są one planowania toomake będzie dostępna dla użytkowników. dostęp do danych Hello granic wszystkich czterech filarach tożsamości, które są:

* Administracja
* Authentication
* Autoryzacja
* Inspekcja

obejmuje Hello sekcje, które wykonuje uwierzytelnianie i autoryzację w bardziej szczegółowe informacje, administracji i inspekcji są częścią cyklu życia tożsamości hybrydowej hello. Odczyt [określić zadań zarządzania tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) Aby uzyskać więcej informacji o tych funkcjach.

> [!NOTE]
> Odczyt [hello czterech filarach tożsamości - Identity Management w hello wieku hybrydowego IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) uzyskać więcej informacji o każdej z nich tych słupków.
> 
> 

## <a name="authentication-and-authorization"></a>Uwierzytelnianie i autoryzacja
Istnieją różne scenariusze uwierzytelniania i autoryzacji, te scenariusze będzie mieć określone wymagania, które muszą być spełnione przez rozwiązania z tożsamością hybrydową hello czy firmy hello jest tooadopt będzie. Scenariusze obejmujące tooBusiness biznesowych (B2B) komunikację można dodać dodatkowe żądania dla administratorów IT ponieważ muszą tooensure metodę uwierzytelniania i autoryzacji hello używaną przez organizację hello mogła komunikować się ze swoich partnerów biznesowych. Podczas projektowania procesu wymagania w zakresie uwierzytelniania i autoryzacji hello upewnij się, odpowiedzi na tym hello następujące pytania:

* Zostanie organizacji uwierzytelniania i autoryzacji tylko użytkownicy znajdujący się w ich tożsamości systemu zarządzania?
  * Czy jest planowane dla scenariusze B2B?
  * Jeśli tak, czy znasz już protokołów (SAML, OAuth, protokołu Kerberos, tokeny lub certyfikatów), będzie można tooconnect używane zarówno firmy?
* Rozwiązania z tożsamością hybrydową hello będą tooadopt obsługuje tych protokołów?

Inną ważną tooconsider punkt jest której zostaną umieszczone hello repozytorium uwierzytelniania, który będzie używany przez użytkowników i partnerów i toobe modelu administracyjnego hello używane. Należy wziąć pod uwagę następujące dwie opcje core hello:

* Scentralizowane: w tym hello modelu poświadczeń użytkownika, zasady i administrowanie może być scentralizowanie lokalne lub w chmurze hello.
* Hybrydowe: w tym hello modelu poświadczeń użytkownika, zasady i administrowanie będzie scentralizowanie lokalne i zreplikowanej w chmurze hello.

Model, który przyjmuje organizacji różnią się zgodnie z wymaganiami biznesowymi tootheir, ma hello tooanswer po tooidentify pytania, gdzie znajdują się system zarządzania tożsamości hello i hello toouse tryb administracyjny:

* Twoja organizacja ma obecnie Zarządzanie tożsamościami lokalnej?
  * Jeśli tak, czy jest planowana tookeep go?
  * Czy istnieją wszystkie rozporządzenia lub wymaganiami dotyczącymi zgodności czy organizacji wykonaj określają, że gdy system zarządzania tożsamościami hello powinien znajdować się?
* Twoja organizacja używa logowania jednokrotnego dla aplikacji znajdujących się lokalnie lub w chmurze hello?
  * Jeśli tak, hello przyjęcia modelu tożsamości hybrydowej wpływa na ten proces?

## <a name="access-control"></a>Kontrola dostępu
Uwierzytelnianie i autoryzacja są podstawowe elementy tooenable dostęp do toocorporate danych przez użytkownika sprawdzania poprawności, jest również toocontrol ważne hello poziom dostępu, który Ci użytkownicy będą mieć i ma poziom hello Administratorzy dostępu za pośrednictwem hello zasoby, które zarządzania. Rozwiązania z tożsamością hybrydową musi być w stanie tooprovide szczegółowego dostępu tooresources, delegowanie i kontrolę dostępu na podstawie ról. Upewnij się, odpowiedzi na tym hello następujące pytania dotyczące kontroli dostępu:

* Czy firma ma więcej niż jednego użytkownika z podwyższonym poziomem uprawnień toomanage systemu tożsamości?
  * Jeśli tak, czy każdy użytkownik musi hello poziom sam dostępu?
* Czy należy toodelegate dostępu toousers toomanage określonych zasobów firmy?
  * Jeśli tak, jak często dzieje się tak?
* Czy firma potrzebuje możliwości kontroli dostępu toointegrate między lokalnymi i w chmurze zasobów?
* Czy firma potrzebuje toolimit tooresources dostępu zgodnie z warunkami toosome?
* Czy firma dysponuje dowolnej aplikacji, która wymaga formantu niestandardowego dostęp do zasobów toosome?
  * Jeśli tak, czy aplikacje lokalizację (lokalnie lub w chmurze hello)?
  * Jeśli tak, gdzie są te docelowych zasobów (lokalnie lub w chmurze hello)?

> [!NOTE]
> Upewnij się, że notatki tootake wszystkie odpowiedzi i zrozumieć hello uzasadnienie hello odpowiedzi. [Definiowanie strategii ochrony danych](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) będą przekazywane hello dostępne opcje oraz zalety/wady każdej opcji.  Udzielenie odpowiedzi na te pytania wybierzesz opcji najlepiej odpowiadała potrzebom biznesowym użytkownika.
> 
> 

## <a name="next-steps"></a>Następne kroki
[Określenie wymagań dotyczących odpowiedzi na zdarzenia](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

