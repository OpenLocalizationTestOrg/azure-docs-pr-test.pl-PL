---
title: "Przekaż obiekt JSON do elementu runbook usługi Automatyzacja Azure | Dokumentacja firmy Microsoft"
description: "Jak do przekazania parametrów do elementu runbook jako obiekt JSON"
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
ms.openlocfilehash: eac0e95a46731b9d396ea0590e629d61ca6a7d70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="pass-a-json-object-to-an-azure-automation-runbook"></a><span data-ttu-id="68cc8-104">Przekaż obiekt JSON do elementu runbook usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="68cc8-104">Pass a JSON object to an Azure Automation runbook</span></span>

<span data-ttu-id="68cc8-105">Może być przydatne do przechowywania danych, które mają zostać przekazane do elementu runbook w pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="68cc8-105">It can be useful to store data that you want to pass to a runbook in a JSON file.</span></span>
<span data-ttu-id="68cc8-106">Na przykład może utworzyć pliku JSON, który zawiera wszystkie parametry, które mają zostać przekazane do elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="68cc8-106">For example, you might create a JSON file that contains all of the parameters you want to pass to a runbook.</span></span>
<span data-ttu-id="68cc8-107">Aby to zrobić, należy skonwertowane do ciągu JSON, a następnie wykonać konwersję ciąg obiekt programu PowerShell przed przekazaniem ich do elementu runbook z jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="68cc8-107">To do this, you have to convert the JSON to a string and then convert the string to a PowerShell object before passing its contents to the runbook.</span></span>

<span data-ttu-id="68cc8-108">W tym przykładzie utworzymy skrypt programu PowerShell, który wywołuje [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) uruchomienia elementu runbook programu PowerShell, przekazywanie zawartości JSON do elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="68cc8-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a PowerShell runbook, passing the contents of the JSON to the runbook.</span></span>
<span data-ttu-id="68cc8-109">Element runbook programu PowerShell uruchamia maszyny Wirtualnej platformy Azure, pobieranie parametrów dla maszyny Wirtualnej z formatu JSON, która została przekazana.</span><span class="sxs-lookup"><span data-stu-id="68cc8-109">The PowerShell runbook starts an Azure VM, getting the parameters for the VM from the JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68cc8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="68cc8-110">Prerequisites</span></span>
<span data-ttu-id="68cc8-111">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="68cc8-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="68cc8-112">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68cc8-112">Azure subscription.</span></span> <span data-ttu-id="68cc8-113">Jeśli nie masz subskrypcji, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub <a href="/pricing/free-account/" target="_blank">[utworzyć bezpłatne konto](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="68cc8-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="68cc8-114">[Konto usługi Automation](automation-sec-configure-azure-runas-account.md) do przechowywania elementu Runbook i uwierzytelniania w zasobach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68cc8-114">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="68cc8-115">To konto musi mieć uprawnienia do uruchamiania i zatrzymywania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="68cc8-115">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="68cc8-116">Maszyna wirtualna platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68cc8-116">An Azure virtual machine.</span></span> <span data-ttu-id="68cc8-117">Będziemy uruchamiać i zatrzymywać tę maszynę, dlatego należy użyć maszyny innej niż produkcyjna.</span><span class="sxs-lookup"><span data-stu-id="68cc8-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="68cc8-118">Program Azure Powershell jest zainstalowane na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="68cc8-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="68cc8-119">Zobacz [Instalowanie i konfigurowanie programu Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) informacji o sposobie pobrania programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68cc8-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-json-file"></a><span data-ttu-id="68cc8-120">Utwórz plik JSON</span><span class="sxs-lookup"><span data-stu-id="68cc8-120">Create the JSON file</span></span>

<span data-ttu-id="68cc8-121">Wpisz następującego testu w pliku tekstowym, a następnie zapisz go jako `test.json` pozwalającego na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="68cc8-121">Type the following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-the-runbook"></a><span data-ttu-id="68cc8-122">Tworzenie elementu runbook</span><span class="sxs-lookup"><span data-stu-id="68cc8-122">Create the runbook</span></span>

<span data-ttu-id="68cc8-123">Utwórz nowy element runbook programu PowerShell o nazwie "Test-Json" automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="68cc8-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="68cc8-124">Aby dowiedzieć się, jak utworzyć nowy element runbook programu PowerShell, zobacz [Moje pierwszego elementu runbook programu PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="68cc8-124">To learn how to create a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="68cc8-125">Aby zaakceptować dane JSON, elementu runbook musi pobrać obiektu jako parametr wejściowy.</span><span class="sxs-lookup"><span data-stu-id="68cc8-125">To accept the JSON data, the runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="68cc8-126">Element runbook można użyć właściwości zdefiniowane w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="68cc8-126">The runbook can then use the properties defined in the JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect to Azure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object to actual JSON
$json = $json | ConvertFrom-Json

# Use the values from the JSON object as the parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="68cc8-127">Zapisz i Opublikuj ten element runbook do Twojego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="68cc8-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-the-runbook-from-powershell"></a><span data-ttu-id="68cc8-128">Wywołanie elementu runbook z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="68cc8-128">Call the runbook from PowerShell</span></span>

<span data-ttu-id="68cc8-129">Teraz można wywołać elementu runbook z komputera lokalnego przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68cc8-129">Now you can call the runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="68cc8-130">Uruchom następujące polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="68cc8-130">Run the following PowerShell commands:</span></span>

1. <span data-ttu-id="68cc8-131">Logowanie do platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="68cc8-131">Log in to Azure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="68cc8-132">Monit o podanie poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68cc8-132">You are prompted to enter your Azure credentials.</span></span>
1. <span data-ttu-id="68cc8-133">Pobierz zawartość pliku JSON i przekonwertować na ciąg:</span><span class="sxs-lookup"><span data-stu-id="68cc8-133">Get the contents of the JSON file and convert it to a string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="68cc8-134">`JsonPath`jest to ścieżka, w którym zapisano plik JSON.</span><span class="sxs-lookup"><span data-stu-id="68cc8-134">`JsonPath` is the path where you saved the JSON file.</span></span>
1. <span data-ttu-id="68cc8-135">Konwertowanie wartości ciągu `$json` na obiekt programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="68cc8-135">Convert the string contents of `$json` to a PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="68cc8-136">Utworzyć obiektu hashtable parametrów dla `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="68cc8-136">Create a hashtable for the parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="68cc8-137">Zwróć uwagę, że ustawiasz wartość `Parameters` na obiekt programu PowerShell, który zawiera wartości z pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="68cc8-137">Notice that you are setting the value of `Parameters` to the PowerShell object that contains the values from the JSON file.</span></span> 
1. <span data-ttu-id="68cc8-138">Uruchomić element runbook</span><span class="sxs-lookup"><span data-stu-id="68cc8-138">Start the runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="68cc8-139">Element runbook używa wartości z pliku JSON do uruchamiania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="68cc8-139">The runbook uses the values from the JSON file to start a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68cc8-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68cc8-140">Next steps</span></span>

* <span data-ttu-id="68cc8-141">Aby dowiedzieć się więcej na temat edytowania elementów runbook programu PowerShell i przepływ pracy programu PowerShell za pomocą edytora tekstową, zobacz [edycji tekstową elementy runbook automatyzacji Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="68cc8-141">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="68cc8-142">Aby dowiedzieć się więcej o tworzeniu i importowania elementów runbook, zobacz [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="68cc8-142">To learn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


