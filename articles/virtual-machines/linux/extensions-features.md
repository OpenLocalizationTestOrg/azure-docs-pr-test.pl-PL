---
title: "aaaVirtual komputera rozszerzeń i funkcji w systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie rozszerzenia są dostępne dla maszyn wirtualnych platformy Azure, pogrupowane według co ich Podaj puli zasobów i zwiększyć."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a>Rozszerzenia maszyn wirtualnych i funkcji w systemie Linux

Rozszerzenia maszyny wirtualnej platformy Azure są małe aplikacji, które mają po wdrożeniu i automatyzację zadań na maszynach wirtualnych Azure. Na przykład, jeśli maszyna wirtualna wymaga instalacji oprogramowania, ochrony oprogramowania antywirusowego lub Docker konfiguracji, rozszerzenia maszyny Wirtualnej mogą być używane toocomplete tych zadań. Rozszerzenia maszyny Wirtualnej platformy Azure mogą być uruchamiane przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, szablony usługi Azure Resource Manager i hello portalu Azure. Rozszerzenia mogą być powiązane z nowego wdrożenia maszyny wirtualnej lub uruchomienia dowolnego istniejącego systemu.

Ten dokument zawiera omówienie rozszerzeń maszyny Wirtualnej, wymagań wstępnych dotyczących używania rozszerzenia maszyny Wirtualnej platformy Azure i wskazówki na sposób toodetect, zarządzania i usunąć rozszerzenia maszyny Wirtualnej. Ten dokument zawiera informacje uogólniony wielu rozszerzeń maszyny Wirtualnej nie są dostępne, każde z nich potencjalnie unikatowych konfiguracji. Rozszerzenie szczegółowe znajdują się w poszczególnych rozszerzeń poszczególnych toohello określonego dokumentu.

## <a name="use-cases-and-samples"></a>Przypadki użycia i przykłady

Dostępnych jest kilka różnych rozszerzeń maszyny Wirtualnej platformy Azure, każde z nich określony przypadek użycia. Przykłady to:

- Zastosowanie programu PowerShell żądany stan konfiguracji tooa maszyny wirtualnej za pomocą hello rozszerzenia konfiguracji DSC dla systemu Linux. Aby uzyskać więcej informacji, zobacz [Azure żądany stan konfiguracji rozszerzenia](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).
- Konfigurowanie monitorowania maszyny wirtualnej z hello rozszerzenia maszyny Wirtualnej agenta monitorowania firmy Microsoft. Aby uzyskać więcej informacji, zobacz [jak toomonitor Maszynę wirtualną systemu Linux](tutorial-monitoring.md).
- Skonfiguruj Monitorowanie infrastruktury platformy Azure z hello Datadog rozszerzenia. Aby uzyskać więcej informacji, zobacz hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Konfigurowanie hosta Docker na maszynie wirtualnej platformy Azure przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker hello. Aby uzyskać więcej informacji, zobacz [rozszerzenia maszyny Wirtualnej platformy Docker](dockerextension.md).

Ponadto rozszerzenia tooprocess rozszerzenia niestandardowego skryptu dostępnej dla maszyn wirtualnych w systemach Windows i Linux. Witaj rozszerzenia niestandardowego skryptu dla systemu Linux umożliwia żadnych Bash toobe skrypt uruchamiany na maszynie wirtualnej. Niestandardowe skrypty są przydatne w przypadku projektowania wdrożeń platformy Azure, które wymagają konfiguracji oprócz zapewniają jakie natywnego narzędzia Azure. Aby uzyskać więcej informacji, zobacz [rozszerzenie skryptu niestandardowego maszyny Wirtualnej systemu Linux](extensions-customscript.md).


## <a name="prerequisites"></a>Wymagania wstępne

Każde rozszerzenie maszyny wirtualnej może mieć własny zestaw wymagań wstępnych. Na przykład hello rozszerzenia maszyny Wirtualnej platformy Docker ma wymagań wstępnych obsługiwanych dystrybucji systemu Linux. Wymagania dotyczące poszczególnych rozszerzeń są szczegółowo opisane w dokumentacji konkretnego rozszerzenia hello.

### <a name="azure-vm-agent"></a>Agent maszyny wirtualnej platformy Azure

