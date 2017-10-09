---
title: "aaaTroubleshoot wdrożenia maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Menedżer zasobów Rozwiązywanie problemów dotyczących wdrożenia podczas tworzenia nowej maszyny wirtualnej systemu Windows na platformie Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a>Rozwiązywanie problemów dotyczących wdrożenia podczas tworzenia nowej maszyny Wirtualnej systemu Windows na platformie Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Najważniejsze problemy
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

Inne problemy z wdrażaniem maszyny Wirtualnej i pytania, zobacz [rozwiązać wdrażanie systemu Windows maszyny wirtualnej na platformie Azure](troubleshoot-deploy-vm.md).

## <a name="collect-activity-logs"></a>Rejestruje działania zbieranie
toostart rozwiązywania problemów, zbieranie hello działania rejestruje błąd hello tooidentify skojarzone z hello problem. Witaj poniższe łącza zawierają szczegółowe informacje na powitania toofollow procesu.

[Wyświetlanie operacji wdrażania](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Wyświetl toomanage Dzienniki aktywności Azure zasobów](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**/ Y:** Jeśli hello systemu operacyjnego Windows uogólniony i jest przekazany lub przechwycone z hello uogólniony ustawienie, wówczas nie będzie błędów. Podobnie jeśli hello systemu operacyjnego jest specjalizowany systemu Windows i jest przekazany lub przechwycone z hello specjalizowany ustawienie, nie będzie błędów, a następnie.

**Przekazywanie błędów:**

**N<sup>1</sup>:** Jeśli hello systemu operacyjnego Windows uogólniony, a jest przekazywany jako wyspecjalizowane, wystąpi błąd limitu czasu inicjowania obsługi administracyjnej z maszyny Wirtualnej jest zablokowany na ekranie OOBE hello hello.

**N<sup>2</sup>:** Jeśli hello systemu operacyjnego jest specjalizowany systemu Windows, a przesłaniem jako uogólniony, otrzyma inicjowania obsługi administracyjnej błąd awarii z maszyny Wirtualnej jest zablokowany na ekranie OOBE hello ponieważ hello nowej maszyny Wirtualnej został uruchomiony z oryginalnego komputera hello hello Nazwa, nazwa użytkownika i hasło.

**Rozdzielczość**

użyć obu tych błędów, tooresolve [tooupload AzureRmVhd Dodaj hello oryginalny dysk VHD](https://msdn.microsoft.com/library/mt603554.aspx), dostępnych na lokalnym, hello samo ustawienie jak dla hello systemu operacyjnego (uogólniony/specjalizowany). tooupload jako uogólniony, najpierw należy pamiętać toorun programu sysprep.

**Zapisz błędy:**

**N<sup>3</sup>:** Jeśli hello systemu operacyjnego Windows uogólniony, a jest przechwytywany jako wyspecjalizowane, otrzymasz inicjowania obsługi administracyjnej błąd upływu limitu czasu, ponieważ oryginalne hello maszyny Wirtualnej nie jest używany jako jest oznaczony jako uogólniony.

**N<sup>4</sup>:** w przypadku hello systemu operacyjnego Windows specjalizowany i jest przechwytywany jako uogólniony, otrzymasz błędem błąd inicjowania obsługi administracyjnej, ponieważ hello nowej maszyny Wirtualnej został uruchomiony z hello oryginalną nazwę komputera, nazwę użytkownika i hasło. Ponadto oryginalne hello maszyny Wirtualnej nie jest używany, ponieważ jest on oznaczony jako specjalne.

**Rozdzielczość**

tooresolve obu tych błędów, Usuń hello bieżącego obrazu z portalu hello i [je ponownie przechwycić z hello bieżącego wirtualne dyski twarde](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) z hello sam, jak ustawienie hello systemu operacyjnego (uogólniony/specjalizowany).

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a>Problem: Niestandardowy/galerii/obrazu witryny marketplace; Błąd alokacji
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
Jeśli wystąpią problemy podczas uruchamiania zatrzymanej maszyny Wirtualnej systemu Windows lub zmień rozmiar istniejącej maszyny Wirtualnej systemu Windows na platformie Azure, zobacz [problemy z wdrażaniem Rozwiązywanie problemów z Menedżera zasobów z ponownym uruchomieniem lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Windows na platformie Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

