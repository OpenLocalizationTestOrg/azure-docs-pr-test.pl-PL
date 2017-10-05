---
title: "Wdrażanie aplikacji w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrożyć aplikację w usłudze Azure App Service."
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
ms.openlocfilehash: f41be4e00a9250b07ca260c2858e5fc45143f746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-azure-app-service"></a>Wdrażanie aplikacji w usłudze Azure App Service
Ten artykuł ułatwia określenie najlepszej opcji wdrażania plików dla aplikacji sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)i przeprowadza Cię do odpowiednich zasobów przy użyciu instrukcji specyficznych dla preferowaną opcję.

## <a name="overview"></a>Omówienie wdrożenia usługi Azure App Service
Usługa aplikacji Azure obsługuje struktury aplikacji dla Ciebie (ASP.NET, PHP, Node.js itp.). Niektóre struktury są włączone domyślnie, podczas gdy inne, takie jak Java i Python, może być konieczne konfiguracji proste znacznik wyboru, aby je włączyć. Ponadto można dostosować z struktury aplikacji, takich jak wersja PHP lub bitowości programu runtime. Aby uzyskać więcej informacji, zobacz [Konfigurowanie aplikacji w usłudze Azure App Service](web-sites-configure.md).

Ponieważ nie trzeba martwić struktury serwera lub aplikacji sieci web, wdrażanie aplikacji do usługi App Service jest wdrażanie kodu, pliki binarne, pliki zawartości i struktury ich odpowiednich katalogu, do sprawę [ **/lokacji/wwwroot** katalogu](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) na platformie Azure (lub **/lokacji/wwwroot/App_Data/zadania/** katalogu dla zadań Webjob). Usługa aplikacji obsługuje trzy procesy inne wdrożenie. Wszystkich metod wdrażania, w tym artykule, użyj jednej z poniższych procedur: 

* [FTP i FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): Korzystanie z ulubionych FTP lub FTPS włączone narzędzia do przenoszenia plików do platformy Azure, z [FileZilla](https://filezilla-project.org) do IDEs oferujący wszystkie funkcje, takie jak [NetBeans](https://netbeans.org). Jest to ściśle procesu przekazywania plików. Żadnych dodatkowych usług są dostarczane przez usługę App Service, takich jak kontrola wersji, zarządzanie struktury plików itp. 
* [Aparat kudu (Git/Mercurial lub OneDrive/Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu jest [aparat wdrażania](https://github.com/projectkudu/kudu/wiki) w usłudze App Service. Wypychanie kodu do Kudu bezpośrednio z dowolnym repozytorium. Program kudu udostępnia również dodany usług zawsze, gdy kod jest wypychana do niego, łącznie z kontroli wersji, Przywracanie pakietu MSBuild, i [sieci web punkty zaczepienia](https://github.com/projectkudu/kudu/wiki/Web-hooks) ciągłego wdrażania i inne zadania automatyzacji. Aparat wdrażania Kudu obsługuje 3 różnych rodzajów źródeł wdrażania:   
  
  * Zawartości synchronizacji usługi OneDrive lub Dropbox   
  * Repozytorium na podstawie ciągłego wdrażania z automatyczna synchronizacja z serwisu GitHub, Bitbucket i Visual Studio Team Services  
  * Wdrożenie oparte na repozytorium z ręczną synchronizację z lokalnego repozytorium Git  
* [Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): Wdróż kod, aby usługi aplikacji — bezpośrednio z programu Microsoft ulubionych narzędzi takich jak Visual Studio korzystającej z tego samego narzędzia, która automatyzuje wdrożenia do serwerów IIS. To narzędzie obsługuje tylko do różnicowania wdrożenia, tworzenie bazy danych, transformacje parametry połączenia, itd. Narzędzie Web Deploy różni się od Kudu, w tym plików binarnych aplikacji są wbudowane, przed ich wdrożeniem na platformie Azure. Podobnie jak FTP, żadnych dodatkowych usług są dostarczane przez usługę App Service.

Narzędzia deweloperskie popularnych sieci web obsługuje co najmniej jednego z tych procesów wdrażania. Gdy narzędzie, które możesz wybrać sprawdza procesów wdrażania, które można wykorzystać, rzeczywistej funkcji DevOps dyspozycji użytkownika zależy od kombinacji procesu wdrażania i określone narzędzia, możesz wybrać. Na przykład, jeśli należy wykonać, narzędzie Web Deploy z: [programu Visual Studio z zestawem Azure SDK](#vspros), nawet jeśli nie otrzymasz automatyzacji przez aparat Kudu, w programie Visual Studio uzyskać Przywracanie pakietu i automatyzacji programu MSBuild. 

> [!NOTE]
> Te procesy wdrażania faktycznie nie [udostępniania zasobów Azure](../azure-resource-manager/resource-group-template-deploy-portal.md) który aplikacji może być konieczne. Jednak większość połączonego artykuły pokazano, jak udostępnić aplikacji i wdrażania kodu na trasie. Możesz również znaleźć dodatkowe opcje inicjowania obsługi administracyjnej zasobów platformy Azure w [zautomatyzować wdrożenie za pomocą narzędzia wiersza polecenia](#automate) sekcji.
> 
> 

## <a name="ftp"></a>Ręczne wdrażanie przez przekazywanie plików przy użyciu FTP
Jeśli są używane do ręczne kopiowanie zawartości sieci web na serwerze sieci web, możesz użyć [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) narzędzie do kopiowania plików, takich jak Eksplorator Windows lub [FileZilla](https://filezilla-project.org/).

Specjaliści z ręcznego kopiowania plików są następujące:

* Ponadto i złożoność minimalnego do oprzyrządowania FTP. 
* Znajomość dokładnie gdzie będą plików.
* Zwiększyć bezpieczeństwo z FTPS.

Wad ręcznego kopiowania plików są następujące:

* Konieczności wiedzieć, jak wdrożyć pliki poprawne katalogów w usłudze App Service. 
* Nie kontroli wersji na potrzeby wycofywania w przypadku wystąpienia awarii.
* Brak historii wdrożenia wbudowanych Rozwiązywanie problemów dotyczących wdrożenia.
* Potencjalne wdrożenia długich okresach, ponieważ wiele narzędzi FTP nie zapewniają różnicowego — tylko do kopiowania i po prostu skopiuj wszystkie pliki.  

### <a name="howtoftp"></a>Sposób przekazywania plików przy użyciu FTP
[Azure Portal](https://portal.azure.com) zapewnia wszystkie informacje potrzebne do nawiązania połączenia przy użyciu FTP i FTPS katalogów aplikacji.

* [Wdrażanie aplikacji w usłudze Azure App Service przy użyciu protokołu FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Wdrażanie przez synchronizację z folderem, w chmurze
Dobrą alternatywą do [ręcznego kopiowania plików](#ftp) synchronizuje pliki i foldery do aplikacji usługi z usługą magazynu w chmurze, takich jak OneDrive lub Dropbox. Synchronizowanie z folderem chmury korzysta z procesu wdrażania Kudu (zobacz [Przegląd procesów wdrażania](#overview)).

Specjaliści z synchronizację z folderem, w chmurze są następujące:

* Łatwość wdrażania. Usługi jak OneDrive lub Dropbox zapewnić klientom synchronizacji pulpitu, więc lokalny katalog roboczy jest również katalogu wdrożenia.
* Wdrażanie jednego kliknięcia.
* Znajduje wszystkie funkcje w aparat wdrażania Kudu (np. Przywracanie pakietu, automatyzacji).

Wad synchronizację z folderem, w chmurze są następujące:

* Nie kontroli wersji na potrzeby wycofywania w przypadku wystąpienia awarii.
* Nie zautomatyzowanego wdrażania ręczną synchronizację jest wymagana.

### <a name="howtodropbox"></a>Jak wdrożyć przez synchronizację z folderem, w chmurze
W [Azure Portal](https://portal.azure.com), można wyznaczyć folder do synchronizacji zawartości w magazynie w chmurze usługi OneDrive lub Dropbox, pracy z kodu aplikacji, a zawartość w tym folderze oraz synchronizacji w usłudze App Service z kliknięcie przycisku.

* [Synchronizowanie zawartości z folderu chmury w usłudze Azure App Service](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Wdrażanie stale z usługi kontroli źródła w chmurze
Jeśli zespół deweloperów używa usługi zarządzania (SCM) kodu źródłowego oparte na chmurze, takiej jak [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), lub [BitBucket](https://bitbucket.org/), można skonfigurować usługę aplikacji do integracji z repozytorium i wdrożyć w sposób ciągły. 

Specjaliści wdrażania z usługi kontroli źródła oparte na chmurze są następujące:

* Kontrola wersji, aby umożliwić wycofanie.
* Konfigurowanie ciągłego wdrażania dla Git (i Mercurial, jeśli ma to zastosowanie) repozytoriów. 
* Wdrożenie specyficzne dla gałęzi, można wdrożyć różnych gałęziach do różnych [miejsc](web-sites-staged-publishing.md).
* Znajduje wszystkie funkcje w aparat wdrażania Kudu (np. versioning wdrożenia, wycofywanie, Przywracanie pakietu, automatyzacji).

Kon wdrażania z usługi kontroli źródła oparte na chmurze jest:

* Niektóre znajomość odpowiedniej usługi SCM wymagane.

### <a name="vsts"></a>Jak wdrożyć stale z usługi kontroli źródła w chmurze
W [Azure Portal](https://portal.azure.com), można skonfigurować ciągłego wdrażania od serwisu GitHub, Bitbucket i Visual Studio Team Services.

* [Wdrożenie ciągłej w usłudze Azure App Service](app-service-continuous-deployment.md). 

Aby dowiedzieć się, jak skonfigurować ciągłe wdrażanie ręcznie z repozytorium chmury nie są wyświetlane w portalu Azure (takich jak [GitLab](https://gitlab.com/)), zobacz [Konfigurowanie ciągłego wdrażania przy użyciu ręczne](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Wdrażanie z lokalnego repozytorium Git
Jeśli zespół deweloperów używa lokalnego źródła lokalnego kodu usługi zarządzania (SCM) oparte na Git, można skonfigurować to jako źródło wdrożenia do usługi App Service. 

Specjaliści wdrażania z lokalnego repozytorium Git są:

* Kontrola wersji, aby umożliwić wycofanie.
* Wdrożenie specyficzne dla gałęzi, można wdrożyć różnych gałęziach do różnych [miejsc](web-sites-staged-publishing.md).
* Znajduje wszystkie funkcje w aparat wdrażania Kudu (np. versioning wdrożenia, wycofywanie, Przywracanie pakietu, automatyzacji).

Cons wdrażania z lokalnego repozytorium Git jest:

* Niektóre znajomość odpowiedniej systemu SCM wymagane.
* Nie rozwiązań gotowe do ciągłego wdrażania. 

### <a name="vsts"></a>Wdrażanie z lokalnego repozytorium Git
W [Azure Portal](https://portal.azure.com), można skonfigurować lokalnego wdrożenia usługi Git.

* [Wdrażanie Git lokalnego do usługi Azure App Service](app-service-deploy-local-git.md). 
* [Publikowanie aplikacji sieci Web z dowolnym repozytorium git/hg](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Wdrażanie przy użyciu środowiska IDE
Jeśli korzystasz już z [programu Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) z [zestawu Azure SDK](https://azure.microsoft.com/downloads/), lub innych mechanizmów IDE, takich jak [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), i [IntelliJ IDEA](https://www.jetbrains.com/idea/), można wdrożyć na platformie Azure bezpośrednio z wewnątrz środowiskiem IDE. Ta opcja jest idealny dla poszczególnych deweloperów.

Program Visual Studio obsługuje wszystkie procesy wdrażania trzy (FTP, Git i Web Deploy), w zależności od swoich preferencji, podczas gdy inne IDEs można wdrożyć do usługi App Service, gdy mają integracji FTP lub Git (zobacz [Przegląd procesów wdrażania](#overview)).

Specjaliści z wdrożenia za pomocą środowiska IDE są:

* Potencjalnie zminimalizować narzędzi dla cyklu życia Twojej aplikacji na trasie. Tworzenie, debugowanie, śledzenie i wdrażanie aplikacji w usłudze Azure wszystkie bez przenoszenia poza środowiskiem IDE. 

Wad wdrażanie przy użyciu IDE są:

* Dodano złożoności narzędzi.
* Nadal wymaga systemu kontroli źródła dla projektu zespołowego.

<a name="vspros"></a>Dostępne są następujące dodatkowe specjaliści wdrażania przy użyciu programu Visual Studio z zestawem Azure SDK:

* Zestaw Azure SDK sprawia, że zasoby platformy Azure obywateli pierwszej klasy w programie Visual Studio. Tworzenia, usuwania, edytować, uruchomić i Zatrzymaj aplikacji, wewnętrznej bazy danych SQL w bazie danych, live debugowania aplikacji Azure i o wiele więcej. 
* Na żywo edycji plików kodu na platformie Azure.
* Na platformie Azure na żywo debugowania aplikacji.
* Zintegrowane explorer platformy Azure.
* Wdrażanie tylko do porównania. 

### <a name="vs"></a>Jak wdrożyć bezpośrednio z programu Visual Studio
* [Wprowadzenie do platformy Azure i ASP.NET](app-service-web-get-started-dotnet.md). Sposób tworzenia i wdrażania prostego projektu sieci web platformy ASP.NET MVC przy użyciu programu Visual Studio i Web Deploy.
* [Jak wdrożyć zadań Webjob Azure przy użyciu programu Visual Studio](websites-dotnet-deploy-webjobs.md). Jak skonfigurować projektów aplikacji konsoli, tak aby ich wdrożyć jako zadań Webjob.  
* [Wdrażanie sieci Web ASP.NET przy użyciu programu Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). 12 części samouczka serię, która obejmuje więcej pełną gamę zadań wdrożeniowych niż inne, na tej liście. Niektóre funkcje wdrożenia usługi Azure zostały dodane, ponieważ samouczka zostało zapisane, ale notatki później dodane wyjaśniają, czego brakuje.
* [Wdrażanie witryny internetowej ASP.NET na platformie Azure w programie Visual Studio 2012 z repozytorium Git bezpośrednio](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Wyjaśniono, jak wdrożyć projekt sieci web ASP.NET w programie Visual Studio przy użyciu usługi Git wtyczki można przekazać kod do usługi Git i łączenia Azure do repozytorium Git. Począwszy od programu Visual Studio 2013 obsługi systemu Git jest wbudowana i nie wymagają instalacji dodatku typu plug-in.

### <a name="aztk"></a>Jak wdrożyć za pomocą narzędzi Azure dla programu Eclipse i IntelliJ IDEA
Microsoft umożliwia wdrażanie aplikacji sieci Web na platformie Azure bezpośrednio z programu Eclipse i IntelliJ za pośrednictwem [zestawu narzędzi platformy Azure dla programu Eclipse](../azure-toolkit-for-eclipse.md) i [narzędzi Azure dla IntelliJ](../azure-toolkit-for-intellij.md). Następujące samouczki przedstawiono kroki, które nie są związane z wdrażaniem world prosty tekst "Hello" aplikacja sieci Web na platformie Azure przy użyciu albo IDE:

* [Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). Ten samouczek pokazuje, jak używać zestawu narzędzi platformy Azure dla programu Eclipse do tworzenia i wdrażania Hello World aplikacji sieci Web dla platformy Azure.
* [Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). W tym samouczku przedstawiono sposób Toolkit Azure for IntelliJ umożliwia tworzenie i wdrażanie Hello World aplikacji sieci Web dla platformy Azure.

## <a name="automate"></a>Zautomatyzować wdrożenie za pomocą narzędzia wiersza polecenia
Jeśli wolisz terminal wiersza polecenia jako środowisko projektowe wyboru można skrypt zadania wdrażania dla aplikacji usługi App Service przy użyciu narzędzia wiersza polecenia. 

Specjaliści z wdrożenia za pomocą narzędzia wiersza polecenia są:

* Umożliwia pisanie skryptów scenariuszy wdrażania.
* Integracja udostępniania zasobów platformy Azure i wdrażanie kodu.
* Włączenie wdrożenia usługi Azure do istniejących ciągłej integracji skryptów.

Cons wdrażania przy użyciu narzędzia wiersza polecenia są:

* Nie dla deweloperów preferowanie graficznego interfejsu użytkownika.

### <a name="automatehow"></a>Jak zautomatyzować wdrażanie za pomocą narzędzia wiersza polecenia

Zobacz [automatyzację wdrażania aplikacji Azure za pomocą narzędzia wiersza polecenia](app-service-deploy-command-line.md) listę narzędzi wiersza polecenia i linki do samouczki. 

## <a name="nextsteps"></a>Następne kroki
W niektórych scenariuszach może być można było łatwo przełączać się między przemieszczania i wersji produkcyjnej aplikacji. Aby uzyskać więcej informacji, zobacz [przemieszczane wdrożenia aplikacji sieci Web](web-sites-staged-publishing.md).

Posiadanie planu tworzenia kopii zapasowej i przywracania jest ważnym elementem każdy przepływ pracy wdrożenia. Informacje o usłudze aplikacji kopii zapasowej i przywracanie funkcji, zobacz [kopie zapasowe aplikacji sieci Web](web-sites-backup.md).  

Aby uzyskać informacje o sposobie używania kontroli dostępu opartej na rolach platformy Azure, aby zarządzać dostępem do wdrożenia usługi App Service, zobacz [RBAC i publikowania aplikacji sieci Web](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

