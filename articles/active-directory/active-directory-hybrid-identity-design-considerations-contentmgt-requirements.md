---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących zarządzania zawartością | Dokumentacja firmy Microsoft"
description: "Zapewnia wgląd w sposób toodetermine hello wymagania dotyczące zarządzania zawartością firmy. Zazwyczaj gdy użytkownik ma swój własny urządzenia on może być również wiele poświadczeń, które będą naprzemiennych zgodnie z toohello aplikacji, której używa. Jest ważne toodifferentiate zawartość została utworzona przy użyciu poświadczeń osobistych i hello te utworzone przy użyciu poświadczeń firmowych. Rozwiązanie tożsamości powinno być możliwe toointeract z tooprovide usługi w chmurze nie zakłóca pracy użytkownika końcowego dla toohello podczas zapewnienia prywatności i zwiększenia ochrona powitalnych przed wyciekiem danych."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a>Określenie wymagań dotyczących zarządzania zawartością dla rozwiązania z tożsamością hybrydową
Wymagania dotyczące zarządzania zawartością hello opis dla Twojej firmy może bezpośrednia decyzję wpływ na które toouse rozwiązania tożsamości hybrydowej. Z hello mnożenie wiele urządzeń i możliwości hello toobring użytkownikom ich własnych urządzeń ([BYOD](http://aka.ms/byodcg)), hello firmy muszą chronić własnych danych, ale jego również należy zachowane prywatność użytkowników. Zazwyczaj gdy użytkownik ma swój własny urządzenia on może być również wiele poświadczeń, które będą naprzemiennych zgodnie z toohello aplikacji, której używa. Jest ważne toodifferentiate zawartość została utworzona przy użyciu poświadczeń osobistych i hello te utworzone przy użyciu poświadczeń firmowych. Rozwiązanie tożsamości powinno być możliwe toointeract z tooprovide usługi w chmurze nie zakłóca pracy użytkownika końcowego dla toohello podczas zapewnienia prywatności i zwiększenia ochrona powitalnych przed wyciekiem danych. 

Rozwiązania tożsamości będzie można wykorzystywane przez różnych kontroli technicznej w zarządzania zawartością tooprovide kolejności, jak pokazano na poniższej ilustracji hello:

![](./media/hybrid-id-design-considerations/securitycontrols.png)

**Opcji zabezpieczeń, które będą wykorzystaniu systemu zarządzania tożsamościami**

Ogólnie rzecz biorąc wymagania dotyczące zarządzania zawartością będzie korzystać z systemu zarządzania tożsamościami w hello następujące obszary:

* Prywatność: identyfikacji hello użytkownika, który jest właścicielem zasobu i stosowania hello odpowiednie formanty toomaintain integralności.
* Klasyfikacja danych: zidentyfikować hello użytkownika lub grupy i poziom dostępu do obiektów tooan zgodnie z klasyfikacją tooits. 
* Ochrona wycieku danych: wyłączną odpowiedzialność za ochronę danych tooavoid wyciek kontroli bezpieczeństwa należy toointeract z hello tożsamości systemu toovalidate hello tożsamości użytkownika. To ważne jest również cel dziennik inspekcji.

> [!NOTE]
> Odczyt [klasyfikacji danych pod kątem gotowości do chmury](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) Aby uzyskać więcej informacji na temat najlepszych rozwiązań i wytyczne dotyczące klasyfikacji danych.
> 
> 

Podczas planowania rozwiązania z tożsamością hybrydową upewnij się, że powitania po odpowiedzi na pytania zgodnie z wymaganiami organizacji tooyour:

* Czy firma dysponuje kontroli bezpieczeństwa w miejscu tooenforce danych prywatności
  * Jeśli tak, te opcje zabezpieczeń będą mogli toointegrate z rozwiązania z tożsamością hybrydową hello czy tooadopt będzie?
* Czy firma korzysta klasyfikacji danych?
  * Jeśli tak, jest hello bieżącego rozwiązania stanie toointegrate z rozwiązania z tożsamością hybrydową hello czy będzie tooadopt?
* Czy firma ma obecnie wszystkie rozwiązania do wycieku danych? 
  * Jeśli tak, jest hello bieżącego rozwiązania stanie toointegrate z rozwiązania z tożsamością hybrydową hello czy będzie tooadopt?
* Czy firma potrzebuje tooaudit tooresources dostępu?
  * Jeśli tak, jakiego typu zasobów?
  * Jeśli tak, jakie informacje są niezbędne?
  * Jeśli tak, gdy dziennik inspekcji hello musi znajdować się? Lokalnie lub w chmurze hello?
* Czy firma potrzebuje tooencrypt żadnych wiadomości e-mail zawierających poufne dane (numerów PESEL, numerów kart kredytowych, itp.)?
* Czy firma potrzebuje tooencrypt wszystkie dokumenty/zawartości udostępnione zewnętrznymi partnerami biznesowymi?
* Czy firma potrzebuje tooenforce firmowych zasad na określonych rodzajów wiadomości e-mail (nie ma wszystkich odpowiedzi, nie przekazuj)?

> [!NOTE]
> Upewnij się, że notatki tootake wszystkie odpowiedzi i zrozumieć hello uzasadnienie hello odpowiedzi. [Definiowanie strategii ochrony danych](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) będą przekazywane hello dostępne opcje oraz zalety/wady każdej opcji.  Po udzieleniu odpowiedzi na te pytania można wybrać opcji najlepiej pasujące do firmy wymaga.
> 
> 

## <a name="next-steps"></a>Następne kroki
[Określenie wymagań dotyczących kontroli dostępu](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

