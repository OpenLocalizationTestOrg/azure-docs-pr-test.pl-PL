---
title: "Konfigurowanie środowiska deweloperskiego w systemie Windows dla mikrousług platformy Azure | Microsoft Docs"
description: "Zainstaluj środowisko uruchomieniowe, zestaw SDK i narzędzia oraz utwórz lokalny klaster projektowy. Po ukończeniu tej konfiguracji wszystko będzie gotowe do kompilowania aplikacji w systemie Windows."
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
ms.date: 09/25/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 0691f26168feacf290b732afd7dfd680a2537179
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="prepare-your-development-environment-on-windows"></a>Przygotowywanie środowiska deweloperskiego w systemie Windows
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 Aby móc tworzyć i uruchamiać [aplikacje usługi Azure Service Fabric][1] na maszynie deweloperskiej z systemem Windows, zainstaluj środowisko uruchomieniowe, zestaw SDK oraz narzędzia. Należy również włączyć wykonywanie skryptów programu Windows PowerShell zawartych w zestawie SDK.

## <a name="prerequisites"></a>Wymagania wstępne
### <a name="supported-operating-system-versions"></a>Obsługiwane wersje systemu operacyjnego
Na potrzeby tworzenia aplikacji obsługiwane są następujące wersje systemu operacyjnego:

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> System Windows 7 domyślnie zawiera program Windows PowerShell wyłącznie w wersji 2.0. Polecenia cmdlet programu PowerShell usługi Service Fabric wymagają programu PowerShell w wersji 3.0 lub nowszej. Możesz [pobrać program Windows PowerShell 5.0][powershell5-download] w Centrum pobierania Microsoft.
> 
> 

## <a name="install-the-sdk-and-tools"></a>Instalowanie zestawu SDK i narzędzi
### <a name="to-use-visual-studio-2017"></a>Używanie programu Visual Studio 2017
Narzędzia Service Fabric Tools są częścią pakietu roboczego projektowania i zarządzania na platformie Azure w programie Visual Studio 2017. Włącz to obciążenie w ramach instalacji programu Visual Studio.
Ponadto należy zainstalować zestaw SDK usługi Microsoft Azure Service Fabric przy użyciu instalatora platformy sieci Web.

* [Instalowanie zestawu SDK usługi Microsoft Azure Service Fabric][core-sdk]

### <a name="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>Używanie programu Visual Studio 2015 (wymaga programu Visual Studio 2015 Update 2 lub nowszego)
W przypadku programu Visual Studio 2015 narzędzia Service Fabric są instalowane razem z zestawem SDK przy użyciu instalatora platformy sieci Web:

* [Instalowanie zestawu SDK i narzędzi usługi Microsoft Azure Service Fabric][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>Instalowanie samego zestawu SDK
Jeśli potrzebujesz tylko zestawu SDK, możesz zainstalować ten pakiet:
* [Instalowanie zestawu SDK usługi Microsoft Azure Service Fabric][core-sdk]

Bieżące wersje:
* Zestaw SDK usługi Service Fabric w wersji 2.8.211
* Środowisko uruchomieniowe usługi Service Fabric w wersji 6.0.211
* Narzędzia usługi Service Fabric dla programu Visual Studio 2015 w wersji 1.7.50721
* Program Visual Studio 2017 Update 3 obejmuje narzędzia usługi Service Fabric dla programu Visual Studio w wersji 1.7.20170817
* Program Visual Studio 2017 Update 4 Preview 1 (15.4.0 Preview 1.0) obejmuje narzędzia usługi Service Fabric dla programu Visual Studio w wersji 1.7.20170721

Listę obsługiwanych wersji można znaleźć na stronie [pomocy technicznej usługi Service Fabric](service-fabric-support.md)

## <a name="enable-powershell-script-execution"></a>Włączanie wykonywania skryptów programu PowerShell
Platforma Service Fabric korzysta ze skryptów programu Windows PowerShell do tworzenia lokalnego klastra projektowego i do wdrażania aplikacji z programu Visual Studio. Domyślnie system Windows blokuje uruchamianie tych skryptów. Aby je włączyć, należy zmienić zasady wykonywania w programie PowerShell. Uruchom program PowerShell jako administrator i wprowadź następujące polecenie:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Następne kroki
Po skonfigurowaniu środowiska projektowego możesz zacząć kompilować i uruchamiać aplikacje.

* [Tworzenie pierwszej aplikacji platformy Service Fabric w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
* [Informacje o wdrażaniu aplikacji i zarządzaniu nimi w klastrze lokalnym](service-fabric-get-started-with-a-local-cluster.md)
* [Informacje o modelach programowania: Reliable Services i Reliable Actors](service-fabric-choose-framework.md)
* [Przykłady kodu platformy Service Fabric w witrynie GitHub](https://aka.ms/servicefabricsamples)
* [Wizualizowanie klastra przy użyciu narzędzia Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)
* [Ścieżka szkoleniowa platformy Service Fabric — pełne wprowadzenie do platformy](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Strona kampanii usługi Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI — link"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI — link"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI — link"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
