---
title: "Konfiguracja konta usługi Automatyzacja Azure aaaValidate | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfiguracji hello tooconfirm Twojego konta automatyzacji jest poprawnie skonfigurowana."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a>Sprawdzanie uwierzytelniania konta Uruchom jako usługi Azure Automation
Po pomyślnym utworzeniu konta automatyzacji, można wykonywać tooconfirm prosty test, możesz toosuccessfully uwierzytelniania usługi Azure Resource Manager lub Azure wdrożenie klasyczne z nowo utworzonych lub zaktualizowanych automatyzacji konta Uruchom jako.    

## <a name="automation-run-as-authentication"></a>Uwierzytelnianie konta Uruchom jako usługi Automation
Za pomocą hello przykładowy kod poniżej[tworzenia elementu runbook programu PowerShell](automation-creating-importing-runbook.md) tooverify uwierzytelnianie przy użyciu hello Uruchom jako konta, a także w tooauthenticate z niestandardowych elementów runbook oraz zarządzanie tymi zasobami usługi Resource Manager przy użyciu konta automatyzacji.   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

Zwróć uwagę, hello polecenie cmdlet używane do uwierzytelniania w elemencie runbook hello - **Add-AzureRmAccount**, używa hello *ServicePrincipalCertificate* zestaw parametrów.  Uwierzytelnia się ono za pomocą certyfikatu nazwy głównej usługi, a nie poświadczeń.  

Gdy możesz [uruchamiania elementu runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate konta Uruchom jako [zadanie elementu runbook](automation-runbook-execution.md) jest utworzony, bloku zadania hello jest wyświetlane, a stan zadania hello w hello **Podsumowanie zadania**kafelka. Stan zadania Hello zostanie uruchomiona jako *w kolejce* wskazujący, że oczekuje na proces roboczy elementu runbook, w toobecome chmury hello dostępne. Będzie on przenoszony za*uruchamianie* gdy pracownik oświadczeń hello zadania, a następnie *systemem* , gdy element runbook hello faktycznie zacznie działać.  Po zakończeniu zadania elementu runbook hello, możemy powinna zostać wyświetlona stan **Ukończono**.

toosee hello szczegółowe wyniki hello elementu runbook, kliknij na powitania **dane wyjściowe** kafelka.  Na powitania **dane wyjściowe** bloku, powinien zostać wyświetlony został pomyślnie uwierzytelniony i zwraca listę wszystkich zasobów we wszystkich grupach zasobów w ramach subskrypcji.  

Pamiętaj tylko tooremove hello blok kodu, począwszy od komentarza hello `#Get all ARM resources from all resource groups` kiedy ponowne użycie hello kodu dla elementy runbook.

## <a name="classic-run-as-authentication"></a>Uwierzytelnianie klasycznego konta Uruchom jako
Za pomocą hello przykładowy kod poniżej[tworzenia elementu runbook programu PowerShell](automation-creating-importing-runbook.md) tooverify uwierzytelnianie przy użyciu hello Classic Uruchom jako konta, a także w tooauthenticate z niestandardowych elementów runbook i zarządzanie zasobami w hello klasycznego modelu wdrażania.  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

Gdy możesz [uruchamiania elementu runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate konta Uruchom jako [zadanie elementu runbook](automation-runbook-execution.md) jest utworzony, bloku zadania hello jest wyświetlane, a stan zadania hello w hello **Podsumowanie zadania**kafelka. Stan zadania Hello zostanie uruchomiona jako *w kolejce* wskazujący, że oczekuje na proces roboczy elementu runbook, w toobecome chmury hello dostępne. Będzie on przenoszony za*uruchamianie* gdy pracownik oświadczeń hello zadania, a następnie *systemem* , gdy element runbook hello faktycznie zacznie działać.  Po zakończeniu zadania elementu runbook hello, możemy powinna zostać wyświetlona stan **Ukończono**.

toosee hello szczegółowe wyniki hello elementu runbook, kliknij na powitania **dane wyjściowe** kafelka.  Na powitania **dane wyjściowe** bloku, powinien zostać wyświetlony został pomyślnie uwierzytelniony i zwraca listę wszystkich maszyn wirtualnych platformy Azure przez VMName, które są wdrażane w ramach subskrypcji.  

Pamiętaj tylko polecenia cmdlet hello tooremove **Get AzureVM** kiedy ponowne użycie hello kodu dla elementy runbook.

## <a name="next-steps"></a>Następne kroki
* tooget pracę z elementów runbook programu PowerShell, zobacz [Moje pierwszego elementu runbook programu PowerShell](automation-first-runbook-textual-powershell.md).
* Zobacz toolearn więcej informacji na temat tworzenia graficznego [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md).
