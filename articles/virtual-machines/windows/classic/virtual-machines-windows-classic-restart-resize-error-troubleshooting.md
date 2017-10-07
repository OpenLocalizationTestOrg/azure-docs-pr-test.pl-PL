---
title: "aaaVM ponownego uruchamiania lub zmiana rozmiaru problemów | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów wdrożenie klasyczne z ponownego uruchamiania lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Windows na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a>Rozwiązywanie problemów wdrożenie klasyczne z ponownego uruchamiania lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Windows na platformie Azure
> [!div class="op_single_selector"]
> * [Wdrożenie klasyczne](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [Resource Manager](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

Spróbuj toostart zatrzymania maszyny wirtualnej Azure (VM), lub zmień rozmiar istniejącej maszyny Wirtualnej Azure, hello typowym błędem występujących po błąd alokacji. Ten błąd powoduje hello klastra lub regionie nie ma dostępnych zasobów lub nie hello Obsługa żądany rozmiar maszyny Wirtualnej.

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Dzienniki inspekcji zbieranie
Rozwiązywanie problemów, toostart hello zbierania danych inspekcji rejestruje błąd hello tooidentify skojarzone z hello problem.

W portalu Azure hello, kliknij przycisk **Przeglądaj** > **maszyn wirtualnych** > *maszyny wirtualnej systemu Windows*  >   **Ustawienia** > **dzienniki inspekcji**.

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problem: Błąd podczas uruchamiania zatrzymanej maszyny Wirtualnej
Spróbuj toostart zatrzymanej maszyny Wirtualnej, ale jest wyświetlany błąd alokacji.

### <a name="cause"></a>Przyczyna
Żądanie hello toostart hello zatrzymana maszyna wirtualna ma toobe podjęto na powitania oryginalnego klastra obsługującego hello usługi w chmurze. Witaj klaster nie ma jednak żądania hello toofulfill dostępne wolne miejsce.

### <a name="resolution"></a>Rozwiązanie
* Utwórz nową usługę w chmurze i skojarzyć go z jednego regionu lub sieci wirtualnej region, ale nie grupy koligacji.
* Usuń hello zatrzymana maszyna wirtualna.
* Utwórz ponownie hello maszyny Wirtualnej w hello nową usługę w chmurze przy użyciu hello dysków.
* Uruchom hello ponownie utworzyć maszyny Wirtualnej.

Jeśli wystąpi błąd podczas próby toocreate nową usługę w chmurze, spróbuj ponownie później lub zmienić regionu hello hello usłudze w chmurze.

> [!IMPORTANT]
> Hello nową usługę w chmurze będzie miała nowej nazwy i adresu VIP, dlatego należy toochange te informacje dla wszystkich zależności hello korzystających z tych informacji w celu hello istniejącą usługę w chmurze.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problem: Błąd podczas zmiany rozmiaru istniejącej maszyny Wirtualnej
Spróbuj tooresize istniejącej maszyny Wirtualnej, ale jest wyświetlany błąd alokacji.

### <a name="cause"></a>Przyczyna
żądania Hello hello tooresize maszyna wirtualna ma toobe nastąpiła w oryginalnym klastrze hello danej usługi w chmurze hello hostów. Witaj klastra nie obsługuje jednak hello żądany rozmiar maszyny Wirtualnej.

### <a name="resolution"></a>Rozwiązanie
Zmniejsz hello żądany rozmiar maszyny Wirtualnej i ponów próbę hello rozmiaru żądania.

* Kliknij przycisk **Przeglądaj wszystkie** > **maszyn wirtualnych (klasyczne)** > *maszyny wirtualnej* > **ustawienia**  >  **Rozmiar**. Aby uzyskać szczegółowe instrukcje, zobacz [zmienić rozmiaru maszyny wirtualnej hello](https://msdn.microsoft.com/library/dn168976.aspx).

Jeśli nie jest możliwe tooreduce hello rozmiar maszyny Wirtualnej, wykonaj następujące kroki:

* Utwórz nową usługę w chmurze, zapewnienie, że nie jest połączona grupa koligacji tooan i nie są skojarzone z sieci wirtualnej jest tooan połączonej grupy koligacji.
* Utwórz nowy, o większym rozmiarze maszyny Wirtualnej w nim.

Umożliwiającej obsługę wszystkich maszyn wirtualnych w hello sama usługa w chmurze. Jeśli istniejącą usługę w chmurze jest skojarzone z sieci wirtualnej na podstawie regionu, możesz połączyć hello nowe chmury usługi toohello istniejącej sieci wirtualnej.

Jeśli hello istniejącej usługi chmury nie jest skojarzony z sieci wirtualnej na podstawie regionu, następnie należy mieć toodelete hello maszyn wirtualnych w hello istniejącą usługę w chmurze i utwórz je ponownie hello nowego w usłudze w chmurze z ich dysków. Jest jednak ważne tooremember hello nową usługę w chmurze że nowej nazwy i adresu VIP, dlatego należy tooupdate tych opcji dla wszystkich zależności hello, które obecnie korzystanie z tej informacji hello istniejącą usługę w chmurze.

## <a name="next-steps"></a>Następne kroki
Jeśli wystąpią problemy podczas tworzenia maszyny Wirtualnej systemu Windows na platformie Azure, zobacz [Rozwiązywanie problemów dotyczących wdrożenia z tworzenia maszyny wirtualnej systemu Windows na platformie Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

