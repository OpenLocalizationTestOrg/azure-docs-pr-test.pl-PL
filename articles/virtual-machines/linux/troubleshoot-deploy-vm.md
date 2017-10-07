---
title: "aaaTroubleshoot wdrażanie problemy dotyczące maszyny wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z wdrażanie problemy dotyczące maszyny wirtualnej systemu Linux w modelu wdrażania Menedżera zasobów Azurethe."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Rozwiązywanie problemów z wdrażanie problemy dotyczące maszyny wirtualnej systemu Linux na platformie Azure

problemy z wdrażaniem tootroubleshoot maszyny wirtualnej (VM) na platformie Azure, przejrzyj hello [Najważniejsze problemy](#top-issues) dla typowych błędów i rozwiązania.

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.

## <a name="top-issues"></a>Najważniejsze problemy
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>Witaj klastra nie może obsługiwać hello żądany rozmiar maszyny Wirtualnej
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Ponów żądanie hello przy użyciu mniejszego rozmiaru maszyny Wirtualnej.
- Jeśli hello żądany rozmiar hello się, że nie można zmienić maszyny Wirtualnej:
    - Zatrzymaj wszystkie hello maszyn wirtualnych w zestawie dostępności hello. Kliknij przycisk **grup zasobów** > grupy zasobów > **zasobów** > zestawu dostępności > **maszyn wirtualnych** > maszyny wirtualnej > **zatrzymać**.
    - Po wszystkich hello zatrzymywania maszyn wirtualnych, należy utworzyć hello maszyny Wirtualnej w hello żądanego rozmiaru.
    - Uruchom najpierw hello nowej maszyny Wirtualnej, a następnie wybierz każdego z hello zatrzymana maszyn wirtualnych i kliknij przycisk Start.


## <a name="hello-cluster-does-not-have-free-resources"></a>Witaj klastra nie ma wolnego zasobów
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Ponów żądanie hello później.
- Jeśli hello nowej maszyny Wirtualnej można ustawić część różnych dostępności
    - Tworzenie maszyny Wirtualnej w innym zestawem dostępności (w hello tego samego regionu).
    - Dodaj nowe toohello wirtualna hello tej samej sieci wirtualnej.

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Jak aktywować Moje miesięczny kredyt dla programu Visual studio Enterprise (BizSpark)

tooactivate miesięcznych Twojej karty kredytowej, zobacz ten [artykułu](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a>Dlaczego I nie można zainstalować sterownik procesora GPU powitania dla maszyny Wirtualnej systemu Ubuntu wirtualizacją sieci?

Obecnie Obsługa Linux GPU jest dostępna tylko na maszynach wirtualnych NC Azure systemem Ubuntu Server 16.04 LTS. Aby uzyskać więcej informacji, zobacz [Konfigurowanie wersji sterowników procesora GPU dla maszyn wirtualnych N-series systemem Linux](n-series-driver-setup.md).

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>Brak sterowników, dla mojej wirtualna N-Series systemu Linux

Sterowniki dla maszyn wirtualnych w systemie Linux znajdują się [tutaj](n-series-driver-setup.md). 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Nie można znaleźć wystąpienia procesora GPU w mojej wirtualna N serii

tootake korzystać z funkcji GPU hello Azure N-series maszyny wirtualne z systemami Windows Server 2016 lub Windows Server 2012 R2, należy zainstalować sterowniki grafiki NVIDIA na każdej maszynie Wirtualnej po wdrożeniu. Sterownik instalacji informacje są dostępne dla [maszyn wirtualnych systemu Windows](../windows/n-series-driver-setup.md) i [maszyn wirtualnych systemu Linux](n-series-driver-setup.md).

## <a name="is-n-series-vms-available-in-my-region"></a>N-Series maszyn wirtualnych jest dostępny w moim regionie?

Możesz sprawdzić dostępność hello z hello [produkty dostępne przez tabelę region](https://azure.microsoft.com/regions/services)i cenach [tutaj](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Nie mam stanie toosee rodziny rozmiar maszyny Wirtualnej, która przy zmianie rozmiaru Moja maszyna wirtualna.

Kiedy maszyna wirtualna jest uruchomiona, jest tooa wdrożonego serwera fizycznego. serwerów fizycznych Hello w regionach platformy Azure są pogrupowane w klastrach wspólnej sprzętu fizycznego. Zmiana rozmiaru maszyny Wirtualnej, który wymaga hello wirtualna toobe przenieść toodifferent sprzętu klastrów różni się w zależności od modelu wdrażania został hello toodeploy używane maszyny Wirtualnej.

- Maszyn wirtualnych wdrożonych w klasycznym modelu wdrażania, wdrożenie usługi chmury hello muszą zostać usunięte i wdrożone toochange hello maszyn wirtualnych tooa rozmiar innej rodziny.

- Maszyn wirtualnych wdrożonych w modelu wdrażania usługi Resource Manager, należy zatrzymać wszystkie maszyny wirtualne w zestawie przed zmianą rozmiaru hello żadnej maszyny Wirtualnej w zestawie dostępności hello dostępności hello.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Witaj wymienionych rozmiar maszyny Wirtualnej nie jest obsługiwana podczas wdrażania w zestawie dostępności.

Wybierz rozmiar, który jest obsługiwany w zestawie dostępności hello klastra. Zaleca się podczas tworzenia zestawu dostępności toochoose hello największy rozmiar maszyny Wirtualnej przez uważasz, że należy, i mieć stosowania Twojego pierwszego toohello wdrożenia zestawu dostępności.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>Dystrybucje systemu Linux/wersji są obsługiwane na platformie Azure?

Listę hello w systemie Linux można znaleźć na [dystrybucje Azure-Endorsed](endorsed-distros.md).

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>Można dodać istniejącego zestawu dostępności tooan klasyczne maszyny Wirtualnej?

Tak. Można dodać istniejącego klasycznego wirtualna tooa nowego lub istniejącego zestawu dostępności. Aby uzyskać więcej informacji, zobacz [Dodawanie istniejącego zestawu dostępności maszyny wirtualnej tooan](../windows/classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Następne kroki
Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/).

Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.
