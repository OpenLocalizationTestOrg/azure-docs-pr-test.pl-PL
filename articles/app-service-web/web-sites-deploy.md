---
title: "aaaDeploy tooAzure Twojej aplikacji usługi App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy Twojego tooAzure aplikację usługi aplikacji."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 5c84e4ca502874209d750c94efeb86a59aa71a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service"></a>Wdrażanie sieci tooAzure aplikację usługi aplikacji
Ten artykuł pomaga ustalić hello najlepszych opcji toodeploy hello plików dla aplikacji sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API za[usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)i przeprowadza Cię po tooappropriate zasobów przy użyciu określonych tooyour instrukcje preferowaną opcję.

## <a name="overview"></a>Omówienie wdrożenia usługi Azure App Service
Usługa aplikacji Azure obsługuje struktury aplikacji hello automatycznie (ASP.NET, PHP, Node.js itp.). Niektóre struktury są włączone domyślnie, podczas gdy inne, takie jak Java i Python, może być konieczne tooenable konfiguracji prostego wyboru go. Ponadto można dostosować z struktury aplikacji, takich jak wersja PHP hello lub bitowości hello Twojego środowiska uruchomieniowego. Aby uzyskać więcej informacji, zobacz [Konfigurowanie aplikacji w usłudze Azure App Service](web-sites-configure.md).

