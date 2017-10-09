### <a name="app-service-plan"></a><span data-ttu-id="bcd61-101">Plan usługi App Service</span><span class="sxs-lookup"><span data-stu-id="bcd61-101">App Service plan</span></span>
<span data-ttu-id="bcd61-102">Tworzy plan usługi hello hostingu hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="bcd61-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="bcd61-103">Podaj nazwę hello plan hello przy użyciu hello **hostingPlanName** parametru.</span><span class="sxs-lookup"><span data-stu-id="bcd61-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="bcd61-104">Lokalizacja Hello planu hello jest używany tę samą lokalizację dla grupy zasobów hello hello.</span><span class="sxs-lookup"><span data-stu-id="bcd61-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="bcd61-105">Witaj cenową rozmiar warstwy i proces roboczy są określone w hello **sku** i **workerSize** parametrów</span><span class="sxs-lookup"><span data-stu-id="bcd61-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

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

