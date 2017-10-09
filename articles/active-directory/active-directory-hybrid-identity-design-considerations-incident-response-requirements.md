---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących zdarzenia rResponse | Dokumentacja firmy Microsoft"
description: "Określić możliwości monitorowania i raportowania dla hello rozwiązania z tożsamością hybrydową, które mogą zostać wykorzystane przez tooidentify akcje tootake IT i ograniczyć potencjalne zagrożenia"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a>Określenie wymagań dotyczących odpowiedzi na zdarzenia dla rozwiązania z tożsamością hybrydową
Duża lub średnich firmach najprawdopodobniej będzie mieć [odpowiedzi na zdarzenia zabezpieczeń](https://technet.microsoft.com/library/cc700825.aspx) w miejscu toohelp IT podjąć działania w związku z tym toohello poziom zdarzenia. system zarządzania tożsamościami Hello jest ważne składnika w procesie odpowiedzi na zdarzenia hello może być używane toohelp identyfikujący, kto wykonał określonej akcji przed hello docelowej. rozwiązania z tożsamością hybrydową Hello musi być możliwe tooprovide funkcje, które mogą zostać wykorzystane przez tooidentify akcje tootake IT i ograniczyć potencjalne zagrożenie monitorowania i raportowania. W planie odpowiedzi na typowe zdarzenia mają następujące etapy jako część planu hello hello:

1. Ocena początkowej.
2. Komunikat zdarzenia.
3. Formant uszkodzenia i zmniejszenia ryzyka.
4. Identyfikacja, co było naruszenia i ważności.
5. Dowód konserwacji.
6. Strony tooappropriate powiadomień.
7. Odzyskiwania systemu.
8. Dokumentacja.
9. Ocena uszkodzenia, a jego kosztem.
10. Proces i plan korekty.

Podczas identyfikacji hello jakie naruszenia i ważności fazy, będzie konieczne tooidentify hello systemów, które zostały naruszone, pliki, które uzyskiwały zostały i określenie czułości hello tych plików. Systemu tożsamości hybrydowej powinno być możliwe toofulfill tooassist tych wymagań należy identyfikowanie hello użytkownik, który wprowadził zmiany. 

## <a name="monitoring-and-reporting"></a>Monitorowanie i raportowanie
System obsługi tożsamości hello wiele razy może również pomóc w fazie oceny początkowej głównie w przypadku, jeśli hello system są wbudowane inspekcji i funkcje raportowania. Podczas oceny początkowej hello administrator IT musi być możliwe tooidentify podejrzanego działania lub hello system powinien być tootrigger stanie, który go automatycznie na podstawie wstępnie skonfigurowane zadania. Wiele działań może wskazywać na atak możliwe, jednak w innych przypadkach nieprawidłowo skonfigurowany system może prowadzić tooa liczbę fałszywych alarmów systemu wykrywania nieautoryzowanego dostępu. 

system zarządzania tożsamościami Hello powinna pomagać tooidentify Administratorzy IT i raportu tych podejrzanych działań. Zazwyczaj te wymagania techniczne mogą być spełnione przez monitorowanie wszystkich systemów i o możliwości raportowania, który można wyróżnić potencjalne zagrożenia. Użycie tych pytań hello poniżej toohelp zaprojektowanie rozwiązania hybrydowe tożsamości, biorąc pod uwagę wymagania odpowiedzi na zdarzenia:

* Czy firma występują odpowiedzi na zdarzenia zabezpieczeń w miejscu?
  * Jeśli tak, hello obecnym systemie zarządzania tożsamościami służy jako część procesu hello?
* Czy firma potrzebuje liczba prób logowania jednokrotnego podejrzanych użytkowników tooidentify wielu różnych urządzeniach
* Czy firma potrzebuje toodetect potencjalnych przejęciem poświadczeń użytkownika?
* Czy firma potrzebuje dostępu i akcji tooaudit użytkownika?
* Czy firma potrzebuje tooknow, gdy użytkownik resetowania jego hasła?

## <a name="policy-enforcement"></a>Wymuszanie zasad
Podczas fazy zmniejszenie ryzyka i kontroli uszkodzenia ważne jest tooquickly zmniejszyć hello rzeczywistych i potencjalnych skutków ataku. Ta akcja, która spowoduje przejście na tym etapie wprowadzić hello różnica między pomocnicze i głównych jeden. Dokładna reakcja Hello będzie zależeć od organizacji i hello rodzaj atak powitania, którego czoła. Jeśli oceny początkowej hello zawarte, czy konto zostało naruszone, konieczne będzie tooblock zasad tooenforce tego konta. To tylko jeden przykład, w którym skorzystać system zarządzania hello tożsamości. Użycie tych pytań hello poniżej toohelp Projektowanie rozwiązania z tożsamością hybrydową wymuszane biorąc pod uwagę, jak zasady będą tooreact tooan trwającą zdarzenia:

* Czy firma dysponuje zasady w miejscu tooblock użytkownikom dostępu do sieci hello w razie potrzeby?
  * Jeśli tak, czy bieżące rozwiązanie hello można zintegrować z systemu zarządzania tożsamości hybrydowej hello czy będzie tooadopt?
* Czy firma musi tooenforce dostępu warunkowego dla użytkowników, którzy są w kwarantannie 

> [!NOTE]
> Upewnij się, że notatki tootake wszystkie odpowiedzi i zrozumieć hello uzasadnienie hello odpowiedzi. [Definiowanie strategii ochrony danych](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) będą przekazywane hello dostępne opcje oraz zalety/wady każdej opcji.  Po udzieleniu odpowiedzi na te pytania można wybrać opcji najlepiej pasujące do firmy wymaga.
> 
> 

## <a name="next-steps"></a>Następne kroki
[Definiowanie strategii ochrony danych](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

