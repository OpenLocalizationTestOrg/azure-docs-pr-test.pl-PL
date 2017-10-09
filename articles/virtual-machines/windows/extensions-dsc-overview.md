---
title: "aaaDesired stanu konfiguracji dla platformy Azure — omówienie | Dokumentacja firmy Microsoft"
description: "Omówienie używania hello Microsoft Azure rozszerzenia obsługi dla konfiguracji żądanego stanu programu PowerShell. W tym wymagania wstępne, architektura, polecenia cmdlet."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>Wprowadzenie toohello Azure konfiguracji żądanego stanu rozszerzenia obsługi
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Witaj Agent maszyny Wirtualnej i skojarzonych rozszerzeń są częścią hello usługi infrastruktury platformy Microsoft Azure. Rozszerzenia maszyny Wirtualnej są składniki oprogramowania, które rozszerzyć funkcjonalność maszyny Wirtualnej hello i uproszczenia różne operacje zarządzania maszyny Wirtualnej. Na przykład hello rozszerzenia VMAccess może być tooreset używane hasło administratora lub hello niestandardowego skryptu rozszerzenia mogą być używane tooexecute skrypt na powitania maszyny Wirtualnej.

W tym artykule przedstawiono hello rozszerzenia konfiguracji żądanego stanu środowiska PowerShell (DSC) dla maszyn wirtualnych Azure w ramach hello zestawu SDK usługi Azure PowerShell. Można użyć nowego polecenia cmdlet tooupload i zastosowanie konfiguracji DSC środowiska PowerShell na maszynie Wirtualnej platformy Azure, włączyć hello rozszerzenia DSC środowiska PowerShell. wywołań rozszerzenia DSC środowiska PowerShell Hello hello tooenact DSC środowiska PowerShell otrzymała konfiguracji DSC na powitania maszyny Wirtualnej. Ta funkcja jest również dostępny za pośrednictwem hello portalu Azure.

## <a name="prerequisites"></a>Wymagania wstępne
**Komputer lokalny** toointeract z hello rozszerzenia maszyny Wirtualnej platformy Azure, należy toouse albo hello portalu Azure lub hello zestawu SDK usługi Azure PowerShell. 

**Agent gościa** hello maszyny Wirtualnej platformy Azure, skonfigurowaną przy konfiguracji hello DSC musi toobe systemu operacyjnego obsługującego albo Windows Management Framework (WMF) 4.0 lub 5.0. Witaj pełną listę obsługiwanych wersji systemu operacyjnego znajduje się w temacie hello [Historia wersji rozszerzenia DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).

## <a name="terms-and-concepts"></a>Definicje terminów i pojęć
W tym przewodniku zakłada się znajomość hello następujące pojęcia:

Konfiguracja — dokumentacja konfiguracji DSC. 

Węzeł - obiektu docelowego dla konfiguracji DSC. W tym dokumencie "węzła" zawsze dotyczy tooan maszyny Wirtualnej platformy Azure.

Dane konfiguracji — psd1 pliku zawierającego dane środowiska konfiguracji

## <a name="architectural-overview"></a>Omówienie architektury
Hello rozszerzenia usługi Konfiguracja DSC Azure używa toodeliver framework agenta maszyny Wirtualnej Azure hello, wprowadza i raport o konfiguracji DSC uruchomionych na maszynach wirtualnych platformy Azure. Witaj rozszerzenia DSC oczekuje, że plik zip zawiera co najmniej jeden dokument konfiguracji, a zestaw parametrów dostarczane za pośrednictwem hello zestawu SDK usługi Azure PowerShell lub hello portalu Azure.

Rozszerzenie hello jest wywoływana dla powitania po raz pierwszy, jest uruchamiany proces instalacji. Ten proces instaluje wersję hello Windows Management Framework (WMF) przy użyciu następującego logiki hello:

1. Witaj system operacyjny maszyny Wirtualnej platformy Azure w przypadku systemu Windows Server 2016, nie podjęto żadnej akcji. Windows Server 2016 już hello najnowszą wersję programu PowerShell jest zainstalowane.
2. Jeśli hello `wmfVersion` właściwość zostanie określony, ta wersja hello WMF jest zainstalowane, chyba że nie jest zgodny z systemem operacyjnym hello maszyny Wirtualnej.
3. Jeśli nie `wmfVersion` określona właściwość, hello najnowszych dotyczy hello WMF jest zainstalowana wersja.

