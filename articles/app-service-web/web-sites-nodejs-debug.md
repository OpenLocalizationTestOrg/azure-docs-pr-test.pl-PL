---
title: "How to debug a Node.js web app in Azure App Service (Jak debugować aplikację sieci Web Node.js w usłudze Azure App Service)"
description: "Dowiedz się, jak debugować aplikację sieci web Node.js w usłudze Azure App Service."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a>How to debug a Node.js web app in Azure App Service (Jak debugować aplikację sieci Web Node.js w usłudze Azure App Service)
Platforma Azure oferuje wbudowane narzędzia diagnostyczne z debugowanie aplikacji Node.js hostowanych w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web. W tym artykule dowiesz się, jak włączyć rejestrowanie stdout i stderr, wyświetlane informacje o błędzie w przeglądarce i sposobu pobierania i wyświetlania plików dziennika.

Diagnostyka dla aplikacji programu Node.js hostowanej na platformie Azure jest zapewniana przez [IISNode]. Gdy w tym artykule omówiono najczęściej używane do zbierania informacji diagnostycznych, nie dostarcza pełne odwołanie do pracy z programu IISNode. Aby uzyskać więcej informacji na temat pracy z programu IISNode, zobacz [plik Readme programu IISNode] w witrynie GitHub.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Włącz rejestrowanie
Domyślnie aplikacji sieci web usługi aplikacji — tylko przechwytuje informacje diagnostyczne dotyczące wdrożeń, takich jak podczas wdrażania aplikacji sieci web przy użyciu narzędzia Git. Informacje te są przydatne, jeśli masz problemy podczas wdrażania, takiej jak awaria podczas instalowania modułu, do którego odwołuje się **package.json**, lub jeśli używasz skryptu wdrażania niestandardowego.

Aby włączyć rejestrowanie ze strumienia stdout i stderr, należy utworzyć **plik IISNode.yml** plików w katalogu głównym aplikacji Node.js i Dodaj następujący kod:

    loggingEnabled: true

Dzięki temu rejestrowanie stderr i stdout z poziomu aplikacji Node.js.

**Plik IISNode.yml** pliku może również służyć do kontroli czy przyjazne komunikaty o błędach lub developer błędy są zwracane do przeglądarki, gdy wystąpi błąd. Aby włączyć błędy developer, Dodaj następujący wiersz do **plik IISNode.yml** pliku:

    devErrorsEnabled: true

Po włączeniu tej opcji program IISNode zwróci ostatniego 64 KB informacje wysyłane do strumienia wyjściowego stderr zamiast błędu przyjazną, takie jak "Wystąpił wewnętrzny błąd serwera".

> [!NOTE]
> Gdy devErrorsEnabled jest przydatne, gdy diagnozowanie problemów w czasie projektowania, włączenie jej w środowisku produkcyjnym może powodować błędy programowanie są wysyłane do użytkowników końcowych.
> 
> 

Jeśli **plik IISNode.yml** plik nie istnieje już w aplikacji, należy ponownie uruchomić aplikacji sieci web po opublikowaniu aplikacji zaktualizowane. W przypadku po prostu zmiany ustawień w istniejącym **plik IISNode.yml** pliku, który wcześniej został opublikowany, nie jest ponowne uruchomienie wymagane.

> [!NOTE]
> Jeśli aplikacja sieci web została utworzona za pomocą narzędzia wiersza polecenia platformy Azure lub poleceń cmdlet Azure PowerShell, domyślny **plik IISNode.yml** plik jest tworzony automatycznie.
> 
> 

