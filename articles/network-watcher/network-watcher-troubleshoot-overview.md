---
title: "Rozwiązywanie problemów w obserwatora sieciowego Azure tooresource aaaIntroduction | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie funkcji hello obserwatora sieciowego zasobów rozwiązywania problemów"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a>Rozwiązywanie problemów w obserwatora sieciowego Azure tooresource wprowadzenie

Bramy sieci wirtualnej zapewniają łączność między zasobami lokalnymi i innych sieci wirtualnych w obrębie platformy Azure. Bardzo ważne jest monitorowanie ich połączeń i te bram tooensuring komunikacja nie jest uszkodzona. Obserwatora sieciowego zapewnia hello tootroubleshoot możliwości połączenia i bramy sieci wirtualnej. Można go wywołać za pomocą portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST. Po wywołaniu obserwatora sieciowego diagnozuje hello kondycji bramy sieci wirtualnej hello lub połączenia i zwracany hello odpowiednie wyniki. To żądanie jest długo działającą transakcję, hello są zwracane po zakończeniu hello diagnostyki.

![portal][2]

## <a name="results"></a>Wyniki

Witaj wstępne wyniki zwracane nadaj ogólny obraz kondycji hello hello zasobu. Więcej informacji można podać dla zasobów pokazane na powitania następujących sekcji:

Witaj poniżej znajduje się hello wartości zwracane z hello Rozwiązywanie problemów z interfejsu API:

* **wartość startTime** — ta wartość jest czas hello hello Rozwiązywanie problemów z wywołania interfejsu API uruchomiona.
* **wartość endTime** — ta wartość jest hello czas zakończenia hello rozwiązywania problemów.
* **Kod** — ta wartość jest zła, w przypadku awarii jednego diagnostyki.
* **wyniki** -wyników jest zbiór wyników zwróconych na powitania połączenie lub hello bramy sieci wirtualnej.
    * **Identyfikator** — ta wartość jest typem błędu hello.
    * **Podsumowanie** — ta wartość jest podsumowanie hello błędów.
    * **szczegółowe** -wartość zawiera szczegółowy opis błędu hello.
    * **recommendedActions** — ta właściwość jest kolekcją tootake zalecane działania.
      * **actionText** — ta wartość zawiera hello tekst opisujący jakie tootake akcji.
      * **actionUri** — ta wartość zawiera hello URI toodocumentation tooact.
      * **actionUriText** — ta wartość jest krótki opis hello akcji tekstu.

Hello następujące tabele Pokaż hello błędów różne typy (identyfikator w obszarze wyniki z powyższej listy hello) dostępnych i jeśli błędów hello tworzy dzienniki.

### <a name="gateway"></a>Brama

| Typ błędu | Przyczyna | Log|
|---|---|---|
| NoFault | Gdy błąd nie została wykryta. |Tak|
| GatewayNotFound | Nie można odnaleźć bramy lub bramy nie jest obsługiwana administracyjnie. |Nie|
| PlannedMaintenance |  Wystąpienie bramy jest w trakcie konserwacji.  |Nie|
| UserDrivenUpdate | Gdy aktualizacja użytkownika jest w toku. Może to być operacji zmiany rozmiaru. | Nie |
| VipUnResponsive | Nie można osiągnąć hello głównej wystąpienie hello bramy. Dzieje się tak, gdy hello badania kondycji nie powiodło się. | Nie |
| PlatformInActive | Istnieje problem z platformą hello. | Nie|
| ServiceNotRunning | Usługa podstawowej Hello nie jest uruchomiona. | Nie|
| NoConnectionsFoundForGateway | Połączenia nie istnieje w bramie hello. Jest to tylko ostrzeżenie.| Nie|
| ConnectionsNotConnected | Połączenia nie są połączone. Jest to tylko ostrzeżenie.| Tak|
| GatewayCPUUsageExceeded | Bieżące użycie procesora CPU bramy Hello jest > 95%. | Tak |

### <a name="connection"></a>Połączenie

