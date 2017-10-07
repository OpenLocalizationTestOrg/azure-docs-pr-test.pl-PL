---
title: "aaaMitigations — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
description: "Strona środki zaradcze dla hello narzędzia do modelowania zagrożeń Microsoft wyróżnienia możliwych rozwiązań toohello najbardziej widoczne wygenerowana zagrożeń."
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
ms.openlocfilehash: 000c0980d976b09fc9287e582e3776efaf7e390c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-mitigations"></a>Środki zaradcze narzędzie modelowania zagrożeń firmy Microsoft

Narzędzia do modelowania zagrożeń Hello jest elementem core hello Microsoft Security Development Lifecycle (SDL). Umożliwia oprogramowania architects tooidentify i wcześnie łagodzenia potencjalnych problemów z zabezpieczeniami, jeśli są one względnie łatwe i ekonomiczne tooresolve. W związku z tym znacznie zmniejsza całkowity koszt hello rozwoju. Możemy zaprojektowany narzędzia hello z ekspertami z systemem innym niż zabezpieczeń pamiętać, ułatwiając modelowanie zagrożeń dla wszystkich deweloperów zapewniając wyraźnych wskazówek dotyczących tworzenia i analizowanie modeli zagrożeń.

Odwiedź hello  **[narzędzie modelowania zagrożeń](./azure-security-threat-modeling-tool.md)**  tooget uruchomiony dziś!

## <a name="mitigation-categories"></a>Środki zaradcze kategorii

środki zaradcze narzędzie modelowania zagrożeń Hello są podzielone według toohello ramki zabezpieczeń aplikacji sieci Web, która składa się z następujących hello:

| Kategoria | Opis |
| -------- | ----------- |
| **[Inspekcja i rejestrowanie](./azure-security-threat-modeling-tool-auditing-and-logging.md)** | Czy kto, co i kiedy? Zobacz inspekcji i rejestrowanie toohow zdarzeń związanych z zabezpieczeniami rekordów aplikacji |
| **[Uwierzytelnianie](./azure-security-threat-modeling-tool-authentication.md)** | Kim jesteś? Uwierzytelnianie to proces hello jednostki, w przypadku gdy okaże się tożsamości hello innego podmiotu, zwykle za pomocą poświadczeń, takie jak nazwa użytkownika i hasło |
| **[Autoryzacji](./azure-security-threat-modeling-tool-authorization.md)** | Co należy zrobić? Autoryzacja jest jak aplikacja udostępnia kontroli dostępu do zasobów i operacje |
| **[Zabezpieczenia komunikacji](./azure-security-threat-modeling-tool-communication-security.md)** | Kto należy mówimy do Zabezpieczenia komunikacji gwarantuje, że cała komunikacja wykonywane jest należycie zabezpieczone |
| **[Zarządzanie konfiguracją](./azure-security-threat-modeling-tool-configuration-management.md)** | Kto czy aplikacja działa jako? Które bazy danych łączy go z? Jak jest zarządzany aplikacji? Jak są zabezpieczone tych ustawień? Zarządzanie konfiguracją odwołuje się toohow aplikacji obsługuje te problemy z działaniem |
| **[Kryptografia](./azure-security-threat-modeling-tool-cryptography.md)** | Jak są przechowywanie kluczy tajnych (poufność)? Jak czy sprawdzające manipulacji danymi lub biblioteki (integralność)? Jak należy podaje ziarna dla losowych wartości, które muszą być silną kryptograficznie? Kryptografia odwołuje się toohow aplikacja wymusza poufność i integralność |
| **[Zarządzanie wyjątkami](./azure-security-threat-modeling-tool-exception-management.md)** | Po wywołaniu metody w aplikacji nie powiedzie się, czego aplikacji? Ile ujawnieniem? Czy powrócisz przyjazną błąd informacji tooend użytkowników? Czy należy przekazać wyjątek cenne informacje wstecz toohello wywołującego Aplikacja powiedzie bezpiecznie zamknąć? |
| **[Sprawdzania poprawności danych wejściowych](./azure-security-threat-modeling-tool-input-validation.md)** | Jak sprawdzić, czy dane wejściowe hello, którą otrzymuje aplikacji jest prawidłowy i bezpieczny? Sprawdzania poprawności danych wejściowych odwołuje się toohow aplikacji filtry, scrubs lub odrzucenia danych wejściowych przed dodatkowego przetwarzania. Należy wziąć pod uwagę ograniczający dane wejściowe za pośrednictwem punktów wejścia i kodowanie danych wyjściowych przez punkty wyjścia. Czy można ufać danych ze źródeł, takich jak bazy danych i udziałów plików |
| **[Dane poufne](./azure-security-threat-modeling-tool-sensitive-data.md)** | Jak aplikacja obsługuje poufnych danych? Poufnych danych odwołuje się toohow aplikacji obsługuje dowolne dane, które muszą być chronione w pamięci, za pośrednictwem sieci hello, lub w magazynach trwałych |
| **[Zarządzanie sesjami](./azure-security-threat-modeling-tool-session-management.md)** | Jak aplikacji obsługi i chronić sesje użytkowników? Sesja odwołuje się tooa serii powiązane interakcje między użytkownikiem i aplikacji sieci Web |

Dzięki temu można zidentyfikować:

* Gdzie są hello najbardziej typowych pomyłek popełnianych
* Gdzie są hello ulepszenia najbardziej przydatnych wyników

W związku z tym używać tych kategorii toofocus oraz ustalić ich priorytety służbowy zabezpieczeń, tak, że jeśli wiadomo, że występują hello najczęstszych problemów z zabezpieczeniami w hello wejściowych kategorii sprawdzania poprawności, uwierzytelniania i autoryzacji, możesz uruchomić istnieje. Aby uzyskać więcej informacji można znaleźć  **[to łącze patentowe](https://www.google.com/patents/US7818788)**

## <a name="next-steps"></a>Następne kroki

Odwiedź  **[zagrożenia narzędzia do modelowania zagrożeń](./azure-security-threat-modeling-tool-threats.md)**  toolearn więcej na temat hello zagrożeń narzędzie hello kategorii używa toogenerate projektu możliwe zagrożenia.
