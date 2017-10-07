---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących ochrony danych | Dokumentacja firmy Microsoft"
description: "Podczas planowania rozwiązania tożsamości hybrydowej zidentyfikować hello wymagań dotyczących ochrony danych firmy i które opcje są dostępne toobest spełnia te wymagania."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>Planowanie wzmocnienia bezpieczeństwa danych za pośrednictwem rozwiązania silnej tożsamości
Hello pierwszy krok tooprotect hello danych jest określenie, kto ma dostęp do danych i w ramach tego procesu należy toohave, które rozwiązanie tożsamości, które można integruje się z systemu tooprovide uwierzytelniania i autoryzacji możliwości. Uwierzytelnianie i autoryzacja są często pomylić ze sobą i ich role błędnie interpretowane. W rzeczywistości różnią się one dość, jak pokazano na poniższej ilustracji hello:

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**Etapy cyklu życia zarządzania urządzeniami przenośnymi**

Podczas planowania rozwiązania z tożsamością hybrydową muszą zrozumieć, że hello wymagań dotyczących ochrony danych firmy i które opcje są dostępne toobest spełniają te wymagania.

> [!NOTE]
> Po zakończeniu planowania zabezpieczeń danych, przejrzyj [ustalić wymagania dotyczące uwierzytelniania wieloskładnikowego](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) tooensure opcje dotyczące wymagań usługi Multi-Factor authentication nie zostały zainfekowane przez hello decyzji można w tej sekcji.
> 
> 

## <a name="determine-data-protection-requirements"></a>Określenie wymagań dotyczących ochrony danych
W wieku hello wynikające z mobilności, w większości firm celem wspólnej: Włącz ich produktywności na swoich urządzeniach przenośnych podczas lokalnie lub zdalnie z dowolnej lokalizacji w kolejności tooincrease wydajność toobe użytkowników. Może to być typowe cel, firm, które mają takich wymagań będzie również obawy dotyczące hello ilość zagrożenia, które trzeba zminimalizować w kolejności tookeep danych firmy bezpiecznego i zadbać o zachowanie poufności użytkownika. Każda firma może mieć różne wymagania w tym zakresie; reguły zgodności różnych, które różnią się zgodnie z firmy hello branży toowhich działa będzie prowadzić toodifferent decyzje dotyczące projektu. 

Istnieją jednak niektóre zabezpieczeń aspekty, które powinny być przedstawione i zweryfikowany, niezależnie od branży hello, które opisano szczegółowo w następnej sekcji hello.

## <a name="data-protection-paths"></a>Ścieżki ochrony danych
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**Ścieżki ochrony danych**

W hello powyżej diagramu składnik tożsamości hello będzie hello pierwszy z nich toobe weryfikacji przed uzyskaniem dostępu do danych. Jednak może to być w różnych stanach w czasie hello, który był on dostępny. Każdą liczbę na tym diagramie reprezentuje ścieżkę, w którym dane można zlokalizować w pewnym momencie w czasie. Poniżej opisano te liczby:

1. Ochrona danych na poziomie urządzeń hello.
2. Ochrony danych podczas przesyłania.
3. Ochrona danych przy jednoczesnym lokalnym rest.
4. Ochrona danych magazynowanych w chmurze hello.

Mimo że hello kontroli technicznej umożliwiających IT tooprotect hello same dane o każdym z tych fazach nie są bezpośrednio oferowane przez hello rozwiązania z tożsamością hybrydową, konieczne jest rozwiązania z tożsamością hybrydową hello jest w stanie wykorzystaniu lokalnie i w chmurze tożsamości zarządzania zasobami tooidentify hello użytkownika przed Udziel dostępu toohello danych. Podczas planowania rozwiązania z tożsamością hybrydową upewnij się, że powitania po odpowiedzi na pytania zgodnie z wymaganiami organizacji tooyour:

## <a name="data-protection-at-rest"></a>Ochrona danych w stanie spoczynku
Niezależnie od tego, gdzie hello danych jest w stanie spoczynku (urządzenia, chmurze lub lokalnie) ważne jest tooperform organizacji hello toounderstand oceny musi w tym zakresie. Dla tego obszaru upewnij się prośba o tym hello następujące pytania:

* Czy firma potrzebuje tooprotect przechowywanych danych?
  * Jeśli tak, jest toointegrate możliwe rozwiązania hello hybrydowego tożsamości z bieżącej infrastruktury lokalnej?
  * Jeśli tak, jest toointegrate możliwe rozwiązania hello hybrydowego tożsamości z obciążeń znajduje się w chmurze hello?
* Jest hello chmury tożsamości zarządzania stanie tooprotect hello poświadczenia użytkownika i innych danych przechowywanych w chmurze hello?

## <a name="data-protection-in-transit"></a>Ochrona danych podczas przesyłania
Dane przesyłane między urządzeniem hello i hello centrum danych lub między hello urządzenia i w chmurze hello muszą być chronione. Jednak jest w drodze nie musi oznaczać proces komunikacji ze składnikiem poza usługi w chmurze; powoduje również przeniesienie w wewnętrznie, na przykład między dwoma sieci wirtualnych. Dla tego obszaru upewnij się prośba o tym hello następujące pytania:

* Czy firma potrzebuje tooprotect przesyłanych danych?
  * Jeśli tak, jest toointegrate możliwe rozwiązania hello hybrydowego tożsamości z bezpiecznego formanty, takie jak SSL/TLS?
* Zarządzanie tożsamościami w chmurze hello utrzymanie hello tooand ruchu w ramach hello katalogu magazynu (w ramach i między centrami danych) podpisany

## <a name="compliance"></a>Zgodność
Wymagania dotyczące zgodności z przepisami, ustawowe i przepisy różnią się zgodnie z branży toohello należącego do firmy. Przedsiębiorstwa w branży podlegającymi ochronie wysokiej musi rozwiązania zarządzania tożsamościami dotyczy toocompliance pokrewne. Przepisy, takie jak Sarbanes-Oxley (SOX), Health Insurance Portability hello i Accountability Act (HIPAA), hello Gramm-wypłukującej-Bliley Act (GLBA) i Payment Card Industry Data Security Standard (PCI DSS) hello są bardzo rygorystyczny dotyczące tożsamości i dostępu. Witaj rozwiązania z tożsamością hybrydową, która przyjmuje firmy musi mieć hello podstawowych możliwości, które będą spełniać wymagania hello co najmniej jednego z tych rozporządzeń. Dla tego obszaru upewnij się prośba o tym hello następujące pytania:

* Rozwiązania z tożsamością hybrydową hello jest zgodne z hello przepisami dotyczącymi działalności firmy?
* Czy rozwiązania z tożsamością hybrydową hello są wbudowane funkcje pozwalające z toobe zgodny z przepisami wymaganiami firmy? 

> [!NOTE]
> Upewnij się, że notatki tootake wszystkie odpowiedzi i zrozumieć hello uzasadnienie hello odpowiedzi. [Definiowanie strategii ochrony danych](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) będą przekazywane hello dostępne opcje oraz zalety/wady każdej opcji.  Po udzieleniu odpowiedzi na te pytania można wybrać opcji najlepiej pasujące do firmy wymaga.
> 
> 

## <a name="next-steps"></a>Następne kroki
 [Określenie wymagań dotyczących zarządzania zawartością](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

