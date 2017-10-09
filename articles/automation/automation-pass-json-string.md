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
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a><span data-ttu-id="68451-104">Przekaż element runbook usługi Automatyzacja Azure tooan obiekt JSON</span><span class="sxs-lookup"><span data-stu-id="68451-104">Pass a JSON object tooan Azure Automation runbook</span></span>

<span data-ttu-id="68451-105">Może to być przydatne toostore danych, które mają runbook tooa toopass w pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="68451-105">It can be useful toostore data that you want toopass tooa runbook in a JSON file.</span></span>
<span data-ttu-id="68451-106">Na przykład można utworzyć pliku JSON, który zawiera wszystkie parametry hello ma toopass tooa runbook.</span><span class="sxs-lookup"><span data-stu-id="68451-106">For example, you might create a JSON file that contains all of hello parameters you want toopass tooa runbook.</span></span>
<span data-ttu-id="68451-107">toodo, możesz mieć tooconvert hello JSON tooa ciągu, a następnie wykonać konwersję obiekt programu PowerShell tooa ciąg hello przed przekazaniem runbook toohello jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="68451-107">toodo this, you have tooconvert hello JSON tooa string and then convert hello string tooa PowerShell object before passing its contents toohello runbook.</span></span>

<span data-ttu-id="68451-108">W tym przykładzie utworzymy skrypt programu PowerShell, który wywołuje [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart runbook programu PowerShell, przekazywanie zawartości hello hello JSON toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="68451-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a PowerShell runbook, passing hello contents of hello JSON toohello runbook.</span></span>
<span data-ttu-id="68451-109">runbook programu PowerShell Hello uruchamia maszyny Wirtualnej platformy Azure, pobierania parametrów hello hello maszyny Wirtualnej z hello JSON, która została przekazana.</span><span class="sxs-lookup"><span data-stu-id="68451-109">hello PowerShell runbook starts an Azure VM, getting hello parameters for hello VM from hello JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68451-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="68451-110">Prerequisites</span></span>
<span data-ttu-id="68451-111">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="68451-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="68451-112">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68451-112">Azure subscription.</span></span> <span data-ttu-id="68451-113">Jeśli nie masz subskrypcji, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub <a href="/pricing/free-account/" target="_blank">[utworzyć bezpłatne konto](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="68451-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="68451-114">[Konto automatyzacji](automation-sec-configure-azure-runas-account.md) toohold hello elementu runbook i ich uwierzytelniać tooAzure zasobów.</span><span class="sxs-lookup"><span data-stu-id="68451-114">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="68451-115">To konto musi mieć uprawnienie toostart i zatrzymać hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="68451-115">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="68451-116">Maszyna wirtualna platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68451-116">An Azure virtual machine.</span></span> <span data-ttu-id="68451-117">Będziemy uruchamiać i zatrzymywać tę maszynę, dlatego należy użyć maszyny innej niż produkcyjna.</span><span class="sxs-lookup"><span data-stu-id="68451-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="68451-118">Program Azure Powershell jest zainstalowane na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="68451-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="68451-119">Zobacz [Instalowanie i konfigurowanie programu Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) informacje na temat tooget programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68451-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-json-file"></a><span data-ttu-id="68451-120">Utwórz plik JSON hello</span><span class="sxs-lookup"><span data-stu-id="68451-120">Create hello JSON file</span></span>

<span data-ttu-id="68451-121">Następujące hello typu testu w pliku tekstowym, a następnie zapisz go jako `test.json` pozwalającego na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="68451-121">Type hello following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a><span data-ttu-id="68451-122">Tworzenie elementu runbook hello</span><span class="sxs-lookup"><span data-stu-id="68451-122">Create hello runbook</span></span>

<span data-ttu-id="68451-123">Utwórz nowy element runbook programu PowerShell o nazwie "Test-Json" automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="68451-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="68451-124">toolearn toocreate nowy element runbook programu PowerShell, zobacz temat [Moje pierwszego elementu runbook programu PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="68451-124">toolearn how toocreate a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="68451-125">dane JSON hello tooaccept hello runbook należy wykonać obiekt jako parametr wejściowy.</span><span class="sxs-lookup"><span data-stu-id="68451-125">tooaccept hello JSON data, hello runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="68451-126">Hello runbook można użyć właściwości hello zdefiniowane w hello JSON.</span><span class="sxs-lookup"><span data-stu-id="68451-126">hello runbook can then use hello properties defined in hello JSON.</span></span>

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

 <span data-ttu-id="68451-127">Zapisz i Opublikuj ten element runbook do Twojego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="68451-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-hello-runbook-from-powershell"></a><span data-ttu-id="68451-128">Wywołanie elementu runbook hello z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="68451-128">Call hello runbook from PowerShell</span></span>

<span data-ttu-id="68451-129">Teraz można wywołać elementu runbook hello z komputera lokalnego przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68451-129">Now you can call hello runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="68451-130">Uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="68451-130">Run hello following PowerShell commands:</span></span>

1. <span data-ttu-id="68451-131">Zaloguj się tooAzure:</span><span class="sxs-lookup"><span data-stu-id="68451-131">Log in tooAzure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="68451-132">Możesz są tooenter zostanie wyświetlony monit o poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68451-132">You are prompted tooenter your Azure credentials.</span></span>
1. <span data-ttu-id="68451-133">Pobierz hello zawartość pliku JSON hello i przekonwertować go tooa ciągu:</span><span class="sxs-lookup"><span data-stu-id="68451-133">Get hello contents of hello JSON file and convert it tooa string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="68451-134">`JsonPath`jest ścieżką hello, w którym zapisano plik JSON hello.</span><span class="sxs-lookup"><span data-stu-id="68451-134">`JsonPath` is hello path where you saved hello JSON file.</span></span>
1. <span data-ttu-id="68451-135">Konwertuj ciąg hello zawartość `$json` tooa obiekt programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="68451-135">Convert hello string contents of `$json` tooa PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="68451-136">Utworzyć obiektu hashtable hello parametrów dla `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="68451-136">Create a hashtable for hello parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="68451-137">Zwróć uwagę, że ustawiasz wartość hello `Parameters` toohello obiekt programu PowerShell, który zawiera wartości hello z pliku JSON hello.</span><span class="sxs-lookup"><span data-stu-id="68451-137">Notice that you are setting hello value of `Parameters` toohello PowerShell object that contains hello values from hello JSON file.</span></span> 
1. <span data-ttu-id="68451-138">Uruchom hello runbook</span><span class="sxs-lookup"><span data-stu-id="68451-138">Start hello runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="68451-139">Hello runbook są używane wartości hello z toostart pliku JSON hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="68451-139">hello runbook uses hello values from hello JSON file toostart a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68451-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68451-140">Next steps</span></span>

* <span data-ttu-id="68451-141">Zobacz toolearn więcej informacji na temat edytowania elementów runbook programu PowerShell i przepływ pracy programu PowerShell w edytorze tekstową [edycji tekstową elementy runbook automatyzacji Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="68451-141">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="68451-142">toolearn więcej informacji na temat tworzenia i importowania elementów runbook, zobacz [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="68451-142">toolearn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


