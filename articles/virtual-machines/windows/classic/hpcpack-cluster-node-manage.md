---
title: "węzły obliczeniowe klastra HPC Pack aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o tooadd narzędzia skrypt programu PowerShell, Usuń, start i Zatrzymaj węzły obliczeniowe klastra HPC Pack 2012 R2 na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Zarządzanie numer hello i dostępności węzłów obliczeniowych w klastrze HPC Pack na platformie Azure
Utworzono klaster HPC Pack 2012 R2 w maszynach wirtualnych platformy Azure, możesz się, że sposoby tooeasily Dodawanie, usuwanie, start (zainicjować obsługi administracyjnej) lub niektóre Zatrzymaj (deprovision) obliczeniowe maszyn wirtualnych węzła w klastrze. toodo te zadania są uruchamiane skrypty programu Azure PowerShell, które są zainstalowane w węźle głównym hello maszyny Wirtualnej. Skrypty te umożliwiają kontrolę liczby hello i dostępności zasobów klastra HPC Pack, można kontrolować koszty.

> [!IMPORTANT] 
> Ten artykuł dotyczy tylko tooHPC Pack 2012 R2 klastrów w systemie Azure utworzonych przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.
> Ponadto hello skryptów programu PowerShell opisanych w tym artykule nie są dostępne w HPC Pack 2016.

## <a name="prerequisites"></a>Wymagania wstępne
* **Klaster HPC Pack 2012 R2 w maszynach wirtualnych platformy Azure**: Tworzenie klastra HPC Pack 2012 R2 w hello klasycznego modelu wdrażania. Na przykład można zautomatyzować hello wdrożenia przy użyciu obrazu HPC Pack 2012 R2 wirtualna hello w portalu Azure Marketplace hello i skrypt programu PowerShell systemu Azure. Aby uzyskać informacje i wymagania wstępne, zobacz [utworzyć klaster HPC z hello skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md).
  
    Po wdrożeniu Znajdź hello skrypty zarządzania węzła w lokalizacji % hello CCP\_folder bin % głównej na powitania węzła głównego. Uruchomić skrypty hello jako administrator.
* **Certyfikat zarządzania lub pliku ustawień publikowania na platformie Azure**: należy toodo jedną z następujących hello na powitania węzła głównego:
  
  * **Plik ustawień publikowania importu hello Azure**. toodo tego hello uruchom następujące polecenia cmdlet programu PowerShell Azure na powitania węzła głównego:
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * **Konfigurowanie certyfikatu zarządzania platformy Azure hello na powitania węzła głównego**. Jeśli plik .cer hello, zaimportuj go w magazynie certyfikatów CurrentUser\My hello, a następnie uruchom następujące polecenia cmdlet programu PowerShell Azure do środowiska Azure (AzureCloud lub AzureChinaCloud) hello:
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a>Dodaj węzeł obliczeniowy maszyny wirtualne
Dodaj węzły obliczeniowe z hello **HpcIaaSNode.ps1 Dodaj** skryptu.

### <a name="syntax"></a>Składnia
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a>Parametry
* **ServiceName**: Nazwa hello usługi w chmurze obliczeniowe nowego węzła maszyny wirtualne są dodawane do.
* **Nazwa_obrazu**: Nazwa obrazu maszyny Wirtualnej platformy Azure, który można uzyskać za pośrednictwem hello klasycznego portalu Azure lub polecenia cmdlet programu Azure PowerShell **Get-AzureVMImage**. Obraz powitania musi spełniać następujące wymagania hello:
  
  1. Musi być zainstalowany w systemie operacyjnym Windows.
  2. HPC Pack musi być zainstalowany w roli węzła obliczeń hello.
  3. Obraz powitania musi być prywatny obrazu w kategorii użytkownika hello nie publicznego obrazu maszyny Wirtualnej platformy Azure.
* **Ilość**: liczba toobe maszyn wirtualnych węzła obliczeń dodane.
* **InstanceSize**: rozmiar hello obliczeniowe węzła maszyn wirtualnych.
* **DomainUserName**: nazwa użytkownika domeny, które jest używane toojoin hello nowej domeny toohello maszyn wirtualnych.
* **DomainUserPassword**: hasło użytkownika domeny hello.
* **NodeNameSeries** (opcjonalnie): wzorzec nazewnictwa dla hello węzłów obliczeniowych. musi mieć Hello format &lt; *głównego\_nazwa*&gt;&lt;*Start\_numer*&gt;%. Na przykład MyCN % 10% środki szeregów hello obliczeniowe od MyCN11 nazwy węzła. Jeśli nie zostanie określony, hello skrypt używa hello skonfigurowany nazwy serii węzła w klastrze HPC hello.

