---
title: "aaaAzure porównanie usługi aplikacji, maszyn wirtualnych, sieci szkieletowej usług i usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak jest toochoose między usłudze Azure App Service, maszyn wirtualnych, sieci szkieletowej usług i usługi w chmurze do obsługi aplikacji sieci web."
services: app-service\web, virtual-machines, cloud-services
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 7d346a23-532a-42a9-98a8-23b7286d32a8
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 07/07/2016
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7577332ed049df66178c7b2cd5c440a7f93a7865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-virtual-machines-service-fabric-and-cloud-services-comparison"></a>Usługa Azure App Service, maszyn wirtualnych, sieci szkieletowej usług i usługi w chmurze porównania
## <a name="overview"></a>Omówienie
Platforma Azure oferuje kilka sposobów witryn sieci web toohost: [usłudze Azure App Service][Azure App Service], [maszyn wirtualnych][Virtual Machines], [sieci szkieletowej usług ] [ Service Fabric], i [usługi w chmurze][Cloud Services]. Ten artykuł pomaga zrozumieć hello opcje i wybrać opcje hello aplikacji sieci web.

Usługa aplikacji Azure jest hello najlepszym rozwiązaniem w przypadku większości aplikacji sieci web. Wdrażania i zarządzania są zintegrowane z platformy hello witryny można skalować szybko toohandle obciążeń dużego natężenia ruchu sieciowego i Menedżera ruchu i równoważenie obciążenia wbudowanych hello zapewnić wysoką dostępność. Można przenieść istniejące lokacje tooAzure App Service ułatwia [narzędzia migracji w trybie online](https://www.migratetoazure.net/), użyj aplikacji open source z hello Galeria aplikacji sieci Web albo utwórz nową witrynę za pomocą narzędzia wybranych przez użytkownika lub hello framework. Witaj [Webjob] [ WebJobs] funkcja umożliwia łatwe tooadd tła zadania przetwarzania tooyour aplikacji sieci web usługi aplikacji.

Sieć szkieletowa usług jest dobrym rozwiązaniem, jeśli tworzysz nową aplikację lub ponownego zapisywania istniejącą aplikację toouse architektury mikrousługi. Aplikacje, które działają w udostępnionej puli maszyn, można rozpoczęcie od czegoś małego i zwiększa skalowalność toomassive, setek lub tysięcy komputerów, zgodnie z potrzebami. Usługi stanowej była tooconsistently łatwe i niezawodne przechowywanie stanu aplikacji i sieci szkieletowej usług automatycznie zarządza partycjonowania usługi, skalowanie i dostępność dla Ciebie.  Sieć szkieletowa usług obsługuje również WebAPI z interfejsu Open Web dla platformy .NET (OWIN) i ASP.NET Core.  Porównaniu tooApp usługi, usługi sieć szkieletowa dostępne są także więcej kontroli nad lub bezpośredni dostęp do podstawowej infrastruktury hello. Możesz zdalnym do serwerów lub skonfigurować zadania uruchamiania serwera. Usługi w chmurze jest podobne tooService sieci szkieletowej w programie stopień kontroli i łatwość użycia, ale jest teraz starszej wersji usługi i sieci szkieletowej usług jest zalecane w przypadku nowych wdrożeń.

Jeśli masz istniejącej aplikacji, które wymagałyby toorun istotne zmiany w usłudze aplikacji lub usługi sieć szkieletowa, można wybrać w kolejności toosimplify migracji toohello chmury maszyn wirtualnych. Jednak poprawne skonfigurowanie zabezpieczania i obsługi maszyn wirtualnych wymaga znacznie więcej czasu i doświadczenia IT porównaniu tooAzure usługi aplikacji i usług sieci szkieletowej. Planując maszynach wirtualnych platformy Azure, upewnij się, uwzględnienia konta hello rutynowej konserwacji wymagany nakład pracy toopatch, aktualizacji i zarządzania w środowisku maszyny Wirtualnej. Maszyny wirtualne platformy Azure jest infrastruktury jako — usługa (IaaS), a usługi aplikacji i sieci szkieletowej usług platformy jako — usługa (Paas). 

## <a name="features"></a>Porównanie funkcji
Hello w poniższej tabeli porównano możliwości hello usługi App Service, usługi w chmurze, maszyn wirtualnych i sieci szkieletowej usług toohelp wprowadzeniu hello najlepszym rozwiązaniem. Aby uzyskać aktualne informacje o hello umowy SLA dla każdej opcji, zobacz [umowy dotyczące poziomu usług Azure](https://azure.microsoft.com/support/legal/sla/).

| Funkcja | Usługi aplikacji (aplikacje sieci web) | Usługi w chmurze (role sieci web) | Maszyny wirtualne | Service Fabric | Uwagi |
| --- | --- | --- | --- | --- | --- |
| Niemal natychmiastowe wdrożenia |X | | |X |Wdrażanie aplikacji lub tooa aktualizacji aplikacji usługi w chmurze lub tworzenia maszyny Wirtualnej, może zająć kilka minut co najmniej; Wdrażanie aplikacji sieci web tooa aplikacji trwa sekund. |
| Skalowanie w górę maszyny toolarger bez ponownego wdrażania |X | | |X | |
| Wystąpienia serwera sieci Web udostępniać zawartość i konfigurację, co oznacza, że nie masz tooredeploy lub zmienić konfigurację podczas skalowania. |X | | |X | |
| Wiele środowisk wdrażania (produkcyjnym i pomostowym) |X |X | |X |Sieć szkieletowa usług pozwala toohave środowiskach wielu aplikacji lub toodeploy różne wersje Twojej aplikacji side-by-side. |
| Automatyczne zarządzanie aktualizacjami systemu operacyjnego |X |X | | |Automatyczne aktualizacje systemu operacyjnego są planowane dla wersji przyszłych sieci szkieletowej usług. |
| Przełączanie bezproblemowe platformy (łatwo przenosić między 32-bitowe i 64-bitowe) |X |X | | | |
| Wdrażanie kodu za pomocą narzędzia GIT, FTP |X | |X | | |
| Wdrażanie kodu za pomocą narzędzia Web Deploy |X | |X | |Usługi w chmurze obsługuje hello przy użyciu narzędzia Web Deploy wystąpień roli tooindividual aktualizacje toodeploy. Jednak nie można używać go do początkowego rozmieszczania roli i użycie narzędzia Web Deploy aktualizacji oddzielnie masz toodeploy tooeach wystąpienie roli. Wiele wystąpień są wymagane w kolejności tooqualify dla hello umowy SLA dla usługi chmury dla środowisk produkcyjnych. |
| Obsługa programu WebMatrix |X | |X | | |
| Tooservices dostępu, takich jak usługi Service Bus, magazynu, baza danych SQL |X |X |X |X | |
| Witryna sieci web hosta lub warstwy usługi sieci web architektury wielowarstwowe |X |X |X |X | |
| Host warstwy środkowej architektury wielowarstwowe |X |X |X |X |Aplikacje sieci web usługi aplikacji można łatwo hostowania warstwy środkowej interfejsu API REST i hello [Webjob](http://go.microsoft.com/fwlink/?linkid=390226) funkcji może zawierać zadań przetwarzania w tle. Można uruchomić zadania Webjob w dedykowanej witrynie sieci Web tooachieve niezależne skalowalność dla warstwy hello. Podgląd Hello [aplikacje interfejsu API](../app-service-api/app-service-api-apps-why-best-platform.md) funkcja zapewnia więcej funkcji dla usługi REST obsługi. |
| Obsługa zintegrowanego MySQL jako usługa |X |X |X | |Usługi w chmurze można zintegrować MySQL jako usługa, za pośrednictwem jego ClearDB oferty, ale nie jako część hello portalu Azure w przepływie pracy. |
| Obsługę programów ASP.NET i classic ASP, Node.js, PHP, Python |X |X |X |X |Sieć szkieletowa usług obsługuje tworzenia hello frontonu sieci web przy użyciu [ASP.NET 5](../service-fabric/service-fabric-add-a-web-frontend.md) lub dowolnego typu aplikacji (Node.js, Java itp.) można wdrożyć jako [pliku wykonywalnego gościa](../service-fabric/service-fabric-deploy-existing-app.md). |
| Skalowanie w poziomie wystąpień toomultiple bez ponownego wdrażania |X |X |X |X |Maszyny wirtualne można skalować w poziomie toomultiple wystąpienia, ale działającymi na nich usługami hello musi być napisana toohandle tym skalowalnych w poziomie. Ma tooconfigure tooroute żądań modułu równoważenia obciążenia na maszynach hello, a następnie utworzyć grupy koligacji tooprevent jednoczesnych ponowne uruchomienie wszystkich wystąpień z powodu niepowodzenia toomaintenance lub sprzętu. |
| Obsługa protokołu SSL |X |X |X |X |Dla aplikacji sieci web usługi aplikacji protokół SSL dla nazwy domeny niestandardowej jest obsługiwana tylko dla trybu Basic i Standard. Aby dowiedzieć się, jak przy użyciu protokołu SSL z aplikacjami sieci web, zobacz [Konfigurowanie certyfikatu SSL dla witryny sieci Web platformy Azure](app-service-web-tutorial-custom-ssl.md). |
| Integracja z programem Visual Studio |X |X |X |X | |
| Debugowanie zdalne |X |X |X | | |
| Wdrażanie kodu z programem TFS |X |X |X |X | |
| Izolacja z sieci [sieci wirtualnej platformy Azure](/azure/virtual-network/) |X |X |X |X |Zobacz też [integracji sieci wirtualnej platformy Azure witryn sieci Web](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/) |
| Obsługa [usługi Azure Traffic Manager](/azure/traffic-manager/) |X |X |X |X | |
| Monitorowanie zintegrowanego punktu końcowego |X |X |X | | |
| Tooservers dostępu do pulpitu zdalnego | |X |X |X | |
| Zainstaluj wszelkie niestandardowe MSI | |X |X |X |Sieć szkieletowa usług pozwala toohost pliku każdego pliku wykonywalnego jako [pliku wykonywalnego gościa](../service-fabric/service-fabric-deploy-existing-app.md) lub dowolną aplikację można zainstalować na powitania maszyn wirtualnych. |
| Zdolność toodefine/wykonywanie uruchamiania zadania | |X |X |X | |
| Można nasłuchiwać zdarzeń tooETW | |X |X |X | |

## <a name="scenarios"></a>Scenariusze i zalecenia
Oto kilka typowych scenariuszy aplikacji wraz z zaleceniami opcja hostingu sieci web platformy Azure toowhich może być najbardziej właściwa dla każdego.

* [Potrzebuję frontonu sieci web z przetwarzania w tle i bazy danych zaplecza toorun aplikacji biznesowych zintegrowany z zasobów lokalnych.](#onprem)
* [Potrzebuję toohost niezawodny sposób osiągnąć Moje firmowych witryn sieci Web która może obsłużyć również i ofert globalnego.](#corp)
* [Masz IIS6 aplikacji uruchomionej w systemie Windows Server 2003.](#iis6)
* [Jestem właścicielem małych firm i potrzebna toohost niedrogich sposób mojej lokacji, ale z przyszłego rozwoju pamiętać.](#smallbusiness)
* [Sieci web lub projektanta grafiki i chcę toodesign, tworzenie witryn sieci web dla klientów.](#designer)
* [Jestem I Migrowanie aplikację wielowarstwową z sieci web toohello frontonu chmury.](#multitier)
* [Moja aplikacja jest zależna od wysoce dostosowane systemu Windows lub w środowiskach Linux oraz toomove on toohello chmury.](#custom)
* [Moja witryna korzysta z oprogramowania typu open source, a ma toohost go na platformie Azure.](#oss)
* [Masz aplikacji — biznesowych, która potrzebuje tooconnect toohello firmowej sieci.](#lob)
* [Chcę toohost interfejsu API REST lub usługą sieci web dla klientów mobilnych.](#mobile)

### <a id="onprem"></a>Potrzebuję frontonu sieci web z przetwarzania w tle i bazy danych zaplecza toorun aplikacji biznesowych zintegrowany z zasobów lokalnych.
Usługa aplikacji Azure to doskonałe rozwiązanie dla aplikacji biznesowych. Dzięki temu można utworzyć aplikacje, które automatycznie skalować na platformie równoważeniem obciążenia, są zabezpieczone przy użyciu usługi Active Directory i połącz tooyour lokalnymi zasobami. Sprawia, że tych aplikacji za pośrednictwem portalu światowej klasy i interfejsy API łatwe zarządzanie i pozwala toogain wgląd w jaki sposób klienci są używane w narzędzia szczegółowe informacje o aplikacji. Witaj [Webjob] [ Webjobs] funkcja umożliwia uruchamianie procesów w tle i zadań w ramach warstwę web podczas połączenia hybrydowe i funkcje sieci Wirtualnej stał się łatwo tooconnect wstecz tooon lokalnych zasobach. Usługa aplikacji Azure udostępnia trzy 9 umowy SLA dla aplikacji sieci web i umożliwia:

* Niezawodny sposób uruchomienia aplikacji na platformie chmury samonaprawiania, automatyczne stosowanie poprawek.
* Skalować automatycznie w globalnej sieci centrów danych.
* Tworzenie kopii zapasowej i przywracania dla odzyskiwania po awarii.
* Być zgodne, ISO, SOC2 i PCI.
* Integracja z usługą Active Directory

### <a id="corp"></a>Potrzebuję toohost niezawodny sposób osiągnąć Moje firmowych witryn sieci Web która może obsłużyć również i ofert globalnego.
Usługa aplikacji Azure to doskonałe rozwiązanie do obsługi firmowej witryn sieci Web. Tooscale aplikacji sieci web umożliwia szybkie i łatwe toomeet żądania w globalnej sieci centrów danych. Oferuje reach lokalnego, odporność na uszkodzenia i zarządzanie ruchem inteligentnego. Na platformie, która udostępnia narzędzia do zarządzania światowej klasy umożliwiając toogain wgląd w kondycję lokacji i ruch w witrynie szybkie i łatwe. Usługa aplikacji Azure udostępnia trzy 9 umowy SLA dla aplikacji sieci web i umożliwia:

* Niezawodnie uruchomić witryny sieci Web na platformie chmury samonaprawiania, automatyczne stosowanie poprawek.
* Skalować automatycznie w globalnej sieci centrów danych.
* Tworzenie kopii zapasowej i przywracania dla odzyskiwania po awarii.
* Zarządzanie dziennikami i ruch z zintegrowane narzędzia.
* Być zgodne, ISO, SOC2 i PCI.
* Integracja z usługą Active Directory

### <a id="iis6"></a>Masz IIS6 aplikacji uruchomionej w systemie Windows Server 2003.
Usługa aplikacji Azure umożliwia łatwe tooavoid hello infrastruktury kosztów związanych z Migrowanie starszych aplikacji usług IIS 6. Firma Microsoft opracowała [migracji szczegółowe wskazówki i narzędzi migracji toouse łatwe](https://www.movemetowebsites.net/) czy umożliwiają toocheck zgodności i odszukaj wszelkie zmiany wymagające toobe wprowadzone. Integracja z programu Visual Studio, TFS i narzędziom CMS umożliwia łatwe toodeploy IIS6 aplikacji bezpośrednio toohello w chmurze. Po wdrożeniu hello Azure Portal udostępnia narzędzia niezawodne funkcje zarządzania, które umożliwiają tooscale toomanage kosztów i zapasowej żądanie toomeet w razie potrzeby. Narzędzie migracji hello można:

* Szybko i łatwo przeprowadzić migrację chmury toohello starszej wersji aplikacji sieci web systemu Windows Server 2003.
* OPT tooleave Twojego dołączone SQL bazy danych lokalnych toocreate hybrydowej aplikacji.
* Automatyczne przenoszenie bazy danych SQL wraz ze starszej wersji aplikacji.

### <a id="smallbusiness"></a>Jestem właścicielem małych firm i potrzebna toohost niedrogich sposób mojej lokacji, ale z przyszłego rozwoju pamiętać.
Usługa aplikacji Azure to doskonałe rozwiązanie w tym scenariuszu, ponieważ może rozpocząć korzystanie z niej bezpłatnie i następnie dodać więcej możliwości, gdy są potrzebne. Każdej aplikacji sieci web wolnego pochodzi z domeną dostarczany przez platformę Azure (*your_company*. azurewebsites.net), i platformy hello zawiera zintegrowane narzędzia wdrażania i zarządzania, a także galerii aplikacji, że łatwo tooget uruchomiona. Istnieje wiele innych usług i opcje skalowania, umożliwiających hello tooevolve lokacji z żądanie zwiększenia użytkownika. Za pomocą usługi Azure App Service można:

* Rozpoczyna się od warstwę bezpłatna hello i następnie skalować zgodnie z potrzebami.
* Użyj tooquickly galerii aplikacji hello Konfigurowanie popularne aplikacje sieci web, takich jak WordPress.
* W razie potrzeby dodaj dodatkowe funkcje i usługi tooyour aplikacji Azure.
* Zabezpieczenia aplikacji sieci web za pomocą protokołu HTTPS.

### <a id="designer"></a>Sieci web lub projektanta grafiki i chcę toodesign, tworzenie witryn sieci Web dla klientów
Dla deweloperów sieci web i projektantów usłudze Azure App Service zapewnia prostą integrację z różnych platform i narzędzi, obsługuje wdrożenia usługi Git i FTP i ścisłą integrację z narzędzi i usług, takich jak Visual Studio i bazy danych SQL. Możliwości zapewniane przez usługę App Service:

* Użyj narzędzia wiersza polecenia dla [zautomatyzowane zadania][scripting].
* Praca z popularnych języków, takich jak [.Net][dotnet], [PHP][PHP], [Node.js] [ nodejs], i [Python][Python].
* Wybierz trzy różne poziomy skalowania skalowania w górę toovery wysokiej wydajności.
* Integracja z innymi usługami Azure, takich jak [bazy danych SQL][sqldatabase], [usługi Service Bus] [ servicebus] i [magazynu] [ Storage], lub partnerów ofert z hello [magazynu Azure][azurestore], takie jak MySQL i bazy danych MongoDB.
* Integracja z narzędzi, takich jak Visual Studio, Git programu WebMatrix, WebDeploy, TFS i FTP.

### <a id="multitier"></a>Jestem I Migrowanie aplikację wielowarstwową z sieci web toohello frontonu chmury
Jeśli używasz aplikacji wielowarstwowej, na przykład serwera sieci web, który łączy tooa bazy danych, usługi Azure App Service jest dobrym rozwiązaniem, które ścisłą integrację z bazy danych SQL Azure. I funkcja hello zadań Webjob dla uruchomionych procesów wewnętrznej bazy danych.

Wybierz sieć szkieletowa usług dla jednego lub więcej z warstwami, jeśli potrzebujesz więcej kontrolę nad środowiskiem serwera hello, takich jak hello tooremote zdolność do serwera należy skonfigurować zadania uruchamiania serwera.

Wybierz maszyny wirtualne dla co najmniej jeden z poziomów toouse obrazu komputera lub uruchom serwer oprogramowania lub usług, których nie można skonfigurować w sieci szkieletowej usług.

### <a id="custom"></a>Moja aplikacja jest zależna od wysoce dostosowane systemu Windows lub w środowiskach Linux oraz toomove on toohello chmury.
Jeśli aplikacja wymaga złożonych instalacji lub konfiguracji systemu operacyjnego i oprogramowania hello, maszyn wirtualnych jest prawdopodobnie hello najlepszym rozwiązaniem. Maszyny wirtualne można:

* Toostart galerii maszyny wirtualnej hello przy użyciu systemu operacyjnego, takie jak Windows lub Linux, a następnie dostosować ją do wymagań aplikacji.
* Utwórz i Przekaż obraz niestandardowy istniejących toorun serwera lokalnego na maszynie wirtualnej na platformie Azure.

### <a id="oss"></a>Moja witryna korzysta z oprogramowania typu open source, a ma toohost go na platformie Azure
Jeśli używany framework typu open source jest obsługiwane z usługi aplikacji hello języków i struktur wymagane przez aplikację są automatycznie skonfigurowana za użytkownika. Usługi aplikacji umożliwia:

* Korzystanie z wielu popularnych Otwórz źródła języków, takich jak [.NET][dotnet], [PHP][PHP], [Node.js] [ nodejs], i [Python][Python].
* Konfigurowanie WordPress, Drupal, Umbraco, DNN i wielu innych aplikacji sieci web innych firm.
* Migrowanie istniejących aplikacji lub Utwórz nową z galerii aplikacji hello.

Jeśli Twoje framework typu open source nie jest obsługiwana w usłudze aplikacji, możesz uruchomić ją na jeden hello inne opcje hostingu sieci web platformy Azure. Z maszynami wirtualnymi, instalowania i konfigurowania hello oprogramowania w obrazie maszyny hello, który może być systemu Windows lub opartych na systemie Linux.

### <a id="lob"></a>Mam aplikacji — biznesowych, która potrzebuje sieci firmowej toohello tooconnect
Jeśli chcesz toocreate aplikacji biznesowych z witryny sieci Web może wymagać tooservices bezpośredni dostęp lub danych w sieci firmowej hello. Jest to możliwe w aplikacji usługi sieci szkieletowej usług i maszyn wirtualnych za pomocą hello [usługi Azure Virtual Network](/azure/virtual-network/). Usługi aplikacji można użyć na powitania [funkcji integracji sieci Wirtualnej](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/), co pozwala toorun z aplikacjami platformy Azure, jak gdyby znajdowały się w sieci firmowej.

### <a id="mobile"></a>Chcę toohost interfejsu API REST lub usługą sieci web dla klientów mobilnych
Usługi sieci web opartych na HTTP włączyć toosupport szerokiego zakresu klientów, w tym klientów mobilnych. Struktury, takich jak ASP.NET Web API integrują się z toomake Visual Studio go toocreate łatwiejsze i korzystać z usługi REST.  Te usługi są dostępne z punktu końcowego sieci web, dzięki czemu możliwe toouse dowolnej sieci web hostingu technika na Azure toosupport w tym scenariuszu. Jednak usługi aplikacji jest doskonałym wyborem do hostowania interfejsów API REST. Możliwości zapewniane przez usługę App Service:

* Szybkie tworzenie [aplikacji mobilnej](../app-service-mobile/app-service-mobile-value-prop.md) lub [aplikacji interfejsu API](../app-service-api/app-service-api-apps-why-best-platform.md) toohost usługi sieci web hello HTTP w jednym z rozproszonych globalnie centrach danych platformy Azure.
* Migrowanie istniejących usług lub utworzyć nowe.
* Osiągnięcia SLA dostępności z jednego wystąpienia lub skalowanie w poziomie dedykowane toomultiple maszyny.
* Użyj hello opublikowane lokacji tooprovide interfejsów API REST tooany HTTP klientów, w tym klientów mobilnych.

> [!NOTE]
> Jeśli chcesz korzystać z usługi Azure App Service przed utworzeniem konta tooget Przejdź zbyt<a href="https://trywebsites.azurewebsites.net/">https://trywebsites.azurewebsites.net</a>, w którym można od razu utworzyć krótkotrwałą wersję początkową aplikacji w usłudze Azure App Service bezpłatnie. Bez karty kredytowej i bez zobowiązań.
> 
> 

## <a id="nextsteps"></a>Następne kroki
Aby uzyskać więcej informacji na temat Opcje hostingu hello trzech zobacz [Introducing Azure](../fundamentals-introduction-to-azure.md).

tooget wprowadzenie hello wybrane opcje aplikacji, zobacz następujące zasoby hello:

* [Azure App Service](/azure/app-service/)
* [Azure Cloud Services](/azure/cloud-services/)
* [Maszyny wirtualne platformy Azure](/azure/virtual-machines/)
* [Service Fabric](/azure/service-fabric/)

<!-- URL List -->

[Azure App Service]: /azure/app-service/
[Cloud Services]: /azure/cloud-services/
[Virtual Machines]: /azure/virtual-machines/
[Service Fabric]: /azure/service-fabric/
[ClearDB]: http://www.cleardb.com/
[WebJobs]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Configuring an SSL certificate for an Azure Website]: app-service-web-tutorial-custom-ssl.md
[azurestore]: https://azuremarketplace.microsoft.com/en-us/marketplace/apps
[scripting]: https://azure.microsoft.com/documentation/scripts/?services=web-sites
[dotnet]: https://azure.microsoft.com/develop/net/
[nodejs]: https://azure.microsoft.com/develop/nodejs/
[PHP]: https://azure.microsoft.com/develop/php/
[Python]: https://azure.microsoft.com/develop/python/
[servicebus]: /azure/service-bus/
[sqldatabase]: /azure/sql-database/
[Storage]: /azure/storage/

<!-- IMG List -->

[ChoicesDiagram]: ./media/choose-web-site-cloud-service-vm/Websites_CloudServices_VMs_3.png
