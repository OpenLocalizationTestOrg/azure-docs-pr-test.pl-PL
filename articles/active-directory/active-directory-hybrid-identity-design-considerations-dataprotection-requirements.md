---
title: "Azure Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących ochrony danych | Dokumentacja firmy Microsoft"
description: "Podczas planowania rozwiązania z tożsamością hybrydową, określenie wymagań dotyczących ochrony danych firmy i które opcje są dostępne do najlepiej spełnia te wymagania."
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
ms.openlocfilehash: 96bf9d4c26a22f718c29804c11681199e775f589
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>Planowanie wzmocnienia bezpieczeństwa danych za pośrednictwem rozwiązania silnej tożsamości
Pierwszy krok w celu ochrony danych jest określenie, kto ma dostęp do danych i w ramach tego procesu, musisz mieć tożsamości rozwiązania, które można integruje się z systemu w celu zapewnienia funkcji uwierzytelniania i autoryzacji. Uwierzytelnianie i autoryzacja są często pomylić ze sobą i ich role błędnie interpretowane. W rzeczywistości różnią się one dość, jak pokazano na poniższej ilustracji:

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**Etapy cyklu życia zarządzania urządzeniami przenośnymi**

Podczas planowania rozwiązania z tożsamością hybrydową muszą zrozumieć wymagania dotyczące ochrony danych firmy i które opcje są dostępne do najlepiej spełnia te wymagania.

> [!NOTE]
> Po zakończeniu planowania zabezpieczeń danych, przejrzyj [ustalić wymagania dotyczące uwierzytelniania wieloskładnikowego](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) zapewnienie nie zostały wybrane opcje dotyczące wymagań uwierzytelnianie wieloskładnikowe dotyczy decyzje możesz wprowadzone w tej sekcji.
> 
> 

## <a name="determine-data-protection-requirements"></a>Określenie wymagań dotyczących ochrony danych
W wieku mobilności w większości firm celem wspólnej: umożliwianie użytkownikom produktywność na swoich urządzeniach przenośnych podczas lokalnie lub zdalnie z dowolnego miejsca w celu zwiększenia wydajności. Może to być typowe cel, firm, które mają takich wymagań będzie również obawy dotyczące ilości zagrożenia, które musi zostać skorygowane Aby chronić dane firmy i zadbać o zachowanie poufności użytkownika. Każda firma może mieć różne wymagania w tym zakresie; reguły zgodności różnych, które różnią się w zależności od branży, którym działa firma doprowadzi do decyzji dotyczących projektowania. 

Istnieją jednak niektóre zabezpieczeń aspekty, które powinny być przedstawione i zweryfikowany, niezależnie od branży, które opisano szczegółowo w następnej sekcji.

## <a name="data-protection-paths"></a>Ścieżki ochrony danych
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**Ścieżki ochrony danych**

Na powyższym diagramie składnik tożsamości będzie pierwsza z nich należy zweryfikować przed uzyskaniem dostępu do danych. Jednak może to być w różnych stanach czasie, gdy był on dostępny. Każdą liczbę na tym diagramie reprezentuje ścieżkę, w którym dane można zlokalizować w pewnym momencie w czasie. Poniżej opisano te liczby:

1. Ochrona danych na poziomie urządzeń.
2. Ochrony danych podczas przesyłania.
3. Ochrona danych przy jednoczesnym lokalnym rest.
4. Ochrona danych magazynowanych w chmurze.

Mimo że techniczne Określa, że będzie Włącz IT, aby chronić dane o każdym z tych fazach nie są bezpośrednio oferowane przez rozwiązania z tożsamością hybrydową, konieczne jest, że rozwiązania z tożsamością hybrydową jest w stanie wykorzystaniu lokalnie i w chmurze Zasoby dotyczące zarządzania tożsamością do identyfikowania użytkownika przed udzielać dostępu do danych. Podczas planowania rozwiązania z tożsamością hybrydową upewnij się, że zgodnie z wymaganiami organizacji są odpowiedzieć na następujące pytania:

## <a name="data-protection-at-rest"></a>Ochrona danych w stanie spoczynku
Niezależnie od tego, gdzie dane są magazynowane (urządzenia, chmurze lub lokalnie) ważne jest przeprowadzenie oceny zrozumienie potrzeb organizacji w tym zakresie. Dla tego obszaru upewnij się, że prośba o następujące kwestie:

* Czy firma potrzebuje do ochrony danych magazynowanych?
  * Jeśli tak, to rozwiązania z tożsamością hybrydową można zintegrować z bieżącej infrastruktury lokalnej?
  * Jeśli tak, to rozwiązania z tożsamością hybrydową można zintegrować z obciążeń znajdujących się w chmurze?
* Zarządzanie tożsamościami w chmurze jest w stanie chronić poświadczenia użytkownika i inne dane przechowywane w chmurze?

## <a name="data-protection-in-transit"></a>Ochrona danych podczas przesyłania
Należy chronić dane przesyłane między urządzeniem i centrum danych lub między urządzeniem i chmurą. Jednak jest w drodze nie musi oznaczać proces komunikacji ze składnikiem poza usługi w chmurze; powoduje również przeniesienie w wewnętrznie, na przykład między dwoma sieci wirtualnych. Dla tego obszaru upewnij się, że prośba o następujące kwestie:

* Czy firma potrzebuje do ochrony przesyłanych danych?
  * Jeśli tak, jest możliwość integracji z bezpiecznego formanty, takie jak SSL/TLS rozwiązania z tożsamością hybrydową?
* Zarządzanie tożsamościami w chmurze zachować ruch do i w magazynie katalogu (w ramach i między centrami danych) podpisany?

## <a name="compliance"></a>Zgodność
Wymagania dotyczące zgodności z przepisami, ustawowe i wykonawcze różny w zależności od branży, należącego do firmy. Przedsiębiorstwa w branży podlegającymi ochronie wysokiej muszą spełnić Zarządzanie tożsamościami kwestie związane z problemów ze zgodnością. Przepisy, takie jak Sarbanes-Oxley (SOX), kondycji Insurance Portability and Accountability Act (HIPAA), Gramm-wypłukującej-Bliley Act (GLBA) i Payment Card Industry Data zabezpieczeń Standard (PCI DSS) jest bardzo rygorystyczny tożsamościami i dostępem. Rozwiązania z tożsamością hybrydową, która przyjmuje firmy musi mieć podstawowych możliwości, które będą spełniać wymagania co najmniej jednego z tych rozporządzeń. Dla tego obszaru upewnij się, że prośba o następujące kwestie:

* Rozwiązania z tożsamością hybrydową jest zgodne z wymogami przepisów dla Twojej firmy?
* Rozwiązania z tożsamością hybrydową ma wbudowane funkcje pozwalające być zgodny z przepisami dotyczącymi działalności firmy? 

> [!NOTE]
> Upewnij się zanotować wszystkie odpowiedzi i zrozumieć ich uzasadnienie. [Definiowanie strategii ochrony danych](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) będą przekazywane dostępne opcje oraz zalety/wady każdej opcji.  Po udzieleniu odpowiedzi na te pytania można wybrać opcji najlepiej pasujące do firmy wymaga.
> 
> 

## <a name="next-steps"></a>Następne kroki
 [Określenie wymagań dotyczących zarządzania zawartością](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