Ponieważ nie masz tooworry o hello framework serwer lub aplikacja sieci web, wdrażanie tooApp Twojej aplikacji usługi jest kwestią wdrażanie kodu, pliki binarne, pliki zawartości i struktury ich odpowiednich katalogów, toohello [   **/lokacji /Wwwroot** katalogu](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) na platformie Azure (lub hello **/lokacji/wwwroot/App_Data/zadania/** katalogu dla zadań Webjob). Usługa aplikacji obsługuje trzy procesy inne wdrożenie. Wszystkich metod wdrażania hello w tym artykule, użyj jednej z hello następujących procesów: 

* [FTP i FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): korzystania z ulubionych FTP lub FTPS można włączyć narzędzia toomove Twojego tooAzure pliki [FileZilla](https://filezilla-project.org) umieszczony toofull IDEs, takich jak [NetBeans](https://netbeans.org). Jest to ściśle procesu przekazywania plików. Żadnych dodatkowych usług są dostarczane przez usługę App Service, takich jak kontrola wersji, zarządzanie struktury plików itp. 
* [Aparat kudu (Git/Mercurial lub OneDrive/Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): hello jest Kudu [aparat wdrażania](https://github.com/projectkudu/kudu/wiki) w usłudze App Service. Wypchnij tooKudu Twojego kodu bezpośrednio z dowolnym repozytorium. Program kudu udostępnia również dodany usług zawsze, gdy kod spoczywa tooit, łącznie z kontroli wersji, Przywracanie pakietu MSBuild, i [sieci web punkty zaczepienia](https://github.com/projectkudu/kudu/wiki/Web-hooks) ciągłego wdrażania i inne zadania automatyzacji. Aparat wdrażania Kudu Hello obsługuje 3 różnych rodzajów źródeł wdrażania:   
  
  * Zawartości synchronizacji usługi OneDrive lub Dropbox   
  * Repozytorium na podstawie ciągłego wdrażania z automatyczna synchronizacja z serwisu GitHub, Bitbucket i Visual Studio Team Services  
  * Wdrożenie oparte na repozytorium z ręczną synchronizację z lokalnego repozytorium Git  
* [Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): Wdróż kod tooApp usługi bezpośrednio z programu Microsoft ulubionych narzędzi takich, jak za pomocą programu Visual Studio hello tego samego narzędzia, która automatyzuje serwerów tooIIS wdrożenia. To narzędzie obsługuje tylko do różnicowania wdrożenia, tworzenie bazy danych, transformacje parametry połączenia, itd. Narzędzie Web Deploy różni się od Kudu w tej aplikacji, są tworzone pliki binarne, zanim staną się wdrożyć tooAzure. Podobne tooFTP żadnych dodatkowych usług są dostarczane przez usługę App Service.

Narzędzia deweloperskie popularnych sieci web obsługuje co najmniej jednego z tych procesów wdrażania. Gdy hello narzędzia, możesz wybrać sprawdza hello procesów wdrażania można wykorzystać, hello rzeczywistej funkcji DevOps z dyspozycji zależy od hello kombinację hello procesu wdrażania i hello określone narzędzia wybierzesz. Na przykład, jeśli należy wykonać, narzędzie Web Deploy z: [programu Visual Studio z zestawem Azure SDK](#vspros), nawet jeśli nie otrzymasz automatyzacji przez aparat Kudu, w programie Visual Studio uzyskać Przywracanie pakietu i automatyzacji programu MSBuild. 

> [!NOTE]
> Te procesy wdrażania faktycznie nie [udostępniania hello zasobów Azure](../azure-resource-manager/resource-group-template-deploy-portal.md) który aplikacji może być konieczne. Jednak większość hello połączone jak tooarticles opisano sposób tooprovision hello aplikacji i wdrażania z kodu tooit end-to-end. Możesz również znaleźć dodatkowe opcje inicjowania obsługi administracyjnej zasobów platformy Azure w hello [zautomatyzować wdrożenie za pomocą narzędzia wiersza polecenia](#automate) sekcji.
> 
> 

## <a name="ftp"></a>Ręczne wdrażanie przez przekazywanie plików przy użyciu FTP
Jeśli są używane toomanually kopiowanie serwerze sieci web tooa zawartości sieci web, możesz użyć [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) narzędzie toocopy plików, takich jak Eksplorator Windows lub [FileZilla](https://filezilla-project.org/).

Specjaliści Hello ręcznego kopiowania plików są następujące:

* Ponadto i złożoność minimalnego do oprzyrządowania FTP. 
* Znajomość dokładnie gdzie będą plików.
* Zwiększyć bezpieczeństwo z FTPS.

ręczne kopiowanie plików wad Hello są:

* O tooknow jak toodeploy pliki toohello poprawne katalogów w usłudze App Service. 
* Nie kontroli wersji na potrzeby wycofywania w przypadku wystąpienia awarii.
* Brak historii wdrożenia wbudowanych Rozwiązywanie problemów dotyczących wdrożenia.
* Potencjalne wdrożenia długich okresach, ponieważ wiele narzędzi FTP nie zapewniają różnicowego — tylko do kopiowania i po prostu skopiuj wszystkie pliki hello.  

### <a name="howtoftp"></a>Jak tooupload pliki przy użyciu FTP
Witaj [Azure Portal](https://portal.azure.com) zapewnia wszystkie informacje hello należy katalogów tooconnect tooyour aplikacji przy użyciu FTP i FTPS.

* [Wdrażanie tooAzure Twojej aplikacji usługi App Service przy użyciu protokołu FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Wdrażanie przez synchronizację z folderem, w chmurze
Dobrą alternatywą zbyt[ręcznego kopiowania plików](#ftp) synchronizuje pliki i foldery tooApp usługi z usługą magazynu w chmurze, takich jak OneDrive lub Dropbox. Synchronizowanie z folderem chmury korzysta hello Kudu procesu wdrożenia (zobacz [Przegląd procesów wdrażania](#overview)).

Witaj specjaliści z synchronizację z folderem, w chmurze są następujące:

* Łatwość wdrażania. Usługi jak OneDrive lub Dropbox zapewnić klientom synchronizacji pulpitu, więc lokalny katalog roboczy jest również katalogu wdrożenia.
* Wdrażanie jednego kliknięcia.
* Wszystkie funkcje w aparat wdrażania Kudu hello jest dostępna (np. Przywracanie pakietu, automatyzacji).

Witaj wad synchronizację z folderem, w chmurze są następujące:

* Nie kontroli wersji na potrzeby wycofywania w przypadku wystąpienia awarii.
* Nie zautomatyzowanego wdrażania ręczną synchronizację jest wymagana.

### <a name="howtodropbox"></a>Jak toodeploy przez synchronizację z folderem, w chmurze
W hello [Azure Portal](https://portal.azure.com), możesz wyznaczyć folder do synchronizacji zawartości w magazynie w chmurze usługi OneDrive lub Dropbox, Praca z kodu aplikacji i zawartości w tym folderze, a tooApp synchronizacji usługi z powitania kliknij przycisku.

* [Synchronizowanie zawartości z chmury tooAzure folderu usługi aplikacji](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Wdrażanie stale z usługi kontroli źródła w chmurze
Jeśli zespół deweloperów używa usługi zarządzania (SCM) kodu źródłowego oparte na chmurze, takiej jak [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), lub [BitBucket](https://bitbucket.org/), można skonfigurować aplikacji Usługi toointegrate z repozytorium i wdrożyć w sposób ciągły. 

Specjaliści Hello wdrażania z usługi kontroli źródła oparte na chmurze są następujące:

* Wycofywanie tooenable kontroli wersji.
* Możliwość tooconfigure ciągłego wdrażania dla Git (i Mercurial, jeśli ma to zastosowanie) repozytoriów. 
* Wdrożenie specyficzne dla gałęzi, można wdrożyć różnych gałęziach toodifferent [miejsc](web-sites-staged-publishing.md).
* Wszystkie funkcje w aparat wdrażania Kudu hello jest dostępna (np. versioning wdrożenia, wycofywanie, Przywracanie pakietu, automatyzacji).

Kon Hello wdrażania z usługi kontroli źródła oparte na chmurze jest:

* Niektóre wiedzy hello odpowiednich SCM usługa wymagana.

### <a name="vsts"></a>Metody kontrolowania przez toodeploy stale ze źródła oparte na chmurze usługi
W hello [Azure Portal](https://portal.azure.com), można skonfigurować ciągłego wdrażania od serwisu GitHub, Bitbucket i Visual Studio Team Services.

* [TooAzure ciągłej wdrożenia usługi App Service](app-service-continuous-deployment.md). 

toofind się jak tooconfigure ciągłe wdrażanie ręcznie z repozytorium chmury nie są wyświetlane według hello portalu Azure (takich jak [GitLab](https://gitlab.com/)), zobacz [Konfigurowanie ciągłego wdrażania przy użyciu ręczne](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Wdrażanie z lokalnego repozytorium Git
Jeśli zespół deweloperów używa lokalnego źródła lokalnego kodu usługi zarządzania (SCM) oparte na Git, można to skonfigurować jako tooApp źródło wdrożenia usługi. 

Specjaliści wdrażania z lokalnego repozytorium Git są:

* Wycofywanie tooenable kontroli wersji.
* Wdrożenie specyficzne dla gałęzi, można wdrożyć różnych gałęziach toodifferent [miejsc](web-sites-staged-publishing.md).
* Wszystkie funkcje w aparat wdrażania Kudu hello jest dostępna (np. versioning wdrożenia, wycofywanie, Przywracanie pakietu, automatyzacji).

Cons wdrażania z lokalnego repozytorium Git jest:

* Niektóre wiedzy hello odpowiednich systemu SCM wymagane.
* Nie rozwiązań gotowe do ciągłego wdrażania. 

### <a name="vsts"></a>Jak toodeploy z lokalnego repozytorium Git
W hello [Azure Portal](https://portal.azure.com), można skonfigurować lokalnego wdrożenia usługi Git.

* [Lokalnego wdrożenia Git tooAzure usługi aplikacji](app-service-deploy-local-git.md). 
* [Publikowanie aplikacji tooWeb z dowolnym repozytorium git/hg](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Wdrażanie przy użyciu środowiska IDE
Jeśli korzystasz już z [programu Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) z [zestawu Azure SDK](https://azure.microsoft.com/downloads/), lub innych mechanizmów IDE, takich jak [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), i [ IntelliJ IDEA](https://www.jetbrains.com/idea/), tooAzure bezpośrednio z można wdrożyć w ramach programu IDE. Ta opcja jest idealny dla poszczególnych deweloperów.

Visual Studio obsługuje wszystkie procesy wdrażania trzy (FTP, Git i Web Deploy), w zależności od swoich preferencji, a inne IDEs można wdrożyć tooApp usługi, jeśli dysponują integracji FTP lub Git (zobacz [Przegląd procesów wdrażania](#overview)).

Specjaliści Hello wdrażania przy użyciu IDE są:

* Potencjalnie zminimalizować hello narzędzi dla cyklu życia Twojej aplikacji na trasie. Tworzenie, debugowanie, śledzenie i wdrażanie tooAzure Twojej aplikacji bez przenoszenia poza środowiskiem IDE. 

Wdrażanie przy użyciu IDE wad Hello są:

* Dodano złożoności narzędzi.
* Nadal wymaga systemu kontroli źródła dla projektu zespołowego.

<a name="vspros"></a>Dostępne są następujące dodatkowe specjaliści wdrażania przy użyciu programu Visual Studio z zestawem Azure SDK:

* Zestaw Azure SDK sprawia, że zasoby platformy Azure obywateli pierwszej klasy w programie Visual Studio. Utwórz, Usuń edytować, uruchomić i zatrzymać aplikacji, zapytania hello wewnętrznej bazy danych SQL w bazie danych debugowania na żywo hello aplikacji Azure i wiele innych. 
* Na żywo edycji plików kodu na platformie Azure.
* Na platformie Azure na żywo debugowania aplikacji.
* Zintegrowane explorer platformy Azure.
* Wdrażanie tylko do porównania. 

### <a name="vs"></a>Jak toodeploy bezpośrednio z programu Visual Studio
* [Wprowadzenie do platformy Azure i ASP.NET](app-service-web-get-started-dotnet.md). Jak toocreate i wdrażanie prostego projektu sieci web platformy ASP.NET MVC przy użyciu programu Visual Studio i Web Deploy.
* [Jak tooDeploy zadań Webjob Azure przy użyciu programu Visual Studio](websites-dotnet-deploy-webjobs.md). Jak tooconfigure aplikacji konsoli projektów, tak aby ich wdrażanie jako zadań Webjob.  
* [Wdrażanie sieci Web ASP.NET przy użyciu programu Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). 12 części samouczka serię, która obejmuje szereg bardziej szczegółowy zadania wdrażania niż inne hello na tej liście. Niektóre funkcje wdrożenia usługi Azure zostały dodane, ponieważ samouczek hello zostało zapisane, ale notatki później dodane wyjaśniają, czego brakuje.
* [Wdrażanie tooAzure witryny ASP.NET w programie Visual Studio 2012 z repozytorium Git bezpośrednio](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). W tym artykule wyjaśniono, jak toodeploy sieci web ASP.NET projektu programu Visual Studio za pomocą hello Git toocommit wtyczki hello kodu tooGit i łączenie Azure toohello repozytorium Git. Począwszy od programu Visual Studio 2013 obsługi systemu Git jest wbudowana i nie wymagają instalacji dodatku typu plug-in.

### <a name="aztk"></a>Jak przy użyciu toodeploy hello zestaw narzędzi platformy Azure dla programu Eclipse i IntelliJ IDEA
Microsoft ułatwia możliwe toodeploy tooAzure aplikacje sieci Web bezpośrednio z programu Eclipse i IntelliJ za pośrednictwem hello [zestawu narzędzi platformy Azure dla programu Eclipse](../azure-toolkit-for-eclipse.md) i [narzędzi Azure dla IntelliJ](../azure-toolkit-for-intellij.md). Witaj następujące samouczki przedstawiają hello kroki, które nie są związane z wdrażaniem aplikacji sieci Web tooAzure world prosty tekst "Hello", przy użyciu albo IDE:

* [Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). W tym samouczku przedstawiono sposób toouse hello Azure zestawu narzędzi dla programu Eclipse toocreate i wdrażania aplikacji sieci Web Hello World na platformie Azure.
* [Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). W tym samouczku przedstawiono sposób toouse hello Azure zestawu narzędzi dla IntelliJ toocreate i wdrażania aplikacji sieci Web Hello World na platformie Azure.

## <a name="automate"></a>Zautomatyzować wdrożenie za pomocą narzędzia wiersza polecenia
Jeśli wolisz terminal wiersza polecenia hello jako środowisko projektowe hello wyboru można skrypt zadania wdrażania dla aplikacji usługi App Service przy użyciu narzędzia wiersza polecenia. 

Specjaliści z wdrożenia za pomocą narzędzia wiersza polecenia są:

* Umożliwia pisanie skryptów scenariuszy wdrażania.
* Integracja udostępniania zasobów platformy Azure i wdrażanie kodu.
* Włączenie wdrożenia usługi Azure do istniejących ciągłej integracji skryptów.

Cons wdrażania przy użyciu narzędzia wiersza polecenia są:

* Nie dla deweloperów preferowanie graficznego interfejsu użytkownika.

### <a name="automatehow"></a>Jak wdrażanie tooautomate za pomocą narzędzia wiersza polecenia

Zobacz [automatyzację wdrażania aplikacji Azure za pomocą narzędzia wiersza polecenia](app-service-deploy-command-line.md) listę wiersza polecenia tootutorials narzędzi i linki. 

## <a name="nextsteps"></a>Następne kroki
W niektórych scenariuszach może być toobe tooeasily można przełączać jej i z powrotem między przemieszczania i wersji produkcyjnej aplikacji. Aby uzyskać więcej informacji, zobacz [przemieszczane wdrożenia aplikacji sieci Web](web-sites-staged-publishing.md).

Posiadanie planu tworzenia kopii zapasowej i przywracania jest ważnym elementem każdy przepływ pracy wdrożenia. Uzyskać informacji o hello usługi aplikacji kopii zapasowej i przywracania funkcji, zobacz [kopie zapasowe aplikacji sieci Web](web-sites-backup.md).  

Aby dowiedzieć się jak toomanage kontroli dostępu opartej na roli toouse Azure uzyskują dostęp do wdrożenia usługi tooApp, zobacz [RBAC i publikowania aplikacji sieci Web](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

