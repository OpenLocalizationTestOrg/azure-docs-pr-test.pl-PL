---
title: "aaaTroubleshoot wdrożenia maszyny Wirtualnej systemu Linux — Classic | Dokumentacja firmy Microsoft"
description: "Klasycznym Rozwiązywanie problemów dotyczących wdrożenia podczas tworzenia nowej maszyny wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: c8a963fa-6b2a-4c7a-a1f4-7793adb02b19
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cjiang
ms.openlocfilehash: a642bfd9a543cd6d2104b03fe04193d9352ccae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Rozwiązywanie problemów wdrożenie klasyczne z Tworzenie nowej maszyny wirtualnej systemu Linux na platformie Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Wersja usługi Resource Manager hello w tym artykule, dla [tutaj](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Dzienniki inspekcji zbieranie
Rozwiązywanie problemów, toostart hello zbierania danych inspekcji rejestruje błąd hello tooidentify skojarzone z hello problem.

W portalu Azure hello, kliknij przycisk **Przeglądaj** > **maszyn wirtualnych** > *maszyny wirtualnej systemu Windows*  >   **Ustawienia** > **dzienniki inspekcji**.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**/ Y:** Jeśli hello systemu operacyjnego Linux uogólniony i jest przekazany lub przechwycone z hello uogólniony ustawienie, wówczas nie będzie żadnych błędów. Podobnie jeśli jest hello systemu operacyjnego Linux specjalizowany i jest przekazany lub przechwycić przy hello specjalizowany ustawienie, nie będzie błędów, a następnie.

**Przekazywanie błędów:**

**N<sup>1</sup>:** Jeśli hello systemu operacyjnego Linux uogólniony, a jest przekazywany jako wyspecjalizowane, otrzymasz inicjowania obsługi administracyjnej błąd upływu limitu czasu ponieważ hello maszyny Wirtualnej jest zablokowany na powitania inicjowania obsługi administracyjnej etapu.

**N<sup>2</sup>:** w przypadku hello systemu operacyjnego Linux specjalizowany, a przesłaniem jako uogólniony, otrzymasz błędem błąd inicjowania obsługi administracyjnej, ponieważ hello nowej maszyny Wirtualnej został uruchomiony z hello oryginalną nazwę komputera, nazwę użytkownika i hasło.

**Rozwiązanie:**

tooresolve obu tych błędów, Przekaż hello oryginalny dysk VHD, dostępnych na lokalnym, z hello takie same jak ustawienie hello systemu operacyjnego (uogólniony/specjalizowany). tooupload jako uogólniony, pamiętaj toorun-anulowanie zastrzeżenia najpierw. Zobacz [tworzenie i przekazywanie wirtualnego dysku twardego tego hello zawiera System operacyjny Linux](create-upload-vhd.md) Aby uzyskać więcej informacji.

**Zapisz błędy:**

**N<sup>3</sup>:** Jeśli hello systemu operacyjnego Linux uogólniony, a jest przechwytywany jako wyspecjalizowane, otrzymasz inicjowania obsługi administracyjnej błąd upływu limitu czasu, ponieważ oryginalne hello maszyny Wirtualnej nie jest używany jako jest oznaczony jako uogólniony.

**N<sup>4</sup>:** w przypadku hello systemu operacyjnego Linux specjalizowany i jest przechwytywany jako uogólniony, otrzymasz błędem błąd inicjowania obsługi administracyjnej, ponieważ hello nowej maszyny Wirtualnej został uruchomiony z hello oryginalną nazwę komputera, nazwę użytkownika i hasło. Ponadto oryginalne hello maszyny Wirtualnej nie jest używany, ponieważ jest on oznaczony jako specjalne.

**Rozwiązanie:**

tooresolve obu tych błędów, Usuń hello bieżącego obrazu z portalu hello i [je ponownie przechwycić z hello bieżącego wirtualne dyski twarde](capture-image.md) z hello sam, jak ustawienie hello systemu operacyjnego (uogólniony/specjalizowany).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problem: Niestandardowy / galerii / obrazu z witryny marketplace; Błąd alokacji
Ten błąd pojawia się w sytuacji gdy hello nowe żądanie maszyny Wirtualnej są wysyłane tooa klastra, który nie ma wolnego miejsca tooaccommodate hello żądania, albo nie obsługuje żądanej rozmiar maszyny Wirtualnej hello. Nie jest możliwe toomix innej serii maszyn wirtualnych w hello sama usługa w chmurze. Więc jeśli chcesz toocreate nowej maszyny Wirtualnej o innym rozmiarze niż to, co może obsługiwać usługi w chmurze, hello obliczeń żądanie zakończy się niepowodzeniem.

W zależności od ograniczeń hello hello usługi w chmurze Użyj toocreate hello nowej maszyny Wirtualnej, może wystąpić błąd spowodowane jedną z dwóch sytuacji.

**Przyczyna 1:** usługa w chmurze hello jest przypięty tooa określonego klastra lub jest połączony tooan grupy koligacji i dlatego przypiętych tooa określonego klastra zgodnie z projektem. Dlatego żądania nowych zasobów obliczeniowych w tej grupie koligacji są sprawdzane w hello sam klastra, gdzie hostowane są hello istniejących zasobów. Jednak hello tego samego klastra może nie hello Obsługa żądany rozmiar maszyny Wirtualnej lub ma za mało dostępnego miejsca, powodując błąd alokacji. Jest to możliwe, czy nowe zasoby hello są tworzone przez nową usługę w chmurze albo przez istniejącą usługę w chmurze.

**Rozwiązanie 1:**

* Utwórz nową usługę w chmurze i powiązać ją z obszarem lub sieci wirtualnej na podstawie regionu.
* Utwórz nową maszynę Wirtualną w hello nową usługę w chmurze.
  Jeśli wystąpi błąd podczas próby toocreate nową usługę w chmurze, spróbuj ponownie później lub zmienić regionu hello hello usłudze w chmurze.

> [!IMPORTANT]
> Jeśli zostały próby toocreate nową maszynę Wirtualną w istniejącej usługi w chmurze, ale nie i ma toocreate nową usługę chmury dla nowej maszyny Wirtualnej, można wybrać tooconsolidate wszystkich maszyn wirtualnych w hello sama usługa w chmurze. toodo tak, Usuń maszyny wirtualne hello hello istniejących w usłudze w chmurze i ponownie je przechwycić z ich dysków w hello nową usługę w chmurze. Jest jednak ważne tooremember hello nową usługę w chmurze że nowej nazwy i adresu VIP, dlatego należy tooupdate tych opcji dla wszystkich zależności hello, które obecnie korzystanie z tej informacji hello istniejącą usługę w chmurze.
> 
> 

**Przyczyny 2:** usługa w chmurze hello jest skojarzona z siecią wirtualną, która jest tooan połączonej grupy koligacji, dlatego jest przypięty tooa określonego klastra zgodnie z projektem. Wszystkie nowe żądania zasobów obliczeniowych w tej grupie koligacji, w związku z tym są sprawdzane w hello sam klastra, gdzie hostowane są hello istniejących zasobów. Jednak hello tego samego klastra może nie hello Obsługa żądany rozmiar maszyny Wirtualnej lub ma za mało dostępnego miejsca, powodując błąd alokacji. Jest to możliwe, czy nowe zasoby hello są tworzone przez nową usługę w chmurze albo przez istniejącą usługę w chmurze.

**Rozdzielczość 2:**

* Tworzenie nowego regionalnej sieci wirtualnej.
* Tworzenie nowej maszyny Wirtualnej w nowej sieci wirtualnej hello hello.
* [Połączenie z istniejącą siecią wirtualną](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello nowej sieci wirtualnej. Zobacz więcej informacji [regionalnych sieci wirtualnych](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). Można też [migracji sieci wirtualnej na podstawie grupy koligacji tooa regionalnej sieci wirtualnej](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), a następnie utwórz hello nowej maszyny Wirtualnej.

## <a name="next-steps"></a>Następne kroki
Jeśli wystąpią problemy podczas uruchamiania zatrzymanej maszyny Wirtualnej systemu Linux lub zmień rozmiar istniejącej maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [klasycznego Rozwiązywanie problemów dotyczących wdrożenia z ponownym uruchomieniem lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Linux na platformie Azure](restart-resize-error-troubleshooting.md).

