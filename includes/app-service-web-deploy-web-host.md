### <a name="app-service-plan"></a>Plan usługi App Service
Tworzy plan usługi hello hostingu hello aplikacji sieci web. Podaj nazwę hello plan hello przy użyciu hello **hostingPlanName** parametru. Lokalizacja Hello planu hello jest używany tę samą lokalizację dla grupy zasobów hello hello. Witaj cenową rozmiar warstwy i proces roboczy są określone w hello **sku** i **workerSize** parametrów

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

