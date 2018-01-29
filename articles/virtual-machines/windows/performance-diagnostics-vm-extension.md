---
title: "Rozszerzenia maszyny Wirtualnej diagnostyki Azure wydajności dla systemu Windows | Dokumentacja firmy Microsoft"
description: "Wprowadza rozszerzenia maszyny Wirtualnej diagnostyki Azure wydajności dla systemu Windows."
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: troubleshooting
ms.date: 09/29/2017
ms.author: genli
ms.openlocfilehash: 5a7dc313f1d6453562e4d5a11ceca03e4459b043
ms.sourcegitcommit: 3fca41d1c978d4b9165666bb2a9a1fe2a13aabb6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2017
---
# <a name="azure-performance-diagnostics-vm-extension-for-windows"></a>Rozszerzenia maszyny Wirtualnej diagnostyki Azure wydajności dla systemu Windows

Rozszerzenie maszyny Wirtualnej diagnostyki wydajności Azure pomaga diagnostycznych zbieranie danych dotyczących wydajności z maszyn wirtualnych systemu Windows. Rozszerzenie przeprowadza analizę i udostępnia raport wyników i zaleceń, aby zidentyfikować i rozwiązać problemy z wydajnością na maszynie wirtualnej. To rozszerzenie instaluje narzędzie rozwiązywania problemów [PerfInsights](http://aka.ms/perfinsights).

## <a name="prerequisites"></a>Wymagania wstępne

To rozszerzenie można zainstalować na Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 i Windows Server 2016. Można go również zainstalować na Windows 8.1 i Windows 10.

## <a name="extension-schema"></a>Rozszerzenie schematu
Następujące JSON zawiera schemat rozszerzenia maszyny Wirtualnej systemu Azure wydajności diagnostyki. To rozszerzenie wymaga nazwy i klucza konta magazynu do przechowywania danych wyjściowych diagnostyki i raportów. Te wartości są poufne i powinien być przechowywany w chronionym konfiguracji. Azure VM ustawienie rozszerzenia chronione dane są szyfrowane, a jest odszyfrowane tylko na docelowej maszynie wirtualnej. Należy pamiętać, że **storageAccountName** i **storageAccountKey** jest rozróżniana wielkość liter. Inne wymagane parametry są wymienione w poniższej sekcji.

```JSON
    {
      "name": "[concat(parameters('vmName'),'/AzurePerformanceDiagnostics')]",
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "location": "[parameters('location')]",
      "apiVersion": "2015-06-15",
      "properties": {
        "publisher": "Microsoft.Azure.Performance.Diagnostics",
        "type": "AzurePerformanceDiagnostics",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "performanceScenario": "[parameters('performanceScenario')]",
                  "traceDurationInSeconds": "[parameters('traceDurationInSeconds')]",
                  "perfCounterTrace": "[parameters('perfCounterTrace')]",
                  "networkTrace": "[parameters('networkTrace')]",
                  "xperfTrace": "[parameters('xperfTrace')]",
                  "storPortTrace": "[parameters('storPortTrace')]",
            "srNumber": "[parameters('srNumber')]",
            "requestTimeUtc":  "[parameters('requestTimeUtc')]"
        },
          "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]"        
            }
      }
    }
```

### <a name="property-values"></a>Wartości właściwości

|   **Nazwa**   |**Wartość / przykład**|       **Opis**      |
|--------------|-------------------|----------------------------|
|apiVersion|2015-06-15|Wersja interfejsu API.
|Wydawcy|Microsoft.Azure.Performance.Diagnostics|Przestrzeń nazw wydawcy rozszerzenia.
|type|AzurePerformanceDiagnostics|Typ rozszerzenia maszyny Wirtualnej.
|typeHandlerVersion|1.0|Wersja rozszerzenia obsługi.
|performanceScenario|podstawowe|Scenariusz wydajności, dla której do przechwytywania danych. Prawidłowe wartości to: **podstawowe**, **vmslow**, **azurefiles**, i **niestandardowych**.
|traceDurationInSeconds|300|Czas trwania śledzenia, jeśli nie wybrano opcji śledzenia.
|perfCounterTrace|P|Opcję w celu włączenia śledzenia licznika wydajności. Prawidłowe wartości to **p** lub wartość pusta. Jeśli nie chcesz przechwytywać ślad, pozostaw wartość jako pusty.
|networkTrace|n|Opcję w celu włączenia śledzenia ścieżek połączeń sieciowych. Prawidłowe wartości to  **n**  lub wartość pusta. Jeśli nie chcesz przechwytywać ślad, pozostaw wartość jako pusty.
|xperfTrace|x|Opcję, aby włączyć program XPerf śledzenia. Prawidłowe wartości to **x** lub wartość pusta. Jeśli nie chcesz przechwytywać ślad, pozostaw wartość jako pusty.
|storPortTrace|s|Opcję, aby włączyć StorPort śledzenia. Prawidłowe wartości to **s** lub wartość pusta. Jeśli nie chcesz przechwytywać ślad, pozostaw wartość jako pusty.
|srNumber|123452016365929|Numer biletu pomocy technicznej, jeśli jest dostępna. Pozostaw wartość jako pusty, jeśli go nie masz.
|storageAccountName|mojekontomagazynu|Nazwa konta magazynu do przechowywania dzienników diagnostyki i wyników.
|storageAccountKey|lDuVvxuZB28NNP... hAiRF3voADxLBTcc ==|Klucz konta magazynu.

## <a name="install-the-extension"></a>Instalowanie rozszerzenia

Wykonaj następujące kroki, aby zainstalować rozszerzenie na maszynach wirtualnych systemu Windows:

1. Zaloguj się w witrynie [Azure Portal](http://portal.azure.com).
2. Wybierz maszynę wirtualną, której chcesz zainstalować tego rozszerzenia.

    ![Zrzut ekranu Azure portalu, z wyróżnionym maszyny wirtualne](media/performance-diagnostics-vm-extension/select-the-virtual-machine.png)
3. Wybierz **rozszerzenia** bloku, a następnie wybierz **Dodaj**.

    ![Zrzut ekranu rozszerzenia blok Dodaj wyróżnione](media/performance-diagnostics-vm-extension/select-extensions.png)
4. Wybierz **Azure wydajności diagnostyki**, zapoznaj się z warunkami i wybierz **Utwórz**.

    ![Zrzut ekranu z nowym ekranie zasobów Azure Diagnostyka wydajności wyróżniane](media/performance-diagnostics-vm-extension/create-azure-performance-diagnostics-extension.png)
5. Podaj wartości parametrów dla instalacji, a następnie wybierz **OK** do zainstalowania rozszerzenia. Aby uzyskać więcej informacji na temat obsługiwanych scenariuszy, zobacz [sposób użycia PerfInsights](how-to-use-perfInsights.md#supported-troubleshooting-scenarios). 

    ![Zrzut ekranu Zainstaluj rozszerzenie okno dialogowe](media/performance-diagnostics-vm-extension/install-the-extension.png)
6. Jeśli instalacja się powiodła, zobaczysz komunikat informujący o tym stanie.

    ![Zrzut ekranu udostępniania zakończyło się pomyślnie wiadomości](media/performance-diagnostics-vm-extension/provisioning-succeeded-message.png)

    > [!NOTE]
    > Rozszerzenie jest uruchamiany podczas inicjowania obsługi zakończyła się pomyślnie. Trwa dwóch minut lub mniej, aby ukończyć scenariusz podstawowy. W innych sytuacjach działa przez czas określony podczas instalacji.

## <a name="remove-the-extension"></a>Usuń rozszerzenie
Aby usunąć rozszerzenia z maszyny wirtualnej, wykonaj następujące kroki:

1. Zaloguj się do [portalu Azure](http://portal.azure.com), wybierz maszynę wirtualną, z którego chcesz usunąć to rozszerzenie, a następnie wybierz **rozszerzenia** bloku. 
2. Wybierz (**...** ) wydajności diagnostyki rozszerzenia wpisu z listy, a następnie wybierz **Odinstaluj**.

    ![Zrzut ekranu rozszerzenia blok odinstalowywanie wyróżnionym](media/performance-diagnostics-vm-extension/uninstall-the-extension.png)

    > [!NOTE]
    > Można również wybrać wpis rozszerzenia i wybierz **Odinstaluj** opcji.

## <a name="template-deployment"></a>Wdrażanie na podstawie szablonu
Rozszerzenia maszyny wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager. Schematu JSON szczegółowo opisane w poprzedniej sekcji można użyć w szablonie usługi Azure Resource Manager. Ta funkcja jest uruchamiana rozszerzenia maszyny Wirtualnej Azure wydajności diagnostyki podczas wdrażania szablonu usługi Azure Resource Manager. Poniżej przedstawiono przykładowy szablon:

````
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "vmName": {
      "type": "string",
      "defaultValue": "yourVMName"
    },
    "location": {
      "type": "string",
      "defaultValue": "southcentralus"
    },
    "storageAccountName": {
      "type": "securestring"
      "defaultValue": "yourStorageAccount"
    },
    "storageAccountKey": {
      "type": "securestring"
      "defaultValue": "yourStorageAccountKey"
    },
    "performanceScenario": {
      "type": "string",
      "defaultValue": "basic"
    },
    "srNumber": {
      "type": "string",
      "defaultValue": ""
    },
    "traceDurationInSeconds": {
      "type": "int",
    "defaultValue": 300
    },
    "perfCounterTrace": {
      "type": "string",
      "defaultValue": "p"
    },
    "networkTrace": {
      "type": "string",
      "defaultValue": ""
    },
    "xperfTrace": {
      "type": "string",
      "defaultValue": ""
    },
    "storPortTrace": {
      "type": "string",
      "defaultValue": ""
    },
    "requestTimeUtc": {
      "type": "string",
      "defaultValue": "10/2/2017 11:06:00 PM"
    }       
  },
  "resources": [
    {
      "name": "[concat(parameters('vmName'),'/AzurePerformanceDiagnostics')]",
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "location": "[parameters('location')]",
      "apiVersion": "2015-06-15",
      "properties": {
        "publisher": "Microsoft.Azure.Performance.Diagnostics",
        "type": "AzurePerformanceDiagnostics",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "performanceScenario": "[parameters('performanceScenario')]",
                  "traceDurationInSeconds": "[parameters('traceDurationInSeconds')]",
                  "perfCounterTrace": "[parameters('perfCounterTrace')]",
                  "networkTrace": "[parameters('networkTrace')]",
                  "xperfTrace": "[parameters('xperfTrace')]",
                  "storPortTrace": "[parameters('storPortTrace')]",
            "srNumber": "[parameters('srNumber')]",
            "requestTimeUtc":  "[parameters('requestTimeUtc')]"
        },
          "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]"        
            }
      }
    }
  ]
}
````

