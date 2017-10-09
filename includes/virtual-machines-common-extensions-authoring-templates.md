## <a name="overview-of-azure-resource-manager-templates"></a>Omówienie szablonów usługi Azure Resource Manager
Szablony usługi Azure Resource Manager pozwala toodeclaratively Określ hello Azure IaaS infrastruktury w języku Json, definiując hello zależności między zasobami. Szczegółowe omówienie szablony Menedżera zasobów Azure przeczytaj artykuł toohello poniżej:

[Omówienie grupy zasobów](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Przykładowy szablon fragment dotyczący rozszerzeń maszyny Wirtualnej
Wdrażanie rozszerzeń maszyny Wirtualnej, zgodnie z częścią szablonu usługi Azure Resource Manager wymaga toodeclaratively Określ Konfiguracja rozszerzenia hello hello szablonu.
Oto hello format służący do określania hello konfiguracji rozszerzenia.

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
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

Jak widać z powyższych hello hello rozszerzenia szablonu zawiera dwie główne części:

1. Rozszerzenie nazwy, wydawcy i wersji
2. Konfiguracja rozszerzenia.

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>Identyfikowanie hello wydawcy, typ i typeHandlerVersion dla dowolnego rozszerzenia
Rozszerzenia maszyny Wirtualnej platformy Azure są opublikowane przez firmę Microsoft i zaufane 3 wydawców firm i każde rozszerzenie jest unikatowo identyfikowana przez jej wydawcę, typ i hello typeHandlerVersion. Te można określić jako następujące czynności:  

