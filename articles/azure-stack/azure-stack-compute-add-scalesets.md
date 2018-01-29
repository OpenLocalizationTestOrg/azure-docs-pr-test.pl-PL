---
title: "Udostępnia zestawy skalowania maszyny wirtualnej Azure stosu"
description: "Dowiedz się, jak administrator chmury nie może dodać skalowania maszyny wirtualnej w portalu Azure Marketplace stosu"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 9/25/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: 31aeb963bdf4fd32712bc6f29f64060ec1c77cb8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a>Udostępnia zestawy skalowania maszyny wirtualnej Azure stosu

*Dotyczy: Azure stosu zintegrowanych systemów i Azure stosu Development Kit*

Zestawy skalowania maszyny wirtualnej są zasobów obliczeniowych Azure stosu. Można używać ich do wdrażania i zarządzania zestaw wiele identycznych maszyn wirtualnych. Z wszystkie maszyny wirtualne skonfigurowane tak samo, zestawy skalowania nie wymagają wstępnego inicjowania obsługi administracyjnej maszyn wirtualnych. Możliwe jest łatwiejsze tworzenie usług na dużą skalę, przeznaczonych dla dużych obliczeniowych, dane big data i konteneryzowanych obciążeń.

W tym temacie prowadzi użytkownika przez proces, aby udostępnić zestawy skalowania w portalu Azure Marketplace stosu. Po zakończeniu tej procedury użytkownicy mogą dodawać zestawy skalowania maszyny wirtualnej do subskrypcji.

Zestawy skalowania maszyny wirtualnej na stosie Azure są podobne zestawy skalowania maszyny wirtualnej na platformie Azure. Aby uzyskać więcej informacji zobacz następujące filmy wideo:
* [Mark Russinovich omawia zestawy skalowania na platformie Azure](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)
* [Zestawy skalowania maszyn wirtualnych według Guya Bowermana](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

Na stosie Azure zestawy skalowania maszyny wirtualnej nie obsługują automatycznego skalowania. Można dodać więcej wystąpień do skalowania, ustawić za pomocą portalu Azure stosu, szablony usługi Resource Manager lub programu PowerShell.

## <a name="prerequisites"></a>Wymagania wstępne
* **Narzędzia i programu PowerShell**

   Instalowanie i PowerShell skonfigurowanych dla stosu Azure i narzędzi Azure stosu. Zobacz [rozpocząć pracę przy użyciu programu PowerShell w stosie Azure](azure-stack-powershell-configure-quickstart.md).

   Po zainstalowaniu narzędzi Azure stosu, upewnij się, należy zaimportować następujące moduł programu PowerShell (ścieżka względem. \ComputeAdmin folderu w folderze AzureStack Narzędzia główne):

        Import-Module .\AzureStack.ComputeAdmin.psm1

* **Obraz systemu operacyjnego**

   Jeśli nie dodano obrazu systemu operacyjnego do programu Azure Marketplace stosu, zobacz [Dodaj obraz maszyny Wirtualnej systemu Windows Server 2016 do stosu Azure marketplace](azure-stack-add-default-image.md).

   Obsługę systemu Linux, Pobierz Ubuntu Server 16.04 i dodać go za pomocą ```Add-AzsVMImage``` z następującymi parametrami: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.

## <a name="add-the-virtual-machine-scale-set"></a>Dodaj zestaw skali maszyny wirtualnej

Edytuj poniższy skrypt programu PowerShell dla danego środowiska, a następnie uruchom go, aby dodać zestaw do programu Azure Marketplace stosu skalowania maszyny wirtualnej. 

``$User``to konto, które są używane do łączenia z portalu administratora. Na przykład serviceadmin@contoso.onmicrosoft.com.

```
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds
Select-AzureRmProfile -Profile $AzsEnvContext

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
```

## <a name="remove-a-virtual-machine-scale-set"></a>Usuń zestaw skali maszyny wirtualnej

Aby usunąć maszynę wirtualną skalować zestawu z elementem galerii, uruchom następujące polecenie programu PowerShell:

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> Nie można bezpośrednio usunąć elementu galerii. Należy odświeżyć portal kilka razy, zanim zostanie usunięte z portalu Marketplace.


## <a name="next-steps"></a>Następne kroki
[Często zadawane pytania dotyczące usługi Azure stosu](azure-stack-faq.md)

