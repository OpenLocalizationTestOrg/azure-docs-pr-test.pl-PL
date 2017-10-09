---
title: aaaAzure monitorowanie i maszyn wirtualnych z systemem Windows | Dokumentacja firmy Microsoft
description: "Samouczek — Monitor maszyny wirtualnej systemu Windows przy użyciu programu Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a>Umożliwia monitorowanie maszyny wirtualnej systemu Windows przy użyciu programu Azure PowerShell

Azure monitorowanie używa rozruchu toocollect agentów i danych dotyczących wydajności z maszyn wirtualnych platformy Azure, przechowywania tych danych w magazynie Azure i był dostępny za pośrednictwem portalu, hello modułu Azure PowerShell i hello wiersza polecenia platformy Azure. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Włącz diagnostykę rozruchu na maszynie Wirtualnej
> * Wyświetlanie diagnostyki rozruchu
> * Wyświetlaj metryki hosta maszyny Wirtualnej
> * Zainstaluj rozszerzenie diagnostyki hello
> * Wyświetlaj metryki maszyny Wirtualnej
> * Utwórz alert
> * Skonfiguruj zaawansowane monitorowanie

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

przykład Witaj toocomplete w tym samouczku, musi mieć istniejącej maszyny wirtualnej. Jeśli to konieczne, to [przykładowym skrypcie](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) można utworzyć. Podczas pracy samouczkiem hello, zastąp nazwę maszyny Wirtualnej, lokalizacji i grupy zasobów hello w razie potrzeby.

## <a name="view-boot-diagnostics"></a>Wyświetlanie diagnostyki rozruchu

Jak rozruchu maszyn wirtualnych systemu Windows, agenta diagnostyki rozruchu hello przechwytuje danych wyjściowych ekranu, który może służyć do rozwiązywania problemów z celem. Ta funkcja jest domyślnie włączona. Hello przechwycony ekran zrzuty są przechowywane na koncie magazynu platformy Azure, tworzona jest również domyślnie. 

Można uzyskać danych diagnostycznych hello rozruchu z hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) polecenia. W hello poniższy przykład, diagnostyki rozruchu są toohello pobranego katalogu głównego hello * c:\* dysku. 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a>Wyświetlaj metryki hosta

Maszyny Wirtualnej systemu Windows ma dedykowanego hosta maszyny Wirtualnej na platformie Azure, która współdziała ona z. Metryki są automatycznie pobierane dla hello hosta i mogą być wyświetlane w portalu Azure hello.

1. W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.
2. Kliknij przycisk **metryki** na hello bloku maszyny Wirtualnej, a następnie wybierz dowolną hello hosta metryki w obszarze **dostępne metryki** toosee jak wykonuje hello hosta maszyny Wirtualnej.

    ![Wyświetlaj metryki hosta](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a>Zainstaluj rozszerzenie diagnostyki

Witaj hosta podstawowe metryki są dostępne, ale toosee bardziej szczegółowe i metryki specyficzne dla maszyny Wirtualnej, możesz tooneed tooinstall hello Azure diagnostics rozszerzenia na powitania maszyny Wirtualnej. Witaj rozszerzenia diagnostyki Azure umożliwia dodatkowe funkcje monitorowania i diagnostyki toobe dane pobrane z hello maszyny Wirtualnej. Możesz wyświetlić te metryki wydajności i tworzyć alerty oparte na sposób wykonywania hello maszyny Wirtualnej. rozszerzenie diagnostycznych Hello jest instalowany za pośrednictwem portalu Azure hello:

1. W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.
2. Kliknij przycisk **ustawienia diagnostyki**. Lista Hello wskazuje, że *diagnostyki rozruchu* są już włączone w poprzedniej sekcji hello. Kliknij pole wyboru hello *podstawowe metryki*.
3. Kliknij przycisk hello **Włącz monitorowanie na poziomie gościa** przycisku.

    ![Wyświetlaj metryki diagnostycznych](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a>Wyświetlaj metryki maszyny Wirtualnej

Witaj metryki maszyny Wirtualnej można wyświetlić w hello taki sam sposób, aby wyświetlić metryki maszyny Wirtualnej hosta hello:

1. W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.
2. toosee wykonuje hello maszyny Wirtualnej, kliknij **metryki** na hello bloku maszyny Wirtualnej, a następnie wybierz dowolną hello diagnostyki metryki w obszarze **dostępne metryki**.

    ![Wyświetlaj metryki maszyny Wirtualnej](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a>Tworzenie alertów

Można tworzyć alertów w oparciu metryki dotyczące wydajności. Alerty można używane toonotify, który podczas średniego użycia procesora CPU przekracza określonego progu lub wolnego miejsca na dysku spada poniżej pewnego, np. Alerty są wyświetlane w portalu Azure hello lub mogą być wysyłane za pośrednictwem poczty e-mail. W odpowiedzi tooalerts generowaną może także wyzwolić elementu runbook usługi Automatyzacja Azure lub usługi Azure Logic Apps.

Witaj poniższy przykład tworzy alert dla średniego użycia procesora CPU.

1. W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.
2. Kliknij przycisk **reguły alertów** na powitania bloku maszyny Wirtualnej, następnie kliknij przycisk **Dodaj alert metryki** hello górze hello blok alerty.
4. Podaj **nazwa** alertu, takie jak *myAlertRule*
5. tootrigger alert, gdy procent użycia procesora CPU przekracza 1.0 przez pięć minut, pozostaw hello wszystkich innych wartości domyślnych wybrane.
6. Opcjonalnie, zaznacz pole hello *E-mail właściciele, współautorzy i czytelnicy* toosend powiadomienia e-mail. Akcja domyślna Hello jest toopresent powiadomienia w portalu hello.
7. Kliknij przycisk hello **OK** przycisku.

## <a name="advanced-monitoring"></a>Zaawansowane monitorowanie 

Możliwość bardziej zaawansowane monitorowanie maszyny wirtualnej za pomocą [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Jeśli nie zostało to jeszcze zrobione, należy zarejestrować się w celu [bezpłatnej wersji próbnej](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) programu Operations Management Suite.

Jeśli masz portalu OMS toohello dostępu można znaleźć identyfikator obszaru roboczego hello klucza i obszar roboczy w bloku ustawień hello. Użyj hello [AzureRmVMExtension zestaw](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) przekazana tootooadd hello OMS rozszerzenia toohello maszyny Wirtualnej. Aktualizacja hello zmiennej wartości w hello poniżej przykładowy tooreflect możesz OMS klucz obszaru roboczego i identyfikator obszaru roboczego  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

Po upływie kilku minut powinien zostać wyświetlony hello nowej maszyny Wirtualnej w obszarze roboczym pakietu OMS hello. 

![Blok OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Następne kroki
W tym samouczku został skonfigurowany i przejrzeć maszyn wirtualnych w Centrum zabezpieczeń Azure. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie sieci wirtualnej
> * Tworzenie grupy zasobów i maszyny Wirtualnej 
> * Włącz diagnostykę rozruchu na powitania maszyny Wirtualnej
> * Wyświetlanie diagnostyki rozruchu
> * Wyświetlaj metryki hosta
> * Zainstaluj rozszerzenie diagnostyki hello
> * Wyświetlaj metryki maszyny Wirtualnej
> * Utwórz alert
> * Skonfiguruj zaawansowane monitorowanie

Przejdź dalej toolearn samouczka toohello temat Centrum zabezpieczeń Azure.

> [!div class="nextstepaction"]
> [Zarządzanie zabezpieczeniami maszyn wirtualnych](./tutorial-azure-security.md)