Instalacja hello WMF wymaga ponownego uruchomienia komputera. Po ponownym uruchomieniu, rozszerzenia hello pobiera hello pliku zip określonego w hello `modulesUrl` właściwości. Jeśli ta lokalizacja znajduje się w magazynie obiektów blob platformy Azure, można określić tokenu sygnatury dostępu Współdzielonego w hello `sasToken` tooaccess właściwości hello pliku. Po pobraniu hello zip i rozpakowane, hello konfiguracji funkcji zdefiniowanej w `configurationFunction` uruchomieniu pliku MOF hello toogenerate. następnie uruchamia rozszerzenia Hello `Start-DscConfiguration -Force` w pliku MOF hello wygenerowany. rozszerzenie Hello przechwytuje dane wyjściowe i zapisuje go ponownie limit toohello Azure stan kanału. Z tego punktu na powitania DSC LCM obsługuje monitorowanie i korekty normalnie. 

## <a name="powershell-cmdlets"></a>Polecenia cmdlet programu PowerShell
Polecenia cmdlet programu PowerShell można używać z usługą Azure Resource Manager lub hello wdrażania klasycznego modelu toopackage, publikowanie i monitorować wdrożenia rozszerzenia usługi Konfiguracja DSC. Hello są następujące polecenia cmdlet na liście modułów wdrożenie klasyczne hello, ale można zastąpić "Azure" "AzureRm" toouse hello Azure Resource Manager modelu. Na przykład `Publish-AzureVMDscConfiguration` używa hello klasycznego modelu wdrażania, gdzie `Publish-AzureRmVMDscConfiguration` używa usługi Azure Resource Manager. 

`Publish-AzureVMDscConfiguration`przyjmuje w pliku konfiguracji, szuka zasoby zależne DSC i tworzy plik zip zawierający hello konfiguracji i DSC zasoby potrzebne tooenact hello. Można również utworzyć pakiet hello lokalnie za pomocą hello `-ConfigurationArchivePath` parametru. W przeciwnym razie publikuje magazynu obiektów blob tooAzure pliku zip hello i zabezpiecza go z tokenem sygnatury dostępu Współdzielonego.

plik zip Hello utworzone przez to polecenie cmdlet ma skryptu konfiguracji ps1 hello w głównym hello hello archiwum folder. Zasoby mają folder modułu hello umieszczony w folderze archiwum hello. 

`Set-AzureVMDscExtension`injects hello ustawienia wymagane przez rozszerzenia DSC środowiska PowerShell hello do obiektu konfiguracji maszyny Wirtualnej. W hello klasycznego modelu wdrażania, hello wirtualna zmiany muszą być zastosowane tooan maszyny Wirtualnej platformy Azure z `Update-AzureVM`. 

`Get-AzureVMDscExtension`pobiera stan rozszerzenia usługi Konfiguracja DSC hello określonej maszyny wirtualnej. 

`Get-AzureVMDscExtensionStatus`pobiera stan hello konfiguracji DSC hello wdrożonych przez hello DSC rozszerzenia obsługi. Akcję tę można wykonać na jednej maszyny Wirtualnej lub grupy maszyn wirtualnych.

`Remove-AzureVMDscExtension`Usuwa hello rozszerzenia obsługi z danej maszyny wirtualnej. To polecenie cmdlet jest **nie** Usuń konfigurację hello, odinstaluj hello WMF lub zmień ustawienia hello zastosowane na maszynie wirtualnej hello. Powoduje usunięcie tylko hello rozszerzenia obsługi. 

**Podstawowe różnice w poleceniach cmdlet ASM i usługi Azure Resource Manager**

