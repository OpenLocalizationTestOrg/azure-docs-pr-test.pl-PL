---
title: "Przykładowa konfiguracja rozszerzenia maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft"
description: "Przykładowa konfiguracja do tworzenia szablonów z rozszerzeniami"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a1cee6c-51ea-4c03-b607-f158586d7175
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: a22962690854d273377f7295ab5dd49419f5a354
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-windows-vm-extension-configuration-samples"></a><span data-ttu-id="97272-103">Przykłady konfiguracji rozszerzenia maszyn wirtualnych systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="97272-103">Azure Windows VM Extension Configuration Samples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97272-104">PowerShell — szablonu</span><span class="sxs-lookup"><span data-stu-id="97272-104">PowerShell - Template</span></span>](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> * [<span data-ttu-id="97272-105">Interfejs wiersza polecenia - szablonu</span><span class="sxs-lookup"><span data-stu-id="97272-105">CLI - Template</span></span>](../linux/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="97272-106">Ten artykuł zawiera Przykładowa konfiguracja konfigurowanie Azure VM rozszerzeń dla maszyn wirtualnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="97272-106">This article provides sample configuration for configuring Azure VM Extensions for Windows VMs.</span></span>

<span data-ttu-id="97272-107">Aby dowiedzieć się więcej na temat tych rozszerzeń, zobacz [omówienie rozszerzeń maszyny Wirtualnej Azure.](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="97272-107">To learn more about these extensions, see [Azure VM Extensions Overview.](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="97272-108">Aby dowiedzieć się więcej na temat tworzenia szablonów rozszerzenia, zobacz [tworzenia szablonów rozszerzenia.](extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="97272-108">To learn more about authoring extension templates, see [Authoring Extension Templates.](extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="97272-109">W tym artykule wymieniono konfiguracji oczekiwanej wartości dla niektórych rozszerzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="97272-109">This article lists expected configuration values for some of the Windows Extensions.</span></span>

## <a name="sample-template-snippet-for-vm-extensions-with-iaas-vms"></a><span data-ttu-id="97272-110">Przykładowy szablon fragment kodu dotyczący rozszerzeń maszyny Wirtualnej z maszyn wirtualnych IaaS.</span><span class="sxs-lookup"><span data-stu-id="97272-110">Sample template snippet for VM Extensions with IaaS VMs.</span></span>
<span data-ttu-id="97272-111">Fragment kodu szablonu wdrażania rozszerzeń wygląda jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="97272-111">The template snippet for Deploying extensions looks as following:</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "autoUpgradeMinorVersion":true,
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

## <a name="sample-template-snippet-for-vm-extensions-with-vm-scale-sets"></a><span data-ttu-id="97272-112">Przykładowy szablon fragment kodu dotyczący rozszerzeń maszyny Wirtualnej z zestawy skalowania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="97272-112">Sample template snippet for VM Extensions with VM Scale Sets.</span></span>
    {
     "type":"Microsoft.Compute/virtualMachineScaleSets",
    ....
           "extensionProfile":{
           "extensions":[
             {
               "name":"extension Name",
               "properties":{
                 "publisher":"Publisher Namespace",
                 "type":"extension Name",
                 "typeHandlerVersion":"extension version",
                 "autoUpgradeMinorVersion":true,
                 "settings":{
                 // Extension specific configuration goes in here.
                 }
               }
              }
            }
          }

<span data-ttu-id="97272-113">Przed wdrożeniem rozszerzenia Sprawdź najnowszej wersji rozszerzenia i zastąp "typeHandlerVersion" najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="97272-113">Before deploying the extension please check the latest extension version and replace the "typeHandlerVersion" with the current latest version.</span></span>

<span data-ttu-id="97272-114">Pozostałej części artykułu zawiera przykładowe konfiguracje dla rozszerzeń maszyny Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="97272-114">Rest of the article provides sample configurations for Windows VM Extensions.</span></span>

<span data-ttu-id="97272-115">Przed wdrożeniem rozszerzenia Sprawdź najnowszej wersji rozszerzenia i zastąp "typeHandlerVersion" najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="97272-115">Before deploying the extension please check the latest extension version and replace the "typeHandlerVersion" with the current latest version.</span></span>

### <a name="customscript-extension-14"></a><span data-ttu-id="97272-116">Rozszerzenia CustomScript 1.4.</span><span class="sxs-lookup"><span data-stu-id="97272-116">CustomScript Extension 1.4.</span></span>
      {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.4",
          "settings": {
              "fileUris": [
                  "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
              ],
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
          },
          "protectedSettings": {
            "storageAccountName": "yourStorageAccountName",
            "storageAccountKey": "yourStorageAccountKey"
          }
      }

#### <a name="parameter-description"></a><span data-ttu-id="97272-117">Opis parametru:</span><span class="sxs-lookup"><span data-stu-id="97272-117">Parameter description:</span></span>
* <span data-ttu-id="97272-118">fileUris: rozdzielone przecinkami listę adresów URL, plików, które zostaną pobrane na maszynie Wirtualnej przez rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="97272-118">fileUris : Comma seperated list of urls of the files that will be downloaded on the VM by the Extension.</span></span> <span data-ttu-id="97272-119">Jeśli nie określono żadnej wartości, są pobierane żadne pliki.</span><span class="sxs-lookup"><span data-stu-id="97272-119">No files are downloaded if nothing is specified.</span></span> <span data-ttu-id="97272-120">Jeśli pliki znajdują się w usłudze Azure Storage, fileURLs można oznaczyć jako prywatne i correspoding storageAccountName i storageAccountKey mogą być przekazywane jako parametry prywatny dostęp do tych plików.</span><span class="sxs-lookup"><span data-stu-id="97272-120">If the files are in Azure Storage, the fileURLs can be marked private and the correspoding storageAccountName and storageAccountKey can be passed as private parameters to access these files.</span></span>
* <span data-ttu-id="97272-121">commandToExecute: [obowiązkowy parametr]: to polecenie, które będą wykonywane przez rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="97272-121">commandToExecute : [Mandatory Parameter] : This is the command that will be executed by the Extension.</span></span>
* <span data-ttu-id="97272-122">storageAccountName: [parametr opcjonalny]: Nazwa konta magazynu do uzyskiwania dostępu do fileURLs, jeśli są one oznaczone jako prywatny.</span><span class="sxs-lookup"><span data-stu-id="97272-122">storageAccountName : [Optional Parameter] : Storage Account Name for accessing the fileURLs, if they are marked as private.</span></span>
* <span data-ttu-id="97272-123">storageAccountKey: [parametr opcjonalny]: klucz konta magazynu do uzyskiwania dostępu do fileURLs, jeśli są one oznaczone jako prywatny.</span><span class="sxs-lookup"><span data-stu-id="97272-123">storageAccountKey : [Optional Parameter] : Storage Account Key for accessing the fileURLs, if they are marked as private.</span></span>

### <a name="customscript-extension-17"></a><span data-ttu-id="97272-124">Rozszerzenia CustomScript 1.7.</span><span class="sxs-lookup"><span data-stu-id="97272-124">CustomScript Extension 1.7.</span></span>
<span data-ttu-id="97272-125">Zapoznaj się CustomScript w wersji 1.4 opis parametru.</span><span class="sxs-lookup"><span data-stu-id="97272-125">Please refer to CustomScript version 1.4 for parameter description.</span></span> <span data-ttu-id="97272-126">Wersji 1,7 wprowadzono obsługę wysyłania parameters(commandToExecute) skryptu jako protectedSettings, w którym to przypadku będą one szyfrowane przed wysłaniem.</span><span class="sxs-lookup"><span data-stu-id="97272-126">Version 1.7 introduces support for sending script parameters(commandToExecute) as protectedSettings, in which case they will be encrypted before sending.</span></span> <span data-ttu-id="97272-127">Parametr "commandToExecute" można określić ustawienia lub protectedSettings, ale nie w obu.</span><span class="sxs-lookup"><span data-stu-id="97272-127">'commandToExecute' parameter can be specified either in settings or protectedSettings but not in both.</span></span>

        {
            "publisher": "Microsoft.Compute",
            "type": "CustomScriptExtension",
            "typeHandlerVersion": "1.7",
            "settings": {
                "fileUris": [
                    "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
                ],
                "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
            },
            "protectedSettings": {
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1",
              "storageAccountName": "yourStorageAccountName",
              "storageAccountKey": "yourStorageAccountKey"
            }
        }

### <a name="vmaccess-extension"></a><span data-ttu-id="97272-128">Rozszerzenia VMAccess.</span><span class="sxs-lookup"><span data-stu-id="97272-128">VMAccess Extension.</span></span>
      {
          "publisher": "Microsoft.Compute",
          "type": "VMAccessAgent",
          "typeHandlerVersion": "2.0",
          "settings": {
            "UserName" : "New User Name"
          },
          "protectedSettings": {
            "Password" : "New Password"
          }
      }

### <a name="dsc-extension"></a><span data-ttu-id="97272-129">Rozszerzenia usługi Konfiguracja DSC.</span><span class="sxs-lookup"><span data-stu-id="97272-129">DSC Extension.</span></span>
      {
          "publisher": "Microsoft.Powershell",
          "type": "DSC",
          "typeHandlerVersion": "2.1(Recommendation is to use the latest version)",
          "settings": {
              "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
              "SasToken": "Optional : SAS Token if ModulesUrl points to Azure Blob Storage",
              "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
              "Properties": {
                  "ParameterToConfigurationFunction1": "Value1",
                  "ParameterToConfigurationFunction2": "Value2",
                  "ParameterOfTypePSCredential1": {
                      "UserName": "UsernameValue1",
                      "Password": "PrivateSettingsRef:Key1(Value is a reference to a member of the Items object in the protected settings)"
                  },
                  "ParameterOfTypePSCredential2": {
                      "UserName": "UsernameValue2",
                      "Password": "PrivateSettingsRef:Key2"
                  }
              }
          },
          "protectedSettings": {
              "Items": {
                  "Key1": "PasswordValue1",
                  "Key2": "PasswordValue2"
              },
              "DataBlobUri": "optional : https: //UrlToConfigurationData.psd1"
          }
      }


### <a name="symantec-endpoint-protection"></a><span data-ttu-id="97272-130">Symantec Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="97272-130">Symantec Endpoint Protection.</span></span>
      {
        "publisher": "SymantecEndpointProtection",
        "type": "Symantec",
        "typeHandlerVersion": "12.1",
        "settings": {}
      }

### <a name="trend-micro-deep-security-agent"></a><span data-ttu-id="97272-131">Trend Micro zabezpieczeń głębokie agenta.</span><span class="sxs-lookup"><span data-stu-id="97272-131">Trend Micro Deep Security Agent.</span></span>
      {
        "publisher": "TrendMicro.DeepSecurity",
        "type": "TrendMicroDSA",
        "typeHandlerVersion": "9.6",
        "settings": {
          "ManagerAddress" : "Enter the externally accessible DNS name or IP address of the Deep Security Manager. Please enter \"agents.deepsecurity.trendmicro.com\" if using Deep Security as a Service",

          "ActivationPort" : "Enter the port number of the Deep Security Manager, default value - 443",

          "TenantIdentifier" : "Enter the tenant ID, which is a hyphenated, 36-character string available in the Deployment Scripts dialog box in the Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "TenantActivationPassword" : "Enter the tenant activation password, which is a hyphenated, 36-character string available in the Deployment Scripts dialog box in the Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "SecurityPolicy" : "Optional : Enter the name or numeric ID of the security policy defined in the Deep Security Manager which will be applied on agent activation to protect this virtual machine (recommended). No security policy will be applied to the virtual machine if this parameter is blank. This parameter is optional if using Deep Security as a Service."
        }
      }

### <a name="vormertric-transparent-encryption-agent"></a><span data-ttu-id="97272-132">Vormertric przezroczystego szyfrowania agenta.</span><span class="sxs-lookup"><span data-stu-id="97272-132">Vormertric Transparent Encryption Agent.</span></span>
            {
              "publisher": "Vormetric",
              "type": "VormetricTransparentEncryptionAgent",
              "typeHandlerVersion": "5.2",
              "settings": {
              }
            }

### <a name="puppet-enterprise-agent"></a><span data-ttu-id="97272-133">Puppet Enterprise Agent.</span><span class="sxs-lookup"><span data-stu-id="97272-133">Puppet Enterprise Agent.</span></span>
            {
              "publisher": "PuppetLabs",
              "type": "PuppetEnterpriseAgent",
              "typeHandlerVersion": "3.2",
              "settings": {
                "puppet_master_server" : "Puppet Master Server Name"
              }
            }  

### <a name="microsoft-monitoring-agent-for-azure-operational-insights"></a><span data-ttu-id="97272-134">Microsoft Monitoring Agent dla usługi Azure Operational Insights</span><span class="sxs-lookup"><span data-stu-id="97272-134">Microsoft Monitoring Agent for Azure Operational Insights</span></span>
            {
              "publisher": "Microsoft.EnterpriseCloud.Monitoring",
              "type": "MicrosoftMonitoringAgent",
              "typeHandlerVersion": "1.0",
              "settings": {
                "workspaceId" : "The Workspace ID is available from within the Direct Agent Configuration section of the Azure Operational Insights portal"
              }
              "protectedSettings": {
                "workspaceKey"  : "The Workspace Key is a string that is available from within the Direct Agent Configuration section of the Azure Operational Insights portal"
              }
              }
            }

### <a name="mcafee-endpointsecurity"></a><span data-ttu-id="97272-135">McAfee EndpointSecurity</span><span class="sxs-lookup"><span data-stu-id="97272-135">McAfee EndpointSecurity</span></span>
            {
              "publisher": "McAfee.EndpointSecurity",
              "type": "McAfeeEndpointSecurity",
              "typeHandlerVersion": "6.0",
              "settings": {
                "entitlementKey" : "Optional : Enter a valid entitlement key or leave blank for trial version",
                "featureVS"      : "Choose whether or not to install the Virus and Spyware Protection features : true|false",
                "featureBP"      : "Choose whether or not to install the Browser Protection feature : true|false",
                "featureFW"      : "Choose whether or not to install the Firewall Protection feature :true|false",
                "relayServer"    : "Allows VMs on the local subnet to receive updates through this VM when they are not connected to the internet : true|false"
              }
            }

### <a name="azure-iaas-antimalware"></a><span data-ttu-id="97272-136">Azure IaaS ochrony przed złośliwym oprogramowaniem</span><span class="sxs-lookup"><span data-stu-id="97272-136">Azure IaaS Antimalware</span></span>
          {
            "publisher": "Microsoft.Azure.Security",
            "type": "IaaSAntimalware",
            "typeHandlerVersion": "1.2",
            "settings": {
              "AntimalwareEnabled": "true",
              "ExclusionsPaths"        : "Optional : ExclusionsPaths",
              "ExclusionsExtensions"   : "Optional : ExclusionsExtensions",
              "ExclusionsProcesses"   : "Optional : ExclusionsProcesses",
              "RealtimeProtectionEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsIsEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsScanType"   : "Optional : Quick|Full",
              "ScheduledScanSettingsDay"   : "Optional : Sunday-Saturday",
              "ScheduledScanSettingsTime"   : "Optional : When to perform the scheduled scan, measured in minutes from midnight,0-1440"
            }
          }

### <a name="eset-file-security"></a><span data-ttu-id="97272-137">RESETUJ zabezpieczeń pliku</span><span class="sxs-lookup"><span data-stu-id="97272-137">ESET File Security</span></span>
          {
            "publisher": "ESET",
            "type": "FileSecurity",
            "typeHandlerVersion": "6.0",
            "settings": {
            }
          }

### <a name="datadog-agent"></a><span data-ttu-id="97272-138">Datadog Agent</span><span class="sxs-lookup"><span data-stu-id="97272-138">Datadog Agent</span></span>
          {
            "publisher": "Datadog.Agent",
            "type": "DatadogWindowsAgent",
            "typeHandlerVersion": "0.5",
            "settings": {
              "api_key" : "API Key from https://app.datadoghq.com/account/settings#api"
            }
          }

### <a name="confer-advanced-threat-prevention-and-incident-response-for-azure"></a><span data-ttu-id="97272-139">Przyznaje zapobiegania Advanced Threat i odpowiedzi na zdarzenia dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="97272-139">Confer Advanced Threat Prevention and Incident Response for Azure</span></span>
          {
            "publisher": "Confer",
            "type": "ConferForAzure",
            "typeHandlerVersion": "1.0",
            "settings": {
              "ConferRegisterCode" : "Optional : Valid product registration code or leave it blank to register later",
              "ConferRegisterCode" : "Enter a valid server name if your account requires a dedicated confer backend server or leave it blank"
            }
          }

### <a name="cloudlink-securevm-agent"></a><span data-ttu-id="97272-140">CloudLink SecureVM agenta</span><span class="sxs-lookup"><span data-stu-id="97272-140">CloudLink SecureVM Agent</span></span>
          {
            "publisher": "CloudLinkEMC.SecureVM",
            "type": "CloudLinkSecureVMWindowsAgent",
            "typeHandlerVersion": "4.0",
            "settings": {
              "CloudLinkCenter" : "specify valid IP/FQDN to CloudLinkCenter"
            }
          }

### <a name="barracuda-vpn-connectivity-agent-for-microsoft-azure"></a><span data-ttu-id="97272-141">Agent połączenie sieci VPN barracuda platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="97272-141">Barracuda VPN Connectivity Agent for Microsoft Azure</span></span>
          {
            "publisher": "Barracuda.Azure.ConnectivityAgent",
            "type": "BarracudaConnectivityAgent",
            "typeHandlerVersion": "3.5",
            "settings": {
              "ServerAddress" : "Host name or IP address of the VPN server - AES, AES256, Blowfish,CAST,DES,3DES,None",
              "EncryptionAlgorithm" : "Algorithm used to encrypt VPN traffic - MD5,SHA1,SHA256,None",
              "PKCS12File" : "Url for file containing certificate and private key used to authenticate against the VPN server",
              "PKCS12FilePassword" : "Password for the file containing certificate and private key"
            }
          }

### <a name="alert-logic-log-manager"></a><span data-ttu-id="97272-142">Menedżer dzienników logiki alertu</span><span class="sxs-lookup"><span data-stu-id="97272-142">Alert Logic Log Manager</span></span>
          {
            "publisher": "AlertLogic.Extension",
            "type": "AlertLogicLM",
            "typeHandlerVersion": "1.9",
            "settings": {
              "registrationKey" : " Alert Logic Log Manager registration key"
            }
          }

### <a name="chef-agent"></a><span data-ttu-id="97272-143">Chef Agent</span><span class="sxs-lookup"><span data-stu-id="97272-143">Chef Agent</span></span>
          {
            "publisher": "Chef.Bootstrap.WindowsAzure",
            "type": "ChefClient",
            "typeHandlerVersion": "1210.12",
            "settings": {
              "validation_key" : " Validation key",
              "client_rb" : "client_rb file",
              "runlist" : "Optional runlist"
            }
          }

### <a name="azure-diagnostics"></a><span data-ttu-id="97272-144">Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="97272-144">Azure Diagnostics</span></span>
<span data-ttu-id="97272-145">Aby uzyskać więcej informacji o sposobie konfigurowania diagnostyki, zobacz [rozszerzenia Diagnostyka Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="97272-145">For more details about how to configure diagnostics, see [Azure Diagnostics Extension](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

          {
            "publisher": "Microsoft.Azure.Diagnostics",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "1.5",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "xmlCfg": "[base64(variables('wadcfgx'))]",
              "storageAccount": "[parameters('diagnosticsStorageAccount')]"
            },
            "protectedSettings": {
            "storageAccountName": "[parameters('diagnosticsStorageAccount')]",
            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
            "storageAccountEndPoint": "https://core.windows.net"
          }
          }

### <a name="octopus-deploy-tentacle-agent"></a><span data-ttu-id="97272-146">Ośmiornica wdrożyć agenta Tentacle</span><span class="sxs-lookup"><span data-stu-id="97272-146">Octopus Deploy Tentacle Agent</span></span>

<span data-ttu-id="97272-147">Aby uzyskać więcej informacji o sposobie konfigurowania Tentacle wdrażanie Ośmiornica na platformie Azure, zobacz [dokumentacji Ośmiornica](https://octopus.com/docs/installation/installing-tentacles/azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="97272-147">For more details about how to configure the Octopus Deploy Tentacle on Azure, see the [Octopus Documentation](https://octopus.com/docs/installation/installing-tentacles/azure-virtual-machines).</span></span>

          {
            "publisher": "OctopusDeploy.Tentacle",
            "type": "OctopusDeployWindowsTentacle",
            "typeHandlerVersion": "2.0",
            "autoUpgradeMinorVersion": "true",
            "settings": {
              "OctopusServerUrl": "(string, required) The url to the Octopus server portal.",
              "Environments": [ "(array of strings, required) The environments to which the Tentacle should be added." ],
              "Roles": [ "(array of strings, required) The roles to assign to the Tentacle." ],
              "CommunicationMode": "(string, required) Whether the Tentacle should wait for connections from the server ('Listen') or should poll the server ('Poll').",
              "Port": (int, required) The port to listen on for connections from the server (in 'Listen' mode), or the port on which to connect to the Octopus server ('Poll' mode).,
              "PublicHostNameConfiguration": "(string, optional) If in listening mode, how the server should contact the Tentacle. Can be 'PublicIP', 'FQDN', 'ComputerName' or 'Custom'. Defaults to 'PublicIp'.",
              "CustomPublicHostName": "(string, optional) If in listening mode, and 'PublicHostNameConfiguration' is set to 'Custom', the address that the server should use for this Tentacle.",
              "MachinePolicy": "(string, optional) The Machine Policy to assign to the Tentacle. If not specified, uses the default Machine Policy.",
              "Tenants": [ "(array of strings, optional) The tenants to assign to the Tentacle. The tenants feature must be enabled on the Octopus Server." ],
              "TenantTags": [ "(array of strings, optional) The tenant tags to assign to the Tentacle, in the format 'TagSet/TagName'. The tenants feature must be enabled on the Octopus Server." ]
            },
            "protectedSettings": {
              "ApiKey": "(string, required) The Api Key to use to connect to the Octopus server."
            }
          }

<span data-ttu-id="97272-148">W powyższych przykładach Zastąp numer wersji numer najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="97272-148">In the examples above, replace the version number with the latest version number.</span></span>

<span data-ttu-id="97272-149">Oto przykład pełnego szablonu maszyny Wirtualnej z niestandardowe rozszerzenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="97272-149">Here is an example of a full VM template with Custom Script Extension.</span></span>

[<span data-ttu-id="97272-150">Niestandardowe rozszerzenie skryptu Windows maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="97272-150">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