## <a name="powershell-deployment"></a>Wdrożenie programu PowerShell
`Set-AzureRmVMExtension` Polecenia mogą być używane do wdrażania rozszerzenia maszyny Wirtualnej systemu Azure wydajności diagnostyki do istniejącej maszyny wirtualnej. Przed uruchomieniem polecenia należy przechowywać konfiguracje publiczne i prywatne w tablicy skrótów programu PowerShell.

PowerShell

````
$PublicSettings = @{ "performanceScenario":"basic","traceDurationInSeconds":300,"perfCounterTrace":"p","networkTrace":"","xperfTrace":"","storPortTrace":"","srNumber":"","requestTimeUtc":"2017-09-28T22:08:53.736Z" }
$ProtectedSettings = @{"storageAccountName":"mystorageaccount","storageAccountKey":"mystoragekey"}

Set-AzureRmVMExtension -ExtensionName "AzurePerformanceDiagnostics" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.Azure.Performance.Diagnostics" `
    -ExtensionType "AzurePerformanceDiagnostics" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS `
````

## <a name="information-on-the-data-captured"></a>Informacje na temat danych przechwyconych
Narzędzie PerfInsights gromadzi różne dzienniki, konfiguracji i danych diagnostycznych, w zależności od wybranego scenariusza. Aby uzyskać więcej informacji, zobacz [dokumentacji PerfInsights](http://aka.ms/perfinsights).

## <a name="view-and-share-the-results"></a>Wyświetlanie i udostępnianie wyników

Dane wyjściowe z rozszerzenia są przechowywane w folderze. Folder o nazwie log_collection i znajduje się w obszarze dysk Temp (zazwyczaj D:\log_collection) domyślnie. Pliki zip zawierający dzienników diagnostycznych i raport o wyniki i zalecenia można wyświetlić w tym folderze.

Można również znaleźć plik zip na koncie magazynu podane podczas instalacji. Są one udostępniane przez 30 dni przy użyciu [udostępnionego sygnatur dostępu (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md). Plik tekstowy o nazwie *zipfilename*_saslink.txt również jest tworzony w folderze log_collection. Ten plik zawiera łącze SAS utworzone, aby pobrać plik zip. Każdy, kto ma to łącze jest w stanie pobrać plik zip.

Ułatwiających z pracownikiem pomocy technicznej pracuje biletu pomocy technicznej firmy Microsoft może Użyj tego łącza SAS do pobierania danych diagnostyki.

Aby wyświetlić raport, Wyodrębnij plik zip, a następnie otwórz **PerfInsights Report.html** pliku.

Można również pobrać plik zip bezpośrednio z portalu, wybierając rozszerzenie.

![Zrzut ekranu wydajności diagnostyki szczegółowy stan](media/performance-diagnostics-vm-extension/view-detailed-status.png)

> [!NOTE]
> Łącze SAS wyświetlana w portalu może nie działać. To może być spowodowane źle sformułowany adres URL podczas operacji kodowania i dekodowania. Zamiast tego można uzyskać łącze bezpośrednio z pliku *_saslink.txt z maszyny Wirtualnej.

## <a name="troubleshoot-and-support"></a>Rozwiązywanie problemów i obsługa techniczna

- Stan wdrożenia rozszerzenia (w obszarze powiadomień) mogą być wyświetlane "Wdrożenie w toku", mimo że rozszerzenia pomyślnie zainicjowano obsługę administracyjną.

    Ten problem można zignorować, dopóki stan rozszerzenia wskazuje, że rozszerzenie zostanie pomyślnie zainicjowana.
- Niektóre problemy można rozwiązać podczas instalacji przy użyciu dzienników rozszerzenia. Dane wyjściowe wykonania rozszerzenia jest rejestrowany pliki znajdujące się w następującym katalogu:

        C:\Packages\Plugins\Microsoft.Azure.Performance.Diagnostics.AzurePerformanceDiagnostics

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się ekspertów platformy Azure na [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź do [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/)i wybierz **uzyskać pomoc techniczną**. Aby uzyskać informacje o korzystaniu z pomocy technicznej platformy Azure, przeczytaj [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/support/faq/).
