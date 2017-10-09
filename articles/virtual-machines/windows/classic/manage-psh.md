---
title: "aaaManage maszyn wirtualnych przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej poleceń służy tooautomate zadań zarządzania maszyn wirtualnych."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Zarządzanie maszynami wirtualnymi przy użyciu programu Azure PowerShell
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Przy użyciu modelu Resource Manager hello typowych poleceń programu PowerShell, zobacz [tutaj](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Wiele zadań, czy maszyny wirtualne toomanage każdego dnia można zautomatyzować za pomocą poleceń cmdlet programu Azure PowerShell. Ten artykuł zawiera przykładowe polecenia zadania prostszy i tooarticles łącza, zawierające hello polecenia dla bardziej złożonych zadań.

> [!NOTE]
> Jeśli nie zostało to jeszcze zainstalowaniu i skonfigurowaniu programu Azure PowerShell, ale można wyświetlić instrukcje w artykule hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
> 
> 

## <a name="how-toouse-hello-example-commands"></a>Jak toouse hello przykładowe polecenia
Będziesz potrzebować tooreplace część tekstu hello w hello poleceń z tekstem, który jest odpowiedni dla danego środowiska. Witaj < i > symbole wskazują należy tooreplace tekstu. Zastąp tekst hello, Usuń symbole hello, ale pozostawić hello znaki cudzysłowu w miejscu.

## <a name="get-a-vm"></a>Uzyskiwanie maszyny Wirtualnej
Jest to podstawowe zadania, które będzie używane. Używać jej tooget informacji o maszynie Wirtualnej, wykonywania zadań na maszynie Wirtualnej lub pobrać dane wyjściowe toostore w zmiennej.

tooget informacji na temat hello maszynę Wirtualną, uruchom następujące polecenie, zastępując wszystko w cudzysłowy hello, w tym hello < i > znaków:

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

dane wyjściowe w zmiennej $vm hello toostore Uruchom:

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>Zaloguj się na tooa maszyny Wirtualnej z systemem Windows
Uruchom następujące polecenia:

> [!NOTE]
> Witaj maszyny wirtualnej i nazwa usługi w chmurze można uzyskać z widoku hello hello **Get-AzureVM** polecenia.
> 
> $svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< dysk i folder lokalizacji toostore hello pobrany plik RDP, na przykład: c:\temp >" $localFile = $localPath + "\" $vmname +"RDP"Get-AzureRemoteDesktopFile - ServiceName $svcName-Name $vmName - LocalPath $localFile — uruchamianie
> 
> 

## <a name="stop-a-vm"></a>Zatrzymywanie maszyny wirtualnej
Uruchom następujące polecenie:

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> Użyj tego hello tookeep parametru wirtualnego adresu IP (VIP) hello chmury usługi, w razie hello ostatnia maszyna wirtualna w tej usłudze w chmurze. <br><br> Jeśli parametr hello StayProvisioned, nadal zostaną naliczone opłaty dla hello maszyny Wirtualnej.
> 
> 

## <a name="start-a-vm"></a>Uruchamianie maszyny wirtualnej
Uruchom następujące polecenie:

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>Dołączanie dysku danych
To zadanie wymaga kilku kroków. Najpierw użyj hello *** Add-AzureDataDisk *** polecenia cmdlet tooadd hello dysku toohello $vm obiektu. Następnie należy użyć **AzureVM aktualizacji** polecenia cmdlet tooupdate hello konfiguracji hello maszyny Wirtualnej.

Należy również toodecide czy tooattach nowy dysk lub jeden zawierający dane. Dla nowego dysku hello polecenie tworzy plik VHD hello i dołącza go.

tooattach nowego dysku, uruchom następujące polecenie:

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

tooattach istniejący dysk danych, uruchom następujące polecenie:

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

tooattach dysków danych z istniejącego pliku VHD w magazynie obiektów blob, uruchom następujące polecenie:

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Tworzenie maszyny Wirtualnej z systemem Windows
toocreate nowej systemu Windows maszyny wirtualnej na platformie Azure, użyj instrukcji hello w [toocreate użycia programu Azure PowerShell i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](create-powershell.md). Kroki tego tematu użytkownika przez proces tworzenia hello programu Azure PowerShell zestawu poleceń tworzy Maszynę wirtualną z systemem Windows można wstępnie:

* Z członkostwa w domenie usługi Active Directory.
* W przypadku dodatkowych dysków.
* Jako element członkowski istniejącej równoważeniem obciążenia należy ustawić.
* Za pomocą statycznego adresu IP.

