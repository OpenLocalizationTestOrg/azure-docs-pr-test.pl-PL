---
title: wiersz aaaCommand kompilacji dla platformy Azure | Dokumentacja firmy Microsoft
description: Kompilacji wiersza polecenia platformy Azure
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a>Kompilowanie projektów platformy Azure z wiersza polecenia hello
Witaj Microsoft kompilacji Engine (MSBuild) można tworzyć produktów w środowisku laboratorium kompilacji, których nie zainstalowano programu Visual Studio. Program MSBuild używa formatu XML dla plików projektu, które extensible i w pełni obsługiwane przez firmę Microsoft. Przy użyciu formatu pliku MSBuild hello, można opisać co elementów musi być skompilowany dla platformy i konfiguracji.

Można również uruchomić MSBuild hello wiersza polecenia, a w tym temacie opisano tego podejścia. Przez ustawienie właściwości hello w wierszu polecenia, można utworzyć określonej konfiguracji projektu. Podobnie można również zdefiniować hello obiektów docelowych, które kompilacje programu MSBuild. Aby uzyskać więcej informacji na temat parametrów wiersza polecenia i MSBuild, zobacz [dotyczące wiersza polecenia programu MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).

## <a name="msbuild-parameters"></a>Parametry MSBuild
Witaj najprostszy sposób toocreate pakietu jest toorun MSBuild z hello `/t:Publish` opcji. Domyślnie to polecenie tworzy katalog w folderze głównym toohello relacji dla projektu hello, takich jak `<ProjectDirectory>\bin\Configuration\app.publish\`. Podczas tworzenia projektu platformy Azure są generowane dwa pliki: hello sam plik pakietu i towarzyszący plik konfiguracji hello:

* Pakiet z pliku (`project.cspkg`)
* Plik konfiguracji (`ServiceConfiguration.TargetProfile.cscfg`)

Domyślnie każdy projekt Azure zawiera jeden plik konfiguracji usługi dla lokalne kompilacje (debugowanie) i drugi dla kompilacji chmury (tymczasowym czy produkcyjnym). Można jednak dodać lub usunąć pliki konfiguracji usługi, zgodnie z potrzebami. Podczas tworzenia pakietu w programie Visual Studio zapyta, które tooinclude pliku konfiguracji usługi obok hello pakietu. Podczas tworzenia pakietu przy użyciu programu MSBuild, domyślnie znajduje się hello lokalnego pliku konfiguracji usługi. Plik tooinclude różnych konfiguracji usługi, zestaw hello `TargetProfile` właściwości hello polecenia programu MSBuild (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

Jeśli chcesz, aby toouse alternatywny katalog hello przechowywane pliki pakietu i konfiguracji, Ustaw ścieżkę hello przy użyciu hello `/p:PublishDir=Directory\` opcji, w tym hello kończyć się separatorem ukośnika odwrotnego.

## <a name="next-steps"></a>Następne kroki
Po utworzeniu pakietu hello można wdrożyć tooAzure. Samouczek przedstawiający tooautomate który przetworzył, zobacz [ciągłego dostarczania dla usług w chmurze na platformie Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).

