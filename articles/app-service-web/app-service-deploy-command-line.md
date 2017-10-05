---
title: "Automatyzację wdrażania aplikacji Azure za pomocą narzędzia wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Odnajdywanie informacji na temat wdrażania aplikacji Azure z poziomu wiersza polecenia"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 8b65980c-eb75-44a2-8e0f-f9eb9e617d16
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: e0e2e65557911bcac06d4dc355f47e9331934f8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Automatyzację wdrażania aplikacji Azure za pomocą narzędzia wiersza polecenia
Można zautomatyzować wdrożenie aplikacjami platformy Azure za pomocą narzędzia wiersza polecenia. W tym artykule wymieniono dostępne narzędzia i przydatne linki, które opisano, jak używać ich w przepływie pracy wdrażania. 

## <a name="msbuild"></a>Automatyzowanie wdrożenia przy użyciu programu MSBuild
Jeśli używasz [programu Visual Studio IDE](#vs) do tworzenia aplikacji, można użyć [MSBuild](http://msbuildbook.com/) można zautomatyzować niczego w środowiskiem IDE. Można skonfigurować program MSBuild użyć [narzędzia Web Deploy](#webdeploy) lub [FTP/FTPS](#ftp) do kopiowania plików. Narzędzie Web Deploy można również zautomatyzować wiele innych dotyczący wdrażania zadań, takich jak wdrażanie baz danych.

Aby uzyskać więcej informacji o wdrażaniu wiersza polecenia przy użyciu programu MSBuild zobacz następujące zasoby:

* [Wdrażanie sieci Web ASP.NET przy użyciu programu Visual Studio: wdrożenia z wiersza polecenia](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). Dziesiątego serii samouczków dotyczących wdrażania na platformie Azure przy użyciu programu Visual Studio. Pokazuje, jak wdrożyć po Konfigurowanie profilów publikowania w programie Visual Studio przy użyciu wiersza polecenia.
* [W programie Microsoft Build Engine: przy użyciu programu MSBuild i Team Foundation Build](http://msbuildbook.com/). Książki wydruku, która obejmuje rozdziałach dotyczące sposobu używania programu MSBuild dla wdrożenia.

## <a name="powershell"></a>Automatyzowanie wdrożenia przy użyciu programu Windows PowerShell
Można wykonać funkcji wdrażania programu MSBuild lub FTP z [programu Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx). Jeśli możesz to zrobić, można również użyć zbiór poleceń cmdlet programu Windows PowerShell, które ułatwiają wywołania interfejsu API zarządzania Azure REST.

Więcej informacji zawierają następujące zasoby:

* [Wdrażanie aplikacji sieci web, połączony z repozytorium GitHub](app-service-web-arm-from-github-provision.md)
* [Udostępniać aplikacji sieci web z bazą danych SQL](app-service-web-arm-with-sql-database-provision.md)
* [Aprowizacji i wdrażania mikrousług przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md)
* [Tworzenie aplikacji rzeczywistych chmury platformy Azure - zautomatyzować wszystko](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything). Książka elektroniczna rozdział, który objaśnia, jak pokazano w e-book przykładowej aplikacji używa skryptów Windows PowerShell do tworzenia środowiska testowego Azure i wdrażać do niego. Zobacz [zasobów](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) sekcji łącza do dodatkowej dokumentacji programu Azure PowerShell.
* [Za pomocą skryptów programu Windows PowerShell do opublikowania dla deweloperów i środowisk testowych](../vs-azure-tools-publishing-using-powershell-scripts.md). Jak używać programu Windows PowerShell wdrażania skryptów generuje Visual Studio.

## <a name="api"></a>Zautomatyzować wdrożenie z interfejsem API zarządzania platformy .NET
Można napisać kod C# do wykonywania funkcji programu MSBuild lub FTP dla wdrożenia. Można to zrobić, można uzyskać dostępu do zarządzania platformy Azure, interfejsu API REST w celu wykonywania funkcji zarządzania lokacji.

Aby uzyskać więcej informacji zobacz następujące zasoby:

* [Automatyzowanie wszystko z biblioteki zarządzania Azure i .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Wprowadzenie do interfejsu API zarządzania .NET i linki do dokumentacji więcej.

## <a name="cli"></a>Wdrażanie z Azure interfejsu wiersza polecenia (Azure CLI)
Do wdrożenia przy użyciu protokołu FTP, można użyć wiersza polecenia w komputerach z systemem Windows, Mac lub Linux. Można to zrobić, można także przejść management Azure REST interfejsu API przy użyciu wiersza polecenia platformy Azure.

Aby uzyskać więcej informacji zobacz następujące zasoby:

* [Narzędzia wiersza polecenia platformy Azure](https://azure.microsoft.com/downloads/). Portal strony w witrynie Azure.com informacje dotyczące narzędzia wiersza polecenia.

## <a name="webdeploy"></a>Wdrażanie z wiersza polecenia narzędzia Web Deploy
[Web Deploy](http://www.iis.net/downloads/microsoft/web-deploy) jest oprogramowania firmy Microsoft dla wdrożenia usług IIS, która nie tylko udostępnia synchronizacji plików inteligentnego funkcji, ale również wykonać lub koordynacji wielu innych dotyczący wdrażania zadań, które nie mogły zostać zautomatyzowane przy użyciu funkcji. Na przykład narzędzie Web Deploy można wdrożyć nową bazę danych lub aktualizacje bazy danych wraz z aplikacji sieci web. Narzędzie Web Deploy może również zminimalizować czas wymagany do zaktualizowania istniejącej witryny, ponieważ inteligentnie może kopiować tylko zmienione pliki. Microsoft Visual Studio i serwera Team Foundation Server jest obsługiwane dla narzędzia Web Deploy wbudowanych, ale umożliwia także narzędzia Web Deploy bezpośrednio z poziomu wiersza polecenia do automatyzowania wdrażania. Poleceń wdrażania w sieci Web są bardzo zaawansowane, ale mogą mieć problemy z ich opanowaniem.

## <a name="more-resources"></a>Więcej zasobów
Inną opcją wdrażania automatyzacji w wierszu polecenia jest używać jest usługą opartą na chmurze, takich jak [wdrażanie Ośmiornica](http://en.wikipedia.org/wiki/Octopus_Deploy). Aby uzyskać więcej informacji, zobacz [wdrażanie aplikacji programu ASP.NET do witryny sieci Web Azure](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Aby uzyskać więcej informacji dotyczących narzędzia wiersza polecenia zobacz następujące zasoby:

* [Aplikacji sieci Web prosty: Wdrażanie](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). Blog przez Dominika Ebbo o to narzędzie, które on zapisano ułatwiają użycie narzędzia Web Deploy.
* [Narzędzia wdrażania Web](http://technet.microsoft.com/library/dd568996). Oficjalna dokumentacja w witrynie Microsoft TechNet. Z, ale nadal dobrym miejscem do rozpoczęcia.
* [Wdrażanie przy użyciu sieci Web](http://www.iis.net/learn/publish/using-web-deploy). Oficjalna dokumentacja w witrynie Microsoft IIS.NET. Również z, ale dobrym miejscem do rozpoczęcia.
* [Wdrażanie sieci Web ASP.NET przy użyciu programu Visual Studio: wdrożenia z wiersza polecenia](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). MSBuild jest używany przez Visual Studio aparatu kompilacji i może również służyć z wiersza polecenia do wdrożenia aplikacji sieci web do aplikacji sieci Web. W tym samouczku jest częścią serii, która dotyczy głównie wdrożenie programu Visual Studio.

