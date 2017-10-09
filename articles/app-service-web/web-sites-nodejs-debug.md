---
title: "toodebug aaaHow aplikacji sieci web Node.js w usłudze Azure App Service"
description: "Dowiedz się, jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service."
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
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a>Jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service
Platforma Azure oferuje wbudowane narzędzia diagnostyczne tooassist z debugowaniem aplikacji programu Node.js w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web. W tym artykule przedstawiono sposób rejestrowania tooenable stdout i stderr, informacje o błędzie wyświetlanej w przeglądarce hello i jak toodownload i wyświetlanie plików dziennika.

Diagnostyka dla aplikacji programu Node.js hostowanej na platformie Azure jest zapewniana przez [IISNode]. Gdy w tym artykule omówiono hello najczęściej używane do zbierania informacji diagnostycznych, nie dostarcza pełne odwołanie do pracy z programu IISNode. Aby uzyskać więcej informacji na temat pracy z programu IISNode, zobacz hello [plik Readme programu IISNode] w witrynie GitHub.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Włącz rejestrowanie
Domyślnie aplikacji sieci web usługi aplikacji — tylko przechwytuje informacje diagnostyczne dotyczące wdrożeń, takich jak podczas wdrażania aplikacji sieci web przy użyciu narzędzia Git. Informacje te są przydatne, jeśli masz problemy podczas wdrażania, takiej jak awaria podczas instalowania modułu, do którego odwołuje się **package.json**, lub jeśli używasz skryptu wdrażania niestandardowego.

Witaj tooenable rejestrowania ze strumienia stdout i stderr, należy utworzyć **plik IISNode.yml** hello katalogu głównego aplikacji Node.js i dodaj następujące hello:

    loggingEnabled: true

Dzięki temu rejestrowanie hello stderr i stdout z poziomu aplikacji Node.js.

Witaj **plik IISNode.yml** pliku mogą być również używane toocontrol, czy przyjazne komunikaty o błędach lub developer błędy są zwracane toohello przeglądarki, gdy wystąpi błąd. błędy developer tooenable, Dodaj powitania po wierszu toohello **plik IISNode.yml** pliku:

    devErrorsEnabled: true

Po włączeniu tej opcji program IISNode zwróci hello ostatniego 64 KB informacje wysyłane toostderr zamiast przyjazną błędu, takie jak "Wystąpił wewnętrzny błąd serwera".

> [!NOTE]
> Gdy devErrorsEnabled jest przydatne, gdy diagnozowanie problemów w czasie projektowania, włączenie jej w środowisku produkcyjnym może powodować błędy programowanie wysyłane tooend użytkowników.
> 
> 

Jeśli hello **plik IISNode.yml** plik nie istnieje już w aplikacji, należy ponownie uruchomić aplikacji sieci web po opublikowaniu aplikacji hello zaktualizowane. W przypadku po prostu zmiany ustawień w istniejącym **plik IISNode.yml** pliku, który wcześniej został opublikowany, nie jest ponowne uruchomienie wymagane.

> [!NOTE]
> Jeśli aplikacja sieci web została utworzona za pomocą narzędzia wiersza polecenia Azure hello lub poleceń cmdlet Azure PowerShell, domyślny **plik IISNode.yml** plik jest tworzony automatycznie.
> 
> 

aplikacji sieci web hello toorestart, aplikacji sieci web wybierz hello w hello [Azure Portal](https://portal.azure.com), a następnie kliknij przycisk **ponowne URUCHOMIENIE** przycisk:

![Uruchom ponownie przycisku][restart-button]

Jeśli narzędzia wiersza polecenia Azure hello są zainstalowane w środowisku projektowania, możesz użyć hello następującej aplikacji sieci web hello toorestart polecenia:

    azure site restart [sitename]

> [!NOTE]
> Gdy loggingEnabled i devErrorsEnabled są opcje konfiguracji plik IISNode.yml hello najczęściej używane do przechwytywania informacje diagnostyczne, plik IISNode.yml może mieć tooconfigure używane różne opcje środowisku macierzystym. Aby uzyskać pełną listę opcji konfiguracji hello, zobacz hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) pliku.
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Uzyskiwanie dostępu do dzienników
Dzienniki diagnostyczne jest dostępny na trzy sposoby; Przy użyciu hello protokołu FTP (File Transfer), pobieranie archiwum Zip lub jako na żywo zaktualizowane strumienia dziennika hello (fragmentu). Pobieranie archiwum Zip hello plików dziennika hello lub wyświetlanie hello strumień na żywo wymaga narzędzia wiersza polecenia Azure hello. Mogą być instalowane za pomocą hello następujące polecenie:

    npm install azure-cli -g

