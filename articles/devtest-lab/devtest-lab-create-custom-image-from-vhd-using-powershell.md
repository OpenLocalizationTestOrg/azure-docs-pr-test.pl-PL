---
title: "aaaCreate Azure DevTest Labs niestandardowego obrazu z pliku VHD za pomocą programu PowerShell | Dokumentacja firmy Microsoft"
description: "Zautomatyzować tworzenie obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą programu PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 39b4005fa46cdf86cf0800ca376128134bcfb650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a>Tworzenie niestandardowego obrazu z pliku VHD za pomocą programu PowerShell

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Instrukcje krok po kroku

Witaj następujących krokach objaśniono sposób tworzenia niestandardowego obrazu z pliku VHD za pomocą programu PowerShell:

1. W wierszu polecenia programu PowerShell Zaloguj tooyour konto platformy Azure z powitania po wywołaniu toohello **Login-AzureRmAccount** polecenia cmdlet.  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  Wybierz hello pożądane subskrypcji platformy Azure przez wywołanie hello **Select-AzureRmSubscription** polecenia cmdlet. Zastąp powitania po symbolu zastępczego dla hello **$subscriptionId** zmiennej z identyfikatorem ważnej subskrypcji platformy Azure. 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  Pobierz obiekt laboratorium hello przez wywołanie hello **Get-AzureRmResource** polecenia cmdlet. Zastąp następujące symbole zastępcze hello hello **$labRg** i **$labName** zmiennych o hello odpowiednie wartości dla danego środowiska. 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  Pobierz konta magazynu laboratorium hello i konta magazynu laboratorium wartości kluczy z hello laboratorium obiektu. 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  Zastąp powitania po symbolu zastępczego dla hello **$vhdUri** zmiennej z identyfikatora URI hello tooyour przekazany plik VHD. Plik VHD hello identyfikatora URI może pobrać z bloku obiektu blob konta magazynu hello w hello portalu Azure.

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  Tworzenie niestandardowego obrazu hello przy użyciu hello **AzureRmResourceGroupDeployment nowy** polecenia cmdlet. Zastąp następujące symbole zastępcze hello hello **$customImageName** i **$customImageDescription** nazwy toomeaningful zmienne dla danego środowiska.

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a>Toocreate skrypt programu PowerShell niestandardowego obrazu z pliku VHD

Witaj następującego skryptu programu PowerShell może być używane toocreate niestandardowego obrazu z pliku VHD. Zastąp zastępcze hello (początkową i końcową z nawiasy) hello odpowiednie wartości do własnych potrzeb. 

```PowerShell
# Log in tooyour Azure account.  
Login-AzureRmAccount

# Select hello desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get hello lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get hello lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set hello URI of hello VHD file.  
$vhdUri = '<Specify hello VHD URI here>'

# Set hello custom image name and description values.
$customImageName = '<Specify hello custom image name>'
$customImageDescription = '<Specify hello custom image description>'

# Set up hello parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create hello custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a>Wpisy na blogu pokrewne

- [Niestandardowe obrazy lub formuł?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Kopiowanie obrazów niestandardowych między Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Następne kroki

- [Dodawanie laboratorium tooyour maszyny Wirtualnej](./devtest-lab-add-vm-with-artifacts.md)
