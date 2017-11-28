---
title: aaaConnect maszyn wirtualnych platformy Azure tooLog Analytics | Dokumentacja firmy Microsoft
description: "Dla systemu Windows i Linux maszyn wirtualnych działających na platformie Azure, hello zalecane sposób dzienniki zebranych i metryki jest zainstalowanie hello rozszerzenia maszyny Wirtualnej Azure analizy dziennika. Możesz użyć hello portalu Azure lub programu PowerShell tooinstall hello analizy dzienników rozszerzenie maszyny wirtualnej na maszynach wirtualnych platformy Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="a637e-104">Połączenie maszyn wirtualnych platformy Azure tooLog Analytics przy użyciu agenta analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="a637e-104">Connect Azure virtual machines tooLog Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="a637e-105">Na komputerach z systemami Windows i Linux hello zalecana metoda zbierania dzienników i metryki jest zainstalowanie hello analizy dzienników agenta.</span><span class="sxs-lookup"><span data-stu-id="a637e-105">For Windows and Linux computers, hello recommended method for collecting logs and metrics is by installing hello Log Analytics agent.</span></span>

<span data-ttu-id="a637e-106">Hello najprostszy sposób tooinstall hello analizy dzienników agent na maszynach wirtualnych Azure jest za pośrednictwem hello rozszerzenia maszyny Wirtualnej analizy dziennika.</span><span class="sxs-lookup"><span data-stu-id="a637e-106">hello easiest way tooinstall hello Log Analytics agent on Azure virtual machines is through hello Log Analytics VM Extension.</span></span>  <span data-ttu-id="a637e-107">Przy użyciu rozszerzenia hello upraszcza proces instalacji hello i automatycznie konfiguruje hello agenta toosend danych toohello obszaru roboczego analizy dzienników przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a637e-107">Using hello extension simplifies hello installation process and automatically configures hello agent toosend data toohello Log Analytics workspace that you specify.</span></span> <span data-ttu-id="a637e-108">Hello agent jest również uaktualniana automatycznie, zapewnienie, że masz hello najnowsze funkcje i poprawki.</span><span class="sxs-lookup"><span data-stu-id="a637e-108">hello agent is also upgraded automatically, ensuring that you have hello latest features and fixes.</span></span>

