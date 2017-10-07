---
title: "aaaHow toouse io.js z aplikacjami sieci Web usługi aplikacji Azure"
description: "Dowiedz się, jak toouse aplikacji sieci web w usłudze Azure App Service z io.js."
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
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>Jak toouse io.js z aplikacjami sieci Web usługi aplikacji Azure
Witaj popularnych węzeł rozwidlenia [io.js] funkcje projektu Node.js różnych tooJoyent różnice, w tym więcej Otwórz modelu ładu, szybsze cyklu wersji i szybsze przyjęcia nowych i eksperymentalna funkcji JavaScript.

Gdy [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web ma wiele wersji środowiska Node.js preinstalowany, umożliwia także dla pliku binarnego Node.js dostarczane przez użytkownika. W tym artykule opisano dwie metody umożliwiające użycie hello io.js aplikacji sieci Web usługi aplikacji: hello Użyj skryptu wdrożenia rozszerzonego, który automatycznie konfiguruje hello Azure toouse najnowszej wersji io.js dostępne, a także hello ręcznego przekazywania danych binarnych io.js. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Za pomocą skryptu wdrażania
Po wdrożeniu aplikacji Node.js aplikacji usługi sieci Web aplikacji uruchamia liczbę małych poleceń, które tooensure, który hello środowisko jest skonfigurowane poprawnie. Za pomocą skryptu wdrażania, ten proces może być dostosowane tooinclude hello pobierania i konfiguracji io.js.

Witaj [io.js skrypt wdrożenia](https://github.com/felixrieseberg/iojs-azure) jest dostępna w witrynie GitHub. io.js tooenable w aplikacji sieci web, wystarczy skopiować **.deployment**, **pliku deploy.cmd** i **plik IISNode.yml** toohello głównego folderu aplikacji i wdrażanie aplikacji tooWeb.  

pierwszy plik Hello **.deployment**, powoduje, że aplikacje sieci Web toorun **pliku deploy.cmd** po wdrożeniu. Ten skrypt uruchamia wszystkie kroki zwykle hello aplikacji Node.js, ale również pobiera najnowsza wersja io.js hello. Na koniec **plik IISNode.yml** konfiguruje binarne zamiast wstępnie zainstalowane binary Node.js io.js tylko hello pobrane toouse aplikacji sieci Web.

> [!NOTE]
> tooupdate hello używany io.js pliku binarnego, po prostu ponownie wdrożyć aplikację — skryptu hello pobierze nowej wersji io.js wdrożonej aplikacji hello co jeden raz.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Za pomocą ręcznej instalacji
Instalacja ręczna Hello wersji io.js niestandardowych obejmuje tylko dwa kroki. Najpierw pobierz hello **win-x64** binarne bezpośrednio z hello [io.js dystrybucji]. Wymagane są dwa pliki - **iojs.exe** i **iojs.lib**. Zapisz zarówno tooa folder plików w aplikacji sieci web, na przykład w **bin/iojs**.

toouse aplikacje sieci Web tooconfigure **iojs.exe** zamiast wstępnie zainstalowanej wersji węźle, utworzyć **plik IISNode.yml** hello katalogu głównego aplikacji i Dodaj hello następującego wiersza.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono sposób toouse io.js z aplikacjami sieci Web usługi aplikacji, używane są oba programy podane skryptów wdrażania, a także instalacji ręcznej. 

> [!NOTE]
> IO.js jest mocno programowanie i aktualizowane częściej niż Node.js. Liczba modułów Node.js może nie działać na io.js - Sprawdź należy zapoznać się z [io.js w serwisie GitHub] do rozwiązywania problemów.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

[io.js]: https://iojs.org
[io.js dystrybucji]: https://iojs.org/dist/
[io.js w serwisie GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