### <a name="example"></a>Przykład
Witaj poniższy przykład umożliwia dodanie 20 węzła obliczeń duży rozmiar maszyn wirtualnych w usłudze w chmurze hello *hpcservice1*, oparte na obrazie maszyny Wirtualnej hello *hpccnimage1*.

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a>Usuń węzeł obliczeniowy maszyny wirtualne
Usuń węzły obliczeniowe z hello **HpcIaaSNode.ps1 Usuń** skryptu.

### <a name="syntax"></a>Składnia
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a>Parametry
* **Nazwa**: usunięte nazwy toobe węzłów klastra. Symbole wieloznaczne są obsługiwane. Nazwa zestawu parametrów Hello jest. Nie można określić zarówno hello **nazwa** i **węzła** parametrów.
* **Węzeł**: obiekt HpcNode powitania dla toobe węzłów hello usunięty, który można uzyskać za pomocą polecenia cmdlet środowiska PowerShell klastra HPC hello [błędzie Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). Nazwa zestawu parametrów Hello jest węzeł. Nie można określić zarówno hello **nazwa** i **węzła** parametrów.
* **DeleteVHD** (opcjonalnie): ustawienie toodelete hello skojarzone dyski hello maszyn wirtualnych, które zostały usunięte.
* **Wymuś** (opcjonalnie): ustawienie tooforce węzłów HPC w trybie offline przed ich usunięciem.
* **Potwierdź** (opcjonalnie): monitu o potwierdzenie przed wykonaniem polecenia hello.
* **WhatIf**: ustawienie toodescribe, co się stanie, jeśli wykonywane hello polecenie bez rzeczywistego wykonania polecenia hello.

### <a name="example"></a>Przykład
Witaj poniższy przykład wymusza węzłów hello w trybie offline z nazwami od *HPCNode-CN -* i usuwa je hello węzły i ich skojarzone dyski.

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a>Węzeł obliczeń początkowy maszyny wirtualne
Start obliczeniowe węzłów o hello **Start HpcIaaSNode.ps1** skryptu.

### <a name="syntax"></a>Składnia
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a>Parametry
* **Nazwa**: nazwy toobe węzłów klastra hello jest uruchomiona. Symbole wieloznaczne są obsługiwane. Nazwa zestawu parametrów Hello jest. Nie można określić zarówno hello **nazwa** i **węzła** parametrów.
* **Węzeł**-obiekt HpcNode powitania dla toobe węzłów hello pracę, który można uzyskać za pomocą polecenia cmdlet środowiska PowerShell klastra HPC hello [błędzie Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). Nazwa zestawu parametrów Hello jest węzeł. Nie można określić zarówno hello **nazwa** i **węzła** parametrów.

### <a name="example"></a>Przykład
Witaj poniższy przykład węzłów rozpoczyna się od nazwy rozpoczynające się *HPCNode-CN -*.

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a>Zatrzymaj węźle obliczeń maszyny wirtualne
Zatrzymaj węzły obliczeniowe z hello **Stop HpcIaaSNode.ps1** skryptu.

### <a name="syntax"></a>Składnia
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a>Parametry
* **Nazwa**-nazwy toobe węzłów klastra hello zatrzymana. Symbole wieloznaczne są obsługiwane. Nazwa zestawu parametrów Hello jest. Nie można określić zarówno hello **nazwa** i **węzła** parametrów.
* **Węzeł**: obiekt HpcNode powitania dla toobe węzłów hello zatrzymana, który można uzyskać za pomocą polecenia cmdlet środowiska PowerShell klastra HPC hello [błędzie Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). Nazwa zestawu parametrów Hello jest węzeł. Nie można określić zarówno hello **nazwa** i **węzła** parametrów.
* **Wymuś** (opcjonalnie): ustawienie tooforce węzłów HPC w trybie offline przed zatrzymaniem je.

### <a name="example"></a>Przykład
Witaj poniższy przykład wymusza węzłów w trybie offline z nazwami od *HPCNode-CN -* , a następnie zatrzymuje hello węzłów.

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a>Następne kroki
* tooautomatically wzrostu albo zmniejszyć węzłów klastra hello zgodnie z hello bieżące obciążenie zadań i zadań w klastrze hello, zobacz [automatycznie zwiększyć lub zmniejszyć zasobów klastra HPC Pack hello Azure zgodnie z obciążenie klastra toohello](hpcpack-cluster-node-autogrowshrink.md).

