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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>VMSS systemu Windows i konfiguracji żądanego stanu przy użyciu szablonów usługi Azure Resource Manager
W tym artykule opisano hello szablonu usługi Resource Manager dla hello [konfiguracji żądanego stanu rozszerzenia obsługi](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="template-example-for-a-windows-vm"></a>Przykład szablonu maszyny wirtualnej systemu Windows
Witaj poniższy fragment przechodzi w stan hello sekcji zasobów hello szablonu.

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

## <a name="template-example-for-windows-vmss"></a>Przykład szablonu VMSS systemu Windows
Węzeł VMSS ma sekcję "właściwości" z hello "VirtualMachineProfile" atrybutu "extensionProfile". DSC zostanie dodany w obszarze "rozszerzenia". 

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

## <a name="detailed-settings-information"></a>Informacje szczegółowe ustawienia
Witaj następujące schemat jest przeznaczony dla części ustawień hello hello rozszerzenia usługi Konfiguracja DSC Azure w szablonie usługi Azure Resource Manager.

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

## <a name="details"></a>Szczegóły
| Nazwa właściwości | Typ | Opis |
| --- | --- | --- |
| settings.wmfVersion |Ciąg |Określa wersję hello hello Windows Management Framework, która ma zostać zainstalowana na maszynie Wirtualnej. Ustawienie tej właściwości too'latest "hello instaluje najnowsze wersję programu WMF. Witaj tylko bieżące możliwe wartości dla tej właściwości to **"4.0", "5.0", "5.0PP' i"r"**. Te możliwe wartości to tooupdates podmiotu. Witaj wartość domyślna to "najnowsze". |
| Settings.Configuration.URL |Ciąg |Określa hello adres URL lokalizacji, z których toodownload pliku zip konfiguracji DSC. Podany adres URL hello wymaga tokenu sygnatury dostępu Współdzielonego w celu uzyskania dostępu, należy najpierw tooset hello protectedSettings.configurationUrlSasToken toohello wartość właściwości token sygnatury dostępu Współdzielonego. Ta właściwość jest wymagana, jeśli zdefiniowano settings.configuration.script i/lub settings.configuration.function. |
| Settings.Configuration.Script |Ciąg |Określa nazwę pliku hello hello skryptu, który zawiera definicję hello konfiguracji DSC. Ten skrypt musi być w folderze głównym hello hello pliku zip pobranego z hello adres URL określony przez właściwość configuration.url hello. Ta właściwość jest wymagana, jeśli zdefiniowano settings.configuration.url i/lub settings.configuration.script. |
| Settings.Configuration.Function |Ciąg |Określa nazwę hello konfiguracji DSC. konfigurację Hello o nazwie muszą być zawarte w skrypcie hello zdefiniowane przez configuration.script. Ta właściwość jest wymagana, jeśli zdefiniowano settings.configuration.url i/lub settings.configuration.function. |
| settings.configurationArguments |Collection |Definiuje żadnych parametrów, które chcesz konfiguracji DSC tooyour toopass. Ta właściwość nie jest zaszyfrowany. |
| settings.configurationData.url |Ciąg |Określa adres URL hello, z których toodownload dane konfiguracyjne (psd1) pliku toouse jako dane wejściowe dla danej konfiguracji DSC. Podany adres URL hello wymaga tokenu sygnatury dostępu Współdzielonego w celu uzyskania dostępu, należy najpierw tooset hello protectedSettings.configurationDataUrlSasToken toohello wartość właściwości token sygnatury dostępu Współdzielonego. |
| settings.privacy.dataEnabled |Ciąg |Włącza lub wyłącza gromadzenia danych telemetrii. Witaj tylko możliwe wartości dla tej właściwości to **"Włącz", "Wyłączone", ", lub $null**. Puste ani mieć wartości null, pozostawiając ta właściwość umożliwia telemetrii. Witaj, wartością domyślną jest ". [Więcej informacji](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |Collection |Definiuje alternatywne lokalizacje, z których toodownload hello WMF. [Więcej informacji](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |Collection |Definiuje żadnych parametrów, które chcesz konfiguracji DSC tooyour toopass. Ta właściwość jest zaszyfrowany. |
| protectedSettings.configurationUrlSasToken |Ciąg |Określa hello tokenu tooaccess hello adres URL SAS zdefiniowane przez configuration.url. Ta właściwość jest zaszyfrowany. |
| protectedSettings.configurationDataUrlSasToken |Ciąg |Określa hello tokenu tooaccess hello adres URL SAS zdefiniowane przez configurationData.url. Ta właściwość jest zaszyfrowany. |

## <a name="settings-vs-protectedsettings"></a>Ustawienia programu vs. ProtectedSettings
Wszystkie ustawienia są zapisywane w pliku tekstowym ustawień na powitania maszyny Wirtualnej.
Właściwości w obszarze "ustawienia" są właściwości publiczne, ponieważ nie są szyfrowane w pliku tekstowym hello ustawienia.
Właściwości w obszarze "protectedSettings" są szyfrowane przy użyciu certyfikatu i nie są wyświetlane w postaci zwykłego tekstu, w tym pliku na powitania maszyny Wirtualnej.

Jeśli konfiguracja hello wymaga poświadczeń, mogły one zostać uwzględnione w protectedSettings:

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

## <a name="example"></a>Przykład
Hello poniższy przykład pochodzi z hello "Wprowadzenie" sekcji hello [strony Przegląd programu obsługi rozszerzenia DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
W tym przykładzie używane szablony Menedżera zasobów, zamiast polecenia cmdlet toodeploy hello rozszerzenia. Zapisz konfigurację "IisInstall.ps1" hello, umieść ją w. ZIP plik, a przekazywania hello w dostępny adres URL. W tym przykładzie użyto magazynu obiektów blob platformy Azure, ale jest to możliwe toodownload. Pliki ZIP z dowolnego miejsca i dowolnego.

W szablonie usługi Azure Resource Manager hello hello następujący kod nakazuje hello wirtualna toodownload hello poprawnego pliku i uruchom hello odpowiednią funkcję programu PowerShell:

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

## <a name="updating-from-hello-previous-format"></a>Aktualizowanie z hello poprzedniego formatu
Wszystkie ustawienia w hello poprzedniego formatu (zawierający właściwości publiczne hello ModulesUrl, ConfigurationFunction, właściwości lub SasToken) automatycznie dostosowania bieżącego formatu toohello i uruchom tak samo jak przed.

powitania po schematu jest schemat ustawień poprzedniej jakie hello wyszukiwanego, takich jak:

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

Oto, jak poprzedni format hello dostosowuje toohello bieżącego formatu:

| Nazwa właściwości | Odpowiednik w poprzednim schematu |
| --- | --- |
| settings.wmfVersion |Ustawienia. WMFVersion |
| Settings.Configuration.URL |Ustawienia. ModulesUrl |
| Settings.Configuration.Script |Pierwsza część ustawień. ConfigurationFunction (przed "\\\\") |
| Settings.Configuration.Function |Druga część ustawień. ConfigurationFunction (po "\\\\") |
| settings.configurationArguments |Ustawienia. Właściwości |
| settings.configurationData.url |protectedSettings.DataBlobUri (bez tokenu sygnatury dostępu Współdzielonego) |
| settings.privacy.dataEnabled |Ustawienia. Privacy.DataEnabled |
| settings.advancedOptions.downloadMappings |Ustawienia. AdvancedOptions.DownloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |Ustawienia. SasToken |
| protectedSettings.configurationDataUrlSasToken |Token sygnatury dostępu Współdzielonego z protectedSettings.DataBlobUri |

## <a name="troubleshooting---error-code-1100"></a>Rozwiązywanie problemów — kod błędu: 1100
Kod błędu 1100 wskazuje, że istnieje problem z hello rozszerzenia toohello DSC danych wprowadzonych przez użytkownika.
tekst Hello tych błędów jest zmienną i mogą ulec zmianie.
Poniżej przedstawiono niektóre hello błędów, które może napotkać oraz jak je naprawić.

### <a name="invalid-values"></a>Nieprawidłowe wartości
"Jest Privacy.dataCollection"{0}". Witaj tylko możliwe wartości to ","Włącz"i"Wyłącz"" "jest WmfVersion"{0}". Tylko możliwe wartości to... i "najnowsze" "

Problem: Podana wartość nie jest dozwolona.

Rozwiązanie: Zmień hello nieprawidłową wartość tooa prawidłową wartość. Zobacz tabelę hello w sekcji szczegółów hello.

### <a name="invalid-url"></a>Nieprawidłowy adres URL
"Jest ConfigurationData.url"{0}". Nie jest prawidłowym adresem URL""jest DataBlobUri "{0}". Nie jest prawidłowym adresem URL""jest Configuration.url "{0}". Nie jest prawidłowym adresem URL"

Problem: A pod warunkiem, że adres URL jest nieprawidłowy.

Rozwiązanie: Sprawdź wszystkie podane adresami URL. Upewnij się, że wszystkie adresy URL rozwiązania lokalizacji toovalid, które rozszerzenia hello mogą uzyskiwać dostęp do komputera zdalnego hello.

### <a name="invalid-configurationargument-type"></a>Nieprawidłowy typ ConfigurationArgument
"ConfigurationArguments nieprawidłowy typ" {0}

Problem: hello ConfigurationArguments właściwości nie można rozpoznać tooa obiektu Hashtable. 

Rozwiązanie: Upewnij się z właściwości ConfigurationArguments obiektu Hashtable. Postępuj zgodnie z formatu hello podano w przykładzie poprzedzających hello. Zwróć uwagę na cudzysłowy, przecinki oraz nawiasy klamrowe.

### <a name="duplicate-configurationarguments"></a>Zduplikowana ConfigurationArguments
"Znaleziono zduplikowane argumentów"{0}"w publicznych i chronionych configurationArguments"

Problem: hello ConfigurationArguments w ustawieniach publicznego i hello ConfigurationArguments w ustawieniach chronionych zawierać właściwości o hello tej samej nazwy.

Rozwiązanie: Usuń jeden z hello zduplikowane właściwości.

### <a name="missing-properties"></a>Brak właściwości
"Configuration.function wymaga configuration.url lub configuration.module określono"

"Configuration.url wymaga się, że określono tego configuration.script"

"Configuration.script wymaga się, że określono tego configuration.url"

"Configuration.url wymaga się, że określono tego configuration.function"

"ConfigurationUrlSasToken wymaga się, że określono tego configuration.url"

"ConfigurationDataUrlSasToken wymaga się, że określono tego configurationData.url"

Problem: Zdefiniowanych właściwości wymaga innej właściwości, która nie istnieje.

Rozwiązania: 

* Podaj hello Brak właściwości.
* Usuń właściwość hello, wymagającym hello Brak właściwości.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o konfiguracji DSC i zestawach skali maszyn wirtualnych [za pomocą zestawów skali maszyny wirtualnej z hello Azure rozszerzenia usługi Konfiguracja DSC](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

Więcej szczegółów znajduje się na [zarządzania poświadczeniami bezpiecznego DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Aby uzyskać więcej informacji dotyczących obsługi rozszerzenia usługi Konfiguracja DSC Azure hello, zobacz [wprowadzenie toohello Azure konfiguracji żądanego stanu rozszerzenia obsługi](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Aby uzyskać więcej informacji o konfiguracji DSC środowiska PowerShell [odwiedź Centrum dokumentacji programu PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

