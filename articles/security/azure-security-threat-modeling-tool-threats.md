---
title: "aaaThreats — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
description: "Strona kategorii zagrożenie dla narzędzia do modelowania zagrożeń Microsoft hello, zawierający kategorie dla wszystkich narażonych generowane zagrożenia."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a>Narzędzia do modelowania zagrożeń Microsoft zagrożeń

Narzędzia do modelowania zagrożeń Hello jest elementem core hello Microsoft Security Development Lifecycle (SDL). Umożliwia oprogramowania architects tooidentify i wcześnie łagodzenia potencjalnych problemów z zabezpieczeniami, jeśli są one względnie łatwe i ekonomiczne tooresolve. W związku z tym znacznie zmniejsza całkowity koszt hello rozwoju. Możemy zaprojektowany narzędzia hello z ekspertami z systemem innym niż zabezpieczeń pamiętać, ułatwiając modelowanie zagrożeń dla wszystkich deweloperów zapewniając wyraźnych wskazówek dotyczących tworzenia i analizowanie modeli zagrożeń.

> Odwiedź hello  **[narzędzie modelowania zagrożeń](./azure-security-threat-modeling-tool.md)**  tooget uruchomiony dziś!

Narzędzia do modelowania zagrożeń Hello pozwala uzyskać odpowiedzi na niektóre kwestie, takie jak hello widocznych poniżej:

* W jaki sposób atakujący zmienić hello dane uwierzytelniania
* Jaki jest wpływ hello, jeśli osoba atakująca może odczytać dane profilu użytkownika hello?
* Co się stanie w przypadku odmowy dostępu toohello bazy danych profilów użytkowników?

## <a name="stride-model"></a>STRIDE modelu

Pomoc toobetter sformułować tego rodzaju pytania wskazywany, Microsoft używa hello krok modelu, który kategoryzuje różnego rodzaju zagrożenia i upraszcza hello ogólną zabezpieczeń konwersacji.

| Kategoria | Opis |
| -------- | ----------- |
| **Fałszowanie zawartości** | Obejmuje niedozwolony sposób uzyskiwania dostępu do, a następnie użyć informacji uwierzytelniania innego użytkownika, takie jak nazwa użytkownika i hasło |
| **Manipulowanie** | Obejmuje hello złośliwego modyfikacji danych. Przykłady obejmują nieautoryzowane zmiany danych toopersistent, takim jak przechowywać w formacie bazy danych i zmiany hello danych przepływ między dwoma komputerami za pośrednictwem sieci otwarte, takich jak hello Internet |
| **Odrzucenie** | Skojarzone z użytkownikami, którzy Odmów wykonuje akcję bez innych stron, w przeciwnym razie o wszelkich tooprove sposób — na przykład użytkownik wykona niedozwolonej operacji w systemie, która nie ma hello możliwości tootrace hello zabronione operacji. Niemożność wyparcia się odwołuje się możliwość toohello zagrożeń repudiation toocounter systemu. Na przykład użytkownik, który dokonuje zakupu elementu może być toosign dla elementu powitania po otrzymaniu. dostawcy Hello może, a następnie użyj hello podpisany otrzymania jako dowód, że użytkownik hello otrzymały hello pakietu |
| **Ujawnienie informacji** | Poddanie hello tooindividuals informacje, którzy nie powinni toohave tooit dostępu — na przykład możliwość hello tooread użytkowników plików, które nie były uzyskuje dostęp do lub hello możliwości intruzów tooread przesyłane dane między dwoma komputerami |
| **Odmowa usługi** | Ataki odmowy usługi (DoS) odrzucanie usługi toovalid użytkowników — na przykład, przez co serwer sieci Web, tymczasowo niedostępna lub niezdatna do użycia. Należy włączyć ochronę przed określonymi typami systemu DoS zagrożenia po prostu tooimprove systemu dostępności i niezawodności |
| **Podniesienie uprawnień** | Nieuprawnionego użytkownika uzyskuje dostęp uprzywilejowany i tym samym ma wystarczające toocompromise dostępu lub zniszczenie hello całego systemu. Podniesienie uprawnień zagrożenia obejmują tych sytuacji, w których atakujący ma skutecznie przejścia wszystkie zabezpieczenia systemu i stają się częścią hello zaufany system, w rzeczywistości niebezpiecznych sytuacji |

## <a name="next-steps"></a>Następne kroki

Kontynuować zbyt**[środki zaradcze narzędzia do modelowania zagrożeń](./azure-security-threat-modeling-tool-mitigations.md)**  toolearn hello różne sposoby ograniczania tych zagrożeń przy użyciu platformy Azure.
