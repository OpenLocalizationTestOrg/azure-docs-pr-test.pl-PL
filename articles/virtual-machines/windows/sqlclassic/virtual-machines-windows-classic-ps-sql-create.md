---
title: aaaCreate maszyny wirtualnej programu SQL Server w programie Azure PowerShell (klasyczne) | Dokumentacja firmy Microsoft
description: "Zawiera kroki i skryptów programu PowerShell do tworzenia maszyny Wirtualnej platformy Azure z obrazów Galeria maszyny wirtualnej programu SQL Server. W tym temacie używa trybu klasycznego wdrożenia hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Aprowizowanie maszyny wirtualnej programu SQL Server przy użyciu programu Azure PowerShell (klasyczne)

Ten artykuł zawiera kroki opisujące sposób toocreate maszynę wirtualną programu SQL Server na platformie Azure przy użyciu hello poleceń cmdlet programu PowerShell.

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

Wersja usługi Resource Manager hello tego tematu dla [Aprowizowanie maszyny wirtualnej programu SQL Server za pomocą Menedżera zasobów Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).

### <a name="install-and-configure-powershell"></a>Instalowanie i konfigurowanie programu PowerShell:
1. Jeśli nie masz konta platformy Azure, odwiedź stronę [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
2. [Pobierz i zainstaluj najnowsze poleceń programu Azure PowerShell hello](/powershell/azure/overview).
3. Uruchom program Windows PowerShell i podłącz go tooyour subskrypcji platformy Azure z hello **Add-AzureAccount** polecenia.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>Określić urządzenie docelowe region platformy Azure

Maszyny wirtualnej programu SQL Server będzie obsługiwana w systemie usługi chmury, która znajduje się w określonym regionie Azure. Hello następujące kroki pomocy możesz toodetermine Twojego regionu, konta magazynu i usługi w chmurze, który będzie używany dla hello pozostałej części samouczka hello.

1. Określ hello centrum danych, które mają toouse toohost maszyną Wirtualną programu SQL Server. Hello następującego polecenia programu PowerShell Wyświetla listę nazw dostępnych regionów.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. Po wyłaniają preferowanych lokalizacji, ustaw zmienną o nazwie **$dcLocation** toothat regionu. Na przykład Witaj następujące polecenie ustawia hello region zbyt "Wschodnie stany USA":

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>Ustaw konto subskrypcji i magazynu

1. Określ hello subskrypcji platformy Azure, które będą używane dla nowej maszyny wirtualnej hello.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. Przypisywanie sieci docelowej subskrypcji platformy Azure toohello **$subscr** zmiennej. Następnie ustaw jako Twojej bieżącej subskrypcji platformy Azure.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. Następnie sprawdź, czy istniejących kont magazynu. Witaj poniższy skrypt wyświetla wszystkie konta magazynu, które istnieją w wybranym regionie:

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > Jeśli potrzebujesz nowe konto magazynu, należy najpierw utworzyć nazwy konta magazynu liter wszystkich za pomocą polecenia hello AzureStorageAccount nowy jak hello poniższy przykład:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Przypisz hello docelowy magazyn konta Nazwa toohello **$staccount**. Następnie użyj **AzureSubscription zestaw** tooset hello subskrypcji i bieżącego konta magazynu.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>Wybierz obraz maszyny wirtualnej programu SQL Server

1. Dowiedz się hello listę dostępnych obrazów maszyn wirtualnych serwera SQL z galerii hello. Tych obrazów, wszystkie mają **ImageFamily** właściwość, która rozpoczyna się od "SQL". Witaj następujące zapytanie Wyświetla hello obrazu rodziny dostępne tooyou mające preinstalowany programu SQL Server.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Po znalezieniu rodziny obrazu maszyny wirtualnej hello w tej rodzinie może istnieć wiele obrazów opublikowanych. Użyj następujących hello skryptu toofind hello najnowszych opublikowanych nazwę maszyny wirtualnej obrazu dla rodziny wybranego obrazu (takich jak **programu SQL Server 2016 RTM przedsiębiorstwa w systemie Windows Server 2012 R2**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>Utwórz maszynę wirtualną hello

Na koniec Utwórz hello maszyny wirtualnej przy użyciu programu PowerShell:

1. Tworzenie chmury usługi toohost hello nowej maszyny Wirtualnej. Należy pamiętać, że również możliwe toouse istniejącą usługę w chmurze zamiast tego. Utwórz nową zmienną **$svcname** z krótką nazwą hello hello usługi w chmurze.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Określ nazwę maszyny wirtualnej hello i rozmiarze. Aby uzyskać więcej informacji na temat rozmiarów maszyn wirtualnych, zobacz [rozmiarów maszyn wirtualnych na platformie Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Określ hello konta administratora lokalnego i hasło.

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Uruchom hello następującej maszyny wirtualnej hello toocreate skryptu.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> Dla opcji konfiguracji i dodatkowe informacje, zobacz hello **Utwórz zestaw poleceń** sekcji [toocreate Użyj programu PowerShell Azure i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="example-powershell-script"></a>Przykładowy skrypt programu PowerShell

Witaj następującego skryptu przykładowego pełną skryptu, który tworzy **programu SQL Server 2016 RTM przedsiębiorstwa w systemie Windows Server 2012 R2** maszyny wirtualnej. Jeśli używasz tego skryptu, należy dostosować hello początkowej zmiennych hello poprzednie kroki w tym temacie.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>Uzyskuj dostęp do usług pulpitu zdalnego

1. Tworzenie plików RDP hello toolaunch folderu dokumentu hello bieżącego użytkownika instalacji toocomplete tych maszyn wirtualnych:

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. W katalogu dokumenty hello Uruchom plik RDP hello. Łączenie się z nazwą użytkownika administratora hello i hasło podane wcześniej (na przykład, jeśli nazwa użytkownika została VMAdmin, określ "\VMAdmin" jako użytkownik hello i podaj hasło hello).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Konfiguracja pełną hello hello komputera serwera SQL dla dostępu zdalnego

Po zalogowaniu się na komputerze toohello przy użyciu pulpitu zdalnego, skonfigurować program SQL Server na powitania instrukcje w podstawie [kroki związane z konfigurowaniem łączności z serwerem SQL w maszynie Wirtualnej platformy Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

## <a name="next-steps"></a>Następne kroki

Można znaleźć dodatkowe instrukcje dotyczące inicjowania obsługi administracyjnej maszyn wirtualnych przy użyciu programu PowerShell w hello [dokumentacji maszyn wirtualnych](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

W wielu przypadkach hello następnym krokiem jest toomigrate Twojego toothis baz danych nową maszynę Wirtualną programu SQL Server. Aby uzyskać wskazówki dotyczące migracji bazy danych, zobacz [Migrowanie tooSQL bazy danych serwera na maszynie Wirtualnej platformy Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Jeśli interesuje Cię również przy użyciu hello toocreate portalu Azure maszyny wirtualnej SQL, zobacz [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md). Należy pamiętać, że samouczek hello zalecanym modelu Resource Manager, a nie hello modelu klasycznego, używane w tym temacie PowerShell tekst hello przeszukiwań przez hello portal tworzy maszyny wirtualne za pomocą.

Ponadto toothese zasobów, firma Microsoft zaleca przejrzenie [innych tematach dotyczących programu SQL Server w usłudze Azure Virtual Machines toorunning](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
