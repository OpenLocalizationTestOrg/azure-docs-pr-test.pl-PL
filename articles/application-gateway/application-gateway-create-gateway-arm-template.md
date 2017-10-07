---
title: "aaaCreate bramę aplikacji Azure — szablony | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate bramę aplikacji platformy Azure przy użyciu szablonu usługi Azure Resource Manager hello"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a>Tworzenie za pomocą szablonu usługi Azure Resource Manager hello bramy aplikacji

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-gateway-arm.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-create-gateway.md)
> * [Szablon usługi Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interfejs wiersza polecenia platformy Azure](application-gateway-create-gateway-cli.md)

Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7. Udostępnia trybu failover i wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie. Usługa Application Gateway zapewnia wiele funkcji kontrolera dostarczania aplikacji (ADC, Application Delivery Controller), w tym między innymi równoważenie obciążenia HTTP, koligację sesji na podstawie plików cookie, odciążanie protokołu Secure Sockets Layer (SSL), niestandardowe sondy kondycji i obsługę wielu witryn. odwiedź toofind pełną listę obsługiwanych funkcji [omówienie bramy aplikacji](application-gateway-introduction.md)

W tym artykule przedstawiono sposób pobierania i modyfikacji istniejącego szablonu usługi Azure Resource Manager z usługi GitHub i wdrażanie hello szablonu z serwisu GitHub, programu PowerShell i hello wiersza polecenia platformy Azure.

Jeśli po prostu wdrażasz szablon usługi Azure Resource Manager hello bezpośrednio z serwisu GitHub, bez wprowadzania żadnych zmian, Pomiń toodeploy szablonu z serwisu GitHub.

## <a name="scenario"></a>Scenariusz

W ramach tego scenariusza wykonasz następujące czynności:

* Utwórz bramę aplikacji z zapory aplikacji sieci web.
* Tworzenie sieci wirtualnej o nazwie VirtualNetwork1 przy użyciu zarezerwowanego bloku CIDR 10.0.0.0/16.
* Tworzenie podsieci o nazwie Appgatewaysubnet używającej bloku 10.0.0.0/28 jako bloku CIDR.
* Konfigurowanie dwóch wcześniej skonfigurowane adresy IP zaplecza dla serwerów sieci web hello bilans tooload hello ruchu. W tym przykładzie szablon hello zaplecza adresy IP są 10.0.1.10 i 10.0.1.11.

> [!NOTE]
> Te ustawienia są hello parametrów dla tego szablonu. Szablon hello toocustomize, można zmienić zasady, hello odbiornika protokołu SSL i inne opcje w plik azuredeploy.json hello.

