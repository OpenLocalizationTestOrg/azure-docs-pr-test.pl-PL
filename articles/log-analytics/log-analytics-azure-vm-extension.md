---
title: "Nawiązać maszyn wirtualnych platformy Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Dla systemu Windows i Linux maszyn wirtualnych działających na platformie Azure zalecanym sposobem dzienniki zebranych i metryki jest instalowanie rozszerzenia maszyny Wirtualnej Azure analizy dziennika. Aby zainstalować rozszerzenie Log Analytics maszyny wirtualnej na maszynach wirtualnych platformy Azure, można użyć portalu Azure lub programu PowerShell."
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
ms.openlocfilehash: cdae291b546fef4d7fdb8b067c8e4f4c9708d43f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-azure-virtual-machines-to-log-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="becad-104">Uzyskuj dostęp do maszyn wirtualnych platformy Azure do analizy dzienników agenta analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="becad-104">Connect Azure virtual machines to Log Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="becad-105">Na komputerach z systemami Windows i Linux zbierania dzienników i metryki zaleca przez zainstalowanie agenta analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="becad-105">For Windows and Linux computers, the recommended method for collecting logs and metrics is by installing the Log Analytics agent.</span></span>

<span data-ttu-id="becad-106">Najprostszym sposobem zainstalowania agenta analizy dzienników na maszynach wirtualnych Azure jest za pośrednictwem rozszerzenia maszyny Wirtualnej analizy dziennika.</span><span class="sxs-lookup"><span data-stu-id="becad-106">The easiest way to install the Log Analytics agent on Azure virtual machines is through the Log Analytics VM Extension.</span></span>  <span data-ttu-id="becad-107">Przy użyciu rozszerzenia upraszcza proces instalacji i automatycznie konfiguruje agenta do wysyłania danych do obszaru roboczego analizy dzienników, który określisz.</span><span class="sxs-lookup"><span data-stu-id="becad-107">Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify.</span></span> <span data-ttu-id="becad-108">Agent jest również uaktualniana automatycznie, sprawdzeniu, czy masz najnowsze funkcje i poprawki.</span><span class="sxs-lookup"><span data-stu-id="becad-108">The agent is also upgraded automatically, ensuring that you have the latest features and fixes.</span></span>