Po zainstalowaniu narzędzi hello jest możliwy za pomocą polecenia "azure" hello. Witaj narzędzia wiersza polecenia musi najpierw zostać skonfigurowany toouse subskrypcji platformy Azure. Uzyskać informacji o sposobie tooaccomplish to zadań, zobacz hello **jak toodownload, a następnie zaimportuj ustawienia publikowania** sekcji hello [jak tooUse hello narzędzi wiersza polecenia Azure](../xplat-cli-connect.md) artykułu.

### <a name="ftp"></a>FTP
informacje diagnostyczne hello tooaccess za pomocą protokołu FTP, odwiedź stronę hello [Azure Portal](https://portal.azure.com), wybierz aplikację sieci web, a następnie wybierz hello **pulpitu NAWIGACYJNEGO**. W hello **szybkie linki** sekcji, hello **DZIENNIKÓW diagnostycznych FTP** i **DZIENNIKÓW diagnostycznych FTPS** łącza umożliwiają dostęp toohello dzienników przy użyciu protokołu hello FTP.

> [!NOTE]
> Jeśli użytkownik nie zostały wcześniej skonfigurowane nazwy użytkownika i hasła dla FTP lub wdrożenie, możesz to zrobić z hello **szybkiego startu** strony zarządzania przez wybranie **skonfigurowano poświadczeń wdrożenia**.
> 
> 

Witaj FTP adres URL zwracany na pulpicie nawigacyjnym hello jest hello **LogFiles** katalogu, który będzie zawierać Witaj podkatalogi następujące:

* [Metody wdrażania](web-sites-deploy.md) — Jeśli używasz metody wdrażania, takie jak Git katalogu hello takiej nazwie zostanie utworzony i będzie zawierać informacje związane z toodeployments.
* nodejs — informacje Stdout i stderr przechwytywane z wszystkich wystąpień aplikacji (jeśli loggingEnabled ma wartość true.)

### <a name="zip-archive"></a>Archiwum zip
toodownload archiwum Zip hello dzienników diagnostycznych, hello Użyj następującego polecenia z narzędzi wiersza polecenia Azure hello:

    azure site log download [sitename]

Spowoduje to pobranie **diagnostics.zip** w bieżącym katalogu hello. To archiwum zawiera powitania po strukturę katalogów:

* wdrożenia — dziennik informacji o wdrożeniach aplikacji
* LogFiles
  
  * [Metody wdrażania](web-sites-deploy.md) — Jeśli używasz metody wdrażania, takie jak Git katalogu hello takiej nazwie zostanie utworzony i będzie zawierać informacje związane z toodeployments.
  * nodejs — informacje Stdout i stderr przechwytywane z wszystkich wystąpień aplikacji (jeśli loggingEnabled ma wartość true.)

### <a name="live-stream-tail"></a>Strumień na żywo (tail)
tooview strumień na żywo danych dzienników diagnostycznych hello Użyj następującego polecenia z narzędzi wiersza polecenia Azure hello:

    azure site log tail [sitename]

Zwraca strumienia dziennika zdarzeń, które są aktualizowane w miarę ich występowania na powitania serwera. Ten strumień zwraca informacje na temat wdrażania, jak również informacje stdout i stderr (jeśli loggingEnabled ma wartość true.)

<a id="nextsteps"></a>

## <a name="next-steps"></a>Następne kroki
W niniejszym artykule możesz przedstawiono sposób dostępu i tooenable informacje diagnostyczne dla platformy Azure. Gdy informacje te są przydatne w opis problemów, które występują w przypadku aplikacji, może wskazywać problem tooa z modułu, którego używasz lub ta wersja hello Node.js używane przez aplikacje sieci Web usługi aplikacji jest inny niż hello używany we wdrożeniu środowisko.

Informacje w pracy z modułów na platformie Azure, zobacz [przy użyciu modułów Node.js z aplikacjami Azure](../nodejs-use-node-modules-azure-apps.md).

Informacje dotyczące określania wersji środowiska Node.js dla aplikacji, zobacz [określanie wersji środowiska Node.js w aplikacji Azure].

Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów środowiska Node.js](/develop/nodejs/).

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[plik Readme programu IISNode]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[określanie wersji środowiska Node.js w aplikacji Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

