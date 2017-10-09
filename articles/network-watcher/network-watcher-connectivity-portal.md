---
title: "aaaCheck łączność z obserwatora sieciowego Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak łączność toouse skontaktuj się z obserwatora sieciowego przy użyciu hello portalu Azure"
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
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a>Sprawdź łączność z obserwatora sieciowego Azure przy użyciu hello portalu Azure

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-connectivity-cli.md)
> - [Interfejs API Azure REST](network-watcher-connectivity-rest.md)

Dowiedz się, jak można ustalić toouse łączności tooverify Jeśli bezpośrednie połączenie TCP z tooa maszyny wirtualnej, danego punktu końcowego.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym artykule przyjęto założenie, że masz hello następujące zasoby:

* Wystąpienia obserwatora sieciowego w regionie hello ma toocheck łączności.

* Maszyny wirtualne toocheck łączność z.

> [!IMPORTANT]
> Sprawdź łączność wymaga rozszerzenia maszyny wirtualnej `AzureNetworkWatcherExtension`. Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-tooa-virtual-machine"></a>Sprawdź maszyny wirtualnej tooa łączności

W tym przykładzie sprawdza łączność tooa docelowej maszyny wirtualnej za pośrednictwem portu 80.

Przejdź tooyour obserwatora sieciowego i kliknij **sprawdzenia łączności z serwerem (wersja zapoznawcza)**. Wybierz hello łączności toocheck maszyn wirtualnych z. W hello **docelowego** wybierz **wybierz maszynę wirtualną** i wybierz hello poprawne maszyny wirtualnej i portu tootest.

Po kliknięciu **Sprawdź**, hello łączności między maszynami wirtualnymi hello na określony port hello są sprawdzane. W przykładzie hello hello docelowej maszyny Wirtualnej jest nieosiągalny, lista przeskoków są wyświetlane.

![Wyniki sprawdzania łączności dla maszyny wirtualnej][1]

## <a name="check-remote-endpoint-connectivity"></a>Sprawdź łączność zdalny punkt końcowy

toocheck hello łączności i opóźnienia tooa zdalny punkt końcowy, wybierz hello **ręcznie określ** przycisk radiowy na powitania **docelowego** sekcji należy wprowadzić hello adresu url i hello port i kliknij przycisk **Sprawdź** .  Służy to do zdalnego punktów końcowych, takie jak punktów końcowych witryn sieci Web i magazynu.

![Wyniki sprawdzania łączności dla witryny sieci web][2]

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)

Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