<span data-ttu-id="becad-109">Dla maszyn wirtualnych systemu Windows, należy włączyć *programu Microsoft Monitoring Agent* rozszerzenie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="becad-109">For Windows virtual machines, you enable the *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="becad-110">Dla maszyn wirtualnych systemu Linux, możesz włączyć *OMS agenta dla systemu Linux* rozszerzenie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="becad-110">For Linux virtual machines, you enable the *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="becad-111">Dowiedz się więcej o [rozszerzenia maszyny wirtualnej platformy Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i [agenta systemu Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="becad-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and the [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="becad-112">Korzystając z agenta na podstawie kolekcji danych dziennika, należy skonfigurować [źródeł danych w analizy dzienników](log-analytics-data-sources.md) do określenia dzienników i metryki, które mają być zbierane.</span><span class="sxs-lookup"><span data-stu-id="becad-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics that you want to collect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="becad-113">Jeśli można skonfigurować do indeksowania danych dziennika analizy dzienników przy użyciu [diagnostyki Azure](log-analytics-azure-storage.md)i skonfigurować agenta, aby zebrać dzienniki tego samego, a następnie dzienniki są zbierane dwa razy.</span><span class="sxs-lookup"><span data-stu-id="becad-113">If you configure Log Analytics to index log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure the agent to collect the same logs, then the logs are collected twice.</span></span> <span data-ttu-id="becad-114">Naliczane są opłaty za obu źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="becad-114">You are charged for both data sources.</span></span> <span data-ttu-id="becad-115">Jeśli masz zainstalowany agent, zbieranie danych dziennika przy użyciu tylko agenta — nie jest skonfigurowana analizy dzienników do zbierania danych dziennika z diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="becad-115">If you have the agent installed, then collect log data by using only the agent - don't configure Log Analytics to collect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="becad-116">Istnieją trzy sposoby włączyć rozszerzenia maszyny wirtualnej analizy dzienników:</span><span class="sxs-lookup"><span data-stu-id="becad-116">There are three easy ways to enable the Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="becad-117">Za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="becad-117">By using the Azure portal</span></span>
* <span data-ttu-id="becad-118">Przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="becad-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="becad-119">Za pomocą szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="becad-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-the-vm-extension-in-the-azure-portal"></a><span data-ttu-id="becad-120">Włączanie rozszerzenia maszyny Wirtualnej w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="becad-120">Enable the VM extension in the Azure portal</span></span>
<span data-ttu-id="becad-121">Można zainstalować agenta dla analizy dzienników i połączyć maszyny wirtualnej platformy Azure, którym jest on uruchamiany przy użyciu [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="becad-121">You can install the agent for Log Analytics and connect the Azure virtual machine that it runs on by using the [Azure portal](https://portal.azure.com).</span></span>

### <a name="to-install-the-log-analytics-agent-and-connect-the-virtual-machine-to-a-log-analytics-workspace"></a><span data-ttu-id="becad-122">Aby zainstalować agenta analizy dzienników i podłącz maszynę wirtualną do obszaru roboczego analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="becad-122">To install the Log Analytics agent and connect the virtual machine to a Log Analytics workspace</span></span>
1. <span data-ttu-id="becad-123">Zaloguj się do [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="becad-123">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="becad-124">Wybierz **Przeglądaj** po lewej stronie portalu, a następnie przejdź do **analizy dzienników (OMS)** i zaznacz je.</span><span class="sxs-lookup"><span data-stu-id="becad-124">Select **Browse** on the left side of the portal, and then go to **Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="becad-125">Na liście obszarów roboczych usługi Analiza dzienników wybierz jedną, która ma być używany z maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="becad-125">In your list of Log Analytics workspaces, select the one that you want to use with the Azure VM.</span></span>  
   ![Obszary robocze OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="becad-127">W obszarze **dziennika zarządzania analytics**, wybierz pozycję **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="becad-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="becad-128">![Maszyny wirtualne](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="becad-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="becad-129">Na liście **maszyn wirtualnych**, wybierz maszynę wirtualną, na którym chcesz zainstalować agenta.</span><span class="sxs-lookup"><span data-stu-id="becad-129">In the list of **Virtual machines**, select the virtual machine on which you want to install the agent.</span></span> <span data-ttu-id="becad-130">**Stan połączenia OMS** dla maszyny Wirtualnej wskazuje, że jest **niepołączone**.</span><span class="sxs-lookup"><span data-stu-id="becad-130">The **OMS connection status** for the VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="becad-131">![Maszyna wirtualna nie jest połączony](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="becad-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="becad-132">Informacje dotyczące maszyny wirtualnej, wybierz **Connect**.</span><span class="sxs-lookup"><span data-stu-id="becad-132">In the details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="becad-133">Agent jest automatycznie instalowany i konfigurowany dla obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="becad-133">The agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="becad-134">Ten proces trwa kilka minut, w tym czasie jest stan połączenia OMS *łączenie...*</span><span class="sxs-lookup"><span data-stu-id="becad-134">This process takes a few minutes, during which time the OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="becad-135">![Łączenie maszyny Wirtualnej](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="becad-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="becad-136">Po zainstalowaniu i połącz agenta z **połączenia OMS** stan zostanie zaktualizowany w celu wyświetlenia **ten obszar roboczy**.</span><span class="sxs-lookup"><span data-stu-id="becad-136">After you install and connect the agent, the **OMS connection** status will be updated to show **This workspace**.</span></span>  
   <span data-ttu-id="becad-137">![Połączone](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="becad-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-the-vm-extension-using-powershell"></a><span data-ttu-id="becad-138">Włączanie rozszerzenia maszyny Wirtualnej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="becad-138">Enable the VM extension using PowerShell</span></span>
<span data-ttu-id="becad-139">Po skonfigurowaniu maszyny wirtualnej przy użyciu programu PowerShell, należy podać **workspaceId** i **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="becad-139">When you configure your virtual machine by using PowerShell, you need to provide the **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="becad-140">Nazwy właściwości w konfiguracji json są **z uwzględnieniem wielkości liter**.</span><span class="sxs-lookup"><span data-stu-id="becad-140">The property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="becad-141">Można znaleźć identyfikator i klucz na **ustawienia** strony portalu OMS lub przy użyciu programu PowerShell, jak pokazano w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="becad-141">You can find the Id and key on the **Settings** page of the OMS portal, or by using PowerShell as shown in the preceding example.</span></span>

![Identyfikator i klucz podstawowy](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="becad-143">Ma innego polecenia Azure klasycznych maszyn wirtualnych i maszyn wirtualnych Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="becad-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="becad-144">Poniżej przedstawiono przykłady dla klasycznego i maszyn wirtualnych Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="becad-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="becad-145">Klasycznych maszyn wirtualnych skorzystaj z następującego przykładu środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="becad-145">For classic virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="becad-146">Dla maszyn wirtualnych Menedżera zasobów systemu Linux przy użyciu następujących interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="becad-146">For Resource Manager Linux VMs using the following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="becad-147">Dla maszyn wirtualnych Menedżera zasobów skorzystaj z następującego przykładu środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="becad-147">For Resource Manager virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable to find OMS Workspace $workspaceName. Do you need to run Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-the-vm-extension-using-a-template"></a><span data-ttu-id="becad-148">Wdrażanie rozszerzenia maszyny Wirtualnej przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="becad-148">Deploy the VM extension using a template</span></span>
<span data-ttu-id="becad-149">Za pomocą usługi Azure Resource Manager, można utworzyć szablon (w formacie JSON), który definiuje wdrażania i konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="becad-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines the deployment and configuration of your application.</span></span> <span data-ttu-id="becad-150">Jest on nazywany szablonem usługi Resource Manager i pozwala na deklaratywne definiowanie wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="becad-150">This template is known as a Resource Manager template and provides a declarative way to define deployment.</span></span> <span data-ttu-id="becad-151">Za pomocą szablonu, wielokrotnie można wdrożyć aplikację w całym cyklu życia aplikacji i mieć pewność, że zasoby są wdrażane w spójnym stanie.</span><span class="sxs-lookup"><span data-stu-id="becad-151">By using a template, you can repeatedly deploy your application throughout the app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="becad-152">W tym agentem analizy dzienników jako część szablonu usługi Resource Manager, można upewnij się, że każda maszyna wirtualna jest wstępnie skonfigurowana do raportu do obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="becad-152">By including the Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured to report to your Log Analytics workspace.</span></span>

<span data-ttu-id="becad-153">Aby uzyskać więcej informacji na temat szablonów usługi Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="becad-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="becad-154">Poniżej przedstawiono przykład szablonu usługi Resource Manager, który służy do wdrażania maszyny wirtualnej z systemem Windows z rozszerzeniem Microsoft Monitoring Agent zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="becad-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with the Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="becad-155">Ten szablon jest szablon typowej maszyny wirtualnej, z następującymi dodatkami:</span><span class="sxs-lookup"><span data-stu-id="becad-155">This template is a typical virtual machine template, with the following additions:</span></span>

* <span data-ttu-id="becad-156">Parametry workspaceId i workspaceName</span><span class="sxs-lookup"><span data-stu-id="becad-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="becad-157">Sekcja rozszerzenia zasobu Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="becad-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="becad-158">Dane wyjściowe do odszukania workspaceId i workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="becad-158">Outputs to look up the workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for the Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for the Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for the Public IP. Must be lowercase. It should match with the following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
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
        "description": "The Windows version for the VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
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

<span data-ttu-id="becad-159">Szablonu można wdrożyć przy użyciu następującego polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="becad-159">You can deploy a template by using the following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-the-log-analytics-vm-extension"></a><span data-ttu-id="becad-160">Rozwiązywanie problemów z rozszerzenia maszyny Wirtualnej analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="becad-160">Troubleshooting the Log Analytics VM extension</span></span>
<span data-ttu-id="becad-161">Zwykle komunikat o błędzie w sytuacji, gdy elementy nie działają z portalu Azure lub programu Azure powershell.</span><span class="sxs-lookup"><span data-stu-id="becad-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="becad-162">Zaloguj się do [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="becad-162">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="becad-163">Znajdź maszyny Wirtualnej, a następnie otwórz szczegóły maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="becad-163">Find the VM and open VM details.</span></span>
3. <span data-ttu-id="becad-164">Kliknij przycisk **rozszerzenia** do sprawdzenia, czy rozszerzenie OMS jest włączone.</span><span class="sxs-lookup"><span data-stu-id="becad-164">Click **Extensions** to check if OMS extension is enabled or not.</span></span>

   ![Widok rozszerzenia maszyny Wirtualnej](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="becad-166">Kliknij przycisk *MicrosoftMonitoringAgent*(system Windows) lub *OmsAgentForLinux*rozszerzenia i wyświetlenia jej szczegółów (Linux).</span><span class="sxs-lookup"><span data-stu-id="becad-166">Click the *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Szczegóły rozszerzenia maszyny Wirtualnej](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="becad-168">Rozwiązywanie problemów z maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="becad-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="becad-169">Jeśli *programu Microsoft Monitoring Agent* nie instaluje rozszerzenia agenta maszyny Wirtualnej lub raporty, można wykonać następujące kroki, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="becad-169">If the *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="becad-170">Sprawdź, czy agent maszyny Wirtualnej platformy Azure jest zainstalowany i działa prawidłowo przy użyciu kroków w [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="becad-170">Check if the Azure VM agent is installed and working correctly by using the steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="becad-171">Można również przejrzeć plik dziennika agenta maszyny Wirtualnej`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="becad-171">You can also review the VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="becad-172">Jeśli dziennika nie istnieje, nie jest zainstalowany agent maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="becad-172">If the log does not exist, the VM agent is not installed.</span></span>
     * [<span data-ttu-id="becad-173">Zainstaluj agenta maszyny Wirtualnej platformy Azure na klasycznych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="becad-173">Install the Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="becad-174">Upewnij się, że zadanie pulsu rozszerzenie programu Microsoft Monitoring Agent działa, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="becad-174">Confirm the Microsoft Monitoring Agent extension heartbeat task is running using the following steps:</span></span>
   * <span data-ttu-id="becad-175">Zaloguj się do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="becad-175">Log in to the virtual machine</span></span>
   * <span data-ttu-id="becad-176">Otwórz Harmonogram zadań i Znajdź `update_azureoperationalinsight_agent_heartbeat` zadań</span><span class="sxs-lookup"><span data-stu-id="becad-176">Open task scheduler and find the `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="becad-177">Potwierdź zadania jest włączona i działa co minutę.</span><span class="sxs-lookup"><span data-stu-id="becad-177">Confirm the task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="becad-178">Sprawdź w pliku dziennika pulsu`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="becad-178">Check the heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="becad-179">Przejrzyj pliki dziennika rozszerzenia maszyny Wirtualnej agenta monitorowania firmy Microsoft w`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="becad-179">Review the Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="becad-180">Upewnij się, że maszyna wirtualna może uruchamiać skrypty programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="becad-180">Ensure the virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="becad-181">Upewnij się, że nie zostały zmienione uprawnienia C:\Windows\temp</span><span class="sxs-lookup"><span data-stu-id="becad-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="becad-182">Wyświetl stan programu Microsoft Monitoring Agent, wpisując następujące polecenie w oknie programu PowerShell z podwyższonym poziomem uprawnień na maszynie wirtualnej`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="becad-182">View the status of the Microsoft Monitoring Agent by typing the following command in an elevated PowerShell window on the virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="becad-183">Przejrzyj pliki dziennika instalacji programu Microsoft Monitoring Agent w`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="becad-183">Review the Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="becad-184">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z rozszerzeń systemu Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="becad-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="becad-185">Rozwiązywanie problemów z maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="becad-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="becad-186">Jeśli *Agent pakietu OMS Linux* nie instaluje rozszerzenia agenta maszyny Wirtualnej lub raporty, można wykonać następujące kroki, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="becad-186">If the *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="becad-187">Jeśli stan rozszerzenia *nieznany* Sprawdź, czy agent maszyny Wirtualnej platformy Azure jest zainstalowany i działa poprawnie, przeglądając plik dziennika agenta maszyny Wirtualnej`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="becad-187">If the extension status is *Unknown* check if the Azure VM agent is installed and working correctly by reviewing the VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="becad-188">Jeśli dziennika nie istnieje, nie jest zainstalowany agent maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="becad-188">If the log does not exist, the VM agent is not installed.</span></span>
   * [<span data-ttu-id="becad-189">Zainstaluj agenta maszyny Wirtualnej platformy Azure na maszynach wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="becad-189">Install the Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="becad-190">Dla innych stanów złej kondycji, przejrzyj Agent pakietu OMS dla rozszerzenia maszyny Wirtualnej systemu Linux pliki dziennika `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` i`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="becad-190">For other unhealthy statuses, review the OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="becad-191">Jeśli stan rozszerzenia jest w dobrej kondycji, ale nie można przekazać danych Przejrzyj Agent pakietu OMS dla plików dziennika systemu Linux`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="becad-191">If the extension status is healthy, but data is not being uploaded review the OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="becad-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="becad-192">Next steps</span></span>
* <span data-ttu-id="becad-193">Skonfiguruj [źródeł danych w analizy dzienników](log-analytics-data-sources.md) do określenia dzienników i metryk do zbierania.</span><span class="sxs-lookup"><span data-stu-id="becad-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics to collect.</span></span>
* <span data-ttu-id="becad-194">Aby zebrać dane z maszyn wirtualnych [rozwiązań dodać analizy dzienników z galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="becad-194">To gather data from virtual machines [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="becad-195">[Zbieranie danych za pomocą diagnostyki Azure](log-analytics-azure-storage.md) dla innych zasobów, które są uruchomione na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="becad-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="becad-196">Dla komputerów, które nie są na platformie Azure można zainstalować agenta analizy dzienników przy użyciu metod, które zostały opisane w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="becad-196">For computers that are not in Azure, you can install the Log Analytics agent by using the methods that are described in the following articles:</span></span>

* [<span data-ttu-id="becad-197">Łączenie komputerów z systemem Windows do analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="becad-197">Connect Windows computers to Log Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="becad-198">Łączenie komputerów z systemem Linux do analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="becad-198">Connect Linux computers to Log Analytics</span></span>](log-analytics-linux-agents.md)
