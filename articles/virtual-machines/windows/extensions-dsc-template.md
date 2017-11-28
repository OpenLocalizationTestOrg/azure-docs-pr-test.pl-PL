---
title: "aaaDesired stan konfiguracji Menedżera zasobów szablonu | Dokumentacja firmy Microsoft"
description: "Definicja szablonu usługi Resource Manager konfiguracji żądanego stanu systemu Azure wraz z przykładami i rozwiązywania problemów"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="7257c-103">VMSS systemu Windows i konfiguracji żądanego stanu przy użyciu szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7257c-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="7257c-104">W tym artykule opisano hello szablonu usługi Resource Manager dla hello [konfiguracji żądanego stanu rozszerzenia obsługi](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7257c-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="7257c-105">Przykład szablonu maszyny wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="7257c-105">Template example for a Windows VM</span></span>
<span data-ttu-id="7257c-106">Witaj poniższy fragment przechodzi w stan hello sekcji zasobów hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="7257c-106">hello following snippet goes into hello Resource section of hello template.</span></span>

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="7257c-107">Przykład szablonu VMSS systemu Windows</span><span class="sxs-lookup"><span data-stu-id="7257c-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="7257c-108">Węzeł VMSS ma sekcję "właściwości" z hello "VirtualMachineProfile" atrybutu "extensionProfile".</span><span class="sxs-lookup"><span data-stu-id="7257c-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="7257c-109">DSC zostanie dodany w obszarze "rozszerzenia".</span><span class="sxs-lookup"><span data-stu-id="7257c-109">DSC is added under "extensions".</span></span> 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a><span data-ttu-id="7257c-110">Informacje szczegółowe ustawienia</span><span class="sxs-lookup"><span data-stu-id="7257c-110">Detailed Settings Information</span></span>
<span data-ttu-id="7257c-111">Witaj następujące schemat jest przeznaczony dla części ustawień hello hello rozszerzenia usługi Konfiguracja DSC Azure w szablonie usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7257c-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a><span data-ttu-id="7257c-112">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="7257c-112">Details</span></span>
| <span data-ttu-id="7257c-113">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="7257c-113">Property Name</span></span> | <span data-ttu-id="7257c-114">Typ</span><span class="sxs-lookup"><span data-stu-id="7257c-114">Type</span></span> | <span data-ttu-id="7257c-115">Opis</span><span class="sxs-lookup"><span data-stu-id="7257c-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7257c-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="7257c-116">settings.wmfVersion</span></span> |<span data-ttu-id="7257c-117">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7257c-117">string</span></span> |<span data-ttu-id="7257c-118">Określa wersję hello hello Windows Management Framework, która ma zostać zainstalowana na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7257c-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="7257c-119">Ustawienie tej właściwości too'latest "hello instaluje najnowsze wersję programu WMF.</span><span class="sxs-lookup"><span data-stu-id="7257c-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="7257c-120">Witaj tylko bieżące możliwe wartości dla tej właściwości to **"4.0", "5.0", "5.0PP' i"r"**.</span><span class="sxs-lookup"><span data-stu-id="7257c-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="7257c-121">Te możliwe wartości to tooupdates podmiotu.</span><span class="sxs-lookup"><span data-stu-id="7257c-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="7257c-122">Witaj wartość domyślna to "najnowsze".</span><span class="sxs-lookup"><span data-stu-id="7257c-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="7257c-123">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="7257c-123">settings.configuration.url</span></span> |<span data-ttu-id="7257c-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7257c-124">string</span></span> |<span data-ttu-id="7257c-125">Określa hello adres URL lokalizacji, z których toodownload pliku zip konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="7257c-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="7257c-126">Podany adres URL hello wymaga tokenu sygnatury dostępu Współdzielonego w celu uzyskania dostępu, należy najpierw tooset hello protectedSettings.configurationUrlSasToken toohello wartość właściwości token sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="7257c-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="7257c-127">Ta właściwość jest wymagana, jeśli zdefiniowano settings.configuration.script i/lub settings.configuration.function.</span><span class="sxs-lookup"><span data-stu-id="7257c-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="7257c-128">Settings.Configuration.Script</span><span class="sxs-lookup"><span data-stu-id="7257c-128">settings.configuration.script</span></span> |<span data-ttu-id="7257c-129">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7257c-129">string</span></span> |<span data-ttu-id="7257c-130">Określa nazwę pliku hello hello skryptu, który zawiera definicję hello konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="7257c-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="7257c-131">Ten skrypt musi być w folderze głównym hello hello pliku zip pobranego z hello adres URL określony przez właściwość configuration.url hello.</span><span class="sxs-lookup"><span data-stu-id="7257c-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="7257c-132">Ta właściwość jest wymagana, jeśli zdefiniowano settings.configuration.url i/lub settings.configuration.script.</span><span class="sxs-lookup"><span data-stu-id="7257c-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="7257c-133">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="7257c-133">settings.configuration.function</span></span> |<span data-ttu-id="7257c-134">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7257c-134">string</span></span> |<span data-ttu-id="7257c-135">Określa nazwę hello konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="7257c-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="7257c-136">konfigurację Hello o nazwie muszą być zawarte w skrypcie hello zdefiniowane przez configuration.script.</span><span class="sxs-lookup"><span data-stu-id="7257c-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="7257c-137">Ta właściwość jest wymagana, jeśli zdefiniowano settings.configuration.url i/lub settings.configuration.function.</span><span class="sxs-lookup"><span data-stu-id="7257c-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="7257c-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="7257c-138">settings.configurationArguments</span></span> |<span data-ttu-id="7257c-139">Collection</span><span class="sxs-lookup"><span data-stu-id="7257c-139">Collection</span></span> |<span data-ttu-id="7257c-140">Definiuje żadnych parametrów, które chcesz konfiguracji DSC tooyour toopass.</span><span class="sxs-lookup"><span data-stu-id="7257c-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="7257c-141">Ta właściwość nie jest zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="7257c-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="7257c-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="7257c-142">settings.configurationData.url</span></span> |<span data-ttu-id="7257c-143">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7257c-143">string</span></span> |<span data-ttu-id="7257c-144">Określa adres URL hello, z których toodownload dane konfiguracyjne (psd1) pliku toouse jako dane wejściowe dla danej konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="7257c-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="7257c-145">Podany adres URL hello wymaga tokenu sygnatury dostępu Współdzielonego w celu uzyskania dostępu, należy najpierw tooset hello protectedSettings.configurationDataUrlSasToken toohello wartość właściwości token sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="7257c-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="7257c-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="7257c-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="7257c-147">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7257c-147">string</span></span> |<span data-ttu-id="7257c-148">Włącza lub wyłącza gromadzenia danych telemetrii.</span><span class="sxs-lookup"><span data-stu-id="7257c-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="7257c-149">Witaj tylko możliwe wartości dla tej właściwości to **"Włącz", "Wyłączone", ", lub $null**.</span><span class="sxs-lookup"><span data-stu-id="7257c-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="7257c-150">Puste ani mieć wartości null, pozostawiając ta właściwość umożliwia telemetrii.</span><span class="sxs-lookup"><span data-stu-id="7257c-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="7257c-151">Witaj, wartością domyślną jest ".</span><span class="sxs-lookup"><span data-stu-id="7257c-151">hello default value is ''.</span></span> [<span data-ttu-id="7257c-152">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="7257c-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="7257c-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="7257c-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="7257c-154">Collection</span><span class="sxs-lookup"><span data-stu-id="7257c-154">Collection</span></span> |<span data-ttu-id="7257c-155">Definiuje alternatywne lokalizacje, z których toodownload hello WMF.</span><span class="sxs-lookup"><span data-stu-id="7257c-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="7257c-156">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="7257c-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="7257c-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="7257c-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="7257c-158">Collection</span><span class="sxs-lookup"><span data-stu-id="7257c-158">Collection</span></span> |<span data-ttu-id="7257c-159">Definiuje żadnych parametrów, które chcesz konfiguracji DSC tooyour toopass.</span><span class="sxs-lookup"><span data-stu-id="7257c-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="7257c-160">Ta właściwość jest zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="7257c-160">This property is encrypted.</span></span> |
| <span data-ttu-id="7257c-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="7257c-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="7257c-162">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7257c-162">string</span></span> |<span data-ttu-id="7257c-163">Określa hello tokenu tooaccess hello adres URL SAS zdefiniowane przez configuration.url.</span><span class="sxs-lookup"><span data-stu-id="7257c-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="7257c-164">Ta właściwość jest zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="7257c-164">This property is encrypted.</span></span> |
| <span data-ttu-id="7257c-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="7257c-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="7257c-166">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7257c-166">string</span></span> |<span data-ttu-id="7257c-167">Określa hello tokenu tooaccess hello adres URL SAS zdefiniowane przez configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="7257c-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="7257c-168">Ta właściwość jest zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="7257c-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="7257c-169">Ustawienia programu vs. ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="7257c-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="7257c-170">Wszystkie ustawienia są zapisywane w pliku tekstowym ustawień na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7257c-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="7257c-171">Właściwości w obszarze "ustawienia" są właściwości publiczne, ponieważ nie są szyfrowane w pliku tekstowym hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="7257c-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="7257c-172">Właściwości w obszarze "protectedSettings" są szyfrowane przy użyciu certyfikatu i nie są wyświetlane w postaci zwykłego tekstu, w tym pliku na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7257c-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="7257c-173">Jeśli konfiguracja hello wymaga poświadczeń, mogły one zostać uwzględnione w protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="7257c-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a><span data-ttu-id="7257c-174">Przykład</span><span class="sxs-lookup"><span data-stu-id="7257c-174">Example</span></span>
<span data-ttu-id="7257c-175">Hello poniższy przykład pochodzi z hello "Wprowadzenie" sekcji hello [strony Przegląd programu obsługi rozszerzenia DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7257c-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="7257c-176">W tym przykładzie używane szablony Menedżera zasobów, zamiast polecenia cmdlet toodeploy hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="7257c-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="7257c-177">Zapisz konfigurację "IisInstall.ps1" hello, umieść ją w. ZIP plik, a przekazywania hello w dostępny adres URL.</span><span class="sxs-lookup"><span data-stu-id="7257c-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="7257c-178">W tym przykładzie użyto magazynu obiektów blob platformy Azure, ale jest to możliwe toodownload. Pliki ZIP z dowolnego miejsca i dowolnego.</span><span class="sxs-lookup"><span data-stu-id="7257c-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="7257c-179">W szablonie usługi Azure Resource Manager hello hello następujący kod nakazuje hello wirtualna toodownload hello poprawnego pliku i uruchom hello odpowiednią funkcję programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7257c-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="7257c-180">Aktualizowanie z hello poprzedniego formatu</span><span class="sxs-lookup"><span data-stu-id="7257c-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="7257c-181">Wszystkie ustawienia w hello poprzedniego formatu (zawierający właściwości publiczne hello ModulesUrl, ConfigurationFunction, właściwości lub SasToken) automatycznie dostosowania bieżącego formatu toohello i uruchom tak samo jak przed.</span><span class="sxs-lookup"><span data-stu-id="7257c-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="7257c-182">powitania po schematu jest schemat ustawień poprzedniej jakie hello wyszukiwanego, takich jak:</span><span class="sxs-lookup"><span data-stu-id="7257c-182">hello following schema is what hello previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
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
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

<span data-ttu-id="7257c-183">Oto, jak poprzedni format hello dostosowuje toohello bieżącego formatu:</span><span class="sxs-lookup"><span data-stu-id="7257c-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="7257c-184">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="7257c-184">Property Name</span></span> | <span data-ttu-id="7257c-185">Odpowiednik w poprzednim schematu</span><span class="sxs-lookup"><span data-stu-id="7257c-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="7257c-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="7257c-186">settings.wmfVersion</span></span> |<span data-ttu-id="7257c-187">Ustawienia. WMFVersion</span><span class="sxs-lookup"><span data-stu-id="7257c-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="7257c-188">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="7257c-188">settings.configuration.url</span></span> |<span data-ttu-id="7257c-189">Ustawienia. ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="7257c-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="7257c-190">Settings.Configuration.Script</span><span class="sxs-lookup"><span data-stu-id="7257c-190">settings.configuration.script</span></span> |<span data-ttu-id="7257c-191">Pierwsza część ustawień. ConfigurationFunction (przed "\\\\")</span><span class="sxs-lookup"><span data-stu-id="7257c-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="7257c-192">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="7257c-192">settings.configuration.function</span></span> |<span data-ttu-id="7257c-193">Druga część ustawień. ConfigurationFunction (po "\\\\")</span><span class="sxs-lookup"><span data-stu-id="7257c-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="7257c-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="7257c-194">settings.configurationArguments</span></span> |<span data-ttu-id="7257c-195">Ustawienia. Właściwości</span><span class="sxs-lookup"><span data-stu-id="7257c-195">settings.Properties</span></span> |
| <span data-ttu-id="7257c-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="7257c-196">settings.configurationData.url</span></span> |<span data-ttu-id="7257c-197">protectedSettings.DataBlobUri (bez tokenu sygnatury dostępu Współdzielonego)</span><span class="sxs-lookup"><span data-stu-id="7257c-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="7257c-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="7257c-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="7257c-199">Ustawienia. Privacy.DataEnabled</span><span class="sxs-lookup"><span data-stu-id="7257c-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="7257c-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="7257c-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="7257c-201">Ustawienia. AdvancedOptions.DownloadMappings</span><span class="sxs-lookup"><span data-stu-id="7257c-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="7257c-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="7257c-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="7257c-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="7257c-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="7257c-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="7257c-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="7257c-205">Ustawienia. SasToken</span><span class="sxs-lookup"><span data-stu-id="7257c-205">settings.SasToken</span></span> |
| <span data-ttu-id="7257c-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="7257c-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="7257c-207">Token sygnatury dostępu Współdzielonego z protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="7257c-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="7257c-208">Rozwiązywanie problemów — kod błędu: 1100</span><span class="sxs-lookup"><span data-stu-id="7257c-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="7257c-209">Kod błędu 1100 wskazuje, że istnieje problem z hello rozszerzenia toohello DSC danych wprowadzonych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7257c-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="7257c-210">tekst Hello tych błędów jest zmienną i mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="7257c-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="7257c-211">Poniżej przedstawiono niektóre hello błędów, które może napotkać oraz jak je naprawić.</span><span class="sxs-lookup"><span data-stu-id="7257c-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="7257c-212">Nieprawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="7257c-212">Invalid Values</span></span>
<span data-ttu-id="7257c-213">"Jest Privacy.dataCollection"{0}".</span><span class="sxs-lookup"><span data-stu-id="7257c-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="7257c-214">Witaj tylko możliwe wartości to ","Włącz"i"Wyłącz"" "jest WmfVersion"{0}".</span><span class="sxs-lookup"><span data-stu-id="7257c-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="7257c-215">Tylko możliwe wartości to...</span><span class="sxs-lookup"><span data-stu-id="7257c-215">Only possible values are …</span></span> <span data-ttu-id="7257c-216">i "najnowsze" "</span><span class="sxs-lookup"><span data-stu-id="7257c-216">and 'latest'"</span></span>

<span data-ttu-id="7257c-217">Problem: Podana wartość nie jest dozwolona.</span><span class="sxs-lookup"><span data-stu-id="7257c-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="7257c-218">Rozwiązanie: Zmień hello nieprawidłową wartość tooa prawidłową wartość.</span><span class="sxs-lookup"><span data-stu-id="7257c-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="7257c-219">Zobacz tabelę hello w sekcji szczegółów hello.</span><span class="sxs-lookup"><span data-stu-id="7257c-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="7257c-220">Nieprawidłowy adres URL</span><span class="sxs-lookup"><span data-stu-id="7257c-220">Invalid URL</span></span>
<span data-ttu-id="7257c-221">"Jest ConfigurationData.url"{0}".</span><span class="sxs-lookup"><span data-stu-id="7257c-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="7257c-222">Nie jest prawidłowym adresem URL""jest DataBlobUri "{0}".</span><span class="sxs-lookup"><span data-stu-id="7257c-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="7257c-223">Nie jest prawidłowym adresem URL""jest Configuration.url "{0}".</span><span class="sxs-lookup"><span data-stu-id="7257c-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="7257c-224">Nie jest prawidłowym adresem URL"</span><span class="sxs-lookup"><span data-stu-id="7257c-224">This is not a valid URL"</span></span>

<span data-ttu-id="7257c-225">Problem: A pod warunkiem, że adres URL jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="7257c-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="7257c-226">Rozwiązanie: Sprawdź wszystkie podane adresami URL.</span><span class="sxs-lookup"><span data-stu-id="7257c-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="7257c-227">Upewnij się, że wszystkie adresy URL rozwiązania lokalizacji toovalid, które rozszerzenia hello mogą uzyskiwać dostęp do komputera zdalnego hello.</span><span class="sxs-lookup"><span data-stu-id="7257c-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="7257c-228">Nieprawidłowy typ ConfigurationArgument</span><span class="sxs-lookup"><span data-stu-id="7257c-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="7257c-229">"ConfigurationArguments nieprawidłowy typ" {0}</span><span class="sxs-lookup"><span data-stu-id="7257c-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="7257c-230">Problem: hello ConfigurationArguments właściwości nie można rozpoznać tooa obiektu Hashtable.</span><span class="sxs-lookup"><span data-stu-id="7257c-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="7257c-231">Rozwiązanie: Upewnij się z właściwości ConfigurationArguments obiektu Hashtable.</span><span class="sxs-lookup"><span data-stu-id="7257c-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="7257c-232">Postępuj zgodnie z formatu hello podano w przykładzie poprzedzających hello.</span><span class="sxs-lookup"><span data-stu-id="7257c-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="7257c-233">Zwróć uwagę na cudzysłowy, przecinki oraz nawiasy klamrowe.</span><span class="sxs-lookup"><span data-stu-id="7257c-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="7257c-234">Zduplikowana ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="7257c-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="7257c-235">"Znaleziono zduplikowane argumentów"{0}"w publicznych i chronionych configurationArguments"</span><span class="sxs-lookup"><span data-stu-id="7257c-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="7257c-236">Problem: hello ConfigurationArguments w ustawieniach publicznego i hello ConfigurationArguments w ustawieniach chronionych zawierać właściwości o hello tej samej nazwy.</span><span class="sxs-lookup"><span data-stu-id="7257c-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="7257c-237">Rozwiązanie: Usuń jeden z hello zduplikowane właściwości.</span><span class="sxs-lookup"><span data-stu-id="7257c-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="7257c-238">Brak właściwości</span><span class="sxs-lookup"><span data-stu-id="7257c-238">Missing Properties</span></span>
<span data-ttu-id="7257c-239">"Configuration.function wymaga configuration.url lub configuration.module określono"</span><span class="sxs-lookup"><span data-stu-id="7257c-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="7257c-240">"Configuration.url wymaga się, że określono tego configuration.script"</span><span class="sxs-lookup"><span data-stu-id="7257c-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="7257c-241">"Configuration.script wymaga się, że określono tego configuration.url"</span><span class="sxs-lookup"><span data-stu-id="7257c-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="7257c-242">"Configuration.url wymaga się, że określono tego configuration.function"</span><span class="sxs-lookup"><span data-stu-id="7257c-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="7257c-243">"ConfigurationUrlSasToken wymaga się, że określono tego configuration.url"</span><span class="sxs-lookup"><span data-stu-id="7257c-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="7257c-244">"ConfigurationDataUrlSasToken wymaga się, że określono tego configurationData.url"</span><span class="sxs-lookup"><span data-stu-id="7257c-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="7257c-245">Problem: Zdefiniowanych właściwości wymaga innej właściwości, która nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="7257c-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="7257c-246">Rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="7257c-246">Solutions:</span></span> 

* <span data-ttu-id="7257c-247">Podaj hello Brak właściwości.</span><span class="sxs-lookup"><span data-stu-id="7257c-247">Provide hello missing property.</span></span>
* <span data-ttu-id="7257c-248">Usuń właściwość hello, wymagającym hello Brak właściwości.</span><span class="sxs-lookup"><span data-stu-id="7257c-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7257c-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7257c-249">Next Steps</span></span>
<span data-ttu-id="7257c-250">Dowiedz się więcej o konfiguracji DSC i zestawach skali maszyn wirtualnych [za pomocą zestawów skali maszyny wirtualnej z hello Azure rozszerzenia usługi Konfiguracja DSC](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="7257c-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="7257c-251">Więcej szczegółów znajduje się na [zarządzania poświadczeniami bezpiecznego DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7257c-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="7257c-252">Aby uzyskać więcej informacji dotyczących obsługi rozszerzenia usługi Konfiguracja DSC Azure hello, zobacz [wprowadzenie toohello Azure konfiguracji żądanego stanu rozszerzenia obsługi](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7257c-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="7257c-253">Aby uzyskać więcej informacji o konfiguracji DSC środowiska PowerShell [odwiedź Centrum dokumentacji programu PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="7257c-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

