---
title: "aaaHow tooupgrade projekty toohello bieżącej wersji hello Azure narzędzia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak projektu tooupgrade platformy Azure w w programie Visual Studio toohello bieżącej wersji hello narzędzi platformy Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: c89ba43af0f2fd9db46ce0c90f0da3d70dc1510b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupgrade-projects-toohello-current-version-of-hello-azure-tools-for-visual-studio"></a>Jak tooupgrade projektów toohello bieżącej wersji hello Azure Tools dla programu Visual Studio
## <a name="overview"></a>Omówienie
Po zainstalowaniu hello bieżącej wersji narzędzi Azure hello (lub poprzedniej wersji, która jest nowsza niż 1.6), wszystkie projekty, które zostały utworzone przy użyciu narzędzia Azure Zwolnij przed 1.6 (listopad 2011) zostaną automatycznie uaktualnione jak je otworzyć. Jeśli utworzono projektów przy użyciu hello 1.6 (listopad 2011) wersji tych narzędzi i nadal masz zwolnienia zainstalowany, możesz otworzyć te projekty w starszej wersji hello i zdecyduje później, czy tooupgrade je.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>Jak projekt zmiany po uaktualnieniu
Jeśli projekt zostanie automatycznie uaktualniony lub możesz określić, że chcesz tooupgrade, projektu jest modyfikowane toowork z bieżącymi wersjami niektóre zestawy, a niektóre właściwości również są zmieniane, zgodnie z opisem w tej sekcji. Jeśli Twój projekt wymaga innych zmian toobe zgodne z nowszej wersji narzędzia hello hello, musisz wprowadzić te zmiany ręcznie.

* Hello pliku web.config dla ról sieć web i hello pliku app.config dla roli proces roboczy są zaktualizowane tooreference hello nowsza wersja Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll.
* Zestawy Microsoft.WindowsAzure.StorageClient.dll, Microsoft.WindowsAzure.Diagnostics.dll i Microsoft.WindowsAzure.ServiceRuntime.dll Hello są nowe wersje toohello uaktualniony.
* Profilów publikowania, które były przechowywane w pliku projektu Azure hello (ccproj) są oddzielny plik tooa przeniesiony z .azurePubXml rozszerzenia hello, w hello **publikowania** podkatalogu.
* Niektóre właściwości w hello profilu publikowania są zaktualizowane toosupport nowe i zmienione funkcje. **AllowUpgrade** zastępuje **DeploymentReplacementMethod** ponieważ równocześnie lub przyrostowo można zaktualizować usługi w chmurze wdrożone.
* Witaj właściwości **UseIISExpressByDefault** zostanie dodany i ustawić toofalse, dzięki czemu hello serwer sieci web, który jest używany do debugowania zmienią się automatycznie z usług Internet Information Services (IIS) tooIIS Express. Usługi IIS Express to hello domyślnego serwera sieci web dla projektów utworzonych za pomocą hello nowszych wersjach hello narzędzi.
* Jeśli buforowanie Azure znajduje się w co najmniej jeden z projektów ról, niektóre właściwości w konfiguracji usługi hello (plik .cscfg) i definicji usługi (plik csdef) są zmieniane po uaktualnieniu projektu. Jeśli projekt hello korzysta z pakietu NuGet buforowanie Azure hello, projektu hello jest najnowszą wersję pakietu hello toohello uaktualniony. Należy otworzyć plik web.config hello i sprawdź, czy tej konfiguracji klient hello znajdował się prawidłowo podczas procesu uaktualniania hello. Jeśli dodano zestawy hello odwołania tooAzure buforowanie klientów bez użycia pakietu NuGet hello, te zestawy nie zostaną zaktualizowane; należy ręcznie zaktualizować te odwołania toohello nowe wersje.

> [!IMPORTANT]
> Dla projektów języka F # należy ręcznie zaktualizować odwołania do zestawów tooAzure tak, aby odwołujących się do nowszych wersji hello tych zestawów.
> 
> 

### <a name="how-tooupgrade-an-azure-project-toohello-current-release"></a>Jak tooupgrade Azure projektu toohello bieżącej wersji.
1. Zainstaluj hello bieżącą wersję systemu hello Azure Tools na powitania instalację programu Visual Studio mają toouse dla hello uaktualnić projekt, a następnie otwórz hello projektu, które mają tooupgrade. Jeśli projekt hello utworzono za pomocą narzędzia Azure Zwolnij przed 1.6 (listopad 2011), projekt hello jest automatycznie uaktualniony toohello bieżącej wersji. Jeśli hello projekt został utworzony z hello wersji listopad 2011 i nadal zainstalowanej wersji, hello projektu zostanie otwarty w tej wersji.
2. W Eksploratorze rozwiązań Otwórz hello menu skrótów węzła projektu hello, wybierz **właściwości**, a następnie wybierz pozycję hello **aplikacji** pojawi się okno dialogowe hello na karcie.
   
    Witaj **aplikacji** karta zawiera wersja narzędzi hello, który został skojarzony z projektem hello. Jeśli pojawi się hello bieżącej wersji narzędzi platformy Azure, hello projektu już został uaktualniony. Jeśli po zainstalowaniu nowsza wersja narzędzia hello niż jakie karcie hello są wyświetlane, **uaktualnienia** pojawi się przycisk.
3. Wybierz hello **uaktualnienia** tooupgrade przycisk projektu toohello bieżącą wersję narzędzia hello.
4. Kompilacji projektu hello, a następnie Rozwiąż wszystkie błędy, które wynikają z interfejsu API zmiany. Aby dowiedzieć się jak toomodify kodu dla hello nowej wersji, zapoznaj się dokumentacją hello hello interfejsu API.