* Polecenia cmdlet Menedżera zasobów systemu Azure są synchroniczne. Polecenia cmdlet funkcji ASM są asynchroniczne.
* ResourceGroupName, VMName ArchiveStorageAccountName, wersji i lokalizacji są wszystkie wymagane parametry usługi Azure Resource Manager.
* ArchiveResourceGroupName jest nowy parametr opcjonalny dla usługi Azure Resource Manager. Można określić tego parametru, jeśli konta magazynu należy tooa innej grupie zasobów niż hello co gdzie jest tworzona maszyna wirtualna hello.
* ConfigurationArchive jest nazywany ArchiveBlobName usługi Azure Resource Manager
* Właściwość ContainerName jest nazywany ArchiveContainerName usługi Azure Resource Manager
* StorageEndpointSuffix jest nazywany ArchiveStorageEndpointSuffix usługi Azure Resource Manager
* Dodano Hello AutoUpdate przełącznika tooAzure tooenable Resource Manager automatycznego aktualizowania hello rozszerzenia obsługi toohello najnowszej wersji jako i jest dostępny. Należy zauważyć, że ten parametr ma hello potencjalne toocause jest uruchamiany ponownie na powitania maszyny Wirtualnej, jeśli nowa wersja hello wydania WMF. 

## <a name="azure-portal-functionality"></a>Funkcje portalu Azure
Przeglądaj tooa maszyny Wirtualnej. W obszarze Ustawienia -> Ogólne kliknij polecenie "Rozszerzenia". Utworzono nowe okienko. Kliknij przycisk "Dodaj" i wybierz DSC środowiska PowerShell.

Hello portal wymaga danych wejściowych.
**Moduły konfiguracji lub skryptu**: to pole jest obowiązkowe. Wymaga pliku .ps1, zawierający skrypt konfiguracji lub pliku zip o ps1 skrypt konfiguracji w głównym hello i wszystkimi zasobami zależnymi w folderach modułu w ramach hello zip. Można tworzyć z hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` objęte hello zestawu SDK usługi Azure PowerShell polecenia cmdlet. plik zip Hello jest przekazywany do usługi magazynu obiektów blob użytkownika zabezpieczone przez tokenu sygnatury dostępu Współdzielonego. 

**Plik PSD1 danych konfiguracji**: to pole jest opcjonalne. Jeśli konfiguracja wymaga plik danych konfiguracji w psd1, użyj tego pola tooselect go i przekazać go tooyour magazynu obiektów blob użytkownika, gdy jest zabezpieczony przez tokenu sygnatury dostępu Współdzielonego. 

**Kwalifikowanej nazwy konfiguracji**: ps1 pliki mogą mieć wiele funkcji konfiguracyjnych. Wprowadź nazwę hello skryptu ps1 konfiguracji hello następuje "\' i nazwę hello hello konfiguracji funkcji. Na przykład jeśli ps1 skrypt ma nazwę hello "configuration.ps1", a konfiguracja hello jest "IisInstall", możesz wprowadzić:`configuration.ps1\IisInstall`

**Argumenty konfiguracji**: Jeśli funkcja Konfiguracja hello przyjmuje argumenty, wprowadź je tutaj w formacie hello `argumentName1=value1,argumentName2=value2`. Należy zauważyć, że ten format jest innym formacie niż sposób konfiguracji argumenty są akceptowane za pomocą poleceń cmdlet programu PowerShell lub Menedżera zasobów szablonów. 

## <a name="getting-started"></a>Wprowadzenie
Witaj rozszerzenia usługi Konfiguracja DSC Azure przyjmuje w dokumentach konfiguracji DSC i enacts ich na maszynach wirtualnych Azure. Prosty przykład konfiguracji jest zgodny. Zapisz go lokalnie jako "IisInstall.ps1":

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

Witaj, wykonując kroki miejscu hello IisInstall.ps1 skryptu na hello określonej maszyny Wirtualnej, wykonywania hello konfiguracji i wysyłać raporty o stanie.
###<a name="classic-model"></a>Modelu klasycznego
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a>Model usługi Azure Resource Manager

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a>Rejestrowanie
Dzienniki są umieszczane w:

C:\WindowsAzure\Logs\Plugins\Microsoft.PowerShell.DSC\[numer wersji]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o konfiguracji DSC środowiska PowerShell [odwiedź Centrum dokumentacji programu PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

Sprawdź hello [szablonu usługi Azure Resource Manager dla rozszerzenia hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

dodatkowe funkcje toofind można zarządzać w usłudze Konfiguracja DSC środowiska PowerShell, [Przejrzyj galerię programu PowerShell hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) więcej zasobów usługi Konfiguracja DSC.

Aby uzyskać szczegółowe informacje na przekazywanie parametrów poufnych do konfiguracji, zobacz [Zarządzanie poświadczeń bezpiecznie z hello DSC rozszerzenia obsługi](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

