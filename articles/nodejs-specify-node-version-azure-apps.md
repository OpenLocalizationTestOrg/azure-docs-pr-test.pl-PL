---
title: "aaaSpecifying wersji środowiska Node.js"
description: "Dowiedz się, jak toospecify hello wersji środowiska Node.js używane przez witryny sieci Web platformy Azure i usługi w chmurze"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>Specifying a Node.js version in an Azure application (Określanie wersji środowiska Node.js w aplikacji Azure)
Hosting aplikacji Node.js, możesz tooensure, że aplikacja korzysta z określonej wersji środowiska node.js. Istnieje kilka sposobów tooaccomplish to dla aplikacji hostowanej na platformie Azure.

## <a name="default-versions"></a>Wersji domyślnej
wersje Node.js Hello dostarczany przez platformę Azure są stale aktualizowane. Inaczej, hello domyślnej wersji, który określono w hello `WEBSITE_NODE_DEFAULT_VERSION` będzie można użyć zmiennej środowiskowej. toooverride wartość domyślną, wykonaj kroki hello w następujących sekcjach tego artykułu

> [!NOTE]
> Jeśli są obsługę aplikacji we usługi w chmurze Azure (rola sieci web lub procesu roboczego) i jest pierwszym wdrożeniu aplikacji hello hello, Azure podejmie toouse hello tę samą wersję programu Node.js, jak został zainstalowany na środowiska projektowego, jeśli go zgodny z wersjami domyślne hello dostępnymi na platformie Azure.
>
>

## <a name="versioning-with-packagejson"></a>Przechowywanie wersji pliku package.json
Można określić wersji hello toobe Node.js używane przez dodanie powitania po tooyour **package.json** pliku:

    "engines":{"node":version}

Gdzie *wersji* jest toouse numer hello określonej wersji. Można określić bardziej skomplikowane warunki dotyczące wersji, takich jak:

    "engines":{"node": "0.6.22 || 0.8.x"}

Ponieważ 0.6.22 nie jest jednym z hello wersjami dostępnymi w hello Środowisko hostingu, hello najwyższa wersja hello 0,8 serii, która jest dostępna będzie zamiast tego użyć - 0.8.4.

## <a name="versioning-websites-with-app-settings"></a>Przechowywanie wersji witryn sieci Web przy użyciu ustawień aplikacji
Jeśli prowadzą hosting aplikacji hello w witrynie sieci Web, można ustawić zmiennej środowiskowej hello **WEBSITE_NODE_DEFAULT_VERSION** toohello żądanej wersji.

## <a name="versioning-cloud-services-with-powershell"></a>Przechowywanie wersji usługi w chmurze przy użyciu programu PowerShell
Jeśli są hosting aplikacji hello w usłudze w chmurze i wdrażania aplikacji hello przy użyciu programu Azure PowerShell, można zastąpić domyślną wersję środowiska Node.js hello przy użyciu hello **AzureServiceProjectRole zestaw** polecenia cmdlet programu PowerShell. Na przykład:

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

Uwaga hello parametrów w hello powyżej instrukcji jest rozróżniana wielkość liter.  Możesz sprawdzić hello poprawną wersję środowiska Node.js została wybrana sprawdzając hello **aparaty** właściwości w roli użytkownika **package.json**.

Można również użyć hello **Get-AzureServiceProjectRoleRuntime** tooretrieve listę dostępnych dla aplikacji hostowanej jako usługa w chmurze wersji środowiska Node.js.  Zawsze, czy wersja hello Node.js zależy od projektu jest na tej liście.

## <a name="using-a-custom-version-with-azure-websites"></a>Przy użyciu dostosowanej wersji z witrynami sieci Web Azure
Azure zapewnia kilka wersji domyślnej Node.js, jednocześnie może być toouse wersji, która domyślnie nie jest dostępne. Jeśli aplikacja jest obsługiwana jako witryny sieci Web platformy Azure, możesz to zrobić przy użyciu hello **plik iisnode.yml** pliku. Witaj kolejnych krokach objaśniono proces hello przy użyciu dostosowanej wersji środowiska Node.Js z witryny sieci Web platformy Azure:

1. Utwórz nowy katalog, a następnie utwórz **server.js** pliku w katalogu hello. Witaj **server.js** plik powinien zawierać hello następujące czynności:

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    Spowoduje to wyświetlenie wersji środowiska Node.js hello używane podczas przeglądania hello witryny sieci Web.
2. Tworzenie nowej witryny sieci Web i nazwa hello Uwaga hello witryny. Na przykład następujące hello używa hello [narzędzi wiersza polecenia platformy Azure] toocreate nowej witryny internetowej platformy Azure o nazwie **MojaWitrynaSieciWeb**, a następnie włącz repozytorium Git hello witryny sieci Web.

        azure site create mywebsite --git
3. Utwórz nowy katalog o nazwie **bin** jako element podrzędny hello katalog zawierający hello **server.js** pliku.
4. Pobierz hello określonej wersji **node.exe** (wersja systemu Windows hello) mają toouse z aplikacją. Na przykład Witaj następujących używa **curl** toodownload wersji 0.8.1:

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    Zapisz hello **node.exe** pliku do hello **bin** folder utworzony wcześniej.
5. Utwórz **plik iisnode.yml** w pliku hello sam katalogu jako hello **server.js** pliku, a następnie dodaj powitania po zawartości toohello **plik iisnode.yml** pliku:

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    Jest to ścieżka, gdzie hello **node.exe** pliku w projekcie zostaną umieszczone po opublikowaniu toohello Twojej aplikacji witryny sieci Web Azure.
6. Publikowanie aplikacji. Na przykład ponieważ wcześniej utworzona nowej witryny sieci Web z parametrem--git hello, hello następujące polecenia spowoduje dodanie hello aplikacji pliki toomy lokalnego repozytorium Git i następnie wypchniesz toohello repozytorium witryny sieci Web:

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    Po opublikowaniu aplikacji hello ma Otwórz hello witryny sieci Web w przeglądarce. Powinien zostać wyświetlony komunikat z informacją "Hello Azure uruchomionej wersji węzła: v0.8.1".

## <a name="next-steps"></a>Następne kroki
Teraz, że rozumiesz, jak wersja hello toospecify Node.js używanych przez aplikację, Dowiedz się, jak za[Praca z modułami], [tworzenia i wdrażania witryn sieci Web Node.js](app-service-web/app-service-web-get-started-nodejs.md), i [jak toouse hello Azure Narzędzia wiersza polecenia dla komputerów Mac i Linux].

Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów środowiska Node.js](https://azure.microsoft.com/develop/nodejs/).

[jak toouse hello Azure Narzędzia wiersza polecenia dla komputerów Mac i Linux]:cli-install-nodejs.md
[narzędzi wiersza polecenia platformy Azure]:cli-install-nodejs.md
[Praca z modułami]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
