---
title: "aaaAutomate wdrożenia aplikacji platformy Azure za pomocą narzędzia wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Odnajdywanie informacji na temat wdrażania aplikacji Azure z hello wiersza polecenia"
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
ms.openlocfilehash: 3df66cc4bf4e6819ed0eee7278ac79dca2e5daa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Automatyzację wdrażania aplikacji Azure za pomocą narzędzia wiersza polecenia
Można zautomatyzować wdrożenie aplikacjami platformy Azure za pomocą narzędzia wiersza polecenia. W tym artykule wymieniono dostępne narzędzia i hello przydatne linki, które opisano, jak toouse ich w przepływie pracy wdrażania. 

## <a name="msbuild"></a>Automatyzowanie wdrożenia przy użyciu programu MSBuild
Jeśli używasz hello [programu Visual Studio IDE](#vs) do tworzenia aplikacji, można użyć [MSBuild](http://msbuildbook.com/) tooautomate niczego w środowiskiem IDE. Można skonfigurować program MSBuild toouse albo [narzędzia Web Deploy](#webdeploy) lub [FTP/FTPS](#ftp) toocopy plików. Narzędzie Web Deploy można również zautomatyzować wiele innych dotyczący wdrażania zadań, takich jak wdrażanie baz danych.

Aby uzyskać więcej informacji o wdrażaniu wiersza polecenia przy użyciu programu MSBuild zobacz następujące zasoby hello:

* [Wdrażanie sieci Web ASP.NET przy użyciu programu Visual Studio: wdrożenia z wiersza polecenia](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). Dziesiątego serii samouczków dotyczących tooAzure wdrożenia przy użyciu programu Visual Studio. Pokazuje, jak toouse hello toodeploy wiersza polecenia po skonfigurowaniu profilów publikowania w programie Visual Studio.
* [Witaj wewnątrz aparatu kompilacji firmy Microsoft: przy użyciu programu MSBuild i Team Foundation Build](http://msbuildbook.com/). Książki wydruku, która obejmuje rozdziałach na temat toouse MSBuild dla wdrożenia.

## <a name="powershell"></a>Automatyzowanie wdrożenia przy użyciu programu Windows PowerShell
Można wykonać funkcji wdrażania programu MSBuild lub FTP z [programu Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx). Jeśli możesz to zrobić, można również użyć zbiór poleceń cmdlet programu Windows PowerShell, która toocall łatwe interfejsu API management Azure REST hello.

Aby uzyskać więcej informacji zobacz następujące zasoby hello:

* [Wdrażanie repozytorium GitHub tooa połączonych aplikacji sieci web](app-service-web-arm-from-github-provision.md)
* [Udostępniać aplikacji sieci web z bazą danych SQL](app-service-web-arm-with-sql-database-provision.md)
* [Aprowizacji i wdrażania mikrousług przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md)
* [Tworzenie aplikacji rzeczywistych chmury platformy Azure - zautomatyzować wszystko](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything). Rozdział E-book, który objaśnia, jak hello Przykładowa aplikacja hello e-book pokazano używa toocreate skryptów środowiska Windows PowerShell platformy Azure środowiska testowego i wdrażanie tooit. Zobacz hello [zasobów](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) sekcji tooadditional łącza dokumentacji programu Azure PowerShell.
* [Za pomocą skryptów programu Windows PowerShell tooPublish tooDev i środowisk testowych](../vs-azure-tools-publishing-using-powershell-scripts.md). Generuje jak toouse wdrażania środowiska Windows PowerShell skrypty tego programu Visual Studio.

## <a name="api"></a>Zautomatyzować wdrożenie z interfejsem API zarządzania platformy .NET
Można napisać kod w języku C# tooperform MSBuild lub FTP funkcje dla wdrożenia. Można to zrobić, można uzyskać dostępu do funkcji zarządzania lokacji tooperform interfejsu API REST hello zarządzania platformy Azure.

Aby uzyskać więcej informacji zobacz hello następujących zasobów:

* [Automatyzowanie wszystko z biblioteki zarządzania hello Azure i .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Wprowadzenie toohello .NET interfejsu API i linki toomore dokumentacja zarządzania.

## <a name="cli"></a>Wdrażanie z Azure interfejsu wiersza polecenia (Azure CLI)
Przy użyciu protokołu FTP, można użyć wiersza polecenia hello w toodeploy maszyny z systemem Windows, Mac lub Linux. Można to zrobić, można także przejść hello Azure zarządzania interfejsu API REST przy użyciu hello wiersza polecenia platformy Azure.

Aby uzyskać więcej informacji zobacz hello następujących zasobów:

* [Narzędzia wiersza polecenia platformy Azure](https://azure.microsoft.com/downloads/). Portal strony w witrynie Azure.com informacje dotyczące narzędzia wiersza polecenia.

## <a name="webdeploy"></a>Wdrażanie z wiersza polecenia narzędzia Web Deploy
[Web Deploy](http://www.iis.net/downloads/microsoft/web-deploy) jest oprogramowania firmy Microsoft dla tooIIS wdrożenia, które nie tylko udostępnia inteligentnego pliku funkcje synchronizacji, ale również wykonać lub koordynacji wielu innych dotyczący wdrażania zadań, które nie mogły zostać zautomatyzowane przy użyciu funkcji. Na przykład narzędzie Web Deploy można wdrożyć nową bazę danych lub aktualizacje bazy danych wraz z aplikacji sieci web. Narzędzie Web Deploy można również zminimalizować hello czas tooupdate istniejącej witryny, ponieważ inteligentnie może kopiować tylko zmienione pliki. Microsoft Visual Studio i serwera Team Foundation Server jest obsługiwane dla narzędzia Web Deploy wbudowanych, ale umożliwia również narzędzia Web Deploy bezpośrednio z hello wiersza polecenia tooautomate wdrożenia. Poleceń wdrażania w sieci Web są bardzo zaawansowane, ale hello może mieć problemy z ich opanowaniem.

## <a name="more-resources"></a>Więcej zasobów
Inny automatyzacji wiersza toocommand opcji wdrażania jest toouse oparte na chmurze usługi, takich jak [wdrażanie Ośmiornica](http://en.wikipedia.org/wiki/Octopus_Deploy). Aby uzyskać więcej informacji, zobacz [tooAzure aplikacji ASP.NET wdrażanie witryn sieci Web](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Aby uzyskać więcej informacji dotyczących narzędzia wiersza polecenia Zobacz hello następujących zasobów:

* [Aplikacji sieci Web prosty: Wdrażanie](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). Blog przez Dominika Ebbo o narzędziu on zapisano toomake go łatwiejsze toouse narzędzia Web Deploy.
* [Narzędzia wdrażania Web](http://technet.microsoft.com/library/dd568996). Oficjalna dokumentacja w witrynie Microsoft TechNet hello. Z, ale nadal toostart dobrym miejscem.
* [Wdrażanie przy użyciu sieci Web](http://www.iis.net/learn/publish/using-web-deploy). Oficjalna dokumentacja w witrynie Microsoft IIS.NET hello. Również z wyjątkiem toostart dobrym miejscem.
* [Wdrażanie sieci Web ASP.NET przy użyciu programu Visual Studio: wdrożenia z wiersza polecenia](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). MSBuild jest hello kompilacji aparatu używane przez program Visual Studio i może również służyć z hello wiersza polecenia toodeploy sieci web aplikacji tooWeb aplikacji. W tym samouczku jest częścią serii, która dotyczy głównie wdrożenie programu Visual Studio.