agent maszyny Wirtualnej Azure Hello zarządza interakcje między maszyny wirtualnej platformy Azure i hello kontrolera sieci szkieletowej Azure. agent maszyny Wirtualnej Hello jest odpowiedzialny za dużo aspekty funkcjonalne, wdrażania i zarządzania maszynami wirtualnymi platformy Azure, łącznie z rozszerzeniami maszyny Wirtualnej. agent maszyny Wirtualnej Azure Hello jest preinstalowany na portalu Azure Marketplace obrazów i można zainstalować ręcznie w obsługiwanych systemach operacyjnych.

Aby uzyskać informacje dotyczące obsługiwanych systemów operacyjnych i instrukcje dotyczące instalacji, zobacz [agenta maszyny wirtualnej platformy Azure](../windows/classic/agents-and-extensions.md).

## <a name="discover-vm-extensions"></a>Odnajdywanie rozszerzeń maszyny Wirtualnej

Wiele różnych rozszerzeń maszyny Wirtualnej są dostępne do użycia z maszyn wirtualnych platformy Azure. toosee pełną listę, uruchom hello następujące polecenie z wiersza polecenia platformy Azure hello, zastępując lokalizacji przykład hello hello wybranej lokalizacji.

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a>Uruchom rozszerzeń maszyny Wirtualnej

Rozszerzenia maszyny wirtualnej platformy Azure może działać w istniejących maszyn wirtualnych, które są przydatne, gdy potrzebne zmiany w konfiguracji toomake lub Przywróć łączność w przypadku wdrożonej maszyny Wirtualnej. Rozszerzenia maszyny Wirtualnej dołączany także wdrażanie szablonów usługi Azure Resource Manager. Za pomocą rozszerzeń z szablonami usługi Resource Manager, można wdrożyć i konfigurować bez interwencji po wdrożeniu maszyn wirtualnych platformy Azure.

Hello następujące metody mogą być używane toorun rozszerzenie dla istniejącej maszyny wirtualnej.

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

Rozszerzenia maszyny wirtualnej platformy Azure mogą być uruchamiane na istniejącej maszyny wirtualnej za pomocą hello `az vm extension set` polecenia. W tym przykładzie jest uruchamiana hello niestandardowe rozszerzenie skryptu dla maszyny wirtualnej.

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

Witaj skrypt generuje dane wyjściowe podobne toohello następującego tekstu:

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a>Azure Portal

Rozszerzenia maszyny Wirtualnej może być zastosowane tooan istniejącej maszyny wirtualnej za pośrednictwem hello portalu Azure. toodo tak, wybierz maszynę wirtualną hello, wybierz **rozszerzenia**i kliknij przycisk **Dodaj**. Wybierz rozszerzenie hello z hello listę dostępnych rozszerzeń i postępuj zgodnie z instrukcjami powitania w Kreatorze hello.

Witaj poniższy obraz przedstawia hello instalacji hello rozszerzenie skryptu niestandardowego Linux z hello portalu Azure.

