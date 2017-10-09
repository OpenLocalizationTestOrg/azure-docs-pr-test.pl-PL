---
title: "aaaTroubleshoot Brama sieci wirtualnej platformy Azure i połączeń - PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toouse hello Azure obserwatora sieciowego Rozwiązywanie problemów z polecenia cmdlet programu PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Rozwiązywanie problemów z Brama sieci wirtualnej i połączeń przy użyciu programu PowerShell obserwatora sieci platformy Azure

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [Interfejs API REST](network-watcher-troubleshoot-manage-rest.md)

Obserwatora sieciowego zawiera wiele funkcji, co wiąże toounderstanding zasobów sieciowych na platformie Azure. Jeden z tych funkcji jest zasobem rozwiązywania problemów. Rozwiązywanie problemów z zasobów można wywołać za pomocą portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST. Po wywołaniu, obserwatora sieciowego sprawdza kondycję hello Brama sieci wirtualnej lub połączenie i zwraca jego wyniki.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.

Lista odwiedziny typy obsługiwanych bramy [bramy obsługiwane typy](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Omówienie

Rozwiązywanie problemów z zasobów umożliwia określenie hello rozwiązywania problemów, które wynikają z bramy sieci wirtualnej i połączenia. Po wysłaniu żądania jest rozwiązywanie problemów z tooresource, dzienniki są proszeni i inspekcji. Po zakończeniu kontroli hello są zwracane. Zasób, którego rozwiązywania problemów z żądania to długo działające żądania, może to potrwać kilka minut tooreturn wynik. Dzienniki Hello z Rozwiązywanie problemów z są przechowywane w kontenerze na koncie magazynu, który jest określony.

## <a name="troubleshoot-a-gateway-or-connection"></a>Rozwiązywanie problemów z bramy i połączenie

1. Przejdź toohello [portalu Azure](https://portal.azure.com) i kliknij przycisk **sieci** > **obserwatora sieciowego** > **diagnostyki sieci VPN**
2. Wybierz **subskrypcji**, **grupy zasobów**, i **lokalizacji**.
3. Rozwiązywanie problemów z zasobów zwraca dane dotyczące kondycji hello hello zasobu. Zapisuje konta magazynu tooa odpowiednich dzienniki toobe sprawdzone. Kliknij przycisk **konta magazynu** tooselect konta magazynu.
4. Na powitania **kont magazynu** bloku, wybrać istniejące konto magazynu, lub kliknij przycisk **+ konto magazynu** toocreate nowy.
5. Na powitania **kontenery** bloku, wybierz istniejącego kontenera, lub kliknij przycisk **+ kontener** toocreate nowego kontenera. Po zakończeniu kliknij przycisk **wybierz**
6. Wybierz hello bramy i połączenie tootroubleshoot zasobów, a następnie kliknij przycisk **Uruchom Rozwiązywanie problemów**

Jeśli wybrano wiele zasobów, rozwiązywania problemów jest uruchamiane jednocześnie zasobów bramy. Nie można uruchomić na połączenie i związany z bramą w hello tym samym czasie. Zalecane jest bram tootroubleshoot najpierw Rozwiązywanie problemów z połączenia jest procesem dłużej. Podczas diagnostyki sieci VPN jest uruchomiona na powitania zasobów **rozwiązywania problemów stanu** będzie stan kolumny **uruchomiona**

Po zakończeniu hello zmiany stanu kolumny zbyt**dobra kondycja** lub **niezdrowego**.

![Rozwiązywanie problemów ukończone][2]

## <a name="understanding-hello-results"></a>Opis wyników hello

W hello **szczegóły** sekcji okna hello hello **stan** karcie są wyświetlane hello stan ostatniego rozwiązywania hello wykonywania hello wybrane zasobu. Wyniki diagnostyki najnowsze hello są wyświetlane xx minut po hello ostatniego uruchomienia.

|Właściwość  |Opis  |
|---------|---------|
|Zasób     | Zasób toohello łącza.        |
|Ścieżki do magazynu     |  Konto magazynu toohello ścieżki i kontener zawierające dzienniki hello (Jeśli żadnego zostały utworzone podczas uruchamiania hello). To ustawienie nie jest trwały, po zakończeniu działania hello portalu.        |
|Podsumowanie     | Podsumowanie kondycji zasobów hello.        |
|Szczegóły     | Szczegółowe informacje o kondycji zasobów hello.        |
|Ostatniego uruchomienia     | Witaj hello czas ostatniego czasu rozwiązywania problemów zostało uruchomione.        |


Witaj **akcji** karta zawiera ogólne wskazówki dotyczące jak tooresolve hello problem. Jeśli hello problemu można podjąć akcję, link jest dostarczany z dodatkowych wskazówek. W przypadku hello w przypadku, gdy nie ma żadnych dodatkowych wskazówek, odpowiedź hello zapewnia tooopen adres url hello sprawy pomocy technicznej.  Aby uzyskać więcej informacji o właściwościach hello hello odpowiedzi i dostępnych, odwiedź stronę [Rozwiązywanie problemów z obserwatora sieciowego — omówienie](network-watcher-troubleshoot-overview.md)


## <a name="next-steps"></a>Następne kroki

Jeśli ustawienia zostały zmienione które zatrzymania połączenia sieci VPN, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack dół hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które mogą być zagrożona.


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
