---
title: "aaaAzure narzędzi wiersza polecenia Menedżera zasobów na podstawie między platformami dla aplikacji sieci Web platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello nowe toomanage opartej na usłudze Azure Resource Manager narzędzi wiersza polecenia i platform aplikacji sieci Web platformy Azure."
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
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Przy użyciu wiersza polecenia XPlat na podstawie Menedżera zasobów Azure dla usługi aplikacji Azure
> [!div class="op_single_selector"]
> * [Interfejs wiersza polecenia platformy Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

Hello wydanej wersji narzędzi wiersza polecenia usługi Microsoft Azure i platform 0.10.5 zostały dodane nowe polecenia. Te polecenia nadaj hello użytkownika hello możliwości toouse PowerShell usługi Azure Resource Manager na podstawie polecenia toomanage usługi aplikacji.

toolearn o zarządzaniu grupami zasobów, zobacz [Użyj toomanage interfejsu wiersza polecenia Azure hello Azure zasobów i grup zasobów](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> Ponadto wypróbowanie [Azure CLI 2.0](https://github.com/Azure/azure-cli), napisany w języku Python dla modelu wdrażania zarządzania zasobów hello infrastruktury CLI nowej generacji.
>
>

## <a name="managing-app-service-plans"></a>Plany zarządzania z usługi aplikacji
### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi aplikacji
toocreate plan usługi aplikacji, użyj hello **utworzyć azure appserviceplan** polecenia.

Poniżej przedstawiono opisy różnych parametrów hello:

* **--grupy zasobów**: grupy zasobów, która zawiera plan usługi aplikacji hello nowo utworzona.
* **--name**: Nazwa planu usługi aplikacji hello.
* **--lokalizacji**: Lokalizacja planu usługi aplikacji.
* **Jednostka sku —**: hello potrzeby cenową jednostki sku (Opcje hello są: F1 (bezpłatnie). D1 (wspólna). B1 (podstawowe mała liczba godzin), B2 (podstawowa średnia liczba godzin) i B3 (Basic duże). S1 (standardowa mała liczba godzin), S2 (standardowa średnia liczba godzin) i S3 (Standard duże). P1 (mały Premium), P2 (średnia Premium), a P3 (duże Premium).)
* **--wystąpień**: hello liczbę procesów roboczych w planie usługi aplikacji hello (wartość domyślna to 1).

Przykład toouse tego polecenia cmdlet:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Tworzenie planu usługi aplikacji w systemie Linux

Przy użyciu hello sam **utworzyć azure appserviceplan** polecenia z hello dodatkowy parametr **true islinux —**. Zanotuj hello ograniczenia i regiony opisane w [tooApp wprowadzenie usługi w systemie Linux](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Lista istniejących planów usługi aplikacji
toolist hello istniejących planów usługi aplikacji, użyj **listy azure appserviceplan** polecenia.

toolist wszystkich planów usługi aplikacji w obszarze określonej grupy zasobów, należy użyć:

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

Użyj tooget planu usługi aplikacji określonych **Pokaż azure appserviceplan** polecenia:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Skonfiguruj istniejący Plan usługi App Service
toochange hello ustawień dla istniejącego planu usługi aplikacji, użyj hello **azure appserviceplan config** polecenia. Możesz zmienić hello jednostki sku i hello liczbę procesów roboczych 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Skalowanie planu usługi aplikacji
Użyj istniejącego planu usługi App Service, tooscale:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a>Zmiana hello jednostki SKU planu usługi App Service
numer hello toochange istniejący Plan usługi App Service, użyj:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Usuń istniejący Plan usługi App Service
toodelete istniejący plan usługi aplikacji, wszystkie przypisane aplikacje muszą toobe przeniesiono lub usunięto najpierw. Przy użyciu hello **usunąć aplikacji sieci Web azure** polecenia, można usunąć planu usługi aplikacji hello.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>Zarządzanie aplikacjami usługi App Service
### <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web
toocreate aplikacji sieci web, użyj hello **tworzenie aplikacji sieci Web azure** polecenia.

Poniżej przedstawiono opisy różnych parametrów hello:

* **--name**: Nazwa aplikacji sieci web hello.
* **--planu**: nazwa dla hello planu usługi aplikacji sieci web hello toohost.
* **--grupy zasobów**: grupy zasobów, który jest hostem plan usługi aplikacji hello.
* **--lokalizacji**: hello lokalizacji aplikacji sieci web.

Przykład toouse tego polecenia cmdlet:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Usuń istniejącą aplikację
toodelete istniejącej aplikacji, można użyć hello **usunąć aplikacji sieci Web azure** polecenia. Należy toospecify hello nazwę aplikacji hello oraz nazwę grupy zasobów hello.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Listy istniejących aplikacji
toolist hello istniejących aplikacji, użyj hello **listy aplikacji sieci Web azure** polecenia.

toolist wszystkie aplikacje w określonej grupy zasobów, należy użyć:

    azure webapp list --resource-group ContosoAzureResourceGroup

tooget określonej aplikacji, użyj hello **Pokaż aplikacji sieci Web azure** polecenia.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Konfigurowanie istniejącej aplikacji
toochange hello ustawienia i konfiguracje dla istniejącej aplikacji, użyj hello **aplikacji sieci Web azure config set** polecenia.

Przykład (1): Zmień wersję php hello aplikacji 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

Przykład (2): Dodawanie lub zmienianie ustawień aplikacji

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

tooknow, jakie inne konfigurację można zmienić, użyj hello **konfiguracji aplikacji sieci Web azure wartości -h** polecenia.

### <a name="change-hello-state-of-an-existing-app"></a>Zmiana stanu hello istniejącej aplikacji
#### <a name="restart-an-app"></a>Uruchom ponownie aplikację
toorestart usługi aplikacji, należy określić nazwę i zasobów grupę hello aplikacji hello.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Zatrzymaj aplikację
toostop usługi aplikacji, należy określić nazwę i zasobów grupę hello aplikacji hello.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Uruchamiają aplikację
toostart usługi aplikacji, należy określić nazwę i zasobów grupę hello aplikacji hello.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Zarządzanie profilami publikowania aplikacji
Każda aplikacja ma profil publikowania, które mogą być używane toopublish kodu.

#### <a name="get-publishing-profile"></a>Pobierz publikowania profilu
Publikowanie aplikacji, Użyj profilu hello tooget:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

To polecenie zwraca hello publikowania profilu użytkownika i hasło toohello wiersza polecenia.

### <a name="manage-app-hostnames"></a>Zarządzanie nazwy hostów aplikacji
toomanage powiązań z nazwami hostów dla aplikacji, użyj hello **hostnames konfiguracji aplikacji sieci Web azure** polecenia  

#### <a name="list-hostname-bindings"></a>Lista powiązań z nazwami hostów
tooget hello bieżącego powiązań z nazwami hostów dla aplikacji, należy użyć:

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Dodawanie powiązań z nazwami hostów
tooadd hostname powiązania tooan aplikacji, użyj:

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Usuń powiązań z nazwami hostów
toodelete powiązań z nazwami hostów, należy użyć:

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Następne kroki
* toolearn dotyczące obsługi interfejsu wiersza polecenia Menedżera zasobów Azure, zobacz [Użyj toomanage interfejsu wiersza polecenia Azure hello Azure zasobów i grup zasobów.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* toolearn o zarządzaniu App Service przy użyciu programu PowerShell, zobacz [tooManage Using Azure Resource Manager-Based programu PowerShell Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)
* toolearn o usłudze Azure App Service w systemie Linux, zobacz [tooApp wprowadzenie usługi w systemie Linux](app-service-linux-intro.md)
