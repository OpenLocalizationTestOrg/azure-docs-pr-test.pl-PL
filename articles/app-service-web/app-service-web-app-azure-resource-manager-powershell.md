---
title: "polecenia aaaAzure PowerShell oparte na Menedżera zasobów dla aplikacji sieci Web platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello nowe toomanage polecenia PowerShell usługi Azure Resource Manager na podstawie aplikacji sieci Web platformy Azure."
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
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>Przy użyciu programu PowerShell Azure Resource Manager-Based tooManage Azure Web Apps
> [!div class="op_single_selector"]
> * [Interfejs wiersza polecenia platformy Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Przy użyciu programu Microsoft Azure PowerShell w wersji 1.0.0 zostały dodane nowe polecenia, które powodują hello użytkownika hello możliwości toouse PowerShell usługi Azure Resource Manager na podstawie polecenia toomanage aplikacji sieci Web.

toolearn o zarządzaniu grupami zasobów, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md). 

toolearn o hello pełną listę parametrów i opcje dotyczące hello poleceń cmdlet programu PowerShell, zobacz hello [pełne odwołania do polecenia Cmdlet oparte na sieci Web aplikacji usługi Azure Resource Manager poleceń cmdlet programu PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Plany zarządzania z usługi aplikacji
### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi aplikacji
toocreate plan usługi aplikacji, użyj hello **AzureRmAppServicePlan nowy** polecenia cmdlet.

Poniżej przedstawiono opisy różnych parametrów hello:

* **Nazwa**: Nazwa planu usługi aplikacji hello.
* **Lokalizacja**: usługa lokalizacji planu.
* **ResourceGroupName**: grupy zasobów, która zawiera plan usługi aplikacji hello nowo utworzona.
* **Warstwa**: hello żądaną warstwę cenową (domyślna to bezpłatna, inne opcje są współużytkowane, podstawowa, standardowa i Premium).
* **WorkerSize**: hello rozmiar pracowników (wartość domyślna to mały, jeśli określono parametr warstwy hello jako podstawowa, standardowa lub Premium. Inne opcje są średni i duży).
* **NumberofWorkers**: hello liczbę procesów roboczych w planie usługi aplikacji hello (wartość domyślna to 1). 

Przykład toouse tego polecenia cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Tworzenie planu usługi aplikacji w środowisku usługi aplikacji
toocreate planie usługi aplikacji w środowisku usługi aplikacji, użyj hello same polecenie **AzureRmAppServicePlan nowy** polecenia o nazwie dodatkowe parametry toospecify hello w ASE i nazwa grupy zasobów w ASE.

Przykład toouse tego polecenia cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

więcej informacji na temat środowiska usługi aplikacji, sprawdź toolearn [tooApp wprowadzenie środowiska usługi](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Lista istniejących planów usługi aplikacji
toolist hello istniejących planów usługi aplikacji, użyj **Get-AzureRmAppServicePlan** polecenia cmdlet.

Użyj toolist wszystkich planów usługi aplikacji w ramach Twojej subskrypcji: 

    Get-AzureRmAppServicePlan

toolist wszystkich planów usługi aplikacji w obszarze określonej grupy zasobów, należy użyć:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

Użyj tooget planu usługi specyficzne dla aplikacji:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Skonfiguruj istniejący Plan usługi App Service
toochange hello ustawień dla istniejącego planu usługi aplikacji, użyj hello **AzureRmAppServicePlan zestaw** polecenia cmdlet. Można zmienić warstwy hello, rozmiar procesu roboczego i hello liczbę procesów roboczych 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Skalowanie planu usługi aplikacji
Użyj istniejącego planu usługi App Service, tooscale:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>Zmienianie rozmiaru procesu roboczego hello planu usługi App Service
rozmiar hello toochange pracowników w istniejący Plan usługi App Service, użyj:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>Zmiana hello warstwy planu usługi App Service
warstwy hello toochange istniejący Plan usługi App Service, użyj:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Usuń istniejący Plan usługi App Service
toodelete istniejący plan usługi aplikacji, wszystkie przypisane toobe przeniesiony lub usunięty, najpierw należy aplikacji sieci web. Przy użyciu hello **AzureRmAppServicePlan Usuń** polecenia cmdlet można usunąć planu usługi aplikacji hello.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>Zarządzanie aplikacjami sieci Web usługi aplikacji
### <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web
toocreate aplikacji sieci web, użyj hello **AzureRmWebApp nowy** polecenia cmdlet.

Poniżej przedstawiono opisy różnych parametrów hello:

* **Nazwa**: Nazwa aplikacji sieci web hello.
* **AppServicePlan**: nazwa dla hello planu usługi aplikacji sieci web hello toohost.
* **ResourceGroupName**: grupy zasobów, który jest hostem plan usługi aplikacji hello.
* **Lokalizacja**: hello lokalizacji aplikacji sieci web.

Przykład toouse tego polecenia cmdlet:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Tworzenie aplikacji sieci Web w środowisku usługi aplikacji
toocreate aplikacji sieci web w środowisku aplikacji (ASE). Użyj hello sam **AzureRmWebApp nowy** polecenia o nazwie hello ASE toospecify dodatkowe parametry i nazwa grupy zasobów hello hello ASE należącą do.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

więcej informacji na temat środowiska usługi aplikacji, sprawdź toolearn [tooApp wprowadzenie środowiska usługi](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Usuń istniejącą aplikację sieci Web
toodelete istniejącej aplikacji sieci web, można użyć hello **AzureRmWebApp Usuń** polecenia cmdlet, potrzebna nazwa hello toospecify hello aplikacji sieci web i nazwa grupy zasobów hello.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Listy istniejących aplikacji sieci Web
toolist hello istniejących aplikacji sieci web, użyj hello **Get-AzureRmWebApp** polecenia cmdlet.

Użyj toolist wszystkie aplikacje sieci web w ramach Twojej subskrypcji:

    Get-AzureRmWebApp

toolist wszystkie aplikacje sieci web w obszarze określonej grupy zasobów, należy użyć:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

Użyj aplikacji sieci web określonego tooget:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Konfigurowanie istniejącej aplikacji sieci Web
toochange hello ustawienia i konfiguracje dla istniejącej aplikacji sieci web, użyj hello **AzureRmWebApp zestaw** polecenia cmdlet. Aby uzyskać pełną listę parametrów, sprawdź hello [polecenia Cmdlet opis łącza](https://msdn.microsoft.com/library/mt652487.aspx)

Przykład (1): Użyj parametrów połączenia toochange tego polecenia cmdlet

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

Przykład (2): Dodawanie lub zmienianie ustawień aplikacji

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


Przykład (3): Ustaw toorun aplikacji sieci web hello w trybie 64-bitowym

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>Zmiana stanu hello istniejącej aplikacji sieci Web
#### <a name="restart-a-web-app"></a>Ponowne uruchomienie aplikacji sieci web
toorestart aplikacji sieci web, należy określić nazwę i zasobów grupę hello hello aplikacji sieci web.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Zatrzymać aplikacji sieci web
toostop aplikacji sieci web, należy określić nazwę i zasobów grupę hello hello aplikacji sieci web.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Uruchamiają aplikację sieci web
toostart aplikacji sieci web, należy określić nazwę i zasobów grupę hello hello aplikacji sieci web.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Zarządzanie profilami publikowania aplikacji sieci Web
Każda aplikacja sieci web ma profil publikowania, które mogą być używane toopublish aplikacji, można wykonać kilka czynności dla profilów publikowania.

#### <a name="get-publishing-profile"></a>Pobierz publikowania profilu
Publikowanie aplikacji sieci web, Użyj profilu hello tooget:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

To polecenie informujące, że hello również wiersza polecenia toohello profilu publikowania danych wyjściowych hello pliku tekstowego tooa profilu publikowania.

#### <a name="reset-publishing-profile"></a>Resetowanie profilu publikowania
tooreset zarówno hello publikowania hasło, dla sieci web i FTP, wdrożenia dla aplikacji sieci web, użyj:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Zarządzanie certyfikatami aplikacji sieci Web
Zobacz toolearn o jak certyfikatów aplikacji sieci web na toomanage [powiązania certyfikatów SSL przy użyciu programu PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Następne kroki
* toolearn o obsłudze programu PowerShell usługi Azure Resource Manager, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager.](../powershell-azure-resource-manager.md)
* toolearn o środowiska usługi App Service, zobacz [tooApp wprowadzenie środowiska usługi.](app-service-app-service-environment-intro.md)
* toolearn o zarządzaniu certyfikatami SSL usługi aplikacji przy użyciu programu PowerShell, zobacz [powiązania certyfikatów SSL przy użyciu programu PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* toolearn o hello pełną listę na podstawie usługi Azure Resource Manager poleceń cmdlet programu PowerShell dla aplikacji sieci Web platformy Azure, zobacz [referencyjnej poleceń Cmdlet Azure poleceń cmdlet programu PowerShell Menedżera zasobów Azure aplikacje sieci Web.](https://msdn.microsoft.com/library/mt619237.aspx)
* * toolearn o zarządzaniu App Service przy użyciu interfejsu wiersza polecenia, zobacz [wiersza polecenia XPlat Using Azure Resource Manager-Based dla aplikacji sieci Web platformy Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)

