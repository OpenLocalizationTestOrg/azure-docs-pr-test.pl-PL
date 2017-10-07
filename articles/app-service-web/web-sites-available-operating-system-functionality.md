---
title: "funkcje systemu aaaOperating w usłudze Azure App Service"
description: "Dowiedz się więcej o hello systemu operacyjnego funkcje tooweb dostępne aplikacje, zapleczy aplikacji mobilnych i aplikacji API apps w usłudze Azure App Service"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 39d5514f-0139-453a-b52e-4a1c06d8d914
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 695188c48102b10ece326fba8d50a5f55b03b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="operating-system-functionality-on-azure-app-service"></a>Funkcje systemu operacyjnego w usłudze Azure App Service
W tym artykule opisano hello wspólnej linii bazowej systemu operacyjnego funkcje, które są dostępne tooall aplikacje działające na [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Ta funkcja zawiera plik, sieci i dostępu do rejestru i dzienników diagnostyki i zdarzeń. 

<a id="tiers"></a>

## <a name="app-service-plan-tiers"></a>Warstwy planu usług aplikacji
App Service uruchamia aplikacje klienta w środowisku macierzystym wielodostępnej. Aplikacje wdrożone w hello **wolne** i **Shared** warstw, uruchom w procesach roboczych na udostępnionych maszynach wirtualnych podczas aplikacje wdrożone w hello **standardowe** i  **Premium** warstw, uruchom na przeznaczony specjalnie dla aplikacji hello skojarzonych z jednym maszyn wirtualnych.

Ponieważ App Service obsługuje bezproblemowe skalowanie między różnych warstw, konfiguracja zabezpieczeń hello wymuszane dla usługi aplikacji — aplikacje pozostaje hello takie same. Daje to pewność, że aplikacje nie nagle zachowywać się inaczej, niepowodzeniem w nieoczekiwany sposób, jeśli zmienia plan usługi aplikacji z jedną warstwę tooanother.

<a id="developmentframeworks"></a>

## <a name="development-frameworks"></a>Projektowanie struktury
Usługi aplikacji — cennik warstwy sterowania hello ilość zasobów obliczeniowych (Procesora, Magazyn danych na dysku, pamięci i wyjście sieci) tooapps dostępne. Jednak szerokość hello tooapps dostępnych funkcji framework pozostaje powitalne hello takie same, niezależnie od tego, skalowania warstwy.

Usługa aplikacji obsługuje różne środowiska deweloperskie, takich jak ASP.NET, klasyczne środowisko ASP, node.js, PHP i Python - wszystkich jest uruchomiony jako rozszerzenia w usługach IIS. W kolejności toosimplify i normalizacji konfiguracji zabezpieczeń, usługi aplikacji — aplikacje są zazwyczaj uruchamiane hello środowiska deweloperskie dla różnych z ustawień domyślnych. Jednym z podejść tooconfiguring aplikacji mogło być obszaru powierzchni toocustomize hello interfejsu API i funkcje dla każdego platforma programistyczna indywidualnych. Usługi aplikacji ma zamiast tego podejścia bardziej ogólnym przez włączenie linii bazowej typowych funkcji systemu operacyjnego, niezależnie od tego, platforma programistyczna aplikacji.

Witaj poniższe sekcje zawierają podsumowanie hello ogólne rodzaje aplikacje usługi dostępne tooApp funkcji systemu operacyjnego.

<a id="FileAccess"></a>

## <a name="file-access"></a>Dostęp do plików
Istnieją różne dyski w usługi aplikacji, w tym dyski lokalne i dyskach sieciowych.

<a id="LocalDrives"></a>

### <a name="local-drives"></a>Dyski lokalne
Zasadniczo usługi aplikacji — usługa jest uruchomiona na powitania infrastrukturze Azure PaaS (platforma jako usługa). Jako wynik hello dyski lokalne, które są "maszyny wirtualnej tooa dołączony" hello tej samej roli procesu roboczego tooany dostępne typy dysków działają na platformie Azure. Obejmuje to dysk systemu operacyjnego (hello dysku D:\), dysk aplikacji, który zawiera pliki cspkg pakietu Azure używany wyłącznie przez usługi App Service (i toocustomers niedostępny) i dysku "użytkownika" (hello dysku C:\), którego rozmiar może być różna w zależności od wielkości hello z hello maszyny Wirtualnej.

<a id="NetworkDrives"></a>

### <a name="network-drives-aka-unc-shares"></a>Dyski sieciowe (lub udziały UNC)
Jednym z unikatowe aspekty App Service ułatwia wdrażanie aplikacji i konserwacji prostego powitania jest że cała zawartość użytkownika są przechowywane na zbiór udziały UNC. Ten model bardzo dobrze mapuje toohello wspólnego wzorca przechowywania zawartości używana przez lokalną hostingu środowisk, w których wiele serwerów z równoważeniem obciążenia. 

W ramach usługi aplikacji istnieje liczba udziały UNC utworzone w każdej centrum danych. Procent hello zawartość użytkownika dla wszystkich klientów w każdym centrum danych jest przydzielany tooeach udziałem UNC. Ponadto całej zawartości pliku hello jednego odbiorcy subskrypcji jest zawsze umieszczane na powitania udziałem UNC w tym samym. 

Należy pamiętać, że powodu usługi w chmurze toohow pracy, hello określonej maszyny wirtualnej za hosting udziału UNC zmieni się wraz z upływem czasu. Jest gwarancji, że udziały UNC zostanie zainstalowany przez różnych maszyn wirtualnych zgodnie z ich wprowadzenia w górę i w dół podczas hello trakcie normalnego przebiegu operacji. Z tego powodu aplikacje powinny nie należy wprowadzać ustalony założenia, że informacje o maszynie hello w ścieżkę pliku UNC jest trwały na wraz z upływem czasu. Zamiast tego należy użyć hello wygodne *symulowane* ścieżkę bezwzględną **D:\home\site** udostępniający usługi aplikacji. To ścieżka bezwzględna symulowane udostępnia metodę portable, funkcja aplikacji i użytkownika odwoływania się tooone własnych aplikacji. Za pomocą **D:\home\site**, jeden transfer udostępnionych plików z tooapp aplikacji bez konieczności tooconfigure nową ścieżkę bezwzględną do każdego transferu.

<a id="TypesOfFileAccess"></a>

### <a name="types-of-file-access-granted-tooan-app"></a>Typy dostępu do pliku przyznane tooan aplikacji
Subskrypcja każdego klienta ma struktury katalogów zarezerwowane w udziale UNC określone w obrębie centrum danych. Klient może mieć wielu aplikacji utworzony w obrębie centrum danych, więc wszystkie katalogi hello należące tooa jednego odbiorcy subskrypcji są tworzone na powitania sam udziałem UNC. Witaj udział może obejmować katalogi, takich jak zawartość, błąd dzienników diagnostycznych i wcześniejszych wersjach aplikacji hello utworzone przez kontroli źródła. Zgodnie z oczekiwaniami, katalogów aplikacji klienta są dostępne do odczytu i zapisu w czasie wykonywania przez kod aplikacji hello aplikacji.

Na powitania dyski lokalne dołączony toohello maszyny wirtualnej, która uruchamia aplikację, fragmentu miejsca na dysku C:\ do tymczasowego przechowywania lokalnego specyficzny dla aplikacji hello rezerwuje usługi aplikacji. Mimo że aplikacja ma pełne odczytu/zapisu dostępu tooits własnych tymczasowego magazynu lokalnego, że magazynu naprawdę nie jest zamierzone toobe używana bezpośrednio przez kod aplikacji hello. Zamiast hello celem jest magazyn plików tymczasowych tooprovide dla struktury aplikacji sieci web i usług IIS. Usługi aplikacji również ogranicza ilość hello tymczasowego magazynu lokalnego tooeach dostępnych aplikacji tooprevent poszczególnymi aplikacjami zużywanie nadmiernej ilości pamięci masowej pliku lokalnego.

Dwa przykłady używaniu tymczasowy magazyn lokalny usługi aplikacji to hello katalogu plików tymczasowych ASP.NET i hello katalogu dla usług IIS skompresowane pliki. Hello system kompilacji platformy ASP.NET używa katalogu "Temporary ASP.NET Files" hello jako lokalizację pamięci podręcznej tymczasowego kompilacji. Usługi IIS używają hello "IIS skompresowane pliki tymczasowe" katalogu toostore skompresowane odpowiedzi w danych wyjściowych. Oba typy plików użycia (a także innych) są mapowane ponownie w magazynie lokalnym tymczasowego tooper aplikację usługi aplikacji. To ponowne mapowanie gwarantuje, że funkcja będzie nadal występować, zgodnie z oczekiwaniami.

Każdej aplikacji w usłudze App Service uruchamia nazywane tożsamość procesu losowy unikatowy roboczego niskich uprawnieniach hello "tożsamość puli aplikacji", dodatkowe opisane tutaj: [http://www.iis.net/learn/manage/configuring-security/application-pool-identities ](http://www.iis.net/learn/manage/configuring-security/application-pool-identities). Kod aplikacji będą używać tej tożsamości dla dysku systemu operacyjnego toohello podstawowego dostępu tylko do odczytu (hello dysku D:\). Oznacza to, kod aplikacji, można wyświetlić listę wspólnej struktury katalogu i odczytu wspólne pliki na dysku systemu operacyjnego. Mimo że to może występować toobe nieco szerokie poziom dostępu, hello samych katalogach, a pliki są dostępne podczas obsługi administracyjnej roli proces roboczy na platformie Azure usługa hostowana i odczytu zawartości dysku hello. 

<a name="multipleinstances"></a>

### <a name="file-access-across-multiple-instances"></a>Dostęp do plików w wielu wystąpieniach
Katalog macierzysty Hello zawiera zawartość aplikacji, a tooit napisać kod aplikacji. Jeśli aplikacja jest uruchamiana na wiele wystąpień, katalog macierzysty hello jest współdzielona przez wszystkie wystąpienia tak, aby wszystkie wystąpienia Zobacz hello tego samego katalogu. Tak na przykład jeśli aplikacja zapisuje katalogu macierzystego toohello przekazanych plików, pliki będą natychmiast dostępna tooall wystąpień. 

<a id="NetworkAccess"></a>

## <a name="network-access"></a>Dostęp do sieci
Kod aplikacji można używać protokołu TCP/IP i wychodzący toomake protokołów UDP, na podstawie sieci połączeń tooInternet dostępnych punktów końcowych z użyciem usług zewnętrznych. Aplikacje mogą korzystać z tych samym tooservices tooconnect protokołów w ramach Azure & #151, na przykład, ustanawiając tooSQL połączenia HTTPS bazy danych.

Istnieje również ograniczone możliwości aplikacji tooestablish jednego lokalnego sprzężenia zwrotnego połączenia, a aplikacji nasłuchiwać tego gniazda lokalnego sprzężenia zwrotnego. Ta funkcja istnieje głównie tooenable aplikacjom nasłuchiwania sockets lokalnego sprzężenia zwrotnego jako część ich funkcje. Należy pamiętać, że każda aplikacja widzi połączenie "prywatny" sprzężenia zwrotnego. Aplikacja "A" nie może nasłuchiwać gniazda lokalnego sprzężenia zwrotnego tooa ustanowione przez aplikację "B".

Nazwane potoki również są obsługiwane jako mechanizm komunikacji międzyprocesowej (IPC) między różnych procesów, które zbiorczo uruchomienia aplikacji. Na przykład moduł FastCGI usług IIS hello zależy od nazwanych potoków toocoordinate hello poszczególnych procesów uruchomionych stron PHP.

<a id="Code"></a>

## <a name="code-execution-processes-and-memory"></a>Wykonywanie kodu, procesów i pamięci
Jak wspomniano wcześniej, aplikacje będą działać wewnątrz procesów roboczych niskim poziomem uprawnień przy użyciu tożsamości puli aplikacji losowych. Kod aplikacji ma pamięć toohello dostępu skojarzone z hello proces roboczy, a także wszystkie podrzędne procesy, które mogą być zduplikowany przez procesy CGI lub innych aplikacji. Jednak jednej aplikacji nie może uzyskać dostęp do pamięci hello lub danych nawet wtedy, gdy znajduje się ona w innej aplikacji hello tej samej maszyny wirtualnej.

Aplikacje mogą być uruchamiane skrypty lub stron zapisanych z środowiska deweloperskie obsługiwanych w sieci web. Usługi aplikacji nie skonfigurować wszelkie web framework ustawienia toomore ograniczone tryby. Na przykład aplikacji ASP.NET uruchomionych w usłudze aplikacji Uruchom w relacji zaufania "pełnej" jako tryb zaufania min. tooa więcej ograniczone. Struktur sieci Web, w tym ASP klasycznego i ASP.NET, można wywołać składniki modelu COM w trakcie (ale nie poza składniki COM), takich jak ADO (ActiveX Data Objects), które są zarejestrowane domyślnie w systemie operacyjnym Windows hello.

Aplikacje można zduplikować i uruchomić dowolny kod. Jest dozwolony dla aplikacji toodo rzeczy jak zduplikować powłoki poleceń uruchom skrypt programu PowerShell. Jednak nawet jeśli dowolny kod i procesy można zduplikowany z aplikacji, programów wykonywalnych i skrypty są toohello nadal ograniczone uprawnienia przyznane toohello nadrzędnych puli aplikacji. Na przykład aplikację można zduplikować plik wykonywalny, który wykonuje wychodzące wywołanie HTTP, ale ten sam pliku wykonywalnego nie ma możliwości toounbind hello adres IP maszyny wirtualnej na podstawie jego karty sieciowej. Kod z uprawnieniami toolow wywołania wychodzącego jest dozwolone, ale próba tooreconfigure ustawienia sieci na maszynie wirtualnej wymaga uprawnień administracyjnych.

<a id="Diagnostics"></a>

## <a name="diagnostics-logs-and-events"></a>Dzienników diagnostyki i zdarzeń
Informacje w dzienniku jest inny zestaw danych, że niektóre aplikacje podejmować tooaccess. typy Hello toocode dostępne informacje dziennika działające w usłudze aplikacji obejmuje diagnostycznych i rejestrowanie informacji generowanych przez aplikację, która również jest łatwo dostępny toohello aplikacji. 

Na przykład W3C HTTP dzienniki generowane przez aktywnej aplikacji są dostępne, albo w katalogu dzienników w sieci hello udziału lokalizacji utworzone dla aplikacji hello lub dostępne w magazynie obiektów blob, jeśli klient nie został skonfigurowany toostorage rejestrowania W3C. druga opcję Hello umożliwia dużych ilości toobe dzienniki gromadzony bez ryzyka hello przekraczanie limitów magazynowania pliku hello skojarzonego z udziałem sieciowym.

W podobny szyjnej diagnostyki w czasie rzeczywistym informacji z aplikacji .NET mogą również być rejestrowane przy użyciu infrastruktury śledzenia i informacji diagnostycznych hello .NET, z opcji toowrite hello śledzenia informacji tooeither hello aplikacji udziału sieciowego lub tooa magazynu obiektów blob Lokalizacja.

Kwestie diagnostyki rejestrowania i śledzenia, które nie są dostępne tooapps zdarzenia ETW systemu Windows i typowych dzienniki zdarzeń systemu Windows (np. System, zabezpieczenia dzienniki zdarzeń aplikacji i). Zdarzenia tooETW odczytu i zapisu dla komputera (z hello prawej listy ACL), są zablokowane, ponieważ informacje o śledzeniu ETW potencjalnie może być widoczny. Deweloperzy mogą zauważyć tooread i zapisu zdarzenia ETW wywołania tego interfejsu API i wspólne dzienniki zdarzeń systemu Windows są wyświetlane toowork, ale wynika to z usługi aplikacji jest "faking" hello wywołań, aby były wyświetlane toosucceed. W rzeczywistości kodu aplikacji hello nie ma dostępu do toothis zdarzenia danych.

<a id="RegistryAccess"></a>

## <a name="registry-access"></a>Dostęp do rejestru
Aplikacje mają dostęp tylko do odczytu toomuch (choć nie wszystkie) rejestru hello hello maszyny wirtualnej jest uruchomiona. W praktyce oznacza to, że klucze rejestru, które umożliwiają dostęp tylko do odczytu toohello lokalnej grupy użytkowników są dostępne dla aplikacji. Jeden obszar rejestru hello, który nie jest obecnie obsługiwane dla odczytu lub zapisu jest hello HKEY\_bieżącego\_gałęzi użytkownika.

Dostęp do zapisu toohello rejestru jest zablokowany, w tym klucze rejestru użytkownika tooany dostępu. Z perspektywy aplikacji hello rejestru toohello zapisu powinno nigdy nie być stosowane w hello środowiska platformy Azure od aplikacji można (i wykonaj) Pobierz migracji w różnych maszyn wirtualnych. Hello tylko trwałego zapisywalny magazynu, który może być zależny od aplikacji jest struktura katalog zawartości dla aplikacji hello przechowywane na powitalne udziały UNC usługi aplikacji. 

## <a name="more-information"></a>Więcej informacji

[Azure Web App piaskownicy](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox) — Witaj większości aktualne informacje na temat środowiska wykonawczego hello usługi App Service. Ta strona jest obsługiwana bezpośrednio przez hello zespół deweloperów usługi aplikacji.

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 


