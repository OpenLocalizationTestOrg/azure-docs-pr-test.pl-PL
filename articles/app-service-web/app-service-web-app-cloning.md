---
title: "aaaWeb aplikacji klonowania przy użyciu programu PowerShell"
description: "Dowiedz się, jak tooclone aplikacje sieci Web toonew aplikacji sieci Web przy użyciu programu PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>Usługa aplikacji Azure aplikacji klonowania przy użyciu programu PowerShell
Hello wersji programu Microsoft Azure PowerShell z wersji 1.1.0 nową opcję został dodany AzureRMWebApp tooNew, która pozwoli uzyskać hello użytkownika hello możliwości tooclone istniejącej aplikacji tooa nowo utworzona aplikacja sieci Web w innym regionie lub hello tego samego regionu. Spowoduje to włączenie toodeploy klientów liczba aplikacji w różnych regionach, szybkie i łatwe.

Klonowanie aplikacji jest obecnie obsługiwany tylko w przypadku planów usługi aplikacji warstwy premium. Hello nowej używa funkcji hello takie same ograniczenia co funkcja kopii zapasowej aplikacji sieci Web, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn dotyczące korzystania z usługi Azure Resource Manager toomanage poleceń cmdlet programu PowerShell systemu Azure na podstawie wyboru Twojej aplikacji sieci Web [usługi Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>Klonowanie istniejącej aplikacji
Scenariusz: Istniejącej aplikacji sieci web w regionie południowo-środkowe stany, hello użytkownika ma zostać tooclone hello zawartość tooa nowej aplikacji sieci web w regionie północno-środkowe Stany. Można to zrobić przy użyciu wersji usługi Azure Resource Manager hello toocreate polecenia cmdlet programu PowerShell hello nowej aplikacji sieci web z opcją - SourceWebApp hello.

Znajomość hello zasobów nazwy grupy, która zawiera hello źródłowej aplikacji sieci web, możemy użyć hello następujące informacje o aplikacji programu PowerShell polecenie tooget hello źródła sieci web (w tym przypadku o nazwie aplikacji sieci Web źródła):

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

toocreate planu usługi aplikacji, możemy użyć polecenia New-AzureRmAppServicePlan jak hello poniższy przykład

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

Za pomocą polecenia hello AzureRmWebApp nowy, możemy Utwórz nową aplikację sieci web hello w hello północno-środkowe Stany i powiązanie jej tooan istniejące warstwy premium planu usługi App Service, Ponadto możemy użyć hello zasobów w tej samej grupy jako hello źródłowej aplikacji sieci web lub zdefiniuj nową grupę zasobów , następujące hello wykaże, że:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

tooclone istniejącą aplikację sieci web w tym wszystkich miejsc wdrożenia skojarzony, hello użytkownik będzie musiał toouse hello parametru IncludeSourceWebAppSlots, hello następującego polecenia programu PowerShell pokazuje hello Użyj tego parametru z hello polecenia New-AzureRmWebApp:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

tooclone istniejącą aplikację sieci web w obrębie hello tego samego regionu hello użytkownik będzie musiał toocreate plan w hello nową grupę zasobów i nowej usługi aplikacji tego samego regionu, a następnie za pomocą hello następujących aplikacji sieci web hello tooclone polecenia programu PowerShell

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Klonowanie tooan aplikacji istniejącego środowiska usługi aplikacji
Scenariusz: Istniejącej aplikacji sieci web w regionie południowo-środkowe stany, hello użytkownika ma zostać tooclone hello zawartość tooa nowej sieci web aplikacji tooan istniejącego środowiska usługi aplikacji (ASE).

Znajomość hello zasobów nazwy grupy, która zawiera hello źródłowej aplikacji sieci web, możemy użyć hello następujące informacje o aplikacji programu PowerShell polecenie tooget hello źródła sieci web (w tym przypadku o nazwie aplikacji sieci Web źródła):

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

Wiedzy o nazwie hello ASE oraz nazwa grupy zasobów hello hello ASE należącą do, hello użytkownik może użyć polecenia hello nowy AzureRmWebApp toocreate hello nowej aplikacji sieci web w hello istniejących ASE powitania po wykaże, że:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

Parametr lokalizacja Hello jest wymagany powodu Przyczyna toolegacy, ale w przypadku tworzenia aplikacji w elemencie ASE hello zostaną zignorowane. 

## <a name="cloning-an-existing-app-slot"></a>Klonowanie istniejącego miejsca aplikacji
Scenariusz: hello użytkownika ma zostać tooclone istniejących tooeither miejsca aplikacji sieci Web nowej aplikacji sieci Web lub nowe miejsce aplikacji sieci Web. Hello w hello nowej aplikacji sieci Web może być tym samym regionie jako hello oryginalnego miejsca aplikacji sieci Web lub w innym regionie.

Znajomość hello zasobów nazwy grupy, która zawiera hello źródłowej aplikacji sieci web, możemy użyć następującego polecenia programu PowerShell informacji tooget hello źródła miejsca aplikacji sieci web firmy (w tym przypadku o nazwie webappslot źródła) powiązane tooWeb aplikacji źródła-aplikacji sieci Web hello:

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

Hello poniżej przedstawiono utworzenie klona hello źródła sieci web aplikacji tooa nowej aplikacji sieci web:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>Konfigurowanie usługi Traffic Manager podczas klonowania aplikacji
Tworzenie aplikacji sieci web w przypadku i konfigurowanie usługi Azure Traffic Manager tooroute ruchu tooall tych aplikacji sieci web, jest tooinsure n ważne, będące aplikacji klientów wysokiej dostępności w przypadku klonowania istniejącej aplikacji sieci web, do których masz hello tooconnect opcji zarówno w sieci web aplikacje tooeither nowego profilu Menedżera ruchu lub istniejącego — Pamiętaj, że tylko wersja usługi Azure Resource Manager z Menedżera ruchu jest obsługiwana.

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>Tworzenie nowego profilu Menedżera ruchu podczas klonowania aplikacji
Scenariusz: hello użytkownika ma zostać tooclone tooanother region aplikacji sieci web podczas konfigurowania profilu Menedżera ruchu usługi Azure Resource Manager, który obejmuje zarówno aplikacji sieci web. Hello poniżej przedstawiono tworzenie Sklonowanie hello źródła sieci web aplikacji tooa nowej aplikacji sieci web podczas konfigurowania profilu Menedżera ruchu:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a>Dodawanie nowych sklonowany aplikacji sieci Web tooan istniejącego profilu Menedżera ruchu
Scenariusz: hello użytkownik ma już profil Menedżera ruchu usługi Azure Resource Manager czy chciałby tooadd zarówno w sieci web aplikacji jako punktów końcowych. toodo tak, najpierw musimy tooassemble hello istniejący identyfikator profilu Menedżera ruchu, potrzebujemy hello identyfikator subskrypcji, nazwa grupy zasobów i nazwa profilu Menedżera ruchu hello istniejących.

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

Po identyfikatorze Menedżera ruchu hello, hello poniżej przedstawiono tworzenia klonu hello źródła sieci web aplikacji tooa nowej aplikacji sieci web podczas dodawania ich tooan istniejącego profilu Menedżera ruchu:

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>Bieżące ograniczenia
Ta funkcja jest obecnie w wersji zapoznawczej, pracujemy nad tooadd nowe funkcje w czasie, następujące listy hello są hello znane ograniczenia dotyczące hello bieżącej wersji w klonowania aplikacji:

* Ustawienia skalowania automatycznego nie są klonowane.
* Ustawienia harmonogramu tworzenia kopii zapasowej nie są klonowane.
* Ustawienia sieci Wirtualnej nie są klonowane.
* Wgląd w aplikację nie są automatycznie skonfigurowane w aplikacji sieci web docelowym hello
* Łatwe ustawienia uwierzytelniania nie są klonowane.
* Program kudu rozszerzenia nie są klonowane.
* Porada reguły nie są klonowane.
* Baza danych zawartości nie są klonowane.

### <a name="references"></a>Dokumentacja
* [Usługa Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Klonowanie aplikacji sieci Web przy użyciu portalu Azure](app-service-web-app-cloning-portal.md)
* [Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md)
* [Usługa Azure Resource Manager obsługę Azure Traffic Manager w wersji zapoznawczej](../traffic-manager/traffic-manager-powershell-arm.md)
* [Wprowadzenie tooApp środowiska usługi](app-service-app-service-environment-intro.md)
* [Używanie programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md)

