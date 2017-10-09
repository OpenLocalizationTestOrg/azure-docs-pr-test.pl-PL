---
title: "Rejestrowanie tooflow aaaIntroduction dla grup zabezpieczeń sieci z obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono sposób przepływu NSG toouse rejestrowania funkcji Azure obserwatora sieciowego"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a>Rejestrowanie tooflow wprowadzenie dla grup zabezpieczeń sieci

Dzienniki przepływu sieciowej grupy zabezpieczeń są funkcją obserwatora sieciowego, który pozwala tooview informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci. Te dzienniki przepływu są zapisywane w formacie json i Pokaż wychodzących i przepływów przychodzących na podstawie reguł na, hello przepływu hello kart stosuje, 5-elementowej informacji o przepływie hello (źródłowego i docelowego adresu IP, portu źródłowego i docelowego Protocol), a jeśli hello ruchu jest dozwolone, lub Odmowa dostępu.

![Przegląd dzienników przepływu][1]

Podczas przepływu rejestruje grup zabezpieczeń sieci docelowej, nie są wyświetlane hello takie same jak hello inne dzienniki. Przepływ dzienniki są przechowywane tylko w ramach konta magazynu i następująca ścieżka rejestrowania hello, jak pokazano w hello poniższy przykład:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Witaj takie same zasady przechowywania, jak pokazano na inne dzienniki zastosować tooflow dzienników. Dzienniki ma zasady przechowywania, które można ustawić dni too365 1 dzień. Jeśli zasady przechowywania nie jest ustawiona, dzienniki hello są obsługiwane w nieskończoność.

## <a name="log-file"></a>Plik dziennika

Dzienniki przepływu ma wiele właściwości. Witaj poniżej znajduje się lista właściwości hello, które są zwracane w dzienniku przepływu NSG hello:

* **czas** — jest to czas, gdy hello zdarzenia
* **systemId** — identyfikator zasobu grupy zabezpieczeń sieci.
* **Kategoria** -hello kategorii zdarzenia hello to jest zawsze być NetworkSecurityGroupFlowEvent
* **RESOURCEID** — Witaj identyfikator hello NSG zasobu
* **operationName** -zawsze NetworkSecurityGroupFlowEvents
* **właściwości** -zbiór właściwości hello przepływu
    * **Wersja** — numer wersji schematu programu hello przepływu dziennika zdarzeń
    * **przepływy** -kolekcji przepływów. Ta właściwość ma wiele pozycji dla różnych zasad
        * **Reguła** -reguły, które hello są wyświetlane przepływów
            * **przepływy** -kolekcji przepływów
                * **Mac** — Witaj hello karty Sieciowej dla maszyny Wirtualnej, w których zebrano przepływu hello hello adres MAC
                * **flowTuples** — ciąg, który zawiera wiele właściwości krotki przepływu hello w formacie rozdzielone przecinkami
                    * **Sygnatury czasu** — ta wartość jest sygnaturę czasową hello hello przepływu problemu w formacie epoka systemu UNIX.
                    * **Źródłowy adres IP** — Witaj źródłowy adres IP
                    * **Docelowy IP** — Witaj docelowy adres IP
                    * **Port źródłowy** — Witaj port źródłowy
                    * **Port docelowy** — Witaj Port docelowy
                    * **Protokół** — Witaj protokołu hello przepływu. Prawidłowe wartości to **T** dla protokołu TCP i **U** UDP
                    * **Przepływu ruchu** — Witaj kierunek przepływu ruchu hello. Prawidłowe wartości to **I** dla ruchu przychodzącego i **O** dla ruchu wychodzącego.
                    * **Ruch** — czy też odmówiono ruchu. Prawidłowe wartości to **A** dla dozwolone i **D** dla odmowa.


następujące Hello jest przykładem dziennika przepływu. Jak widać, że nie ma wiele rekordów, które należy wykonać opisane w powyższej sekcji hello listę właściwości hello. 

> [!NOTE]
> Wartości właściwości flowTuples hello są listę rozdzielaną przecinkami.
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooenable przepływu logowania po przejściu na stronę [przepływ włączenie rejestrowania](network-watcher-nsg-flow-logging-portal.md).

Więcej informacji na temat rejestrowania NSG, odwiedzając [dziennika analizy grup zabezpieczeń sieci (NSG)](../virtual-network/virtual-network-nsg-manage-log.md).

Dowiedzieć się, jeśli ruch jest dozwolony lub zabroniony na maszynie Wirtualnej, odwiedzając [Sprawdź, sprawdź, czy ruch z przepływem IP](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

