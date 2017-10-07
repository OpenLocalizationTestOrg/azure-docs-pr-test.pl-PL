---
title: "aaaTroubleshoot wdrażanie problemy dotyczące maszyny wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Wdrażanie systemu Windows maszyny wirtualnej Rozwiązywanie problemów z w modelu wdrażania Azurethe Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a>Rozwiązywanie problemów z wdrażanie problemy dotyczące maszyny wirtualnej systemu Windows na platformie Azure

problemy z wdrażaniem tootroubleshoot maszyny wirtualnej (VM) na platformie Azure, przejrzyj hello [Najważniejsze problemy](#top-issues) dla typowych błędów i rozwiązania.

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.

## <a name="top-issues"></a>Najważniejsze problemy
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

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

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a>Jak używać i wdrażanie obrazu klienta systemu windows na platformie Azure?

Służy Windows 7, Windows 8 lub Windows 10 w usłudze Azure scenariusze tworzenia/testowania Jeśli masz odpowiednie subskrypcji programu Visual Studio (dawniej MSDN). To [artykułu](client-images.md) przedstawiono hello kwalifikujących się wymagania dotyczące uruchamiania klienta systemu Windows Azure i używa hello obrazów w galerii Azure.

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a>Jak można wdrożyć maszyny wirtualnej z wykorzystaniem hello korzyści Użyj hybrydowych (KONCENTRATOR)

Istnieje kilka różnych sposobów toodeploy Windows maszynom wirtualnym hello Azure hybrydowego Użyj korzyści.

Dla subskrypcji Enterprise Agreement:

• Wdrażanie maszyn wirtualnych z określonych obrazów Marketplace, które są wstępnie skonfigurowane z korzyści Użyj hybrydowe platformy Azure.

Dla umowy Enterprise agreement:

• Przekazywanie niestandardowych maszyny Wirtualnej i wdrażanie za pomocą szablonu usługi Resource Manager lub programu Azure PowerShell.

Aby uzyskać więcej informacji zobacz następujące zasoby hello:

 - [Omówienie usługi Azure korzyści Użyj hybrydowego](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [Do pobrania — często zadawane pytania](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - [Korzyści Użyj hybrydowe platformy Azure dla systemu Windows Server i klienta systemu Windows](hybrid-use-benefit-licensing.md).

 - [Jak używać hello korzyści Użyj hybrydowe na platformie Azure](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Jak aktywować Moje miesięczny kredyt dla programu Visual studio Enterprise (BizSpark)

tooactivate miesięcznych Twojej karty kredytowej, zobacz ten [artykułu](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a>Jak tooadd przedsiębiorstwa: tworzenie i testowanie toomy Enterprise Agreement (EA) tooget uzyskują dostęp do obrazów klientów tooWindow?

Subskrypcje toocreate możliwości Hello oparte na powitania przedsiębiorstwa i testowania oferty jest ograniczone tooAccount właścicieli, którzy otrzymali uprawnienia toodo tak przez administratora przedsiębiorstwa. Hello właściciela konta tworzy subskrypcji za pośrednictwem portalu konta usługi Azure hello i następnie należy dodać aktywnych subskrybentów usługi Visual Studio jako współadministratorów. Aby mogli zarządzać i użyj hello zasobów niezbędnych do projektowania i testowania. Aby uzyskać więcej informacji, zobacz [przedsiębiorstwa: tworzenie i testowanie](https://azure.microsoft.com/offers/ms-azr-0148p/).

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a>Brak sterowników, dla moich wirtualna N-Series systemu Windows

Sterowniki dla maszyn wirtualnych z systemem Windows znajdują się [tutaj](n-series-driver-setup.md).

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Nie można znaleźć wystąpienia procesora GPU w mojej wirtualna N serii

tootake korzystać z funkcji GPU hello Azure N-series maszyny wirtualne z systemami Windows Server 2016 lub Windows Server 2012 R2, należy zainstalować sterowniki grafiki NVIDIA na każdej maszynie Wirtualnej po wdrożeniu. Sterownik instalacji informacje są dostępne dla [maszyn wirtualnych systemu Windows](n-series-driver-setup.md) i [maszyn wirtualnych systemu Linux](../linux/n-series-driver-setup.md).

## <a name="are-client-images-supported-for-n-series"></a>Obrazy klienta są obsługiwane dla serii N?

Azure obsługuje obecnie tylko N serii na maszynach wirtualnych z systemami operacyjnymi Windows Server i Linux.

## <a name="is-n-series-vms-available-in-my-region"></a>N-Series maszyn wirtualnych jest dostępny w moim regionie?

Możesz sprawdzić dostępność hello z hello [produkty dostępne przez tabelę region](https://azure.microsoft.com/regions/services)i cenach [tutaj](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a>Jakie obrazy klienta I użycia i wdrożyć w Azure i sposobu tooI je uzyskać?

Można użyć systemu Windows 7, Windows 8 lub Windows 10 w usłudze Azure scenariusze tworzenia/testowania, pod warunkiem, że masz odpowiednie subskrypcji programu Visual Studio (dawniej MSDN). 

- Obrazy systemu Windows 10 są dostępne w galerii Azure hello w [oferuje kwalifikujących się tworzenie/testowanie](client-images.md#eligible-offers). 
- Subskrybentów usługi Visual Studio w obrębie dowolnego typu oferty może również [odpowiednio przygotować i utworzyć](prepare-for-upload-vhd-image.md) 64-bitowego obrazu systemu Windows 7, Windows 8 lub Windows 10, a następnie [przekazać tooAzure](upload-generalized-managed.md). Użyj Hello pozostaje toodev i testowanie ograniczone przez aktywnych subskrybentów usługi Visual Studio.

To [artykułu](client-images.md) przedstawiono hello kwalifikujących się wymagania dotyczące uruchamiania klienta systemu Windows Azure i użyj hello obrazów w galerii Azure.

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Nie mam stanie toosee rodziny rozmiar maszyny Wirtualnej, która przy zmianie rozmiaru Moja maszyna wirtualna.

Kiedy maszyna wirtualna jest uruchomiona, jest tooa wdrożonego serwera fizycznego. serwerów fizycznych Hello w regionach platformy Azure są pogrupowane w klastrach wspólnej sprzętu fizycznego. Zmiana rozmiaru maszyny Wirtualnej, który wymaga hello wirtualna toobe przenieść toodifferent sprzętu klastrów różni się w zależności od modelu wdrażania został hello toodeploy używane maszyny Wirtualnej.

- Maszyn wirtualnych wdrożonych w klasycznym modelu wdrażania, wdrożenie usługi chmury hello muszą zostać usunięte i wdrożone toochange hello maszyn wirtualnych tooa rozmiar innej rodziny.

- Maszyn wirtualnych wdrożonych w modelu wdrażania usługi Resource Manager, należy zatrzymać wszystkie maszyny wirtualne w zestawie przed zmianą rozmiaru hello żadnej maszyny Wirtualnej w zestawie dostępności hello dostępności hello.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Witaj wymienionych rozmiar maszyny Wirtualnej nie jest obsługiwana podczas wdrażania w zestawie dostępności.

Wybierz rozmiar, który jest obsługiwany w zestawie dostępności hello klastra. Zaleca się podczas tworzenia zestawu dostępności toochoose hello największy rozmiar maszyny Wirtualnej przez uważasz, że należy, i mieć stosowania Twojego pierwszego toohello wdrożenia zestawu dostępności.

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>Można dodać istniejącego zestawu dostępności tooan klasyczne maszyny Wirtualnej?

Tak. Można dodać istniejącego klasycznego wirtualna tooa nowego lub istniejącego zestawu dostępności. Aby uzyskać więcej informacji, zobacz [Dodawanie istniejącego zestawu dostępności maszyny wirtualnej tooan](classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Następne kroki
Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/).

Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.
