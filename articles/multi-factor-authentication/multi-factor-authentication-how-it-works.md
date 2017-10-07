---
title: "aaaAzure uwierzytelnianie wieloskładnikowe — jak działa"
description: "Uwierzytelnianie wieloskładnikowe platformy Azure ułatwia zabezpieczenie dostępu toodata i aplikacje, spełniając zapotrzebowanie na prosty proces logowania. Zawiera dodatkowe zabezpieczenia, gdyż drugiej formy uwierzytelniania i zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a>Jak działa usługa Azure Multi-Factor Authentication
zabezpieczenia Hello weryfikacji dwuetapowej znajduje się w jego warstwowego podejścia. Naruszenie wiele czynników uwierzytelniania przedstawiono istotne wyzwanie osobom atakującym. Nawet jeśli osoba atakująca zarządza toolearn hello hasło użytkownika, jest bezużyteczny bez również posiadanie hello zaufanego urządzenia. 

![Biurowego](./media/multi-factor-authentication-how-it-works/howitworks.png)

Uwierzytelnianie wieloskładnikowe platformy Azure ułatwia zabezpieczenie dostępu toodata i aplikacje, spełniając zapotrzebowanie na prosty proces logowania.  Zawiera dodatkowe zabezpieczenia, gdyż drugiej formy uwierzytelniania i zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe.


## <a name="methods-available-for-two-step-verification"></a>Dostępne metody na potrzeby weryfikacji dwuetapowej
Gdy użytkownik się zaloguje, dodatkowej weryfikacji są wysyłane toohello użytkownika.  Witaj poniżej przedstawiono listę metod, które mogą być używane dla drugiego weryfikacji.

| Metoda weryfikacji | Opis |
| --- | --- |
| Połączenie telefoniczne |Wywołanie jest umieszczany w zarejestrowany telefon użytkownika tooa. Hello użytkownik wprowadza numeru PIN, jeśli to konieczne, a następnie naciska klawisz # hello. |
| Wiadomość SMS |Wiadomość SMS są wysyłane telefon komórkowy tooa użytkownika z sześciocyfrowy kod. Witaj użytkownik wprowadza ten kod na powitania strony logowania. |
| Powiadomienie aplikacji mobilnej |Smartfon użytkownika tooa wysłaniu żądania weryfikacji. Witaj użytkownik wprowadza numeru PIN, jeśli to konieczne, a następnie wybiera **Sprawdź** na powitania aplikacji mobilnej. |
| Kod weryfikacyjny z aplikacji mobilnej |aplikacji mobilnej Hello, w którym jest uruchomiony przez użytkownika smartfon, wyświetla kod weryfikacyjny, który zmienia co 30 sekund. Użytkownik Hello hello najnowszych kodu i wprowadza ją na powitania strony logowania. |
| Tokeny OATH innej firmy | Azure aplikacji serwer Multi-Factor Authentication może być skonfigurowany tooaccept metody weryfikacji innych firm. |

Uwierzytelnianie wieloskładnikowe platformy Azure udostępnia metody weryfikacji selectable dla chmurą i z serwera. Można wybrać, które metody są dostępne dla użytkowników: połączenie telefoniczne, tekst, powiadomienie aplikacji lub kody aplikacji. Aby uzyskać więcej informacji, zobacz [metody weryfikacji počítačů, které](multi-factor-authentication-whats-next.md#selectable-verification-methods).

## <a name="next-steps"></a>Następne kroki

- Przeczytaj informacje o różnych hello [wersji i metody zużycia uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-versions-plans.md)

- Wybierz czy toodeploy usługi Azure MFA [w chmurze hello lub lokalnie](multi-factor-authentication-get-started.md)

- Odczyt odpowiada [— często zadawane pytania](multi-factor-authentication-faq.md)