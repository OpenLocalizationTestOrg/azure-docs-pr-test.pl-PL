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
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>Połączenie maszyn wirtualnych platformy Azure tooLog Analytics przy użyciu agenta analizy dzienników

Na komputerach z systemami Windows i Linux hello zalecana metoda zbierania dzienników i metryki jest zainstalowanie hello analizy dzienników agenta.

Hello najprostszy sposób tooinstall hello analizy dzienników agent na maszynach wirtualnych Azure jest za pośrednictwem hello rozszerzenia maszyny Wirtualnej analizy dziennika.  Przy użyciu rozszerzenia hello upraszcza proces instalacji hello i automatycznie konfiguruje hello agenta toosend danych toohello obszaru roboczego analizy dzienników przez użytkownika. Hello agent jest również uaktualniana automatycznie, zapewnienie, że masz hello najnowsze funkcje i poprawki.

W przypadku maszyn wirtualnych systemu Windows zostanie włączona hello *programu Microsoft Monitoring Agent* rozszerzenie maszyny wirtualnej.
Dla maszyn wirtualnych systemu Linux, możesz włączyć hello *OMS agenta dla systemu Linux* rozszerzenie maszyny wirtualnej.

Dowiedz się więcej o [rozszerzenia maszyny wirtualnej platformy Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i hello [agenta systemu Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Korzystając z agenta na podstawie kolekcji danych dziennika, należy skonfigurować [źródeł danych w analizy dzienników](log-analytics-data-sources.md) toospecify hello dzienniki i metryki, które mają toocollect.

> [!IMPORTANT]
> Konfigurowanie danych dzienników tooindex analizy dzienników przy użyciu [diagnostyki Azure](log-analytics-azure-storage.md), i skonfiguruj hello toocollect agenta hello sam dzienniki, a następnie dwukrotnie zebraniu dzienników hello. Naliczane są opłaty za obu źródeł danych. Jeśli masz zainstalowany agent hello zbieranie danych dziennika przy użyciu tylko hello agenta — nie jest skonfigurowana danych dziennika toocollect analizy dzienników z diagnostyki Azure.
>
>

Istnieją trzy sposoby łatwego rozszerzenia maszyny wirtualnej analizy dzienników hello tooenable:

* Za pomocą hello portalu Azure
* Przy użyciu programu Azure PowerShell
* Za pomocą szablonu usługi Azure Resource Manager

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>Włącz rozszerzenia maszyny Wirtualnej hello w hello portalu Azure
Można zainstalować agenta powitania dla analizy dzienników i połączyć hello maszyny wirtualnej platformy Azure, którym jest on uruchamiany przy użyciu hello [portalu Azure](https://portal.azure.com).

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall hello agenta analizy dzienników i połącz hello obszaru roboczego analizy dzienników tooa dla maszyny wirtualnej
1. Zaloguj się na powitania [portalu Azure](http://portal.azure.com).
2. Wybierz **Przeglądaj** na powitania po lewej stronie operatora hello portalu, a następnie przejdź zbyt**analizy dzienników (OMS)** i zaznacz je.
3. Na liście obszarów roboczych usługi Analiza dzienników wybierz hello jedną, które mają toouse z hello maszyny Wirtualnej platformy Azure.  
   ![Obszary robocze OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. W obszarze **dziennika zarządzania analytics**, wybierz pozycję **maszyn wirtualnych**.  
   ![Maszyny wirtualne](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. Lista hello **maszyn wirtualnych**, wybierz hello maszyny wirtualnej, na którym chcesz tooinstall hello agenta. Witaj **stan połączenia OMS** hello maszyny Wirtualnej wskazuje, że jest **niepołączone**.  
   ![Maszyna wirtualna nie jest połączony](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. W szczegółach powitania dla maszyny wirtualnej, wybierz **Connect**. Hello agent jest automatycznie instalowany i konfigurowany dla obszaru roboczego analizy dzienników. Ten proces trwa kilka minut, w tym czasie jest hello stan połączenia OMS *łączenie...*  
   ![Łączenie maszyny Wirtualnej](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. Po zainstalowaniu i połącz agenta hello hello **połączenia OMS** stan zostanie zaktualizowany tooshow **ten obszar roboczy**.  
   ![Połączone](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>Włączanie rozszerzenia maszyny Wirtualnej hello przy użyciu programu PowerShell
Po skonfigurowaniu maszyny wirtualnej przy użyciu programu PowerShell, należy tooprovide hello **workspaceId** i **workspaceKey**. Witaj nazw właściwości w konfiguracji json **z uwzględnieniem wielkości liter**.

Witaj identyfikator i klucz na powitania można znaleźć **ustawienia** portalu OMS hello, lub za pomocą programu PowerShell, jak pokazano w hello poprzedzających przykład.

![Identyfikator i klucz podstawowy](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

Ma innego polecenia Azure klasycznych maszyn wirtualnych i maszyn wirtualnych Menedżera zasobów. Poniżej przedstawiono przykłady dla klasycznego i maszyn wirtualnych Menedżera zasobów.

W przypadku klasycznych maszyn wirtualnych Użyj hello poniższy przykład środowiska PowerShell:

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

Dla Menedżera zasobów maszyn wirtualnych systemu Linux przy użyciu powitania po interfejsu wiersza polecenia
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

Dla maszyn wirtualnych Menedżera zasobów Użyj hello poniższy przykład środowiska PowerShell:

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


## <a name="deploy-hello-vm-extension-using-a-template"></a>Wdrażanie hello rozszerzenia maszyny Wirtualnej przy użyciu szablonu
Za pomocą usługi Azure Resource Manager, można utworzyć szablon określający hello wdrażania i konfiguracji aplikacji (w formacie JSON). Ten szablon jest nazywany szablonem usługi Resource Manager i miejsce wdrożenia toodefine deklaratywne. Za pomocą szablonu, wielokrotnie można wdrożyć aplikację w całym cyklu życia aplikacji hello i mieć pewność, że zasoby są wdrażane w spójnym stanie.

W tym hello analizy dzienników agenta w ramach szablonu usługi Resource Manager, można Sprawdź, czy każda maszyna wirtualna jest obszaru roboczego analizy dzienników tooyour tooreport wstępnie skonfigurowane.

Aby uzyskać więcej informacji na temat szablonów usługi Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Poniżej przedstawiono przykład szablonu usługi Resource Manager, który służy do wdrażania maszyny wirtualnej z systemem Windows z hello zainstalowane rozszerzenia programu Microsoft Monitoring Agent. Ten szablon jest szablon typowej maszyny wirtualnej z hello następujące dodatki:

* Parametry workspaceId i workspaceName
* Sekcja rozszerzenia zasobu Microsoft.EnterpriseCloud.Monitoring
* Dane wyjściowe toolook hello workspaceId i workspaceSharedKey

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

Szablonu można wdrożyć przy użyciu następującego polecenia programu PowerShell hello:

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>Rozwiązywanie problemów z rozszerzenia maszyny Wirtualnej analizy dziennika hello
Zwykle komunikat o błędzie w sytuacji, gdy elementy nie działają z portalu Azure lub programu Azure powershell.

1. Zaloguj się na powitania [portalu Azure](http://portal.azure.com).
2. Znajdź hello maszyny Wirtualnej, a następnie otwórz szczegóły maszyny Wirtualnej.
3. Kliknij przycisk **rozszerzenia** toocheck, jeśli rozszerzenie OMS jest włączone.

   ![Widok rozszerzenia maszyny Wirtualnej](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. Kliknij przycisk hello *MicrosoftMonitoringAgent*(system Windows) lub *OmsAgentForLinux*rozszerzenia i wyświetlenia jej szczegółów (Linux). 

   ![Szczegóły rozszerzenia maszyny Wirtualnej](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>Rozwiązywanie problemów z maszyn wirtualnych systemu Windows
Jeśli hello *programu Microsoft Monitoring Agent* nie instaluje rozszerzenia agenta maszyny Wirtualnej lub raportowania, można wykonać następujące kroki tootroubleshoot hello problem hello.

1. Sprawdź, czy agent maszyny Wirtualnej Azure hello jest zainstalowany i kroki pracy poprawnie, używając hello [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).
   * Można również przejrzeć plik dziennika agenta maszyny Wirtualnej hello`C:\WindowsAzure\logs\WaAppAgent.log`
   * Jeśli hello dziennika nie istnieje, agent maszyny Wirtualnej hello nie jest zainstalowany.
     * [Zainstaluj hello Agent maszyny Wirtualnej na klasycznych maszyn wirtualnych](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. Potwierdź hello Microsoft Monitoring Agent rozszerzenia pulsu zadań została uruchomiona z użyciem hello następujące kroki:
   * Zaloguj się na maszynie wirtualnej toohello
   * Otwórz Harmonogram zadań i Znajdź hello `update_azureoperationalinsight_agent_heartbeat` zadań
   * Potwierdź zadań hello jest włączona i działa co minutę.
   * Sprawdź w pliku dziennika pulsu hello`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. Przejrzyj pliki dzienników rozszerzenia maszyny Wirtualnej agenta monitorowania firmy Microsoft hello w`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. Upewnij się, że maszyna wirtualna hello może uruchamiać skrypty programu PowerShell
5. Upewnij się, że nie zostały zmienione uprawnienia C:\Windows\temp
6. Wyświetlanie stanu hello hello Microsoft Monitoring Agent, wpisując następujące polecenie w oknie programu PowerShell z podwyższonym poziomem uprawnień na maszynie wirtualnej hello hello`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. Przejrzyj pliki dziennika instalacji programu Microsoft Monitoring Agent hello w`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z rozszerzeń systemu Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="troubleshooting-linux-virtual-machines"></a>Rozwiązywanie problemów z maszyn wirtualnych systemu Linux
Jeśli hello *Agent pakietu OMS Linux* nie instaluje rozszerzenia agenta maszyny Wirtualnej lub raportowania, można wykonać następujące kroki tootroubleshoot hello problem hello.

1. Jeśli stan rozszerzenia hello jest *nieznany* Sprawdź, czy agent maszyny Wirtualnej Azure hello jest zainstalowany i działa poprawnie, przeglądając plik dziennika agenta maszyny Wirtualnej hello`/var/log/waagent.log`
   * Jeśli hello dziennika nie istnieje, agent maszyny Wirtualnej hello nie jest zainstalowany.
   * [Zainstaluj hello Agent maszyny Wirtualnej na maszynach wirtualnych systemu Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Dla innych stanów złej kondycji, przejrzyj hello Agent pakietu OMS dla rozszerzenia maszyny Wirtualnej systemu Linux pliki dziennika `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` i`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. Jeśli stan rozszerzenia hello jest w dobrej kondycji, ale nie można przekazać danych przeglądać hello Agent pakietu OMS Linux pliki dziennika`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>Następne kroki
* Skonfiguruj [źródeł danych w analizy dzienników](log-analytics-data-sources.md) hello toospecify toocollect dzienniki i metryki.
* toogather danych z maszyn wirtualnych [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).
* [Zbieranie danych za pomocą diagnostyki Azure](log-analytics-azure-storage.md) dla innych zasobów, które są uruchomione na platformie Azure.

Dla komputerów, które nie są na platformie Azure można zainstalować agenta analizy dzienników hello przy użyciu metody hello, które zostały opisane w hello następujące artykuły:

* [Połącz tooLog komputerów z systemem Windows analityka](log-analytics-windows-agents.md)
* [Połącz Linux komputerów tooLog analityka](log-analytics-linux-agents.md)
