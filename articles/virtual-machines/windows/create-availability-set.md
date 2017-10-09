---
title: "Ustaw aaaCreate dostępności maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak ustawić toocreate dostępności zarządzane lub niezarządzane dostępności dla maszyn wirtualnych przy użyciu programu Azure PowerShell lub hello portalu w modelu wdrażania usługi Resource Manager hello."
keywords: "Zestaw dostępności"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Zwiększenie dostępności maszyny Wirtualnej przez utworzenie zestawu dostępności Azure 
Zestawy dostępności zapewniają nadmiarowość tooyour aplikacji. Zalecamy grupowanie co najmniej dwie maszyny wirtualne w zestawie dostępności. Taka konfiguracja powoduje, że podczas albo planowanego lub nieplanowanego zdarzenia konserwacji, co najmniej jedna maszyna wirtualna będzie dostępna i spełniają hello 99,95% umowy SLA platformy Azure. Aby uzyskać więcej informacji, zobacz hello [umowy SLA dla maszyn wirtualnych](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Maszyny wirtualne muszą zostać utworzone w hello sam grupie zasobów co hello zestawu dostępności.
> 

Jeśli chcesz, aby maszyna wirtualna z toobe częścią zestawu dostępności, należy toocreate hello dostępności ustawić pierwszego lub podczas tworzenia pierwszej maszyny Wirtualnej w zestawie hello. Jeśli maszyna wirtualna zostanie używa dysków zarządzanych, zestaw dostępności hello należy utworzyć jako zestaw dostępności zarządzanego.

Aby uzyskać więcej informacji na temat tworzenia i używania zestawów dostępności, zobacz [Zarządzanie hello dostępność maszyn wirtualnych](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a>Użyj portalu toocreate hello zestaw dostępności przed Tworzenie maszyn wirtualnych
1. W menu centralnym powitania kliknij **Przeglądaj** i wybierz **zestawy dostępności**.
2. Na powitania **bloku zestawy dostępności**, kliknij przycisk **Dodaj**.
   
    ![Zrzut ekranu pokazujący hello Dodawanie przycisku do tworzenia nowego zestawu dostępności.](./media/create-availability-set/add-availability-set.png)
3. Na powitania **tworzenia zestawu dostępności** bloku, hello kompletne informacje dla zestawu.
   
    ![Zrzut ekranu, że pokazuje hello informacje dotyczące dostępności hello toocreate tooenter ustawiony.](./media/create-availability-set/create-availability-set.png)
   
   * **Nazwa** -hello nazwa powinna być 1 – 80 znaków składają się z liczb, liter, kropki, podkreślenia i łączniki. Witaj pierwszy znak musi być literą lub cyfrą. Witaj ostatni znak musi być literą, cyfrą lub znakiem podkreślenia.
   * **Odporność domen** -hello grupy maszyn wirtualnych, które współużytkują wspólne przełącznik źródła i sieci zasilania Definiowanie domen błędów. Domyślnie maszyny wirtualne hello są rozdzielone przez się toothree domen błędów i może być zmienione toobetween 1 i 3.
   * **Aktualizowanie domeny** — są domyślnie przypisane pięć domen aktualizacji i można go ustawić toobetween 1 do 20. Aktualizacja domen wskazują grupy maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać uruchomiony ponownie na powitania tym samym czasie. Na przykład jeśli określono domen, gdy więcej niż pięć maszyny wirtualne są skonfigurowane w ramach jednego zestawu dostępności, hello szóstego maszyny wirtualnej zostaną umieszczone w pięciu aktualizacji hello tej samej domenie aktualizacji pierwszej maszyny wirtualnej hello hello siódme w hello takie same UD jako hello drugiej maszyny wirtualnej i tak dalej. kolejność Hello hello ponownych uruchomień komputera nie może być sekwencyjnych, ale tylko jedna aktualizacja domeny zostanie uruchomiony ponownie w czasie.
   * **Subskrypcja** — wybierz hello toouse subskrypcji, jeśli masz więcej niż jeden.
   * **Grupa zasobów** — wybierz istniejącą grupę zasobów, klikając strzałkę hello i wybierając grupy zasobów z hello listy rozwijanej. Można również utworzyć nową grupę zasobów, wpisując nazwę. Witaj nazwa może zawierać żadnego z następujących znaków hello: litery, cyfry, kropki, łączniki, podkreślenia i otwierający i zamykający nawias okrągły. Nazwa Hello nie może kończyć się kropką. Wszystkie hello maszyn wirtualnych w grupie dostępności hello muszą toobe utworzone w hello tej samej grupie zasobów co hello zestawu dostępności.
   * **Lokalizacja** — wybrać lokalizację z listy rozwijanej hello.
   * **Zarządzane** — wybierz tę opcję *tak* toocreate zarządzanych dostępności ustawić toouse z maszynami wirtualnymi, które jako magazynu używały dysków zarządzanych. Wybierz **nr** Jeśli hello maszyn wirtualnych, które będą znajdować się w zestawie hello dysków niezarządzanego na koncie magazynu.
   
4. Po zakończeniu wprowadzania informacji powitania kliknij **Utwórz**. 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a>Użyj hello toocreate portalu maszynę wirtualną i dostępności ustawioną hello sam czas
W przypadku tworzenia nowej maszyny Wirtualnej za pomocą portalu hello, można również utworzyć nowy zbiór dostępności dla maszyny Wirtualnej hello podczas tworzenia hello pierwsza maszyna wirtualna w zestawie hello. Jeśli wybierzesz toouse zarządzane dysków dla maszyny Wirtualnej, zostanie utworzony zestaw dostępności zarządzanego.

![Zrzut ekranu pokazujący hello proces tworzenia dostępność nowych ustawić podczas tworzenia hello maszyny Wirtualnej.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a>Dodawanie nowej maszyny Wirtualnej tooan istniejącego zestawu dostępności w portalu hello
Dla każdej dodatkowe maszyny Wirtualnej tworzonej powinien należeć w zestawie hello, upewnij się, że tworzenie w hello sam **grupy zasobów** , a następnie wybierz hello istniejących zestawem dostępności w kroku 3. 

![Zrzut ekranu przedstawiający tooselect dostępności istniejącej konfiguracji toouse dla maszyny Wirtualnej.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a>Użyj programu PowerShell toocreate dostępności ustawić
W tym przykładzie tworzy zbiór nazwanego dostępności **myAvailabilitySet** w hello **myResourceGroup** grupy zasobów w hello **zachodnie stany USA** lokalizacji. Musi to zrobić przed utworzeniem hello toobe pierwsza maszyna wirtualna, która będzie hello zestawu.

Przed rozpoczęciem upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello. Uruchom hello następujących tooinstall polecenia.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).


Jeśli korzystasz z zarządzanego dyski dla maszyn wirtualnych, wpisz:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

Jeśli używasz konta magazynu dla maszyn wirtualnych, wpisz:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

Aby uzyskać więcej informacji, zobacz [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
* Podczas tworzenia maszyny Wirtualnej, jeśli zestaw dostępności hello nie jest na liście rozwijanej hello w portalu hello może utworzono go w innej grupie zasobów. Jeśli nie znasz hello grupy zasobów dla jego dostępność ustawić, przejdź menu centralnym toohello i kliknij przycisk Przeglądaj > toosee ustawia listę dostępności sieci i grupy zasobów, które należą do zestawy dostępności.

## <a name="next-steps"></a>Następne kroki
Dodaj tooyour dodatkowego magazynu maszyny Wirtualnej przez dodanie dodatkowych [dysku danych](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

