---
title: "aaaSet się Środowisko deweloperskie do platformy Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Zainstaluj hello środowiska uruchomieniowego, zestawu SDK i narzędzia i Utwórz lokalny klaster projektowy. Po ukończeniu tej konfiguracji będzie gotowy toobuild aplikacji."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a>Przygotowywanie środowiska projektowego
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 toobuild i uruchom [aplikacji usługi Azure Service Fabric] [ 1] na komputerze deweloperskim instalowanie hello środowiska uruchomieniowego, zestawu SDK i narzędzia. Należy również tooenable wykonywania skryptów programu Windows PowerShell hello objęte hello zestawu SDK.

## <a name="prerequisites"></a>Wymagania wstępne
### <a name="supported-operating-system-versions"></a>Obsługiwane wersje systemu operacyjnego
następujące wersje systemu operacyjnego Hello są obsługiwane w przypadku rozwoju:

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> System Windows 7 domyślnie zawiera program Windows PowerShell wyłącznie w wersji 2.0. Polecenia cmdlet programu PowerShell usługi Service Fabric wymagają programu PowerShell w wersji 3.0 lub nowszej. Możesz [pobrać program Windows PowerShell 5.0] [ powershell5-download] z hello Microsoft Download Center.
> 
> 

## <a name="install-hello-sdk-and-tools"></a>Zainstaluj hello zestawu SDK i narzędzia
### <a name="toouse-visual-studio-2017"></a>toouse programu Visual Studio 2017 r.
Service Fabric Tools są częścią hello Azure projektowania i zarządzania nimi obciążenia w programie Visual Studio 2017 r. Włącz to obciążenie w ramach instalacji programu Visual Studio.
Ponadto należy hello tooinstall zestaw Microsoft Azure Service Fabric SDK, za pomocą Instalatora platformy sieci Web.

* [Zainstaluj zestaw SDK usługi Microsoft Azure Service Fabric hello][core-sdk]

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>toouse programu Visual Studio 2015 (wymaga programu Visual Studio 2015 Update 2 lub nowszy)
Dla programu Visual Studio 2015 wraz z zestawu SDK, za pomocą Instalatora platformy sieci Web hello hello są zainstalowane narzędzia Service Fabric:

* [Zainstaluj zestaw SDK usługi Microsoft Azure Service Fabric hello i narzędzia][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>Instalowanie samego zestawu SDK
Wymagane jest tylko hello zestawu SDK, po zastosowaniu tego pakietu:
* [Zainstaluj zestaw SDK usługi Microsoft Azure Service Fabric hello][core-sdk]

bieżące wersje Hello są:
* Zestaw SDK usługi Service Fabric w wersji 2.7.198
* Środowisko uruchomieniowe usługi Service Fabric w wersji 5.7.198
* Narzędzia usługi Service Fabric dla programu Visual Studio 2015 w wersji 1.7.50721
* Program Visual Studio 2017 Update 2 obejmuje narzędzia usługi Service Fabric dla programu Visual Studio w wersji 1.6.20170504
* Program Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) obejmuje narzędzia usługi Service Fabric dla programu Visual Studio w wersji 1.7.20170721

Listę obsługiwanych wersji można znaleźć na stronie [pomocy technicznej usługi Service Fabric](service-fabric-support.md)

## <a name="enable-powershell-script-execution"></a>Włączanie wykonywania skryptów programu PowerShell
Platforma Service Fabric korzysta ze skryptów programu Windows PowerShell do tworzenia lokalnego klastra projektowego i do wdrażania aplikacji z programu Visual Studio. Domyślnie system Windows blokuje uruchamianie tych skryptów. tooenable je, należy zmodyfikować zasady wykonywania programu PowerShell. Otwórz program PowerShell jako administrator i wprowadź następujące polecenie hello:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Następne kroki
Po skonfigurowaniu środowiska projektowego możesz zacząć kompilować i uruchamiać aplikacje.

* [Tworzenie pierwszej aplikacji platformy Service Fabric w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
* [Dowiedz się, jak toodeploy aplikacji w klastrze lokalnym i zarządzanie nimi](service-fabric-get-started-with-a-local-cluster.md)
* [Dowiedz się więcej o hello modele programowania: Reliable Services i Reliable Actors](service-fabric-choose-framework.md)
* [Zapoznaj się z sieci szkieletowej usług hello przykłady kodu w witrynie GitHub](https://aka.ms/servicefabricsamples)
* [Wizualizowanie klastra przy użyciu narzędzia Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)
* [Wykonaj hello learning tooget ścieżki platformy toohello obszerne wprowadzenie sieci szkieletowej usług](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Strona kampanii usługi Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI — link"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI — link"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI — link"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
