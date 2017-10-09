---
title: "aaaPass JSON obiekt runbook usługi Automatyzacja Azure tooan | Dokumentacja firmy Microsoft"
description: Jak toopass parametry tooa runbook jako obiekt JSON
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "środowiska PowerShell, elementu runbook, json, usługi Automatyzacja azure"
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a>Przekaż element runbook usługi Automatyzacja Azure tooan obiekt JSON

Może to być przydatne toostore danych, które mają runbook tooa toopass w pliku JSON.
Na przykład można utworzyć pliku JSON, który zawiera wszystkie parametry hello ma toopass tooa runbook.
toodo, możesz mieć tooconvert hello JSON tooa ciągu, a następnie wykonać konwersję obiekt programu PowerShell tooa ciąg hello przed przekazaniem runbook toohello jego zawartość.

W tym przykładzie utworzymy skrypt programu PowerShell, który wywołuje [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart runbook programu PowerShell, przekazywanie zawartości hello hello JSON toohello runbook.
runbook programu PowerShell Hello uruchamia maszyny Wirtualnej platformy Azure, pobierania parametrów hello hello maszyny Wirtualnej z hello JSON, która została przekazana.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy hello następujące:

* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub <a href="/pricing/free-account/" target="_blank">[utworzyć bezpłatne konto](https://azure.microsoft.com/free/).
* [Konto automatyzacji](automation-sec-configure-azure-runas-account.md) toohold hello elementu runbook i ich uwierzytelniać tooAzure zasobów.  To konto musi mieć uprawnienie toostart i zatrzymać hello maszyny wirtualnej.
* Maszyna wirtualna platformy Azure. Będziemy uruchamiać i zatrzymywać tę maszynę, dlatego należy użyć maszyny innej niż produkcyjna.
* Program Azure Powershell jest zainstalowane na komputerze lokalnym. Zobacz [Instalowanie i konfigurowanie programu Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) informacje na temat tooget programu Azure PowerShell.

## <a name="create-hello-json-file"></a>Utwórz plik JSON hello

Następujące hello typu testu w pliku tekstowym, a następnie zapisz go jako `test.json` pozwalającego na komputerze lokalnym.

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a>Tworzenie elementu runbook hello

Utwórz nowy element runbook programu PowerShell o nazwie "Test-Json" automatyzacji Azure.
toolearn toocreate nowy element runbook programu PowerShell, zobacz temat [Moje pierwszego elementu runbook programu PowerShell](automation-first-runbook-textual-powershell.md).

dane JSON hello tooaccept hello runbook należy wykonać obiekt jako parametr wejściowy.

Hello runbook można użyć właściwości hello zdefiniowane w hello JSON.

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 Zapisz i Opublikuj ten element runbook do Twojego konta automatyzacji.

## <a name="call-hello-runbook-from-powershell"></a>Wywołanie elementu runbook hello z programu PowerShell

Teraz można wywołać elementu runbook hello z komputera lokalnego przy użyciu programu Azure PowerShell.
Uruchom następujące polecenia programu PowerShell hello:

1. Zaloguj się tooAzure:
   ```powershell
   Login-AzureRmAccount
   ```
    Możesz są tooenter zostanie wyświetlony monit o poświadczenia platformy Azure.
1. Pobierz hello zawartość pliku JSON hello i przekonwertować go tooa ciągu:
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    `JsonPath`jest ścieżką hello, w którym zapisano plik JSON hello.
1. Konwertuj ciąg hello zawartość `$json` tooa obiekt programu PowerShell:
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. Utworzyć obiektu hashtable hello parametrów dla `Start-AzureRmAutomstionRunbook`:
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   Zwróć uwagę, że ustawiasz wartość hello `Parameters` toohello obiekt programu PowerShell, który zawiera wartości hello z pliku JSON hello. 
1. Uruchom hello runbook
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

Hello runbook są używane wartości hello z toostart pliku JSON hello maszyny Wirtualnej.

## <a name="next-steps"></a>Następne kroki

* Zobacz toolearn więcej informacji na temat edytowania elementów runbook programu PowerShell i przepływ pracy programu PowerShell w edytorze tekstową [edycji tekstową elementy runbook automatyzacji Azure](automation-edit-textual-runbook.md) 
* toolearn więcej informacji na temat tworzenia i importowania elementów runbook, zobacz [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md)