Można ponownie uruchomić aplikacji sieci web, wybierz aplikację sieci web w [Azure Portal](https://portal.azure.com), a następnie kliknij przycisk **ponowne URUCHOMIENIE** przycisk:

![Uruchom ponownie przycisku][restart-button]

Jeśli narzędzia wiersza polecenia platformy Azure są zainstalowane w środowisku projektowania, służy następujące polecenie, aby ponownie uruchomić aplikacji sieci web:

    azure site restart [sitename]

> [!NOTE]
> LoggingEnabled i devErrorsEnabled są najczęściej używane opcje konfiguracji plik IISNode.yml przechwytywania informacje diagnostyczne, plik IISNode.yml może służyć do konfigurowania różnych opcji dla danego środowiska hostingu. Aby uzyskać pełną listę opcji konfiguracji, zobacz [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) pliku.
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Uzyskiwanie dostępu do dzienników
Dzienniki diagnostyczne jest dostępny na trzy sposoby; Za pomocą protokołu FTP (File Transfer), pobieranie archiwum Zip lub jako na żywo zaktualizowane strumienia dziennika (fragmentu). Pobieranie archiwum Zip plików dziennika lub wyświetlanie strumień na żywo wymaga narzędzia wiersza polecenia platformy Azure. Mogą być instalowane za pomocą następującego polecenia:

    npm install azure-cli -g

Po zainstalowaniu narzędzi jest możliwy za pomocą polecenia "azure". Narzędzia wiersza polecenia, należy najpierw skonfigurować do korzystania z subskrypcji platformy Azure. Aby uzyskać informacje na temat sposobu wykonania tego zadania, zobacz **sposób pobierania i importowania ustawień publikowania** sekcji [sposobu użycia narzędzi wiersza polecenia Azure](../xplat-cli-connect.md) artykułu.

### <a name="ftp"></a>FTP
Aby uzyskać dostęp do informacji diagnostycznych za pośrednictwem FTP, odwiedź stronę [Azure Portal](https://portal.azure.com), wybierz aplikację sieci web, a następnie wybierz **pulpitu NAWIGACYJNEGO**. W **szybkie linki** sekcji **DZIENNIKÓW diagnostycznych FTP** i **DZIENNIKÓW diagnostycznych FTPS** łącza zapewniają dostęp do dzienników przy użyciu protokołu FTP.

> [!NOTE]
> Jeśli użytkownik nie zostały wcześniej skonfigurowane nazwy użytkownika i hasła dla FTP lub wdrożenie, możesz to zrobić z **szybkiego startu** strony zarządzania przez wybranie **skonfigurowano poświadczeń wdrożenia**.
> 
> 

Adres URL FTP zwrócił na pulpicie nawigacyjnym jest **LogFiles** katalogu, który będzie zawierać następujące katalogi podrzędne:

* [Metody wdrażania](web-sites-deploy.md) — Jeśli używasz metody wdrażania, takie jak Git, katalog o tej samej nazwie zostanie utworzony i będzie zawierać informacje dotyczące wdrożeń.
* nodejs — informacje Stdout i stderr przechwytywane z wszystkich wystąpień aplikacji (jeśli loggingEnabled ma wartość true.)

### <a name="zip-archive"></a>Archiwum zip
Aby pobrać archiwum Zip dzienników diagnostycznych, użyj następującego polecenia z narzędzi wiersza polecenia platformy Azure:

    azure site log download [sitename]

Spowoduje to pobranie **diagnostics.zip** w bieżącym katalogu. To archiwum zawiera następującą strukturę katalogów:

* wdrożenia — dziennik informacji o wdrożeniach aplikacji
* LogFiles
  
  * [Metody wdrażania](web-sites-deploy.md) — Jeśli używasz metody wdrażania, takie jak Git, katalog o tej samej nazwie zostanie utworzony i będzie zawierać informacje dotyczące wdrożeń.
  * nodejs — informacje Stdout i stderr przechwytywane z wszystkich wystąpień aplikacji (jeśli loggingEnabled ma wartość true.)

### <a name="live-stream-tail"></a>Strumień na żywo (tail)
Aby wyświetlić strumień na żywo informacji diagnostycznych dziennika, użyj następującego polecenia z narzędzi wiersza polecenia platformy Azure:

    azure site log tail [sitename]

Zwraca strumienia dziennika zdarzeń, które są aktualizowane w miarę ich występowania na serwerze. Ten strumień zwraca informacje na temat wdrażania, jak również informacje stdout i stderr (jeśli loggingEnabled ma wartość true.)

<a id="nextsteps"></a>

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono sposób włączenia i dostęp do informacji diagnostycznych dla platformy Azure. Gdy informacje te są przydatne w opis problemów, które występują w przypadku aplikacji, może to wskazywać na problem z modułem używasz lub wersja Node.js używane przez aplikacje sieci Web usługi aplikacji jest inne niż używane w danym środowisku wdrażania.

Informacje w pracy z modułów na platformie Azure, zobacz [przy użyciu modułów Node.js z aplikacjami Azure](../nodejs-use-node-modules-azure-apps.md).

Informacje dotyczące określania wersji środowiska Node.js dla aplikacji, zobacz [określanie wersji środowiska Node.js w aplikacji Azure].

Aby uzyskać więcej informacji, zobacz też [Centrum deweloperów środowiska Node.js](/develop/nodejs/).

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[plik Readme programu IISNode]: https://github.com/tjanczuk/iisnode#readme
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[określanie wersji środowiska Node.js w aplikacji Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

