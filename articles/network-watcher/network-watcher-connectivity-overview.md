---
title: Ewidencjonowanie tooconnectivity aaaIntroduction obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie hello możliwości łączności obserwatora sieciowego"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Wprowadzenie tooconnectivity zaewidencjonowania obserwatora sieciowego Azure

Witaj łączności funkcja obserwatora sieciowego zapewnia toocheck możliwości hello bezpośrednie połączenie TCP z maszyny wirtualnej tooa maszynę wirtualną (VM), pełną nazwę domeny (FQDN), identyfikator URI, lub adres IPv4. Scenariusze sieci są skomplikowane, są implementowane przy użyciu grup zabezpieczeń sieci, zapór, trasy zdefiniowane przez użytkownika i zasobów udostępnianych przez platformę Azure. Złożonych konfiguracji należy trudne Rozwiązywanie problemów z łącznością. Obserwatora sieciowego pomaga skrócić hello toofind czasu i wykrywania problemów z łącznością. zwrócone wyniki Hello zapewniają wgląd w Określa, czy jest problem z łącznością tooa platformy lub problem z konfiguracją użytkownika. Można sprawdzić łączności z [PowerShell](network-watcher-connectivity-powershell.md), [interfejsu wiersza polecenia Azure](network-watcher-connectivity-cli.md), i [interfejsu API REST](network-watcher-connectivity-rest.md).

> [!IMPORTANT]
> Sprawdź łączność wymaga rozszerzenia maszyny wirtualnej `AzureNetworkWatcherExtension`. Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>Odpowiedź

Witaj w poniższej tabeli są wyświetlane właściwości hello zwracany, gdy Sprawdzanie łączności zakończył działanie.

|Właściwość  |Opis  |
|---------|---------|
|ConnectionStatus     | Stan Hello hello sprawdzenia łączności z serwerem. Wyniki są **osiągalne** i **informujący**.        |
|AvgLatencyInMs     | Średni czas oczekiwania, podczas sprawdzania łączności hello w milisekundach. (Tylko widoczne, gdy stan wyboru jest dostępny)        |
|MinLatencyInMs     | Sprawdź minimalnego opóźnienia w łączności hello w milisekundach. (Tylko widoczne, gdy stan wyboru jest dostępny)        |
|MaxLatencyInMs     | Sprawdź maksymalnego czasu oczekiwania podczas łączności hello w milisekundach. (Tylko widoczne, gdy stan wyboru jest dostępny)        |
|ProbesSent     | Liczba wysyłane podczas sprawdzania hello sondy. Wartość maksymalna to 100.        |
|ProbesFailed     | Liczbę sond, których nie powiodła się podczas sprawdzania hello. Wartość maksymalna to 100.        |
|Liczba przeskoków     | Przeskok ścieżka przeskokami z toodestination źródła.        |
|Przeskoków []. Typ     | Typ zasobu. Możliwe wartości to **źródła**, **VirtualAppliance**, **VnetLocal**, i **Internet**.        |
|Przeskoków []. Identyfikator | Unikatowy identyfikator hello przeskoku.|
|Przeskoków []. Adres | Adres IP hello przeskoku.|
|Przeskoków []. Identyfikator zasobu | ResourceID przeskoku hello Jeśli przeskoku hello jest zasobem platformy Azure. Jeśli jest zasobu internetowego, ResourceID jest **Internet**. |
|Przeskoków []. NextHopIds | Witaj Unikatowy identyfikator następnego przeskoku hello podjęte.|
|Przeskoków []. Problemy | Zbiór problemów, które wystąpiły podczas sprawdzania hello przy tym przeskoku. Jeśli nie było żadnych problemów, wartość hello jest pusta.|
|Przeskoków []. Problemy z []. Punkt początkowy | W bieżącej przeskoku hello, którym wystąpił problem. Możliwe wartości:<br/> **Liczba przychodzących** — problem jest łącze hello hello poprzedniej przeskoku toohello bieżącego przeskoku<br/>**Wychodzące** — problem jest łącze hello hello bieżącego przeskoku toohello następnego przeskoku<br/>**Lokalne** — problem jest hello bieżącego przeskoku.|
|Przeskoków []. Problemy z []. Ważność | ważność Hello wykrytego problemu hello. Możliwe wartości to **błąd** i **ostrzeżenie**. |
|Przeskoków []. Problemy z []. Typ |Typ Hello Napotkano problem. Możliwe wartości: <br/>**PROCESOR CPU**<br/>**Pamięci**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|Przeskoków []. Problemy z []. Kontekst |Szczegóły dotyczące Napotkano problem hello.|
|Przeskoków []. Problemy z []. Kontekst .key] |Klucz hello para klucz-wartość zwracana.|
|Przeskoków []. Problemy z []. Kontekst .value] |Zwracana wartość hello para klucz-wartość.|

Witaj poniżej znajduje się przykład problemu znaleziono przeskoku.

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>Typy błędów

Sprawdź łączność Hello zwraca typy błędów dotyczących połączeń hello. Witaj Poniższa tabela zawiera listę hello zwrócił bieżące typy błędów.

|Typ  |Opis  |
|---------|---------|
|Procesor CPU     | Wysokie użycie procesora CPU.       |
|Memory (Pamięć)     | Wysokie użycie pamięci.       |
|GuestFirewall     | Ruch jest zablokowany ze względu na konfigurację zapory tooa maszyny wirtualnej.        |
|DNSResolution     | Adres docelowy hello rozpoznawania nazw DNS nie powiodło się.        |
|NetworkSecurityRule    | Ruch jest blokowany przez reguły NSG (zasada jest zwracany)        |
|UserDefinedRoute|Zdefiniowane przez użytkownika tooa lub trasa systemowa to zatrzymanie ruchu. |

### <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooverify łączności tooa zasobów, odwiedzając: [Sprawdź łączność z obserwatora sieciowego Azure](network-watcher-connectivity-powershell.md).

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

