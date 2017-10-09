---
title: "Przechwytywanie pakietów aaaManage z obserwatora sieciowego Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toomanage hello funkcja przechwytywania pakietów obserwatora sieciowego przy użyciu portalu Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a>Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu portalu hello

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Interfejs API Azure REST](network-watcher-packet-capture-manage-rest.md)

Przechwytywania pakietów obserwatora sieciowego umożliwia toocreate przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej. Filtry są przewidziane tooensure sesji przechwytywania hello przechwytywać tylko hello ruchu. Przechwytywania pakietów pomaga anomalii sieci toodiagnose rozbudowy i aktywne. Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej. Jest przechwytywania pakietów wyzwalacza stanie tooremotely, ta funkcja ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego, jak i na powitania żądanego komputera, który zapisuje cenny czas.

Ten artykuł przedstawia hello zarządzania różnych zadań, które są obecnie dostępne dla przechwytywania pakietów.

- [**Uruchom przechwytywania pakietów**](#start-a-packet-capture)
- [**Zatrzymaj przechwytywania pakietów**](#stop-a-packet-capture)
- [**Usuń przechwytywania pakietów**](#delete-a-packet-capture)
- [**Pobierz przechwytywania pakietów**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym artykule przyjęto założenie, że hello następujące zasoby:

- Wystąpienia obserwatora sieciowego w regionie hello ma toocreate przechwytywania pakietów
- Maszyna wirtualna o pakietów hello przechwytywania rozszerzenie.

> [!IMPORTANT]
> Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`. Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).

### <a name="packet-capture-agent-extension-through-hello-portal"></a>Rozszerzenie agenta przechwytywania pakietów, za pośrednictwem portalu hello

przechwytywania pakietów hello tooinstall agenta maszyny Wirtualnej za pośrednictwem portalu hello Przejdź tooyour maszyny wirtualnej, kliknij pozycję **rozszerzenia** > **Dodaj** i wyszukaj **Agent obserwatorów sieci dla Systemu Windows**

![Widok agenta][agent]

## <a name="packet-capture-overview"></a>Omówienie przechwytywania pakietów

Przejdź toohello [portalu Azure](https://portal.azure.com) i kliknij przycisk **sieci** > **obserwatora sieciowego** > **przechwytywania pakietów**

Strona omówienia Hello przedstawia listę wszystkich pakietów przechwytuje, który istnieje, bez względu na stan hello.

> [!NOTE]
> Przechwytywania pakietów wymaga konta magazynu toohello łączności za pośrednictwem portu 443.

![ekran Przegląd przechwytywania pakietów][1]

## <a name="start-a-packet-capture"></a>Uruchom przechwytywania pakietów

Kliknij przycisk **Dodaj** toocreate przechwytywania pakietów.

właściwości Hello, które mogą być definiowane w przechwytywania pakietów są:

**Ustawienia głównego**

- **Subskrypcja** — ta wartość jest hello subskrypcji, która jest używana, wystąpienia obserwatora sieciowego jest niezbędna w każdej subskrypcji.
- **Grupa zasobów** -grupa zasobów hello hello maszyny wirtualnej, która docelowej.
- **Docelowa maszyna wirtualna** -hello maszyny wirtualnej, która działa przechwytywania pakietów hello
- **Nazwa przechwytywania pakietów** — ta wartość jest nazwą hello przechwytywania pakietów hello.

**Przechwytywanie konfiguracji**

- **Konto magazynu** — Określa, czy przechwytywania pakietów jest zapisywane na koncie magazynu.
- **Plik** — Określa, czy przechwytywania pakietów jest zapisywane lokalnie na maszynie wirtualnej hello.
- **Konta magazynu** -hello wybrane przechwytywania pakietów hello toosave konta magazynu w. Domyślna lokalizacja to identyfikator name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription konta https://{storage} /resourcegroups/ {Nazwa maszyny name}/providers/microsoft.compute/virtualmachines/{virtual grupy zasobów} / {YY} / {MM} / {DD} / {HH} packetcapture__{MM}_CAP _ {XXX} {SS}. (Włączone, tylko jeśli **magazynu** jest zaznaczone)
- **Ścieżka do pliku lokalnego** — ścieżka lokalna hello na przechwytywania pakietów hello toosave maszyny wirtualnej. (Włączone, tylko jeśli **pliku** jest zaznaczona). Należy podać prawidłową ścieżkę
- **Maksymalna liczba bajtów na pakiet** — Witaj liczbę bajtów z każdego pakietu, które są przechwytywane, wszystkie bajty są przechwytywane, jeśli pole pozostanie puste.
- **Maksymalna liczba bajtów na sesji** — jest to całkowita liczba bajtów, które są przechwytywane, gdy wartość hello osiągnięciu zatrzymuje przechwytywania pakietów hello.
- **Limit czasu (w sekundach)** -ustawia limit czasu dla toostop przechwytywania pakietów hello. Domyślna to 18000 sekund.

> [!NOTE]
> Konta Premium magazynu nie są obecnie obsługiwane dla przechwytuje przechowywania pakietów.

**Filtrowanie (opcjonalnie)**

- **Protokół** — Witaj toofilter protokołu dla przechwytywania pakietów hello. Witaj dostępne wartości to TCP, UDP i dowolne.
- **Lokalny adres IP** — ta wartość filtry toopackets przechwytywania pakietów hello Jeśli hello lokalny adres IP odpowiada to wartości filtru.
- **Port lokalny** — ta wartość filtry toopackets przechwytywania pakietów hello gdzie portów lokalnych hello zgodna z tą wartością filtru.
- **Zdalny adres IP** — ta wartość filtry toopackets przechwytywania pakietów hello Jeśli hello zdalny adres IP odpowiada to wartości filtru.
- **Port zdalny** — ta wartość filtry toopackets przechwytywania pakietów hello Jeśli port zdalny hello odpowiada tej wartości filtru.

> [!NOTE]
> Wartości adresów IP i port może być pojedynczą wartością, zakres wartości lub zestawu. (to znaczy port 80 – 1024 dla) Można określić dowolną liczbę filtry.

Po wartości hello są wypełnione, kliknij przycisk **OK** przechwytywania pakietów hello toocreate.

![Utwórz przechwytywania pakietów][2]

Po ustawieniu limitu czasu hello na przechwytywania pakietów hello wygasła, przechwytywania pakietów hello jest zatrzymywane, można wyświetlić. Można też ręcznie zatrzymać sesji przechwytywania pakietów hello.

## <a name="delete-a-packet-capture"></a>Usuń przechwytywania pakietów

W pakiecie hello przechwytywania widok, kliknij przycisk hello **menu kontekstowe** (...) lub kliknij prawym przyciskiem myszy i kliknij przycisk **usunąć** przechwytywania pakietów hello toostop

![Usuń przechwytywania pakietów][3]

> [!NOTE]
> Usunięcie przechwytywania pakietów nie powoduje usunięcia pliku hello hello koncie magazynu.

Zostanie wyświetlona prośba tooconfirm ma przechwytywania pakietów hello toodelete, kliknij przycisk **tak**

![Potwierdzenie][4]

## <a name="stop-a-packet-capture"></a>Zatrzymaj przechwytywania pakietów

W pakiecie hello przechwytywania widok, kliknij przycisk hello **menu kontekstowe** (...) lub kliknij prawym przyciskiem myszy i kliknij przycisk **zatrzymać** przechwytywania pakietów hello toostop

## <a name="download-a-packet-capture"></a>Pobierz przechwytywania pakietów

Po zakończeniu sesji przechwytywania pakietów, plik przechwytywania hello jest przekazane tooblob tooa lub magazynu lokalnego pliku na powitania maszyny Wirtualnej. Lokalizacja przechowywania Hello przechwytywania pakietów hello jest definiowany podczas tworzenia hello sesji. Tooaccess wygodne narzędzie te Przechwytywanie plików, tooa zapisane konto magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/

Jeśli określono konto magazynu, zapisywane są pliki przechwytywania pakietów tooa konta magazynu w następującej lokalizacji hello:
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)

Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













