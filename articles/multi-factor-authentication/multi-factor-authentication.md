---
title: "aaaLearn o weryfikacji dwuetapowej w usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Co to jest usługa Azure Multi-Factor Authentication, dlaczego warto używać usługi MFA, więcej informacji na temat powitania klienta uwierzytelniania wieloskładnikowego i hello różnych metod i wersje dostępne. "
keywords: "tooMFA wprowadzenie omówienie uwierzytelniania mfa, co to jest usługa mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a>Co to jest usługa Multi-Factor Authentication platformy Azure?
Weryfikacja dwuetapowa to metoda uwierzytelniania, która wymaga więcej niż jednej metody weryfikacji i dodaje kluczową drugą warstwę logowania toouser zabezpieczeń i transakcji. Działania, gdyż dowolne dwa lub więcej hello następujące metody weryfikacji:

* Coś znasz (zwykle hasła)
* Coś (zaufanych urządzeń, który nie jest łatwo zduplikowany, takich jak telefon)
* Coś jest (biometria)

<center>![Nazwa użytkownika i hasło](./media/multi-factor-authentication/pword.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![certyfikaty](./media/multi-factor-authentication/phone.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![Inteligentne Phone](./media/multi-factor-authentication/hware.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![kart inteligentnych](./media/multi-factor-authentication/smart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![Wirtualnej karty inteligentnej](./media/multi-factor-authentication/vsmart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![nazwy użytkownika i Hasło](./media/multi-factor-authentication/cert.png)</center>

Azure Multi-Factor Authentication (MFA) to rozwiązanie firmy Microsoft służące do przeprowadzania weryfikacji dwuetapowej. Usługa Azure MFA ułatwia zabezpieczenie dostępu toodata i aplikacje spełniając zapotrzebowanie na prosty proces logowania. Oferuje ona silne uwierzytelnianie za pośrednictwem różnych metod weryfikacji, w tym weryfikacji w trakcie rozmowy telefonicznej albo przy użyciu wiadomości SMS lub aplikacji mobilnej.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a>Dlaczego warto używać usługi Azure Multi-Factor Authentication?
Już dziś, więcej niż kiedykolwiek osoby coraz są połączone. W przypadku inteligentne telefony, tablety, komputery przenośne i komputery osoby mają różne sposoby na sposób będą tooconnect i łączność w dowolnym momencie. Osoby mogą uzyskać dostęp do swoich kont i aplikacji z dowolnego miejsca, co oznacza, że można więcej pracy i obsługi klientów lepiej.

Uwierzytelnianie wieloskładnikowe platformy Azure jest łatwe toouse, skalowalnych i niezawodne rozwiązanie zapewnia druga metoda uwierzytelniania, dlatego użytkownicy są chronione przez cały czas.

| ![Łatwe tooUse](./media/multi-factor-authentication/simple.png) | ![Skalowalność](./media/multi-factor-authentication/scalable.png) | ![Chronione przez cały czas](./media/multi-factor-authentication/protected.png) | ![Niezawodne](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **Łatwe toouse** |**Skalowalne** |**Chronione przez cały czas** |**Niezawodne** |

* **Łatwe tooUse** -Azure Multi-Factor Authentication jest proste tooset się i używania. Witaj dodatkowej ochrony dołączanego do usługi Azure Multi-Factor Authentication umożliwia toomanage użytkowników ich własnych urządzeniach. Najlepsze, w wielu przypadkach go można skonfigurować kilka prostych kliknięć.
* **Skalowalne** — uwierzytelnianie wieloskładnikowe Azure korzysta z możliwości hello hello w chmurze i integruje się z lokalnymi AD i aplikacji niestandardowych. Ta ochrona jest nawet rozszerzony tooyour dużych, kluczowych scenariuszy.
* **Chronione przez cały czas** -Azure Multi-Factor Authentication udostępnia silnego uwierzytelniania za pomocą hello najwyższymi standardami branżowymi.
* **Niezawodne** -gwarantujemy dostępność 99,9% Azure Multi-Factor Authentication. Hello usługa jest uznawana za niedostępną gdy nie jest w stanie tooreceive lub proces weryfikacji żądania hello weryfikacji dwuetapowej.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [jak działa usługa Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md)

- Przeczytaj informacje o różnych hello [wersji i metody zużycia uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-versions-plans.md)