<span data-ttu-id="a637e-109">W przypadku maszyn wirtualnych systemu Windows zostanie włączona hello *programu Microsoft Monitoring Agent* rozszerzenie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a637e-109">For Windows virtual machines, you enable hello *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="a637e-110">Dla maszyn wirtualnych systemu Linux, możesz włączyć hello *OMS agenta dla systemu Linux* rozszerzenie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a637e-110">For Linux virtual machines, you enable hello *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="a637e-111">Dowiedz się więcej o [rozszerzenia maszyny wirtualnej platformy Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i hello [agenta systemu Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a637e-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and hello [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="a637e-112">Korzystając z agenta na podstawie kolekcji danych dziennika, należy skonfigurować [źródeł danych w analizy dzienników](log-analytics-data-sources.md) toospecify hello dzienniki i metryki, które mają toocollect.</span><span class="sxs-lookup"><span data-stu-id="a637e-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics that you want toocollect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a637e-113">Konfigurowanie danych dzienników tooindex analizy dzienników przy użyciu [diagnostyki Azure](log-analytics-azure-storage.md), i skonfiguruj hello toocollect agenta hello sam dzienniki, a następnie dwukrotnie zebraniu dzienników hello.</span><span class="sxs-lookup"><span data-stu-id="a637e-113">If you configure Log Analytics tooindex log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure hello agent toocollect hello same logs, then hello logs are collected twice.</span></span> <span data-ttu-id="a637e-114">Naliczane są opłaty za obu źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="a637e-114">You are charged for both data sources.</span></span> <span data-ttu-id="a637e-115">Jeśli masz zainstalowany agent hello zbieranie danych dziennika przy użyciu tylko hello agenta — nie jest skonfigurowana danych dziennika toocollect analizy dzienników z diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="a637e-115">If you have hello agent installed, then collect log data by using only hello agent - don't configure Log Analytics toocollect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="a637e-116">Istnieją trzy sposoby łatwego rozszerzenia maszyny wirtualnej analizy dzienników hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="a637e-116">There are three easy ways tooenable hello Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="a637e-117">Za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a637e-117">By using hello Azure portal</span></span>
* <span data-ttu-id="a637e-118">Przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a637e-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="a637e-119">Za pomocą szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a637e-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a><span data-ttu-id="a637e-120">Włącz rozszerzenia maszyny Wirtualnej hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a637e-120">Enable hello VM extension in hello Azure portal</span></span>
<span data-ttu-id="a637e-121">Można zainstalować agenta powitania dla analizy dzienników i połączyć hello maszyny wirtualnej platformy Azure, którym jest on uruchamiany przy użyciu hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a637e-121">You can install hello agent for Log Analytics and connect hello Azure virtual machine that it runs on by using hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a><span data-ttu-id="a637e-122">tooinstall hello agenta analizy dzienników i połącz hello obszaru roboczego analizy dzienników tooa dla maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a637e-122">tooinstall hello Log Analytics agent and connect hello virtual machine tooa Log Analytics workspace</span></span>
1. <span data-ttu-id="a637e-123">Zaloguj się na powitania [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a637e-123">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="a637e-124">Wybierz **Przeglądaj** na powitania po lewej stronie operatora hello portalu, a następnie przejdź zbyt**analizy dzienników (OMS)** i zaznacz je.</span><span class="sxs-lookup"><span data-stu-id="a637e-124">Select **Browse** on hello left side of hello portal, and then go too**Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="a637e-125">Na liście obszarów roboczych usługi Analiza dzienników wybierz hello jedną, które mają toouse z hello maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a637e-125">In your list of Log Analytics workspaces, select hello one that you want toouse with hello Azure VM.</span></span>  
   ![Obszary robocze OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="a637e-127">W obszarze **dziennika zarządzania analytics**, wybierz pozycję **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="a637e-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="a637e-128">![Maszyny wirtualne](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="a637e-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="a637e-129">Lista hello **maszyn wirtualnych**, wybierz hello maszyny wirtualnej, na którym chcesz tooinstall hello agenta.</span><span class="sxs-lookup"><span data-stu-id="a637e-129">In hello list of **Virtual machines**, select hello virtual machine on which you want tooinstall hello agent.</span></span> <span data-ttu-id="a637e-130">Witaj **stan połączenia OMS** hello maszyny Wirtualnej wskazuje, że jest **niepołączone**.</span><span class="sxs-lookup"><span data-stu-id="a637e-130">hello **OMS connection status** for hello VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="a637e-131">![Maszyna wirtualna nie jest połączony](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="a637e-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="a637e-132">W szczegółach powitania dla maszyny wirtualnej, wybierz **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a637e-132">In hello details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="a637e-133">Hello agent jest automatycznie instalowany i konfigurowany dla obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="a637e-133">hello agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="a637e-134">Ten proces trwa kilka minut, w tym czasie jest hello stan połączenia OMS *łączenie...*</span><span class="sxs-lookup"><span data-stu-id="a637e-134">This process takes a few minutes, during which time hello OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="a637e-135">![Łączenie maszyny Wirtualnej](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="a637e-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="a637e-136">Po zainstalowaniu i połącz agenta hello hello **połączenia OMS** stan zostanie zaktualizowany tooshow **ten obszar roboczy**.</span><span class="sxs-lookup"><span data-stu-id="a637e-136">After you install and connect hello agent, hello **OMS connection** status will be updated tooshow **This workspace**.</span></span>  
   <span data-ttu-id="a637e-137">![Połączone](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="a637e-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-hello-vm-extension-using-powershell"></a><span data-ttu-id="a637e-138">Włączanie rozszerzenia maszyny Wirtualnej hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a637e-138">Enable hello VM extension using PowerShell</span></span>
<span data-ttu-id="a637e-139">Po skonfigurowaniu maszyny wirtualnej przy użyciu programu PowerShell, należy tooprovide hello **workspaceId** i **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="a637e-139">When you configure your virtual machine by using PowerShell, you need tooprovide hello **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="a637e-140">Witaj nazw właściwości w konfiguracji json **z uwzględnieniem wielkości liter**.</span><span class="sxs-lookup"><span data-stu-id="a637e-140">hello property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="a637e-141">Witaj identyfikator i klucz na powitania można znaleźć **ustawienia** portalu OMS hello, lub za pomocą programu PowerShell, jak pokazano w hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="a637e-141">You can find hello Id and key on hello **Settings** page of hello OMS portal, or by using PowerShell as shown in hello preceding example.</span></span>

![Identyfikator i klucz podstawowy](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="a637e-143">Ma innego polecenia Azure klasycznych maszyn wirtualnych i maszyn wirtualnych Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a637e-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="a637e-144">Poniżej przedstawiono przykłady dla klasycznego i maszyn wirtualnych Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a637e-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="a637e-145">W przypadku klasycznych maszyn wirtualnych Użyj hello poniższy przykład środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a637e-145">For classic virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="a637e-146">Dla Menedżera zasobów maszyn wirtualnych systemu Linux przy użyciu powitania po interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a637e-146">For Resource Manager Linux VMs using hello following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="a637e-147">Dla maszyn wirtualnych Menedżera zasobów Użyj hello poniższy przykład środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a637e-147">For Resource Manager virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a><span data-ttu-id="a637e-148">Wdrażanie hello rozszerzenia maszyny Wirtualnej przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="a637e-148">Deploy hello VM extension using a template</span></span>
<span data-ttu-id="a637e-149">Za pomocą usługi Azure Resource Manager, można utworzyć szablon określający hello wdrażania i konfiguracji aplikacji (w formacie JSON).</span><span class="sxs-lookup"><span data-stu-id="a637e-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines hello deployment and configuration of your application.</span></span> <span data-ttu-id="a637e-150">Ten szablon jest nazywany szablonem usługi Resource Manager i miejsce wdrożenia toodefine deklaratywne.</span><span class="sxs-lookup"><span data-stu-id="a637e-150">This template is known as a Resource Manager template and provides a declarative way toodefine deployment.</span></span> <span data-ttu-id="a637e-151">Za pomocą szablonu, wielokrotnie można wdrożyć aplikację w całym cyklu życia aplikacji hello i mieć pewność, że zasoby są wdrażane w spójnym stanie.</span><span class="sxs-lookup"><span data-stu-id="a637e-151">By using a template, you can repeatedly deploy your application throughout hello app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="a637e-152">W tym hello analizy dzienników agenta w ramach szablonu usługi Resource Manager, można Sprawdź, czy każda maszyna wirtualna jest obszaru roboczego analizy dzienników tooyour tooreport wstępnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="a637e-152">By including hello Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured tooreport tooyour Log Analytics workspace.</span></span>

<span data-ttu-id="a637e-153">Aby uzyskać więcej informacji na temat szablonów usługi Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a637e-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="a637e-154">Poniżej przedstawiono przykład szablonu usługi Resource Manager, który służy do wdrażania maszyny wirtualnej z systemem Windows z hello zainstalowane rozszerzenia programu Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="a637e-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with hello Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="a637e-155">Ten szablon jest szablon typowej maszyny wirtualnej z hello następujące dodatki:</span><span class="sxs-lookup"><span data-stu-id="a637e-155">This template is a typical virtual machine template, with hello following additions:</span></span>

* <span data-ttu-id="a637e-156">Parametry workspaceId i workspaceName</span><span class="sxs-lookup"><span data-stu-id="a637e-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="a637e-157">Sekcja rozszerzenia zasobu Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="a637e-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="a637e-158">Dane wyjściowe toolook hello workspaceId i workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="a637e-158">Outputs toolook up hello workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

<span data-ttu-id="a637e-159">Szablonu można wdrożyć przy użyciu następującego polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="a637e-159">You can deploy a template by using hello following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a><span data-ttu-id="a637e-160">Rozwiązywanie problemów z rozszerzenia maszyny Wirtualnej analizy dziennika hello</span><span class="sxs-lookup"><span data-stu-id="a637e-160">Troubleshooting hello Log Analytics VM extension</span></span>
<span data-ttu-id="a637e-161">Zwykle komunikat o błędzie w sytuacji, gdy elementy nie działają z portalu Azure lub programu Azure powershell.</span><span class="sxs-lookup"><span data-stu-id="a637e-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="a637e-162">Zaloguj się na powitania [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a637e-162">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="a637e-163">Znajdź hello maszyny Wirtualnej, a następnie otwórz szczegóły maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a637e-163">Find hello VM and open VM details.</span></span>
3. <span data-ttu-id="a637e-164">Kliknij przycisk **rozszerzenia** toocheck, jeśli rozszerzenie OMS jest włączone.</span><span class="sxs-lookup"><span data-stu-id="a637e-164">Click **Extensions** toocheck if OMS extension is enabled or not.</span></span>

   ![Widok rozszerzenia maszyny Wirtualnej](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="a637e-166">Kliknij przycisk hello *MicrosoftMonitoringAgent*(system Windows) lub *OmsAgentForLinux*rozszerzenia i wyświetlenia jej szczegółów (Linux).</span><span class="sxs-lookup"><span data-stu-id="a637e-166">Click hello *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Szczegóły rozszerzenia maszyny Wirtualnej](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="a637e-168">Rozwiązywanie problemów z maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a637e-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="a637e-169">Jeśli hello *programu Microsoft Monitoring Agent* nie instaluje rozszerzenia agenta maszyny Wirtualnej lub raportowania, można wykonać następujące kroki tootroubleshoot hello problem hello.</span><span class="sxs-lookup"><span data-stu-id="a637e-169">If hello *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="a637e-170">Sprawdź, czy agent maszyny Wirtualnej Azure hello jest zainstalowany i kroki pracy poprawnie, używając hello [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="a637e-170">Check if hello Azure VM agent is installed and working correctly by using hello steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="a637e-171">Można również przejrzeć plik dziennika agenta maszyny Wirtualnej hello`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="a637e-171">You can also review hello VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="a637e-172">Jeśli hello dziennika nie istnieje, agent maszyny Wirtualnej hello nie jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="a637e-172">If hello log does not exist, hello VM agent is not installed.</span></span>
     * [<span data-ttu-id="a637e-173">Zainstaluj hello Agent maszyny Wirtualnej na klasycznych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="a637e-173">Install hello Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="a637e-174">Potwierdź hello Microsoft Monitoring Agent rozszerzenia pulsu zadań została uruchomiona z użyciem hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a637e-174">Confirm hello Microsoft Monitoring Agent extension heartbeat task is running using hello following steps:</span></span>
   * <span data-ttu-id="a637e-175">Zaloguj się na maszynie wirtualnej toohello</span><span class="sxs-lookup"><span data-stu-id="a637e-175">Log in toohello virtual machine</span></span>
   * <span data-ttu-id="a637e-176">Otwórz Harmonogram zadań i Znajdź hello `update_azureoperationalinsight_agent_heartbeat` zadań</span><span class="sxs-lookup"><span data-stu-id="a637e-176">Open task scheduler and find hello `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="a637e-177">Potwierdź zadań hello jest włączona i działa co minutę.</span><span class="sxs-lookup"><span data-stu-id="a637e-177">Confirm hello task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="a637e-178">Sprawdź w pliku dziennika pulsu hello`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="a637e-178">Check hello heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="a637e-179">Przejrzyj pliki dzienników rozszerzenia maszyny Wirtualnej agenta monitorowania firmy Microsoft hello w`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="a637e-179">Review hello Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="a637e-180">Upewnij się, że maszyna wirtualna hello może uruchamiać skrypty programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a637e-180">Ensure hello virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="a637e-181">Upewnij się, że nie zostały zmienione uprawnienia C:\Windows\temp</span><span class="sxs-lookup"><span data-stu-id="a637e-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="a637e-182">Wyświetlanie stanu hello hello Microsoft Monitoring Agent, wpisując następujące polecenie w oknie programu PowerShell z podwyższonym poziomem uprawnień na maszynie wirtualnej hello hello`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="a637e-182">View hello status of hello Microsoft Monitoring Agent by typing hello following command in an elevated PowerShell window on hello virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="a637e-183">Przejrzyj pliki dziennika instalacji programu Microsoft Monitoring Agent hello w`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="a637e-183">Review hello Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="a637e-184">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z rozszerzeń systemu Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a637e-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="a637e-185">Rozwiązywanie problemów z maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="a637e-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="a637e-186">Jeśli hello *Agent pakietu OMS Linux* nie instaluje rozszerzenia agenta maszyny Wirtualnej lub raportowania, można wykonać następujące kroki tootroubleshoot hello problem hello.</span><span class="sxs-lookup"><span data-stu-id="a637e-186">If hello *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="a637e-187">Jeśli stan rozszerzenia hello jest *nieznany* Sprawdź, czy agent maszyny Wirtualnej Azure hello jest zainstalowany i działa poprawnie, przeglądając plik dziennika agenta maszyny Wirtualnej hello`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="a637e-187">If hello extension status is *Unknown* check if hello Azure VM agent is installed and working correctly by reviewing hello VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="a637e-188">Jeśli hello dziennika nie istnieje, agent maszyny Wirtualnej hello nie jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="a637e-188">If hello log does not exist, hello VM agent is not installed.</span></span>
   * [<span data-ttu-id="a637e-189">Zainstaluj hello Agent maszyny Wirtualnej na maszynach wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="a637e-189">Install hello Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="a637e-190">Dla innych stanów złej kondycji, przejrzyj hello Agent pakietu OMS dla rozszerzenia maszyny Wirtualnej systemu Linux pliki dziennika `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` i`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="a637e-190">For other unhealthy statuses, review hello OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="a637e-191">Jeśli stan rozszerzenia hello jest w dobrej kondycji, ale nie można przekazać danych przeglądać hello Agent pakietu OMS Linux pliki dziennika`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="a637e-191">If hello extension status is healthy, but data is not being uploaded review hello OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="a637e-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a637e-192">Next steps</span></span>
* <span data-ttu-id="a637e-193">Skonfiguruj [źródeł danych w analizy dzienników](log-analytics-data-sources.md) hello toospecify toocollect dzienniki i metryki.</span><span class="sxs-lookup"><span data-stu-id="a637e-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics toocollect.</span></span>
* <span data-ttu-id="a637e-194">toogather danych z maszyn wirtualnych [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="a637e-194">toogather data from virtual machines [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="a637e-195">[Zbieranie danych za pomocą diagnostyki Azure](log-analytics-azure-storage.md) dla innych zasobów, które są uruchomione na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a637e-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="a637e-196">Dla komputerów, które nie są na platformie Azure można zainstalować agenta analizy dzienników hello przy użyciu metody hello, które zostały opisane w hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="a637e-196">For computers that are not in Azure, you can install hello Log Analytics agent by using hello methods that are described in hello following articles:</span></span>

* [<span data-ttu-id="a637e-197">Połącz tooLog komputerów z systemem Windows analityka</span><span class="sxs-lookup"><span data-stu-id="a637e-197">Connect Windows computers tooLog Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="a637e-198">Połącz Linux komputerów tooLog analityka</span><span class="sxs-lookup"><span data-stu-id="a637e-198">Connect Linux computers tooLog Analytics</span></span>](log-analytics-linux-agents.md)
