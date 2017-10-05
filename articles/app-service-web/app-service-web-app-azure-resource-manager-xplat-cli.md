---
title: "Aplikacja sieci Web narzędzia Azure wiersza polecenia i platform opartych na Menedżera zasobów Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak użycie nowych narzędzi wiersza polecenia na podstawie usługi Azure Resource Manager i platform do zarządzania aplikacjami sieci Web platformy Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Przy użyciu wiersza polecenia XPlat na podstawie Menedżera zasobów Azure dla usługi aplikacji Azure
> [!div class="op_single_selector"]
> * [Interfejs wiersza polecenia platformy Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

Wraz z wydaniem wersji narzędzi wiersza polecenia usługi Microsoft Azure i platform 0.10.5 zostały dodane nowe polecenia. Tych poleceń przyznać użytkownikowi możliwość używania poleceń programu PowerShell z systemem Azure Resource Manager do zarządzania z usługi aplikacji.

Aby dowiedzieć się więcej o zarządzaniu grupami zasobów, zobacz [użyć wiersza polecenia platformy Azure do zarządzania zasobami Azure i grup zasobów](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> Ponadto wypróbowanie [Azure CLI 2.0](https://github.com/Azure/azure-cli), napisanych w języku Python dla zarządzania model wdrażania zasobów nowej generacji infrastruktury CLI.
>
>

## <a name="managing-app-service-plans"></a>Plany zarządzania z usługi aplikacji
### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi aplikacji
Aby utworzyć plan usługi aplikacji, użyj **utworzyć azure appserviceplan** polecenia.

Poniżej przedstawiono opisy różnych parametrów:

* **--grupy zasobów**: grupy zasobów, która zawiera plan usługi aplikacji nowo utworzony.
* **--name**: Nazwa planu usługi aplikacji.
* **--lokalizacji**: Lokalizacja planu usługi aplikacji.
* **Jednostka sku —**: żądany cenową jednostki sku (dostępne są następujące opcje: F1 (bezpłatnie). D1 (wspólna). B1 (podstawowe mała liczba godzin), B2 (podstawowa średnia liczba godzin) i B3 (Basic duże). S1 (standardowa mała liczba godzin), S2 (standardowa średnia liczba godzin) i S3 (Standard duże). P1 (mały Premium), P2 (średnia Premium), a P3 (duże Premium).)
* **--wystąpień**: liczba pracowników w aplikacji usługi plan (wartość domyślna to 1).

Przykład można używać tego polecenia cmdlet:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Tworzenie planu usługi aplikacji w systemie Linux

Korzystającej z tego samego **utworzyć azure appserviceplan** polecenia z dodatkowym parametrem **true--islinux**. Należy pamiętać, ograniczenia i regiony opisane w temacie [wprowadzenie do usługi App Service w systemie Linux](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Lista istniejących planów usługi aplikacji
Aby wyświetlić listę istniejących planów usługi aplikacji, należy użyć **listy azure appserviceplan** polecenia.

Aby wyświetlić listę wszystkich planów usługi aplikacji w obszarze określonej grupy zasobów, należy użyć:

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

Aby uzyskać plan usługi specyficzne dla aplikacji, należy użyć **Pokaż azure appserviceplan** polecenia:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Skonfiguruj istniejący Plan usługi App Service
Aby zmienić ustawienia dla istniejącego planu usługi aplikacji, należy użyć **azure appserviceplan config** polecenia. Można zmienić jednostki sku i liczbę procesów roboczych 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Skalowanie planu usługi aplikacji
Aby skalować istniejący Plan usługi App Service, należy użyć:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a>Zmiana jednostki SKU planu usługi aplikacji
Aby zmienić numer istniejący Plan usługi App Service, należy użyć:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Usuń istniejący Plan usługi App Service
Aby usunąć istniejący plan usługi aplikacji, wszystkie aplikacje przypisanej muszą zostać przeniesiony lub usunięciem. Następnie przy użyciu **usunąć aplikacji sieci Web azure** polecenia, można usunąć planu usługi aplikacji.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>Zarządzanie aplikacjami usługi App Service
### <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web
Aby utworzyć aplikację sieci web, użyj **tworzenie aplikacji sieci Web azure** polecenia.

Poniżej przedstawiono opisy różnych parametrów:

* **--name**: Nazwa aplikacji sieci web.
* **--planu**: Nazwa planu usługi używany do obsługi aplikacji sieci web.
* **--grupy zasobów**: grupę zasobów, która obsługuje plan usługi aplikacji.
* **--lokalizacji**: Lokalizacja aplikacji sieci web.

Przykład można używać tego polecenia cmdlet:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Usuń istniejącą aplikację
Aby usunąć istniejącą aplikację, można użyć **usunąć aplikacji sieci Web azure** polecenia. Należy określić nazwę aplikacji i nazwę grupy zasobów.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Listy istniejących aplikacji
Aby wyświetlić listę istniejących aplikacji, należy użyć **listy aplikacji sieci Web azure** polecenia.

Aby wyświetlić listę wszystkich aplikacji w określonej grupy zasobów, należy użyć:

    azure webapp list --resource-group ContosoAzureResourceGroup

Aby uzyskać konkretną aplikację, należy użyć **Pokaż aplikacji sieci Web azure** polecenia.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Konfigurowanie istniejącej aplikacji
Aby zmienić ustawienia i konfiguracje dla istniejącej aplikacji, użyj **aplikacji sieci Web azure config set** polecenia.

Przykład (1): Zmień wersję php aplikacji 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

Przykład (2): Dodawanie lub zmienianie ustawień aplikacji

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

Wiedzieć, co inna konfiguracja może być zmieniona, użyj **konfiguracji aplikacji sieci Web azure wartości -h** polecenia.

### <a name="change-the-state-of-an-existing-app"></a>Zmień stan istniejącej aplikacji
#### <a name="restart-an-app"></a>Uruchom ponownie aplikację
Aby ponownie uruchomić aplikację, należy określić nazwę i zasobów grupy aplikacji.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Zatrzymaj aplikację
Aby zatrzymać aplikację, należy określić nazwę i zasobów grupy aplikacji.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Uruchamiają aplikację
Aby uruchomić aplikację, należy określić nazwę i zasobów grupy aplikacji.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Zarządzanie profilami publikowania aplikacji
Każda aplikacja ma profil publikowania, który może być używana do publikowania kodu.

#### <a name="get-publishing-profile"></a>Pobierz publikowania profilu
Aby pobrać profilu publikowania aplikacji, należy użyć:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

To polecenie zwraca publikowania profilu nazwy użytkownika i hasło w wierszu polecenia.

### <a name="manage-app-hostnames"></a>Zarządzanie nazwy hostów aplikacji
Aby zarządzać powiązań z nazwami hostów dla aplikacji, należy użyć **hostnames konfiguracji aplikacji sieci Web azure** polecenia  

#### <a name="list-hostname-bindings"></a>Lista powiązań z nazwami hostów
Aby uzyskać bieżące powiązań z nazwami hostów, dla aplikacji, należy użyć:

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Dodawanie powiązań z nazwami hostów
Aby dodać powiązań z nazwami hostów do aplikacji, należy użyć:

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Usuń powiązań z nazwami hostów
Aby usunąć powiązań z nazwami hostów, należy użyć:

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się więcej na temat obsługi interfejsu wiersza polecenia Menedżera zasobów Azure, zobacz [użyć wiersza polecenia platformy Azure do zarządzania zasobami Azure i grup zasobów.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* Aby dowiedzieć się więcej o zarządzaniu App Service przy użyciu programu PowerShell, zobacz [Using Azure Resource Manager-Based PowerShell do zarządzania aplikacji sieci Web platformy Azure.](app-service-web-app-azure-resource-manager-powershell.md)
* Aby dowiedzieć się więcej o usłudze Azure App Service w systemie Linux, zobacz [wprowadzenie do usługi App Service w systemie Linux](app-service-linux-intro.md)