![Zainstaluj rozszerzenie skryptu niestandardowego](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a>Szablony usługi Azure Resource Manager

Rozszerzeń maszyny Wirtualnej może być dodany tooan szablonu usługi Azure Resource Manager i wykonany przy użyciu wdrożenia hello hello szablonu. Podczas wdrażania rozszerzenia za pomocą szablonu można tworzyć wdrożeń platformy Azure w pełni skonfigurowany. Na przykład po JSON hello jest pobierana z szablonem usługi Resource Manager. Szablon Hello wdraża zestaw maszyn wirtualnych z równoważeniem obciążenia i bazy danych Azure SQL, a następnie instaluje aplikację .NET Core na każdej maszynie Wirtualnej. Instalacja oprogramowania hello odpowiada on za Hello rozszerzenia maszyny Wirtualnej.

Aby uzyskać więcej informacji, zobacz pełną hello [szablonu usługi Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

Aby uzyskać więcej informacji, zobacz [szablonów Authoring Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).

## <a name="secure-vm-extension-data"></a>Zabezpieczanie danych rozszerzenia maszyny Wirtualnej

Jeśli korzystasz z rozszerzenia maszyny Wirtualnej, może być konieczne tooinclude poufne informacje, takie jak poświadczeń, nazwy konta magazynu i klucze dostępu do konta magazynu. Wiele rozszerzeń maszyny Wirtualnej obejmują konfiguracji chronionych danych i tylko odszyfrowującego wewnątrz hello docelowej maszyny wirtualnej. Każde rozszerzenie ma schematu określonej konfiguracji chronionych, a każdy szczegółowo opisano w dokumentacji konkretnego rozszerzenia.

Witaj poniższy przykład przedstawia wystąpienie hello rozszerzenia niestandardowego skryptu dla systemu Linux. Należy zauważyć, że tego tooexecute polecenia hello zawiera zestaw poświadczeń. W tym przykładzie hello tooexecute polecenia nie będą szyfrowane.


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Przenoszenie hello **tooexecute polecenia** toohello właściwości **chronione** konfiguracja zabezpiecza hello wykonywania ciągu.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a>Rozwiązywanie problemów z rozszerzeń maszyny Wirtualnej

Każde rozszerzenie maszyny Wirtualnej może być Rozwiązywanie problemów z rozszerzenia toohello określonych czynności. Na przykład podczas korzystania z rozszerzenia niestandardowego skryptu hello, szczegóły wykonywania skryptu można znaleźć lokalnie na maszynie wirtualnej hello, na którym uruchomiono hello rozszerzenia. Wszystkie kroki rozwiązywania problemów specyficzne dla rozszerzenia są szczegółowo opisane w dokumentacji specyficzne dla rozszerzenia.

następujące kroki rozwiązywania problemów Hello mają zastosowanie tooall rozszerzenia maszyny wirtualnej.

### <a name="view-extension-status"></a>Wyświetl stan rozszerzenia

Po uruchomieniu rozszerzenie maszyny wirtualnej na maszynie wirtualnej, użyj powitania po stan rozszerzenia tooreturn polecenia wiersza polecenia platformy Azure. Zastąp przykładowe nazwy parametrów własne wartości.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

dane wyjściowe Hello wygląda hello następującego tekstu:

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

Stan wykonania rozszerzenia można znaleźć w portalu Azure hello. Wybierz stan hello tooview rozszerzenia maszyny wirtualnej wybierz hello, **rozszerzenia**, i wybierz hello żądanego rozszerzenia.

### <a name="rerun-a-vm-extension"></a>Uruchom ponownie rozszerzenia maszyny Wirtualnej

Może się zdarzyć, w których toobe, musi mieć rozszerzenie maszyny wirtualnej ponownie. Możesz ponownie uruchomić rozszerzenia, usuwając go i następnie ponowne uruchomienie rozszerzenia hello metodą wykonywania wybranych przez użytkownika. tooremove rozszerzenia, uruchom następujące polecenie z wiersza polecenia platformy Azure hello hello. Zastąp przykładowe nazwy parametrów własne wartości.

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

Rozszerzenie można usunąć przy użyciu hello następujące kroki w portalu Azure hello:

1. Wybierz maszynę wirtualną.
2. Wybierz **rozszerzenia**.
3. Wybierz żądaną hello rozszerzenie.
4. Wybierz **odinstalować**.

## <a name="common-vm-extension-reference"></a>Typowe odwołania do rozszerzenia maszyny Wirtualnej
| Nazwa rozszerzenia | Opis | Więcej informacji |
| --- | --- | --- |
| Niestandardowe rozszerzenie skryptu dla systemu Linux |Uruchom skrypty przed maszyny wirtualnej platformy Azure |[Niestandardowe rozszerzenie skryptu dla systemu Linux](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Rozszerzenie docker |Zainstaluj hello Docker demon toosupport Docker poleceń zdalnych. |[Rozszerzenie maszyny wirtualnej Docker](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Rozszerzenie dostępu do maszyny wirtualnej |Odzyskanie dostępu tooan maszyny wirtualnej platformy Azure |[Rozszerzenie dostępu do maszyny wirtualnej](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| Rozszerzenie Diagnostyka Azure |Zarządzanie Diagnostyka Azure |[Rozszerzenie Diagnostyka Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Rozszerzenia dostępu do maszyny Wirtualnej platformy Azure |Zarządzaj użytkownikami i poświadczenia |[Rozszerzenia dostępu do maszyny Wirtualnej dla systemu Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
