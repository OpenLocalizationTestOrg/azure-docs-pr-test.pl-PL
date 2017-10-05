---
title: "Program Azure PowerShell Menedżera zasobów na podstawie polecenia dla aplikacji sieci Web platformy Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie użycia nowych poleceń na podstawie Menedżera zasobów Azure PowerShell do zarządzania aplikacjami sieci Web platformy Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a>Przy użyciu zasobów platformy Azure na podstawie menedżera programu PowerShell do zarządzania aplikacjami sieci Web platformy Azure
> [!div class="op_single_selector"]
> * [Interfejs wiersza polecenia platformy Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Przy użyciu programu Microsoft Azure PowerShell w wersji 1.0.0 zostały dodane nowe polecenia, który dać użytkownikowi możliwość używania poleceń programu PowerShell z systemem Azure Resource Manager do zarządzania aplikacjami sieci Web.

Aby dowiedzieć się więcej o zarządzaniu grupami zasobów, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md). 

Aby zapoznać się z pełną listą parametrów i opcje dla polecenia cmdlet programu PowerShell, zobacz [pełne odwołania do polecenia Cmdlet oparte na sieci Web aplikacji usługi Azure Resource Manager poleceń cmdlet programu PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Plany zarządzania z usługi aplikacji
### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi aplikacji
Aby utworzyć plan usługi aplikacji, użyj **AzureRmAppServicePlan nowy** polecenia cmdlet.

Poniżej przedstawiono opisy różnych parametrów:

* **Nazwa**: Nazwa planu usługi aplikacji.
* **Lokalizacja**: usługa lokalizacji planu.
* **ResourceGroupName**: grupy zasobów, która zawiera plan usługi aplikacji nowo utworzony.
* **Warstwa**: żądanej warstwy cenowej (domyślna to bezpłatna, inne opcje są współużytkowane, podstawowa, standardowa i Premium).
* **WorkerSize**: rozmiar pracowników (wartość domyślna to mały, jeśli określono parametr warstwy jako podstawowa, standardowa lub Premium. Inne opcje są średni i duży).
* **NumberofWorkers**: liczba pracowników w aplikacji usługi plan (wartość domyślna to 1). 

Przykład można używać tego polecenia cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Tworzenie planu usługi aplikacji w środowisku usługi aplikacji
Aby utworzyć plan usługi aplikacji w środowisku usługi aplikacji, użyj tego samego polecenia **AzureRmAppServicePlan nowy** z dodatkowe parametry, aby określić nazwę ASE i nazwa grupy zasobów w ASE.

Przykład można używać tego polecenia cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

Aby dowiedzieć się więcej na temat środowiska usługi aplikacji, sprawdź [wprowadzenie do środowiska usługi aplikacji](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Lista istniejących planów usługi aplikacji
Aby wyświetlić listę istniejących planów usługi aplikacji, należy użyć **Get-AzureRmAppServicePlan** polecenia cmdlet.

Aby wyświetlić listę wszystkich planów usługi aplikacji w ramach Twojej subskrypcji, należy użyć: 

    Get-AzureRmAppServicePlan

Aby wyświetlić listę wszystkich planów usługi aplikacji w obszarze określonej grupy zasobów, należy użyć:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

Aby uzyskać plan usługi specyficzne dla aplikacji, należy użyć:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Skonfiguruj istniejący Plan usługi App Service
Aby zmienić ustawienia dla istniejącego planu usługi aplikacji, należy użyć **AzureRmAppServicePlan zestaw** polecenia cmdlet. Możesz zmienić warstwę, rozmiar procesu roboczego oraz liczbę procesów roboczych 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Skalowanie planu usługi aplikacji
Aby skalować istniejący Plan usługi App Service, należy użyć:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a>Zmiana rozmiaru procesu roboczego planu usługi App Service
Aby zmienić rozmiar pracowników w istniejący Plan usługi App Service, należy użyć:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a>Zmiana warstwy Plan usługi aplikacji
Aby zmienić warstwę z istniejącego planu usługi App Service, należy użyć:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Usuń istniejący Plan usługi App Service
Aby usunąć istniejący plan usługi aplikacji, wszystkie aplikacje sieci web przypisanej należy przenieść lub usunięciem. Następnie przy użyciu **AzureRmAppServicePlan Usuń** polecenia cmdlet można usunąć planu usługi aplikacji.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>Zarządzanie aplikacjami sieci Web usługi aplikacji
### <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web
Aby utworzyć aplikację sieci web, użyj **AzureRmWebApp nowy** polecenia cmdlet.

Poniżej przedstawiono opisy różnych parametrów:

* **Nazwa**: Nazwa aplikacji sieci web.
* **AppServicePlan**: Nazwa planu usługi używany do obsługi aplikacji sieci web.
* **ResourceGroupName**: grupę zasobów, która obsługuje plan usługi aplikacji.
* **Lokalizacja**: Lokalizacja aplikacji sieci web.

Przykład można używać tego polecenia cmdlet:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Tworzenie aplikacji sieci Web w środowisku usługi aplikacji
Aby utworzyć aplikację sieci web w środowisku aplikacji (ASE). Używać tego samego **AzureRmWebApp nowy** polecenie z dodatkowych parametrów, aby określić nazwę ASE i grupy zasobów nazw, które ASE należy.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

Aby dowiedzieć się więcej na temat środowiska usługi aplikacji, sprawdź [wprowadzenie do środowiska usługi aplikacji](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Usuń istniejącą aplikację sieci Web
Aby usunąć istniejącą aplikację sieci web można użyć **AzureRmWebApp Usuń** polecenia cmdlet, należy określić nazwę aplikacji sieci web i nazwa grupy zasobów.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Listy istniejących aplikacji sieci Web
Aby wyświetlić listę istniejących aplikacji sieci web, należy użyć **Get-AzureRmWebApp** polecenia cmdlet.

Aby wyświetlić listę wszystkich aplikacji sieci web w ramach Twojej subskrypcji, należy użyć:

    Get-AzureRmWebApp

Aby wyświetlić listę wszystkich aplikacji sieci web w obszarze określonej grupy zasobów, należy użyć:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

Aby uzyskać aplikację sieci web określonych, należy użyć:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Konfigurowanie istniejącej aplikacji sieci Web
Aby zmienić ustawienia i konfiguracje dla istniejącej aplikacji sieci web, użyj **AzureRmWebApp zestaw** polecenia cmdlet. Aby uzyskać pełną listę parametrów, sprawdź [polecenia Cmdlet opis łącza](https://msdn.microsoft.com/library/mt652487.aspx)

Przykład (1): Użyj tego polecenia cmdlet, aby zmienić parametry połączenia

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

Przykład (2): Dodawanie lub zmienianie ustawień aplikacji

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


Przykład (3): Ustaw aplikacji sieci web do uruchamiania w trybie 64-bitowym

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a>Zmień stan istniejącej aplikacji sieci Web
#### <a name="restart-a-web-app"></a>Ponowne uruchomienie aplikacji sieci web
Aby ponownie uruchomić aplikacji sieci web, należy określić nazwę i zasobów Grupa aplikacji sieci web.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Zatrzymać aplikacji sieci web
Aby zatrzymać aplikacji sieci web, należy określić nazwę i zasobów Grupa aplikacji sieci web.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Uruchamiają aplikację sieci web
Aby uruchomić aplikację sieci web, należy określić nazwę i zasobów Grupa aplikacji sieci web.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Zarządzanie profilami publikowania aplikacji sieci Web
Każda aplikacja sieci web ma profil publikowania, który może być używana do publikowania aplikacji, można wykonać kilka czynności dla profilów publikowania.

#### <a name="get-publishing-profile"></a>Pobierz publikowania profilu
Aby pobrać profilu publikowania dla aplikacji sieci web, należy użyć:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

To polecenie zwraca profilu publikowania do wiersza polecenia, jak również wyjściowych profilu publikowania do pliku tekstowego.

#### <a name="reset-publishing-profile"></a>Resetowanie profilu publikowania
Aby zresetować zarówno publikowania hasło dla sieci web i FTP wdrażania dla aplikacji sieci web, użyj:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Zarządzanie certyfikatami aplikacji sieci Web
Aby dowiedzieć się więcej o zarządzaniu certyfikatów aplikacji sieci web, zobacz [powiązania certyfikatów SSL przy użyciu programu PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się więcej o obsłudze programu PowerShell usługi Azure Resource Manager, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager.](../powershell-azure-resource-manager.md)
* Aby dowiedzieć się więcej na temat środowiska usługi App Service, zobacz [wprowadzenie do środowiska usługi aplikacji.](app-service-app-service-environment-intro.md)
* Aby dowiedzieć się więcej o zarządzaniu certyfikatami SSL usługi aplikacji przy użyciu programu PowerShell, zobacz [powiązania certyfikatów SSL przy użyciu programu PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* Aby zapoznać się z pełną listą poleceń cmdlet programu PowerShell usługi Azure Resource Manager na podstawie dla aplikacji sieci Web platformy Azure, zobacz [referencyjnej poleceń Cmdlet Azure poleceń cmdlet programu PowerShell Menedżera zasobów Azure aplikacje sieci Web.](https://msdn.microsoft.com/library/mt619237.aspx)
* * Aby dowiedzieć się więcej o zarządzaniu App Service przy użyciu interfejsu wiersza polecenia, zobacz [wiersza polecenia XPlat Using Azure Resource Manager-Based dla aplikacji sieci Web platformy Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)