![Scenariusz](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Pobierz i zrozumieć hello szablonu usługi Azure Resource Manager

Możesz pobrać z witryny GitHub hello istniejącej usługi Azure Resource Manager szablonu toocreate sieci wirtualnej z dwoma podsieciami, zmiany mogą, a następnie użyć go ponownie. toodo tak, użycie hello następujące kroki:

1. Przejdź za[Utwórz bramę aplikacji włączona jest Zapora aplikacji sieci web](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).
1. Kliknij opcję **azuredeploy.json**, a następnie kliknij opcję **RAW**.
1. Zapisz hello pliku tooa lokalnego folderu na komputerze.
1. Jeśli znasz szablony Menedżera zasobów Azure, Pomiń toostep 7.
1. Otwórz zapisany plik hello i przyjrzyj się zawartości hello w obszarze **parametry** w wierszu
1. Parametry szablonu usługi Azure Resource Manager zawierają symbole zastępcze wartości, które można wypełnić podczas wdrażania.

  | Parametr | Opis |
  | --- | --- |
  | **subnetPrefix** |Blok CIDR podsieci bramy aplikacji hello. |
  | **applicationGatewaySize** | Rozmiar hello bramy aplikacji.  Zapory aplikacji sieci Web udostępnia tylko dla średnich i dużych. |
  | **backendIpaddress1** |Adres IP hello na pierwszym serwerze sieci web. |
  | **backendIpaddress2** |Adres IP hello drugi serwer sieci web. |
  | **wafEnabled** | Ustawienie toodetermine zapory aplikacji sieci Web jest włączona.|
  | **wafMode** | Tryb zapory aplikacji sieci web hello.  Dostępne są następujące opcje **zapobiegania** lub **wykrywania**.|
  | **wafRuleSetType** | Typ zestaw reguł zapory aplikacji sieci Web.  Obecnie OWASP jest hello obsługiwane tylko opcja. |
  | **wafRuleSetVersion** |Wersja zestaw reguł. CRS OWASP 2.2.9 i 3.0 są obecnie obsługiwane hello opcje. |

1. Sprawdź zawartość hello w obszarze **zasobów** i hello powiadomienia następujące właściwości:

   * **type**. Typ zasobu tworzonego przez szablon hello. W takim przypadku typ hello jest `Microsoft.Network/applicationGateways`, który reprezentuje bramę aplikacji.
   * **name**. Nazwa zasobu hello. Użycie hello powiadomienia `[parameters('applicationGatewayName')]`, co oznacza, że ta nazwa hello jest podana jako dane wejściowe przez Ciebie lub pliku parametrów podczas wdrażania.
   * **properties**. Lista właściwości zasobu hello. Ten szablon używa hello sieć wirtualna i publiczny adres IP podczas tworzenia bramy aplikacji.

   > [!NOTE]
   > Aby uzyskać więcej informacji na temat szablonów odwiedź: [dokumentacja szablonów usługi Resource Manager](/templates/)

1. Przejdź wstecz zbyt[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).
1. Kliknij przycisk **parameters.JSON następującym kodem azuredeploy**, a następnie kliknij przycisk **RAW**.
1. Zapisz hello pliku tooa lokalnego folderu na komputerze.
1. Otwórz zapisany plik hello i edytowania wartości hello hello parametrów. Użyj hello następujące wartości toodeploy hello brama aplikacji w opisanej w scenariuszu.

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. Zapisz plik hello. Należy przetestować hello JSON szablonu i parametr szablonu przy użyciu online narzędzia sprawdzania poprawności formatu JSON, takie jak [JSlint.com](http://www.jslint.com/).

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a>Wdrażanie szablonu usługi Azure Resource Manager hello przy użyciu programu PowerShell

Jeśli nie znasz programu Azure PowerShell, odwiedź stronę: [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i wykonaj toosign instrukcje hello na platformie Azure i wyboru subskrypcji.

1. TooPowerShell logowania

    ```powershell
    Login-AzureRmAccount
    ```

1. Sprawdź subskrypcje hello hello konta.

    ```powershell
    Get-AzureRmSubscription
    ```

    Jesteś zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.

1. Wybierz z toouse Twojej subskrypcji platformy Azure.

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. W razie potrzeby utwórz grupę zasobów za pomocą hello **New-AzureResourceGroup** polecenia cmdlet. Poniższy przykład hello służy do tworzenia grupy zasobów o nazwie AppgatewayRG w lokalizacji wschodnie stany USA.

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. Uruchom hello **AzureRmResourceGroupDeployment nowy** polecenia cmdlet toodeploy hello nową sieć wirtualną przy użyciu hello poprzedzających plików szablonu i parametr pobrane i modyfikować.
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a>Wdrażanie szablonu usługi Azure Resource Manager hello przy użyciu hello wiersza polecenia platformy Azure

toodeploy hello Azure Resource Manager szablon, który został pobrany przy użyciu wiersza polecenia platformy Azure, wykonaj hello następujące kroki:

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [zainstalować i skonfigurować hello Azure CLI](/cli/azure/install-azure-cli) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.

1. Jeśli to konieczne, uruchom hello `az group create` toocreate polecenia grupę zasobów, jak pokazano w hello następującego fragmentu kodu. Zwróć uwagę, hello dane wyjściowe polecenia hello. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane. Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (lub --name)**. Nazwa nowej grupy zasobów hello. W naszym scenariuszu jest to *appgatewayRG*.
    
    **-l (lub --location)**. Region platformy Azure, w której jest tworzony hello nową grupę zasobów. W naszym scenariuszu ma *westus*.

1. Uruchom hello `az group deployment create` polecenia cmdlet toodeploy hello nową sieć wirtualną przy użyciu szablonu hello i parametr pliki uprzednio pobranego i modyfikować w hello poprzedzających krok. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a>Wdrażanie szablonu usługi Azure Resource Manager hello przy użyciu kliknij wdrażania

Kliknij przycisk deploy jest inny sposób toouse szablonów usługi Azure Resource Manager. Jest łatwy sposób szablonów toouse hello portalu Azure.

1. Przejdź za[Utwórz bramę aplikacji z zapory aplikacji sieci web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).

1. Kliknij przycisk **wdrażanie tooAzure**.

    ![Wdrażanie tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Wypełnianie hello parametrów hello Szablon wdrożenia na powitania portalu, a następnie kliknij przycisk **OK**.

    ![Parametry](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. Wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano** i kliknij przycisk **zakupu**.

1. W bloku wdrożenia niestandardowe hello, kliknij polecenie **Utwórz**.

## <a name="providing-certificate-data-tooresource-manager-templates"></a>Udostępnia szablony Menedżera tooResource dane certyfikatu

Przy korzystaniu z protokołu SSL przy użyciu szablonu certyfikatu hello musi toobe dostarczone w parametrach base64, zamiast przekazywanego. ciąg base64 tooa pfx lub .cer tooconvert użyj jednej z hello następujące polecenia. Witaj następujące polecenia przekonwertować ciąg base64 tooa certyfikatu hello, który można podać toohello szablonu. Witaj oczekiwanych danych wyjściowych jest ciągiem, który może być przechowywana w zmiennej i wkleić w szablonie hello.

### <a name="macos"></a>macOS
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a>Windows
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a>Usuwanie wszystkich zasobów

toodelete wszystkie zasoby są tworzone w tym artykule pełną spośród hello następujące kroki:

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>Następne kroki

Jeśli chcesz tooconfigure odciążanie protokołu SSL można znaleźć: [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).

Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia, odwiedź stronę: [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).

Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć, odwiedzając:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

