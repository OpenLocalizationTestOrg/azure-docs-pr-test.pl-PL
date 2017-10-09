---
title: "aaaTroubleshoot wdrożenia maszyny Wirtualnej systemu Linux-RM | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów dotyczących wdrożenia usługi Resource Manager podczas tworzenia nowej maszyny wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Rozwiązywanie problemów wdrożenia usługi Resource Manager z Tworzenie nowej maszyny wirtualnej systemu Linux na platformie Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Najważniejsze problemy
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

Inne problemy z wdrażaniem maszyny Wirtualnej i pytania, zobacz [Rozwiązywanie problemów z wdrażanie problemy dotyczące maszyny wirtualnej systemu Linux na platformie Azure](troubleshoot-deploy-vm.md).
## <a name="collect-activity-logs"></a>Rejestruje działania zbieranie
toostart rozwiązywania problemów, zbieranie hello działania rejestruje błąd hello tooidentify skojarzone z hello problem. Witaj poniższe łącza zawierają szczegółowe informacje na powitania toofollow procesu.

[Wyświetlanie operacji wdrażania](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Wyświetl toomanage Dzienniki aktywności Azure zasobów](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**/ Y:** Jeśli hello systemu operacyjnego Linux uogólniony i jest przekazany lub przechwycone z hello uogólniony ustawienie, wówczas nie będzie żadnych błędów. Podobnie jeśli jest hello systemu operacyjnego Linux specjalizowany i jest przekazany lub przechwycić przy hello specjalizowany ustawienie, nie będzie błędów, a następnie.

**Przekazywanie błędów:**

**N<sup>1</sup>:** Jeśli hello systemu operacyjnego Linux uogólniony, a jest przekazywany jako wyspecjalizowane, otrzymasz inicjowania obsługi administracyjnej błąd upływu limitu czasu ponieważ hello maszyny Wirtualnej jest zablokowany na powitania inicjowania obsługi administracyjnej etapu.

**N<sup>2</sup>:** w przypadku hello systemu operacyjnego Linux specjalizowany, a przesłaniem jako uogólniony, otrzymasz błędem błąd inicjowania obsługi administracyjnej, ponieważ hello nowej maszyny Wirtualnej został uruchomiony z hello oryginalną nazwę komputera, nazwę użytkownika i hasło.

**Rozwiązanie:**

tooresolve obu tych błędów, Przekaż hello oryginalny dysk VHD, dostępnych na lokalnym, z hello takie same jak ustawienie hello systemu operacyjnego (uogólniony/specjalizowany). tooupload jako uogólniony, pamiętaj toorun-anulowanie zastrzeżenia najpierw.

**Zapisz błędy:**

**N<sup>3</sup>:** Jeśli hello systemu operacyjnego Linux uogólniony, a jest przechwytywany jako wyspecjalizowane, otrzymasz inicjowania obsługi administracyjnej błąd upływu limitu czasu, ponieważ oryginalne hello maszyny Wirtualnej nie jest używany jako jest oznaczony jako uogólniony.

**N<sup>4</sup>:** w przypadku hello systemu operacyjnego Linux specjalizowany i jest przechwytywany jako uogólniony, otrzymasz błędem błąd inicjowania obsługi administracyjnej, ponieważ hello nowej maszyny Wirtualnej został uruchomiony z hello oryginalną nazwę komputera, nazwę użytkownika i hasło. Ponadto oryginalne hello maszyny Wirtualnej nie jest używany, ponieważ jest on oznaczony jako specjalne.

**Rozwiązanie:**

tooresolve obu tych błędów, Usuń hello bieżącego obrazu z portalu hello i [je ponownie przechwycić z hello bieżącego wirtualne dyski twarde](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) z hello sam, jak ustawienie hello systemu operacyjnego (uogólniony/specjalizowany).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problem: Niestandardowy / galerii / obrazu z witryny marketplace; Błąd alokacji
Ten błąd pojawia się w sytuacjach, gdy hello nowe żądanie maszyny Wirtualnej jest przypięty tooa klastra, który nie obsługuje żądanej rozmiar maszyny Wirtualnej hello albo nie ma wolnego miejsca tooaccommodate hello żądania.

**Przyczyna 1:** hello klastra nie może obsługiwać hello żądany rozmiar maszyny Wirtualnej.

**Rozwiązanie 1:**

* Ponów żądanie hello przy użyciu mniejszego rozmiaru maszyny Wirtualnej.
* Jeśli hello żądany rozmiar hello się, że nie można zmienić maszyny Wirtualnej:
  * Zatrzymaj wszystkie hello maszyn wirtualnych w zestawie dostępności hello.
    Kliknij przycisk **grup zasobów** > *grupie zasobów* > **zasobów** > *zestawu dostępności* > **maszyn wirtualnych** > *maszyny wirtualnej* > **zatrzymać**.
  * Po hello wszystkich stopu maszyn wirtualnych, należy utworzyć hello nowej maszyny Wirtualnej w hello żądanego rozmiaru.
  * Uruchom najpierw hello nowej maszyny Wirtualnej, a następnie wybierz każdego z hello zatrzymane maszyn wirtualnych i kliknij przycisk **Start**.

**Przyczyny 2:** hello klastra nie ma wolnego zasobów.

**Rozdzielczość 2:**

* Ponów żądanie hello w późniejszym czasie.
* Jeśli hello nowej maszyny Wirtualnej można ustawić część różnych dostępności
  * Tworzenie nowej maszyny Wirtualnej w innym zestawem dostępności (w hello tego samego regionu).
  * Dodaj nowe toohello wirtualna hello tej samej sieci wirtualnej.

## <a name="next-steps"></a>Następne kroki
Jeśli wystąpią problemy podczas uruchamiania zatrzymanej maszyny Wirtualnej systemu Linux lub zmień rozmiar istniejącej maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [problemy z wdrażaniem Rozwiązywanie problemów z Menedżera zasobów z ponownym uruchomieniem lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Linux na platformie Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

