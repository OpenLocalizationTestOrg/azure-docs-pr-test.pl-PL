---
title: "Rozpoczęto aaaGet przewodnik dla deweloperów na platformie Azure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera ważne informacje dla deweloperów wyszukiwania tooget uruchomić za pomocą platformy Microsoft Azure hello do swoich potrzeb."
services: 
cloud: 
documentationcenter: 
author: ggailey777
manager: erikre
ms.assetid: 
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: glenga
ms.openlocfilehash: 72dc2678db7738923d4bc7783e297fea6fcded83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-guide-for-azure-developers"></a>Przewodnik dla początkujących deweloperów platformy Azure

## <a name="what-is-azure"></a>Co to jest system Azure?

Azure to platforma pełnej chmury hosta istniejących aplikacji, upraszcza programowanie hello nowych aplikacji i nawet zwiększenia lokalnych aplikacji. Azure integruje hello konieczność toodevelop usługi w chmurze, testów, wdrażania i zarządzania aplikacji — wykorzystując efektywność hello chmury obliczeniowej.

Obsługując aplikacji na platformie Azure, możesz rozpoczęcie od czegoś małego i łatwego skalowania aplikacji wraz z rozwojem Twoje żądanie klienta. System Azure oferuje również niezawodności hello jest potrzebne w przypadku aplikacji wysokiej dostępności, nawet w tym tryb failover między różnych regionach. Witaj [portalu Azure](https://portal.azure.com) umożliwia łatwe zarządzanie wszystkich usług platformy Azure. Usługi można również zarządzać programowo przy użyciu interfejsów API i szablony specyficzne dla usługi.

**Kto powinien przeczytać**: ten przewodnik jest wprowadzenie toohello platformy Azure dla deweloperów aplikacji. Zawiera również wskazówki i kierunek konieczność toostart tworzenie nowych aplikacji w Azure, jak i migracji istniejącej tooAzure aplikacji.

## <a name="where-do-i-start"></a>Od czego zacząć?

Ze wszystkimi usługami hello, które platforma Azure oferuje może być czasochłonnym zadaniem toofigure zadań limit usług, które należy toosupport architektury rozwiązania. Ta sekcja najważniejsze funkcje hello Azure usług, deweloperzy zazwyczaj używają. Aby uzyskać listę wszystkich usług platformy Azure, zobacz hello [dokumentacji platformy Azure](../../index.md).

Najpierw należy zdecydować, jak toohost aplikacji na platformie Azure. Czy potrzebna jest toomanage całej infrastruktury jako maszynę wirtualną (VM). Można użyć hello platformy zarządzania urządzeń, które platforma Azure udostępnia? Może być konieczne wykonanie kodu toohost niekorzystającą framework tylko?

Aplikacja wymaga magazynu w chmurze, która Azure zapewnia kilka opcji. Można korzystać z uwierzytelniania enterprise platformy Azure. Dostępne są również narzędzia do programowania opartego na chmurze i monitorowania i większość usług hostingu oferują DevOps integracji.

Teraz przyjrzymy hello określonych usług, które są zalecane do badania dla aplikacji.

### <a name="application-hosting"></a>Obsługa aplikacji

Platforma Azure udostępnia kilka obliczeń oparte na chmurze ofert toorun aplikacji dzięki czemu nie trzeba tooworry o hello infrastruktury szczegóły. Możesz łatwo skalowanie w górę lub skalowania zasobów wraz z rozwojem korzystania z aplikacji.

System Azure oferuje usług, które obsługują programowania aplikacji i hostingu potrzeb. Platforma Azure udostępnia infrastrukturę jako — usługa (IaaS) toogive pełnej kontroli nad hosting aplikacji. Azure platforma jako usługa (PaaS) ofert zapewniają hello pełni zarządzane toopower usług potrzebnych aplikacji. Istnieje nawet true niekorzystającą hostingu na platformie Azure gdzie toodo wystarczy wpisz swój kod.

![Hosting Opcje aplikacji Azure](./media/azure-developer-guide/azure-developer-hosting-options.png)


#### <a name="azure-app-service"></a>Azure App Service 

Najszybszym toopublish ścieżka hello projektów sieci web, należy wziąć pod uwagę usłudze Azure App Service. Usługa App Service udostępnia prosty tooextend użytkownika sieci web toosupport aplikacji mobilnych klientów i opublikować łatwo wykorzystanych interfejsów API REST. Ta platforma umożliwia uwierzytelnianie przy użyciu dostawców sieci społecznościowych, na podstawie ruchu Skalowanie automatyczne testowanie w produkcji i wdrożeń ciągły i na podstawie kontenera.

Po utworzeniu aplikacji w usłudze App Service wybierz hello następujące typy:

- [Web Apps](../../app-service-web/app-service-web-overview.md): umożliwia hostowanie witryny sieci Web i aplikacji sieci web napisane w programie .NET, Java, PHP, Node.js i Python.

- [Aplikacje mobilne](../../app-service-mobile/app-service-mobile-value-prop.md): rozszerzenie aplikacji sieci Web toosupport dostępu z urządzeń przenośnych. Umożliwia uwierzytelnianie za pomocą dostawców sieci społecznościowych i Azure Active Directory (Azure AD), zawiera magazynu wewnętrznej bazy danych i integruje się z [usługi Azure Notification Hubs](../../notification-hubs/notification-hubs-push-notification-overview.md) dla powiadomień wypychanych.

- [Aplikacje interfejsu API](../../app-service-api/app-service-api-apps-why-best-platform.md): pozwala bezpiecznie ujawnia swoje interfejsy API w chmurze hello z metadanych struktury Swagger, dzięki czemu można je łatwo korzystać z klientów.

Ponieważ udział wszystkich trzema typami aplikacji hello środowiska uruchomieniowego usługi aplikacji, hosta witryny sieci Web, obsługuje klientów mobilnych i ujawnia swoje interfejsy API na platformie Azure z hello tego samego projektu lub rozwiązania. toolearn więcej informacji na temat usługi aplikacji, zobacz [jak działa usługa App](../../app-service/app-service-how-works-readme.md).

Usługi aplikacji został zaprojektowany z DevOps zdanie. Obsługuje ona różnych narzędzi do publikowania, jak i ciągłych wdrożeń integracji, w tym GitHub elementów webhook, Wpięć usługi Visual Studio Team Services, TeamCity i inne.

Przeprowadzić migrację istniejących tooApp aplikacji usługi za pomocą hello [narzędzia migracji w trybie online](https://www.migratetoazure.net/).

>**Gdy toouse**: Użyj usługi aplikacji podczas migrowania istniejących tooAzure aplikacji sieci web, oraz gdy są potrzebne pełni zarządzana Platforma macierzysta dla aplikacji sieci web. Umożliwia także usługi aplikacji muszą toosupport klientów mobilnych lub uwidacznia interfejsów API REST z aplikacją.

>**Rozpoczynanie pracy**: App Service umożliwia łatwe toocreate i wdrażanie pierwszej [aplikacji sieci web](../../app-service-web/web-sites-dotnet-get-started.md), [aplikacji mobilnej](../../app-service-mobile/app-service-mobile-ios-get-started.md), lub [aplikacji interfejsu API](../../app-service-api/app-service-api-dotnet-get-started.md).

>**Wypróbuj teraz**: Usługa App Service umożliwia udostępnianie platformę hello tootry tej aplikacji bez konieczności toosign dla konta platformy Azure. Spróbuj hello platformy i [Utwórz aplikację usługi aplikacji Azure](https://tryappservice.azure.com/).

#### <a name="azure-virtual-machines"></a>Azure Virtual Machines

Funkcję dostawcy infrastruktury jako — usługa (IaaS), Azure umożliwia wdrażanie tooor migracji z tooeither aplikacji systemu Windows lub maszyn wirtualnych systemu Linux. Wraz z sieci wirtualnej platformy Azure maszyny wirtualne Azure obsługuje wdrażanie hello tooAzure systemu Windows lub maszyn wirtualnych systemu Linux. Z maszynami wirtualnymi masz pełną kontrolę nad konfiguracji hello hello maszyny. Podczas korzystania z maszyn wirtualnych, wszystko jest odpowiedzialny za serwer instalacji, konfiguracji, obsługi i systemu operacyjnego poprawek oprogramowania.

Ze względu na powitania poziom kontroli maszyn wirtualnych można uruchomić wielu obciążeń serwera na platformie Azure, która nie pasuje do modelu PaaS. Takie obciążenia zawierają serwery baz danych, usługi Active Directory systemu Windows Server i Microsoft SharePoint. Aby uzyskać więcej informacji, zobacz dokumentację maszyn wirtualnych hello jednego [Linux](/azure/virtual-machines/linux/) lub [Windows](/azure/virtual-machines/windows/).

>**Gdy toouse**: Użyj maszyn wirtualnych podczas mają pełną kontrolę nad Twojej aplikacji infrastruktury lub toomigrate lokalnej aplikacji obciążeń tooAzure bez konieczności zmiany toomake.

>**Rozpoczynanie pracy**: tworzenie [maszyny Wirtualnej systemu Linux](../../virtual-machines/virtual-machines-linux-quick-create-portal.md) lub [maszyny Wirtualnej systemu Windows](../../virtual-machines/virtual-machines-windows-hero-tutorial.md) z hello portalu Azure.

#### <a name="azure-functions-serverless"></a>Funkcje platformy Azure (bez serwera)

A nie z martwiąc się o tworzenie wychodzących i zarządzanie nią całej aplikacji lub hello toorun infrastruktury kodu. Co zrobić, jeśli można po prostu wpisz swój kod i go uruchomić w odpowiedzi tooevents lub zgodnie z harmonogramem?  [Środowisko Azure Functions](../../azure-functions/functions-overview.md) jest a "niekorzystającą" — styl oferty, że umożliwia po prostu pisania hello kod należy. Za pomocą funkcji wykonywanie kodu zostanie wywołany przez żądania HTTP, elementów webhook, zdarzenia usługi chmury, lub zgodnie z harmonogramem. Można kodu w języku programowania wyboru, takich jak C\#, F\#, Node.js, Python lub PHP. Z na podstawie zużycia rozliczeń, płacisz tylko za czas hello wykonuje kodu i Azure skaluje zgodnie z potrzebami.

>**Gdy toouse**: Użyj usługi Azure Functions, jeśli masz kod, który zostanie wywołany przez innych usług Azure zdarzeń opartych na sieci web, lub zgodnie z harmonogramem. Możesz również użyć funkcji podczas nie wymagają hello koszty kompletnego projektu hostowanej lub jeśli tylko toopay hello czas działania kodu. toolearn więcej, zobacz [Azure Functions — omówienie](../../azure-functions/functions-overview.md).

>**Rozpoczynanie pracy**: wykonaj samouczek Szybki Start — funkcje hello zbyt[tworzenie pierwszej funkcji](../../azure-functions/functions-create-first-azure-function.md) hello portalu.

>**Wypróbuj teraz**: usługi Azure Functions umożliwia uruchamianie kodu bez konieczności toosign dla konta platformy Azure. Wypróbuj teraz na i [tworzenie pierwszej funkcji platformy Azure](https://tryappservice.azure.com/).

#### <a name="azure-service-fabric"></a>Azure Service Fabric

Sieć szkieletowa usług Azure to platforma systemów rozproszonych, który umożliwia łatwe toobuild pakietów, wdrażanie i zarządzanie mikrousług skalowalne i niezawodne. Zapewnia także możliwości zarządzania kompleksowej aplikacji do udostępniania, wdrażanie, monitorowanie, uaktualnianie poprawki i usuwanie wdrożone aplikacje. Aplikacje, które działają w udostępnionej puli maszyn, można rozpoczęcie od czegoś małego i skalować toohundreds lub tysięcy komputerów, zgodnie z potrzebami.

Sieć szkieletowa usług obsługuje WebAPI z interfejsu Open Web dla platformy .NET (OWIN) i ASP.NET Core. Udostępnia zestawy SDK do tworzenia usług w systemie Linux w .NET Core i Java. toolearn więcej informacji na temat sieci szkieletowej usług, zobacz hello [ścieżka szkoleniowa platformy Service Fabric](https://azure.microsoft.com/documentation/learning-paths/service-fabric/).

>**Gdy toouse:** usługi sieć szkieletowa jest dobrym rozwiązaniem, podczas tworzenia aplikacji lub ponowne zapisywanie istniejących toouse aplikacji architektury mikrousługi. Jeśli potrzebujesz więcej kontroli nad lub bezpośredni dostęp do podstawowej infrastruktury hello za pomocą sieci szkieletowej usług.

>**Wprowadzenie:** [tworzenie pierwszej aplikacji usługi Azure Service Fabric](../../service-fabric/service-fabric-create-your-first-application-in-visual-studio.md).

### <a name="enhance-your-applications-with-azure-services"></a>Ulepszanie aplikacji przy użyciu usług Azure

Ponadto tooapplication hostingu Azure zapewnia oferty usług, zwiększające funkcjonalność hello, projektowanie i utrzymanie aplikacji, zarówno w chmurze hello i lokalnych.

#### <a name="hosted-storage-and-data-access"></a>Hostowanej magazynu i dostępem do danych

Większość aplikacji musi przechowywać dane, tak niezależnie od sposobu podjęcia decyzji toohost aplikacji na platformie Azure, należy wziąć pod uwagę co najmniej jeden hello następujących usług magazynu i danych.

-   **Baza danych SQL Azure**: wersja hello aparatu programu Microsoft SQL Server do przechowywania danych relacyjnych tabelarycznych w chmurze hello platformy Azure. Baza danych SQL oferuje przewidywalną wydajność, skalowalność bez przestojów, ciągłość prowadzenia działalności biznesowej i ochronę danych.

    >**Gdy toouse**: Jeśli aplikacja wymaga magazynu danych z integralności referencyjnej, transakcyjne pomocy i obsługi zapytania TSQL.

    >**Rozpoczynanie pracy**: [Utwórz bazę danych SQL w minutach przy użyciu portalu Azure hello](../../sql-database/sql-database-get-started.md).

-   **Usługa Azure Storage**: oferuje trwałe, wysokiej dostępności magazynu obiektów blob, kolejek, plików oraz innych typów danych nonrelational. Magazyn zapewnia hello foundation magazynu dla maszyn wirtualnych.

    >**Gdy toouse**: gdy aplikacja przechowuje nonrelational dane, takie jak pary klucz wartość (tabele), obiektów blob, udziałów plików lub wiadomości (kolejek).

    >**Rozpoczynanie pracy**: Wybierz jedną z tych typów pamięci masowej: [obiekty BLOB](../../storage/blobs/storage-dotnet-how-to-use-blobs.md), [tabel](../../cosmos-db/table-storage-how-to-use-dotnet.md), [kolejek](../../storage/queues/storage-dotnet-how-to-use-queues.md), lub [pliki](../../storage/files/storage-dotnet-how-to-use-files.md).

-   **Usługa Azure DocumentDB**: pełni zarządzany i skalowalna baza danych nosql, które funkcje zapytań SQL na obiekt danych. Można uzyskać dostępu do usługi DocumentDB przy użyciu istniejących sterowników bazy danych MongoDB.
    >**Gdy toouse:** gdy aplikacja wymaga zapytania SQL stanie tooexecute toobe za pośrednictwem dokumentów JSON lub korzystania z bazy danych MongoDB.

    >**Rozpoczynanie pracy**: [kompilacji DocumentDB C# console application](../../documentdb/documentdb-get-started.md). Jeśli jesteś deweloperem bazy danych MongoDB, zobacz [DocumentDB obsługą protokołu bazy danych MongoDB](../../documentdb/documentdb-protocol-mongodb.md).

Można użyć [fabryki danych Azure](../../data-factory/data-factory-introduction.md) toomove istniejącymi lokalnymi tooAzure danych. Jeśli użytkownik nie jest gotowy toomove danych w chmurze toohello, [połączeń hybrydowych](../../biztalk-services/integration-hybrid-connection-overview.md) w usługi BizTalk Services umożliwia łączenia aplikacji usługi hostowanej zasobów lokalnych tooon aplikacji. TooAzure danych i usługi magazynu umożliwia też łączność z lokalnymi aplikacji.

#### <a name="docker-support"></a>Obsługa docker

Kontenery docker, formę wirtualizacji systemu operacyjnego, umożliwiają wdrażanie aplikacji w sposób bardziej wydajne i przewidywalne. Konteneryzowanych aplikacja działa w produkcji hello sam sposób jak w używanych systemach prac deweloperskich i testowych. Kontenery można zarządzać przy użyciu standardowych narzędzi Docker. Można przy użyciu posiadane umiejętności i narzędzia open source popularnych toodeploy i zarządzać nimi aplikacji kontenera na platformie Azure.

Platforma Azure udostępnia kilka sposobów toouse kontenerów w aplikacji.

-   **Rozszerzenie Azure Docker VM**: umożliwia skonfigurowanie maszyny Wirtualnej z tooact narzędzia Docker jako hosta Docker.

    >**Gdy toouse**: ma toogenerate spójne kontenera wdrożenia aplikacji na maszynie Wirtualnej, lub utworzyć toouse [rozwiązania Docker Compose](https://docs.docker.com/compose/overview/).

    >**Rozpoczynanie pracy**: [utworzyć środowisko Docker na platformie Azure przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker hello](../../virtual-machines/virtual-machines-linux-dockerextension.md).

-   **Usługa kontenera platformy Azure**: umożliwia tworzenie, konfigurowanie i Zarządzanie klastrem maszyn wirtualnych, które są wstępnie toorun konteneryzowanych aplikacji. Zobacz toolearn więcej informacji na temat usługi kontenera [wprowadzenie usługi kontenera platformy Azure](../../container-service/container-service-intro.md).

    >**Gdy toouse**: Jeśli potrzebujesz toobuild gotowe do produkcji, skalowalnej środowisk zawierających dodatkowe planowanie i narzędzia do zarządzania, lub gdy wdrażana klaster Docker Swarm.

    >**Rozpoczynanie pracy**: [wdrażanie klastra usługi kontenera](../../container-service/dcos-swarm/container-service-deployment.md).

-   **Maszyna docker**: pozwala instalować i zarządzać aparatem platformy Docker na hostów wirtualnych za pomocą polecenia docker maszyny.

    >**Gdy toouse**: gdy są potrzebne prototypu tooquickly aplikację przez utworzenie jednego hosta Docker.

-   **Niestandardowy obraz Docker dla aplikacji usługi**: umożliwia używanie kontenerów Docker z rejestru kontenera lub kontener klienta podczas wdrażania aplikacji sieci web w systemie Linux.

    >**Gdy toouse**: w przypadku wdrażania aplikacji sieci web dla systemu Linux tooa Docker obrazu.

    >**Rozpoczynanie pracy**: [użyć niestandardowego obrazu Docker dla usługi App Service w systemie Linux](../../app-service-web/app-service-linux-using-custom-docker-image.md).

### <a name="authentication"></a>Authentication

Jego kluczowe toonot tylko wiedzieć, kto korzysta z aplikacji, ale także tooprevent nieautoryzowany dostęp do zasobów tooyour. Platforma Azure udostępnia kilka sposobów tooauthenticate klientów aplikacji.

-   **Azure Active Directory (Azure AD)**: hello wielodostępnym, oparte na chmurze tożsamości i dostępu do usługi Microsoft management. Dzięki integracji z usługą Azure AD, można dodać jednokrotnego w aplikacjach tooyour (rejestracji jednokrotnej SSO). Są dostępne właściwości katalogu przy użyciu interfejsu API usługi Azure AD Graph hello bezpośrednio lub hello interfejsu API programu Microsoft Graph. Można zintegrować z obsługą usługi Azure AD hello OAuth2.0 autoryzacji framework oraz Open ID Connect za pomocą natywnego punkty końcowe REST protokołu HTTP/i hello bibliotek uwierzytelniania multiplatform usługi Azure AD.

    >**Gdy toouse**: tooprovide jednokrotnej, należy pracować z danymi na podstawie wykres lub uwierzytelnianie oparte na domenie użytkowników.

    >**Rozpoczynanie pracy**: toolearn więcej, zobacz hello [przewodnik dewelopera usługi Azure Active Directory](../../active-directory/active-directory-developers-guide.md).

-   **Uwierzytelnianie usługi aplikacji**: po wybraniu toohost aplikację usługi aplikacji, umożliwia również wyświetlenie obsługę wbudowanego uwierzytelniania za pomocą usługi Azure AD, wraz z dostawców tożsamości społecznościowych — łącznie z usługi Facebook, Google, Microsoft i Twitter.

    >**Gdy toouse**: należy tooenable uwierzytelniania w aplikacji usługi app Service przy użyciu usługi Azure AD, dostawców tożsamości społecznościowych lub oba.

    >**Rozpoczynanie pracy**: toolearn więcej informacji na temat uwierzytelniania w usłudze App Service, zobacz [uwierzytelnianie i autoryzację w usłudze Azure App Service](../../app-service/app-service-authentication-overview.md).

toolearn więcej informacji na temat najlepsze rozwiązania na platformie Azure, zobacz [Azure najlepsze rozwiązania i wzorce](../../security/security-best-practices-and-patterns.md).

### <a name="monitoring"></a>Monitorowanie

Z aplikacji do pracy na platformie Azure, należy wydajność może toomonitor toobe, obejrzyj problemów i sprawdzić, jak klienci korzystają z aplikacji. Platforma Azure oferuje kilka możliwości monitorowania.

-   **Visual Studio Application Insights**: usługi analytics extensible hostowanymi na platformie Azure, która integruje się z programem Visual Studio toomonitor aplikacji sieci web na żywo. Udostępnia dane hello konieczność toocontinuously poprawy hello wydajność oraz poziom użyteczności aplikacji, czy jest hostowana na platformie Azure lub nie.

    >**Rozpoczynanie pracy**: hello wykonaj [samouczek usługi Application Insights](../../application-insights/app-insights-overview.md).

-   **Azure Monitor**: usługa, która pomaga toovisualize, zapytania trasy, archiwum i ustawy o hello metryki i dzienniki, które są generowane przez infrastrukturę platformy Azure i zasobów. Monitor zawiera widoki danych hello zobacz w hello portalu Azure i jest jedynym źródłem monitorowania zasobów platformy Azure.
 
    >**Rozpoczynanie pracy**: [Rozpoczynanie pracy z monitorem Azure](../../monitoring-and-diagnostics/monitoring-get-started.md).

### <a name="devops-integration"></a>Integracja metodyki DevOps

Czy jest obsługa administracyjna maszyn wirtualnych lub publikowania aplikacji sieci web z ciągłej integracji, Azure integruje się z większością popularnych narzędzi DevOps hello. Obsługę narzędzi, takich jak Wpięć, GitHub, Puppet, Chef, TeamCity, Ansible, VSTS i inne osoby może współpracować z narzędzia hello już mieć i zmaksymalizować istniejącego środowiska.

>**Wypróbuj teraz:** [kilka hello integracji DevOps wypróbuj](https://azure.microsoft.com/try/devops/).

>**Rozpoczynanie pracy**: toosee Opcje opracowywania oprogramowania dla aplikacji usługi app Service, zobacz [tooAzure ciągłego wdrażania aplikacji usługi](../../app-service-web/app-service-continuous-deployment.md).


## <a name="azure-regions"></a>Regiony świadczenia usługi Azure

Azure to platforma chmury globalnej, która jest ogólnie dostępna w wielu regionach wokół hello world. Podczas obsługi administracyjnej usługi, aplikacji lub maszyny Wirtualnej na platformie Azure, są zadawane tooselect regionu, który reprezentuje określonych datacenter, którym jest uruchomiona aplikacja lub gdy dane są przechowywane. Te regiony odpowiada toospecific lokalizacje, które są publikowane na powitania [regiony platformy Azure](https://azure.microsoft.com/regions/) strony.

### <a name="choose-hello-best-region-for-your-application-and-data"></a>Wybierz hello region najlepsze dla aplikacji i danych

Jedną z zalet hello korzysta z platformy Azure jest wdrożenie centrów danych Twojej aplikacji toovarious w całym Witaj świecie. Możesz wybrać region Hello może wpłynąć na wydajność hello aplikacji. Na przykład jest lepsze toochoose region, który jest bliżej toomost opóźnienia tooreduce klientów, korzystając z żądania sieciowe. Można także tooselect Twojego regionu toomeet hello wymagania prawne dystrybucji aplikacji w niektórych krajach. Jest zawsze najważniejsze dane aplikacji toostore praktyką hello na tym samym centrum danych lub w centrum danych jak najbliżej jako możliwych toohello centrum danych, który jest hostem aplikacji.

### <a name="multi-region-apps"></a>W przypadku aplikacji

Chociaż mało prawdopodobne, nie jest niemożliwe toogo całe centrum danych w trybie offline z powodu zdarzenia, takie jak klęski żywiołowej lub awaria internetowego. Jest to najlepsze praktyki toohost ważnych aplikacji biznesowych w więcej niż jednej dostępności maksymalna tooprovide centrum danych. Przy użyciu wielu regionach można zmniejszenia opóźnień użytkowników globalne i zapewniają dodatkowe możliwości elastyczność podczas aktualizacji aplikacji.

Niektóre usługi, takie jak maszyny wirtualne i usługi aplikacji, użyj [usługi Azure Traffic Manager](../../traffic-manager/traffic-manager-overview.md) tooenable w przypadku obsługi w trybie failover między aplikacjami przedsiębiorstwa wysokiej dostępności toosupport regionów. Na przykład zobacz [architektura referencyjna Azure: aplikacja sieci Web o wysokiej dostępności](../../guidance/guidance-web-apps-multi-region.md).

>**Gdy toouse**: Jeśli masz aplikacje przedsiębiorstwa o wysokiej dostępności, korzystających z trybu failover i replikacji.

## <a name="how-do-i-manage-my-applications-and-projects"></a>Jak zarządzać Moje aplikacje i projektów

Azure zapewnia bogaty zestaw środowiska możesz toocreate i zarządzania zasobami Azure, aplikacji i projekty — programowo i w hello [portalu Azure](https://portal.azure.com/).

### <a name="command-line-interfaces-and-powershell"></a>Interfejsy wiersza polecenia i programu PowerShell

Platforma Azure udostępnia dwa sposoby toomanage aplikacje i usługi z wiersza polecenia hello za pomocą Bash, terminali, wiersz polecenia hello lub narzędzie wiersza polecenia wyboru. Zazwyczaj hello same zadania można wykonać z wiersza polecenia hello jak hello portalu Azure, takich jak tworzenie i konfigurowanie maszyn wirtualnych, sieci wirtualnych, aplikacje sieci web i innych usług.

-   [Azure interfejsu wiersza polecenia (CLI)](../../xplat-cli-install.md): pozwala połączyć tooan subskrypcji platformy Azure i programu różne zadania przed zasobów platformy Azure z wiersza polecenia hello.

-   [Program Azure PowerShell](../../powershell-install-configure.md): udostępnia zestaw modułów za pomocą poleceń cmdlet umożliwiających toomanage Azure zasobów za pomocą środowiska Windows PowerShell.

### <a name="azure-portal"></a>Azure Portal

Hello portalu Azure to aplikacja sieci web czy można użyć toocreate, zarządzanie i usuwać zasoby platformy Azure i usługi. Witaj portalu Azure znajduje się pod adresem <https://portal.azure.com>. On obejmuje można dostosować pulpit nawigacyjny, narzędzia do zarządzania zasobami Azure i ustawienia toosubscription dostępu i informacji dotyczących rozliczeń. Aby uzyskać więcej informacji, zobacz hello [omówienie portalu Azure](../../azure-portal-overview.md).

### <a name="rest-apis"></a>Interfejsy API REST

Azure jest oparty na zestaw interfejsów API REST, który obsługuje hello interfejsu użytkownika portalu Azure. Większość tych interfejsów API REST jest również obsługiwany toolet programowo udostępniania i zarządzania zasobami Azure i aplikacji z dowolnego urządzenia internetowe. Aby hello pełen zestaw dokumentacji interfejsu API REST, zobacz hello [odwołania do zestawu SDK REST Azure](https://docs.microsoft.com/rest/api/).

### <a name="apis"></a>Interfejsy API

Ponadto tooREST interfejsów API wielu usług Azure pozwalają również programowego zarządzania zasobów z aplikacji przy użyciu specyficzne dla platformy Azure SDK, w tym zestawy SDK dla następującego platformy programistyczne hello:

-   [.NET](https://go.microsoft.com/fwlink/?linkid=834925)
-   [Node.js](http://azure.github.io/azure-sdk-for-node/)
-   [Java](https://docs.microsoft.com/java/api/)
-   [PHP](https://github.com/Azure/azure-sdk-for-php/blob/master/README.md)
-   [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/)
-   [Ruby](https://github.com/Azure/azure-sdk-for-ruby/blob/master/README.md)

Usług takich jak [Mobile Apps](../../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md) i [usługi Azure Media Services](../../media-services/media-services-dotnet-how-to-use.md) toolet zestawów SDK klienta zapewniają dostęp do usług sieci web i aplikacji klientów urządzeń przenośnych.

### <a name="azure-resource-manager"></a>Azure Resource Manager 
    
Uruchamianie aplikacji na platformie Azure mogą obejmuje pracę z wieloma usługami Azure, z których wykonaj hello życia tego samego cyklu wszystkich i można traktować jako jednostki logicznej. Na przykład aplikacja sieci web może użyć aplikacji sieci Web, bazy danych SQL, magazynu, pamięć podręczna Redis Azure i usługi Azure Content Delivery Network. [Usługa Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) umożliwia pracy z zasobami hello w aplikacji jako grupa. Można wdrożyć, zaktualizować lub usunąć wszystkie zasoby hello w jednej, skoordynowanej operacji.

Ponadto toologically grupowanie i zarządzanie nimi powiązanych zasobów, usługi Azure Resource Manager zawiera funkcje wdrażania, które umożliwiają dostosowanie hello wdrażania i konfigurowania powiązanych zasobów. Można na przykład za pomocą Menedżera zasobów, wdrażanie i konfigurowanie aplikacji, która składa się z wielu maszyn wirtualnych, usługi równoważenia obciążenia i bazy danych Azure SQL jako pojedyncza jednostka.

Te wdrożenia jest opracowanie przy użyciu szablonu usługi Azure Resource Manager, który jest dokumentu w formacie JSON. Szablony umożliwiają definiowanie wdrożenia i Zarządzaj aplikacjami za pomocą szablonów deklaratywnych zamiast skryptów. Szablonów można następnie używać w różnych środowiskach, takich jak testowania, przemieszczania i produkcji. Na przykład przy użyciu szablonów, należy dodać repozytorium GitHub tooa przycisku, który wdraża hello kod w zestawie tooa repozytorium hello usług platformy Azure za pomocą jednego kliknięcia.

>**Gdy toouse**: hello szablonów Użyj Menedżera zasobów, należy na podstawie szablonu wdrożenia dla aplikacji, którą można programowo zarządzać za pomocą interfejsów API REST, wiersza polecenia platformy Azure i programu Azure PowerShell.

>**Rozpoczynanie pracy**: tooget uruchomiona za pomocą szablonów, zobacz [szablonów Authoring Azure Resource Manager](../../resource-group-authoring-templates.md).

## <a name="understanding-accounts-subscriptions-and-billing"></a>Opis kont, subskrypcje i rozliczeń

Jako deweloperów firma Microsoft, takich jak toodive bezpośrednio w kodzie hello i spróbuj tooget tak szybko jak to możliwe w tworzeniu nasze aplikacje uruchomione. Na pewno chcemy tooencourage toostart równie łatwo działa na platformie Azure. toohelp była oferuje łatwe, Azure [bezpłatnej wersji próbnej](https://azure.microsoft.com/free/). Niektóre usługi tak samo, jak nawet korzystać z funkcji "Wypróbuj bezpłatnie" [usłudze Azure App Service](https://tryappservice.azure.com/), które nie wymagają zbyt nawet utworzyć konto. Fun jak toodive do kodowania i wdrażanie Twojego tooAzure aplikacji jest również ważne tootake niektórych toounderstand czas działania usługi Azure z punktu widzenia kont użytkowników, subskrypcje i rozliczeń.

### <a name="what-is-an-azure-account"></a>Co to jest konto platformy Azure?

toocreate stanie toobe lub pracy z subskrypcją platformy Azure, musi mieć konto platformy Azure. Konto platformy Azure jest po prostu tożsamości w usłudze Azure AD lub w katalogu, takie jak służbowego organizacji, który jest zaufany przez usługę Azure AD. Jeśli użytkownik nie należy toosuch organizacji, zawsze można utworzyć subskrypcji przy użyciu Account Microsoft, który jest zaufany przez usługę Azure AD. toolearn więcej informacji na temat integracji lokalnego systemu Windows Server Active Directory z usługą Azure AD, zobacz [integrowanie tożsamości lokalnych z usługą Azure Active Directory](../../active-directory/active-directory-aadconnect.md).

Każda subskrypcja platformy Azure jest połączona relacją zaufania z wystąpieniem usługi Azure AD. Oznacza to, że subskrypcja ufa tooauthenticate tego katalogu użytkowników, usług i urządzeń. Wiele subskrypcji może ufać hello tym samym katalogu, ale subskrypcji ufać tylko jednemu katalogowi. toolearn więcej, zobacz [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory](../../active-directory/active-directory-how-subscriptions-associated-directory.md).

Ponadto toodefining tożsamości indywidualne konto platformy Azure, nazywany również *użytkowników*, można również zdefiniować *grup* w usłudze Azure AD. Tworzenie grup użytkowników jest tooresources dostępu toomanage dobrym sposobem, w ramach subskrypcji przy użyciu kontroli dostępu opartej na rolach (RBAC). toolearn toocreate grup, zobacz temat [utworzyć grupę w wersji zapoznawczej usługi Azure Active Directory](../../active-directory/active-directory-groups-create-azure-portal.md). Można również tworzyć i zarządzania grupami przez [przy użyciu programu PowerShell](../../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

### <a name="manage-your-subscriptions"></a>Zarządzanie subskrypcjami

Subskrypcja jest jednostki logicznej usług platformy Azure jest tooan połączonego konta platformy Azure. Każdy skojarzone konto ma rolę w ramach subskrypcji. Rozliczenia dotyczące usługi Azure odbywa się na zasadzie dla subskrypcji. Lista hello subskrypcji dostępnych ofert według typu, zobacz [szczegółach oferty usługi Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/).

#### <a name="administrator-roles"></a>Role administratora

Subskrypcja platformy Azure ma wiele ról administratora konta, które można przypisać w dowolnym momencie.

-   **Konto administratora**: Ta rola ma pełną kontrolę nad hello subskrypcji i konto hello jest odpowiedzialny za rozliczeń.

-   **Administrator usługi**: Ta rola ma kontrolę nad wszystkich usług hello w hello subskrypcji. Domyślnie jest to hello tego samego konta, ponieważ hello administratora konta.

-   **Współadministratorem**: Ta rola ma hello sam dostępu jako hello administratora usługi, z tą różnicą, że nie można zmienić skojarzenie hello hello tooan subskrypcji usługi Azure directory.

toolearn więcej informacji na temat ról administratorów, zobacz [jak tooadd lub zmień role administratora platformy Azure](../../billing/billing-add-change-azure-subscription-administrator.md#add-an-admin-for-a-subscription).

#### <a name="resource-groups"></a>Grupy zasobów

Podczas obsługi administracyjnej nowych usług Azure, możesz to zrobić w ramach danej subskrypcji. Poszczególnych usług Azure, które są nazywane również zasobów, są tworzone w kontekście hello grupy zasobów. Grupy zasobów stał się łatwiejsze toodeploy i zarządzanie zasobami aplikacji. Grupa zasobów powinien zawierać wszystkie zasoby hello aplikacji, które chcesz toowork z jako jednostka. Zasoby można przenosić między grupami zasobów i nawet toodifferent subskrypcji. toolearn dotyczące przenoszenia zasobów, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](../../resource-group-move-resources.md).

Witaj Eksploratora zasobów Azure to doskonałe narzędzie do wizualizacji hello zasobów, które zostały już utworzone w ramach subskrypcji. toolearn więcej, zobacz [tooview Eksploratora zasobów Azure użycia i modyfikowania zasobów](../../resource-manager-resource-explorer.md).

#### <a name="grant-access-tooresources"></a>Udziel dostępu tooresources

Jeśli zezwolisz na dostęp do zasobów tooAzure, zawsze jest najlepszym rozwiązaniem, aby zapewnić użytkownikom hello najmniej uprawnienie to jest wymagana tooperform danego zadania.

-   **Kontrola dostępu oparta na rolach (RBAC)**: W usłudze Azure można przyznać dostęp konta toouser (główne) w określonym zakresie: subskrypcji, grupy zasobów lub pojedynczych zasobów. RBAC umożliwia wdrażanie zestaw zasobów w grupie zasobów i przydzielić uprawnienia tooa określonego użytkownika lub grupy. Pozwalają on również ograniczyć dostęp do zasobów hello tooonly, które należą toohello docelowa grupa zasobów. Można również przyznać dostęp tooa pojedynczego zasobu, takiego jak maszyny wirtualnej lub sieci wirtualnej. dostęp toogrant przypisać użytkownika toohello roli, grupy lub nazwy głównej usługi. Istnieje wiele wstępnie zdefiniowanych ról, a istnieje również możliwość definiowania własnych niestandardowych ról.

    >**Gdy toouse**: Jeśli wymagane jest precyzyjne zarządzanie dostępem dla użytkowników i grup.

    >**Rozpoczynanie pracy**: toolearn więcej, zobacz [wprowadzenie do zarządzania dostępem w portalu Azure hello](../../active-directory/role-based-access-control-what-is.md).

-   **Obiekty główne usługi**: oprócz tooproviding dostępu toouser podmiotów zabezpieczeń i grup, można przyznać hello tej samej nazwy głównej usługi tooa dostępu.

    > **Gdy toouse**: w przypadku gdy programowo zarządzania zasobami platformy Azure lub udzielania dostępu dla aplikacji. Aby uzyskać więcej informacji, zobacz [supplication tworzenia usługi Active Directory i nazwę główną usługi](../../resource-group-create-service-principal-portal.md).

#### <a name="tags"></a>Tagi

Usługa Azure Resource Manager można przypisać znaczniki niestandardowe tooindividual zasobów. Tagi, które są pary klucz wartość, mogą być pomocne, gdy będziesz potrzebować tooorganize zasobów do rozliczeń lub monitorowania. Znaczniki umożliwiają zasobów tootrack sposób w przypadku wielu grup zasobów. Można przypisać znaczniki w portalu hello, w szablonie usługi Azure Resource Manager hello lub programowo, za pomocą hello interfejsu API REST, hello wiersza polecenia platformy Azure lub programu PowerShell. Można przypisać wiele tagów tooeach zasobów. toolearn więcej, zobacz [używanie tagów tooorganize zasobów platformy Azure](../../resource-group-using-tags.md).

### <a name="billing"></a>Rozliczenia

W hello przenoszenie z lokalnej usługi hostowane toocloud obliczeniowych śledzenia i Szacowanie usługi użycia i koszty są istotne problemy. Jest ważne toobe stanie tooestimate nowych zasobów koszt toorun co miesiąc. Należy również toobe tooproject stanie wygląd hello rozliczeń dla danego miesiąca oparte na powitania bieżącego wydatków.

#### <a name="get-resource-usage-data"></a>Pobierz dane o użyciu zasobów

Platforma Azure oferuje zestaw rozliczeń REST interfejsów API, które zapewniają zużycia tooresource dostępu i informacji o metadanych dla subskrypcji platformy Azure. Te pozwalają rozliczeń interfejsów API hello toobetter możliwości prognozowania i zarządzaj nimi kosztów platformy Azure. Można śledzić i analizować wydatków z podziałem na godziny, tworzyć alerty wydatków i przewidywania przyszłych rozliczeń na podstawie bieżącego trendów użycia.

>**Rozpoczynanie pracy**: toolearn więcej informacji na temat przy użyciu hello rozliczeń interfejsów API, zobacz [omówienie użycia rozliczenia Azure i interfejsów API RateCard](../../billing-usage-rate-card-overview.md).

#### <a name="predict-future-costs"></a>Przewidywania przyszłych kosztów

Mimo że utrudnione jest koszty tooestimate wcześniejsze, platforma Azure ma [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/) których można używać podczas szacowania kosztów hello wdrożonych zasobów. Umożliwia także hello bloku rozliczenia w portalu hello i hello rozliczeń interfejsów API REST tooestimate przyszłych kosztów, na podstawie bieżącego zużycia.

>**Rozpoczynanie pracy**: zobacz [omówienie użycia rozliczenia Azure i interfejsów API RateCard](../../billing-usage-rate-card-overview.md).

#### <a name="set-up-billing-alerts"></a>Ustawianie alertów dotyczących rozliczeń

Po wdrożeniu aplikacji lub rozwiązania na platformie Azure, można tworzyć alerty, które wysyłają możesz wiadomość e-mail, gdy próbują hello wydatków ograniczeń, które są zdefiniowane w alercie hello.

>**Rozpoczynanie pracy**: toolearn więcej, zobacz [skonfigurować alerty dotyczące subskrypcji platformy Microsoft Azure billing](../../billing-set-up-alerts.md).