| Typ błędu | Przyczyna | Log|
|---|---|---|
| NoFault | Gdy błąd nie została wykryta. |Tak|
| GatewayNotFound | Nie można odnaleźć bramy lub bramy nie jest obsługiwana administracyjnie. |Nie|
| PlannedMaintenance | Wystąpienie bramy jest w trakcie konserwacji.  |Nie|
| UserDrivenUpdate | Gdy aktualizacja użytkownika jest w toku. Może to być operacji zmiany rozmiaru.  | Nie |
| VipUnResponsive | Nie można osiągnąć hello głównej wystąpienie hello bramy. Zdarza się, gdy hello badania kondycji nie powiodło się. | Nie |
| ConnectionEntityNotFound | Brak konfiguracji połączenia. | Nie |
| ConnectionIsMarkedDisconnected | Witaj połączenia jest oznaczony jako "odłączony". |Nie|
| ConnectionNotConfiguredOnGateway | Witaj podległej usłudze nie ma powitalne skonfigurowane połączenie. | Tak |
| ConnectionMarkedStandy | źródłowa usługa Hello jest oznaczona jako stan wstrzymania.| Tak|
| Authentication | Niezgodność klucz wstępny. | Tak|
| PeerReachability | Brama równorzędnej Hello jest nieosiągalny. | Tak|
| IkePolicyMismatch | Brama równorzędnej Hello ma zasady IKE, które nie są obsługiwane przez platformę Azure. | Tak|
| Błąd WfpParse | Wystąpił błąd podczas analizowania dziennika platformy filtrowania systemu Windows hello. |Tak|

## <a name="supported-gateway-types"></a>Obsługiwane typy bramy

Witaj Poniższa lista zawiera obsługę hello Pokazuje połączenia i bram, które są obsługiwane w rozwiązywaniu problemów obserwatora sieciowego.
|  |  |
|---------|---------|
|**Typy bramy**   |         |
|Sieć VPN      | Obsługiwane        |
|ExpressRoute | Nieobsługiwane |
|Hypernet | Nieobsługiwane|
|**Typy z siecią VPN** | |
|Na podstawie trasy | Obsługiwane|
|Na podstawie zasad | Nieobsługiwane|
|**Typy połączeń**||
|Protokół IPSec| Obsługiwane|
|VNet2Vnet| Obsługiwane|
|ExpressRoute| Nieobsługiwane|
|Hypernet| Nieobsługiwane|
|VPNClient| Nieobsługiwane|

## <a name="log-files"></a>Pliki dziennika

pliki dziennika Hello zasobów rozwiązywania problemów są przechowywane na koncie magazynu po zakończeniu rozwiązywania problemów z zasobów. Witaj poniższy obraz przedstawia zawartość przykład hello wywołanie, które spowodowało wystąpienie błędu.

![plik zip][1]

> [!NOTE]
> W niektórych przypadkach tylko podzbiór plików dzienników hello są zapisywane toostorage.

Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zobacz zbyt[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage. Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj na powitania następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)

### <a name="connectionstatstxt"></a>ConnectionStats.txt

Witaj **ConnectionStats.txt** plik zawiera ogólna Statystyka o hello połączenia, w tym Bajty przychodzące i wychodzące, stan połączenia i hello czasu hello jest nawiązane połączenie.

> [!NOTE]
> Jeśli Rozwiązywanie problemów z interfejsu API toohello wywołania hello zwraca dobrej kondycji, jest jedynym elementem hello zwrócił w pliku zip hello **ConnectionStats.txt** pliku.

Witaj zawartość tego pliku są podobne toohello poniższy przykład:

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a>CPUStats.txt

Witaj **CPUStats.txt** plik zawiera użycie procesora CPU i pamięci w czasie hello testów.  Witaj zawartość tego pliku jest toohello podobnie poniższy przykład:

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a>IKEErrors.txt

Witaj **IKEErrors.txt** plik zawiera błędy IKE, które zostały odnalezione podczas monitorowania.

Witaj poniższy przykład przedstawia hello zawartość pliku IKEErrors.txt. Błędy mogą się różnić w zależności od hello problem.

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a>Wyczyszczona wfpdiag.txt

Witaj **Scrubbed wfpdiag.txt** plik dziennika zawiera hello wfp dziennika. Ten dziennik zawiera rejestrowanie IKE/AuthIP błędy i listy pakietów.

Witaj poniższy przykład przedstawia hello zawartość pliku Scrubbed wfpdiag.txt hello. W tym przykładzie hello klucza współużytkowanego połączenia jest niepoprawny, co wynika z wiersza 3 powitania od dołu hello. Hello poniższy przykład jest po prostu fragment hello cały dziennik dziennika hello mogą być obszerne w zależności od hello problem.

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a>wfpdiag.txt.sum

Witaj **wfpdiag.txt.sum** plik jest dziennika pokazującego buforów hello i przetworzonych zdarzeń.

Witaj poniższym przykładzie jest hello zawartości pliku wfpdiag.txt.sum.
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toodiagnose bramy sieci VPN i połączeń za pośrednictwem hello portalu odwiedzając [bramy Rozwiązywanie problemów — Azure portal](network-watcher-troubleshoot-manage-portal.md).
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
