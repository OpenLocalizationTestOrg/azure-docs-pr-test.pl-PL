---
title: problemy z aaaVM ponownego uruchamiania lub zmiana rozmiaru na platformie Azure | Dokumentacja firmy Microsoft
description: "Rozwiązywanie problemów wdrożenia usługi Resource Manager z ponownego uruchamiania lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a>Rozwiązywanie problemów dotyczących wdrożenia z ponownym uruchomieniem lub zmiana rozmiaru istniejącej maszyny Wirtualnej systemu Linux na platformie Azure
Spróbuj toostart zatrzymania maszyny wirtualnej Azure (VM), lub zmień rozmiar istniejącej maszyny Wirtualnej Azure, hello typowym błędem występujących po błąd alokacji. Ten błąd powoduje hello klastra lub regionie nie ma dostępnych zasobów lub nie hello Obsługa żądany rozmiar maszyny Wirtualnej.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Rejestruje działania zbieranie
toostart rozwiązywania problemów, zbieranie hello działania rejestruje błąd hello tooidentify skojarzone z hello problem. Hello następującego łącza zawierają szczegółowe informacje na temat procesu hello:

[Wyświetlanie operacji wdrażania](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Wyświetl toomanage Dzienniki aktywności Azure zasobów](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problem: Błąd podczas uruchamiania zatrzymanej maszyny Wirtualnej
Spróbuj toostart zatrzymanej maszyny Wirtualnej, ale jest wyświetlany błąd alokacji.

### <a name="cause"></a>Przyczyna
Żądanie hello toostart hello zatrzymana maszyna wirtualna ma toobe podjęto na powitania oryginalnego klastra obsługującego hello usługi w chmurze. Witaj klaster nie ma jednak żądania hello toofulfill dostępne wolne miejsce.

### <a name="resolution"></a>Rozwiązanie
* Zatrzymaj hello wszystkich maszyn wirtualnych w dostępności hello wartość i ponownie uruchom każdej maszyny Wirtualnej.
  
  1. Kliknij przycisk **grup zasobów** > *grupie zasobów* > **zasobów** > *zestawu dostępności* > **maszyn wirtualnych** > *maszyny wirtualnej* > **zatrzymać**.
  2. Po wszystkich hello zatrzymania maszyny wirtualne, wybierz poszczególne maszyny wirtualne hello zatrzymana i kliknij przycisk Start.
* Ponów żądanie ponownego uruchomienia hello w późniejszym czasie.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problem: Błąd podczas zmiany rozmiaru istniejącej maszyny Wirtualnej
Spróbuj tooresize istniejącej maszyny Wirtualnej, ale jest wyświetlany błąd alokacji.

### <a name="cause"></a>Przyczyna
żądania Hello hello tooresize maszyna wirtualna ma toobe nastąpiła w oryginalnym klastrze hello danej usługi w chmurze hello hostów. Witaj klastra nie obsługuje jednak hello żądany rozmiar maszyny Wirtualnej.

### <a name="resolution"></a>Rozwiązanie
* Ponów żądanie hello przy użyciu mniejszego rozmiaru maszyny Wirtualnej.
* Jeśli hello żądany rozmiar hello się, że nie można zmienić maszyny Wirtualnej:
  
  1. Zatrzymaj wszystkie hello maszyn wirtualnych w zestawie dostępności hello.
     
     * Kliknij przycisk **grup zasobów** > *grupie zasobów* > **zasobów** > *zestawu dostępności* > **maszyn wirtualnych** > *maszyny wirtualnej* > **zatrzymać**.
  2. Po wszystkich hello zatrzymania maszyny wirtualne, Zmień rozmiar hello potrzeby maszyny Wirtualnej tooa większy rozmiar.
  3. Wybierz hello zmiany rozmiaru maszyny Wirtualnej i kliknij przycisk **Start**, a następnie uruchom każdą hello zatrzymane maszyn wirtualnych.

## <a name="next-steps"></a>Następne kroki
Jeśli wystąpią problemy podczas tworzenia nowej maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [Rozwiązywanie problemów dotyczących wdrożenia z Tworzenie nowej maszyny wirtualnej systemu Linux na platformie Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

