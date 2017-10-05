---
title: "Sposób użycia platformy io.js z aplikacjami Web Apps w usłudze Azure App Service"
description: "Dowiedz się, jak używać aplikacji sieci web w usłudze Azure App Service z io.js."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a>Sposób użycia platformy io.js z aplikacjami Web Apps w usłudze Azure App Service
Popularne rozwidlenia węzła [io.js] funkcji różnych różnice do projektu Node.js w Joyent, tym bardziej otwarte modelu ładu, szybsze cyklu wersji i szybsze przyjęcia nowych i eksperymentalna funkcji JavaScript.

Gdy [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web ma wiele wersji środowiska Node.js preinstalowany, umożliwia także dla pliku binarnego Node.js dostarczane przez użytkownika. W tym artykule opisano dwie metody umożliwia używanie io.js aplikacji sieci Web usługi aplikacji: Użyj skryptu wdrożenia rozszerzonego, który automatycznie konfiguruje Azure, aby używać najnowszej wersji io.js dostępne, a także ręcznego przekazywania io.js binarnego. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Za pomocą skryptu wdrażania
Po wdrożeniu aplikacji Node.js aplikacji usługi sieci Web aplikacji działa wiele małych poleceń, aby zapewnić poprawne skonfigurowanie środowiska. Za pomocą skryptu wdrażania tego procesu można dostosować do pobierania i konfiguracji io.js.

[Io.js skrypt wdrożenia](https://github.com/felixrieseberg/iojs-azure) jest dostępna w witrynie GitHub. Aby włączyć io.js w aplikacji sieci web, wystarczy skopiować **.deployment**, **pliku deploy.cmd** i **plik IISNode.yml** do głównego folderu aplikacji i wdrażania aplikacji sieci Web.  

Pierwszy plik **.deployment**, powoduje, że aplikacje sieci Web do uruchamiania **pliku deploy.cmd** po wdrożeniu. Ten skrypt uruchamia wszystkie kroki zwykle aplikacji Node.js, ale również pobiera najnowsza wersja io.js. Na koniec **plik IISNode.yml** konfiguruje aplikacje sieci Web do używania właśnie pobrany io.js binarne zamiast wstępnie zainstalowane binarnym środowiska Node.js.

> [!NOTE]
> Aby zaktualizować plik binarny używany io.js, po prostu ponownie wdrożyć aplikację - skrypt pobierze nowej wersji io.js co jeden raz wdrożonej aplikacji.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Za pomocą ręcznej instalacji
Instalacja ręczna wersji niestandardowych io.js obejmuje tylko dwa kroki. Najpierw pobierz **win-x64** binarne bezpośrednio z [io.js dystrybucji]. Wymagane są dwa pliki - **iojs.exe** i **iojs.lib**. Zapisz oba pliki do folderu wewnątrz aplikacji sieci web, na przykład w **bin/iojs**.

Aby skonfigurować aplikacje sieci Web do używania **iojs.exe** zamiast wstępnie zainstalowanej wersji węźle, utworzyć **plik IISNode.yml** plików w katalogu głównym aplikacji i Dodaj następujący wiersz.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono sposób używania io.js z aplikacjami sieci Web usługi aplikacji, używane są oba programy podać skryptów wdrażania oraz jak ręczna instalacja. 

> [!NOTE]
> IO.js jest mocno programowanie i aktualizowane częściej niż Node.js. Liczba modułów Node.js może nie działać na io.js - Sprawdź należy zapoznać się z [io.js w serwisie GitHub] do rozwiązywania problemów.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

[io.js]: https://iojs.org
[io.js dystrybucji]: https://iojs.org/dist/
[io.js w serwisie GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
