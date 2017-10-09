---
title: "Brama zarządzania dla fabryki danych aaaData | Dokumentacja firmy Microsoft"
description: "Konfigurowanie danych toomove bramy danych między lokalnymi i hello chmury. Użyj bramy zarządzania danymi w fabryce danych Azure toomove danych."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a>Brama zarządzania danymi
Brama zarządzania danymi Hello jest agent klienta, które muszą być zainstalowane w danych lokalnych środowiska toocopy między chmury i lokalnych magazynów danych. Witaj danych lokalnych magazynów danych fabryka obsługuje są wymienione w hello [obsługiwanych źródeł danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) sekcji.

W tym artykule uzupełnia wskazówki hello w hello [przenoszenie danych między lokalnymi i w chmurze magazyny danych](data-factory-move-data-between-onprem-and-cloud.md) artykułu. W przewodniku hello utworzysz potok, który korzysta z danych toomove bramy hello z tooan bazy danych programu SQL Server na lokalnych obiektów blob platformy Azure. Ten artykuł zawiera szczegółowe informacje szczegółowe na temat bramy zarządzania danymi hello. 

Możesz skalować w poziomie bramy zarządzania danymi hello bramy można skojarzyć wielu komputerach lokalnych. Możesz skalować w górę zwiększając liczbę zadań przepływu danych, które można uruchomić jednocześnie w węźle. Ta funkcja jest również dostępny do logicznego bramy z jednego węzła. Zobacz [skalowanie brama zarządzania danymi w fabryce danych Azure](data-factory-data-management-gateway-high-availability-scalability.md) artykułu, aby uzyskać szczegółowe informacje.

> [!NOTE]
> Obecnie brama obsługuje tylko działania kopiowania hello i działania procedury składowanej w fabryce danych. Nie jest możliwe toouse hello bramy z działań niestandardowych tooaccess lokalnych źródeł danych.      

## <a name="overview"></a>Omówienie
### <a name="capabilities-of-data-management-gateway"></a>Funkcje bramy zarządzania danymi
Brama zarządzania danymi zapewnia hello następujące możliwości:

* Model lokalnych źródeł danych i źródeł danych w chmurze w hello tej samej fabryki danych i przenoszenia danych.
* Ma jednego okienka szkła monitorowania i zarządzania wgląd w stan bramy z hello strony fabryki danych.
* Zarządzanie bezpieczny dostęp do lokalnych tooon źródła danych.
  * Zapora toocorporate konieczne żadne zmiany. Brama podejmuje tylko połączeń wychodzących oparte na protokole HTTP tooopen internet.
  * Szyfrowania poświadczeń dostępu do sieci lokalnych magazynów danych przy użyciu certyfikatu.
* Przenoszenie danych wydajnie — dane są przesyłane w równoległe, odpornych toointermittent problemy z siecią z logiki ponawiania próby automatycznego.

### <a name="command-flow-and-data-flow"></a>Polecenie przepływu i przepływu danych
Użycie danych toocopy działania kopiowania między lokalnymi i w chmurze, hello działanie używa danych tootransfer bramy z toocloud źródła danych lokalnie i na odwrót.

Poniżej przedstawiono przepływ danych wysokiego poziomu hello i podsumowanie kroków kopii danych bramy: ![przepływ danych przy użyciu bramy](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. Projektant danych tworzy bramy dla fabryki danych Azure przy użyciu albo hello [portalu Azure](https://portal.azure.com) lub [polecenia Cmdlet programu PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).
2. Projektant danych tworzy połączonej usługi magazynu danych lokalnych za pośrednictwem bramy hello. Jako część konfigurowania hello połączonej usługi, danych deweloperów używa typy uwierzytelniania toospecify hello poświadczenia ustawienia aplikacji i poświadczenia.  Witaj ustawienie poświadczeń, których aplikacji w oknie dialogowym komunikuje się z danymi hello przechowywać tootest połączenia i hello toosave poświadczeń bramy.
3. Brama szyfruje poświadczenia hello z certyfikatem hello skojarzone z bramą hello (dostarczonych przez dewelopera danych), przed zapisaniem hello poświadczeń w chmurze hello.
4. Usługi fabryka danych komunikuje się z bramą hello do planowania i zarządzanie zadań za pośrednictwem kanału kontroli, który używa kolejki magistrali usług Azure udostępnionych. Gdy zadanie działania kopiowania musi toobe rozpoczęte, fabryki danych kolejkuje Żądanie hello wraz z informacjami o poświadczenia. Brama dotyczącego hello zadania po sondowania hello kolejki.
5. Brama Hello odszyfrowuje hello poświadczeń z hello sam certyfikatu, a następnie łączy toohello z lokalnym magazynem danych o typie odpowiedniego uwierzytelnienia i poświadczenia.
6. Brama Hello kopiuje dane z magazynu w chmurze tooa lokalnego magazynu lub na odwrót w zależności od sposobu skonfigurowania hello działanie kopiowania w potoku danych hello. W tym kroku hello bramy komunikuje się bezpośrednio z usług magazynu w chmurze, takich jak magazyn obiektów Blob Azure za pośrednictwem bezpiecznego kanału (HTTPS).

### <a name="considerations-for-using-gateway"></a>Zagadnienia dotyczące korzystania z bramy
* Pojedyncze wystąpienie bramy zarządzania danymi może służyć do wielu źródeł danych lokalnych. Jednak **pojedyncze wystąpienie bramy jest jeden fabryki danych Azure wiązanej tooonly** i nie mogą być udostępniane innym fabryki danych.
* Może mieć **tylko jedno wystąpienie bramy zarządzania danymi** zainstalowane na jednym komputerze. Załóżmy, masz dwie fabryki danych, które wymagają tooaccess lokalnych źródeł danych, należy tooinstall bramy na dwóch lokalnych komputerów. Innymi słowy brama jest wiązana tooa danych specyficznych dla fabryki
* Witaj **bramy nie jest konieczne toobe na powitania sam komputer jako źródło danych hello**. Jednak o źródła danych toohello bliżej bramy skraca czas powitania dla źródła danych toohello tooconnect bramy hello. Zalecamy zainstalowanie bramy hello na maszynie, która różni się od hello jednego źródła danych lokalnych hostów. Gdy hello bramy i źródła danych na różnych komputerach, hello bramy nie konkurować o zasoby z źródła danych.
* Może mieć **wielu bram na różnych komputerach łączenie toohello tego samego źródła danych lokalnych**. Na przykład może mieć dwóch bram obsługująca fabryki dwóch danych, ale powitalne tego samego źródła danych lokalnych jest zarejestrowany w obu hello fabryki danych.
* Jeśli masz już bramy zainstalowanej na programu obsługi komputera **usługi Power BI** scenariuszu instalowanie **oddzielnej bramy dla fabryki danych Azure** na innym komputerze.
* Można używać bramy, nawet wtedy, gdy używasz **ExpressRoute**.
* Traktuj źródła danych jako źródło danych lokalnych (który znajduje się za zaporą) nawet jeśli używasz **ExpressRoute**. Użyj hello bramy tooestablish łączność między usługą hello i hello źródła danych.
* Należy **Użyj bramy hello** nawet, jeśli magazyn danych hello jest w chmurze hello na **maszyny Wirtualnej Azure IaaS**.

## <a name="installation"></a>Instalacja
### <a name="prerequisites"></a>Wymagania wstępne
* Witaj obsługiwane **systemu operacyjnego** wersje to Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Instalacja hello brama zarządzania danymi na kontrolerze domeny nie jest obecnie obsługiwana.
* .NET framework 4.5.1 lub nowszy jest wymagany. Jeśli instalujesz bramę na komputerze z systemem Windows 7, zainstaluj program .NET Framework 4.5 lub nowszej. Zobacz [wymagania systemowe programu .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) szczegółowe informacje.
* Witaj zalecane **konfiguracji** hello maszyna bramy jest co najmniej 2 GHz 4 rdzenie, 8 GB pamięci RAM i dysk 80 GB.
* Hibernacja hello komputer hosta, hello bramy nie odpowiada toodata żądań. W związku z tym, skonfigurować odpowiednie **planu zasilania** na komputerze hello przed zainstalowaniem bramy hello. Jeśli maszyna hello jest skonfigurowany toohibernate, instalacja bramy hello monituje komunikat.
* Musisz mieć uprawnienia administratora na powitania tooinstall maszyny i skonfigurować brama zarządzania danymi hello pomyślnie. Możesz dodać kolejnych użytkowników toohello **brama zarządzania danymi użytkowników** lokalnej grupy systemu Windows. Hello członkami tej grupy są hello stanie toouse **Menedżera konfiguracji bramy zarządzania danymi** narzędzie tooconfigure hello bramy.

Jak skopiować uruchomień działania wystąpić na określonej częstotliwości, hello użycia zasobów (procesora CPU, pamięci) na maszynie hello również następuje hello sam wzorca z szczytowe i czas bezczynności. Wykorzystanie zasobów zależy również od silnie hello ilość danych, jest przenoszony. W przypadku wielu kopii zadania w toku, zostanie wyświetlony użycia zasobów, do góry w godzinach szczytu.

### <a name="installation-options"></a>Opcje instalacji
Brama zarządzania danymi można zainstalować w hello następujące sposoby:

* Instalując pakiet Instalatora MSI ze hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).  Witaj MSI może być również używane tooupgrade istniejących danych zarządzania bramy toohello najnowszej wersji, z ustawieniami wszystkie zachowane.
* Klikając **pobieranie i instalowanie bramy danych** łącze w PODRĘCZNIKU instalacji lub **Zainstaluj bezpośrednio na tym komputerze** w obszarze Ustawienia EXPRESS. Zobacz [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje na temat używania instalacji ekspresowej. krok wykonywany ręcznie Hello przyjmuje toohello Centrum pobierania.  Witaj instrukcje dotyczące pobierania i instalowania bramy hello z Centrum pobierania znajdują się w następnej sekcji hello.

### <a name="installation-best-practices"></a>Najlepsze rozwiązania dotyczące instalacji:
1. Skonfiguruj planu zasilania na komputerze-hoście hello hello bramy, dzięki czemu hello maszyny nie hibernacji. Hibernacja hello komputer hosta, hello bramy nie odpowiada toodata żądań.
2. Utwórz kopię zapasową certyfikatu hello skojarzone z bramą hello.

### <a name="install-hello-gateway-from-download-center"></a>Zainstaluj bramę hello z Centrum pobierania
1. Przejdź za[stronę pobierania brama zarządzania danymi firmy Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).
2. Kliknij przycisk **Pobierz**, wybierz hello odpowiednią wersję (**32-bitowych** vs. **64-bitowych**) i kliknij przycisk **dalej**.
3. Uruchom hello **MSI** bezpośrednio lub zapisać go tooyour dysku twardego i uruchom.
4. Na powitania **powitalnej** wybierz pozycję **języka** kliknij **dalej**.
5. **Zaakceptuj** hello umowę licencyjną użytkownika oprogramowania i kliknij przycisk **dalej**.
6. Wybierz **folderu** tooinstall hello bramy i kliknij przycisk **dalej**.
7. Na powitania **gotowe tooinstall** kliknij przycisk **zainstalować**.
8. Kliknij przycisk **Zakończ** toocomplete instalacji.
9. Pobierz klucz hello z hello portalu Azure. Zobacz następną sekcję hello instrukcje krok po kroku.
10. Na powitania **bramy rejestru** strony **Menedżera konfiguracji bramy zarządzania danymi** na komputerze, hello następujące kroki:
    1. Wklej tekst hello hello klucza.
    2. Opcjonalnie kliknij **klucz bramy Pokaż** toosee hello klucza tekstu.
    3. Kliknij przycisk **zarejestrować**.

### <a name="register-gateway-using-key"></a>Rejestrowanie bramy przy użyciu klucza
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a>Jeśli nie zostało utworzone logicznej bramy w portalu hello
toocreate bramy w kluczu hello portalu i get hello z hello **Konfiguruj** strony, wykonaj kroki z wskazówki w hello [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a>Jeśli brama logicznej hello zostały już utworzone w portalu hello
1. W portalu Azure Przejdź toohello **fabryki danych** , a następnie kliknij przycisk **połączonych usług** kafelka.

    ![Strona fabryki danych](media/data-factory-data-management-gateway/data-factory-blade.png)
2. W hello **połączonych usług** strony logicznej wybierz hello **bramy** utworzone w portalu hello.

    ![logiczne bramy](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. W hello **bramy danych** kliknij przycisk **pobieranie i instalowanie bramy danych**.

    ![Pobierz łącze w portalu hello](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. W hello **Konfiguruj** kliknij przycisk **ponowne tworzenie klucza**. Kliknij przycisk Tak na komunikat ostrzegawczy powitania po odczytaniu jej starannie.

    ![Ponowne tworzenie klucza](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Kliknij przycisk Kopiuj dalej klucz toohello. klucz Hello jest skopiowany toohello Schowka.

    ![Kopiowanie klucza](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>Ikony systemowe na pasku zadań / powiadomienia
Witaj poniższej ilustracji przedstawiono niektóre hello ikony na pasku zadań, które są wyświetlane.

![ikony systemowe na pasku zadań](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

Jeśli Przenieś kursor nad komunikat ikona/powiadomień na pasku zadań systemu hello, zobaczysz szczegółowe informacje o stanie hello hello operacji bramy/aktualizacji w oknie podręcznym.

### <a name="ports-and-firewall"></a>Porty i zapory
Istnieją dwa zapory należy tooconsider: **firmowej zapory** uruchomiony na routerze centralnej hello organizacji hello i **zapory systemu Windows** skonfigurowany jako demon na komputerze lokalnym hello, gdzie hello Brama jest instalowana.  

![zapory](./media/data-factory-data-management-gateway/firewalls2.png)

Na poziomie firmowa zapora, należy skonfigurować hello następujące domeny i portów wychodzących:

| Nazwy domen | Porty | Opis |
| --- | --- | --- |
| *. servicebus.windows.net |443, 80 |Używany do komunikacji z zapleczem usługi przenoszenia danych |
| *. core.windows.net |443 |Używany do kopiowania przejściowa przy użyciu obiektów Blob platformy Azure (jeśli jest skonfigurowane)|
| *. frontend.clouddatahub.net |443 |Używany do komunikacji z zapleczem usługi przenoszenia danych |


Na poziomie zapory systemu Windows te porty wyjściowe zwykle są włączone. Nie można skonfigurować portów i domen hello odpowiednio na maszynie bramy.

> [!NOTE]
> 1. Na podstawie Twojego źródła / sink mogą mieć dodatkowe domeny toowhitelist i portów wychodzących w sieci firmowej/Zapora systemu Windows.
> 2. Dla niektórych baz danych w chmurze (na przykład: [bazy danych SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [usługi Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), itd.), może być konieczne toowhitelist adres IP komputera bramy na ich konfiguracji zapory.
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a>Kopiowanie danych z magazynu danych źródła danych magazynu tooa odbioru
Sprawdź, czy reguły zapory hello są włączone prawidłowo na powitania firmowej zapory, Zapora systemu Windows na komputerze bramy hello, i magazyn danych hello, sam. Włączenie tych zasad umożliwia hello bramy tooconnect tooboth źródła i sink pomyślnie. Włącz reguły dla każdego magazynu danych, który jest używany w operacji kopiowania hello.

Na przykład toocopy z **ujścia danych bazy danych SQL Azure tooan magazynu lokalnego lub ujścia magazynu danych SQL Azure**, hello następujące kroki:

* Zezwalaj na wychodzące **TCP** komunikację za pośrednictwem portu **1433** dla zapory systemu Windows i firmowej zapory.
* Skonfiguruj ustawienia zapory hello Azure SQL tooadd hello adresu IP serwera hello bramy maszyny toohello listę dozwolonych adresów IP.

> [!NOTE]
> Jeśli Zapora nie zezwala na wychodzący port 1433, brama nie bezpośredni dostęp Azure SQL. W takim przypadku można użyć [przemieszczane kopiowania](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL bazy danych platformy Azure / SQL Azure DW. W tym scenariuszu do przenoszenia danych hello są tylko wymagane HTTPS (port 443).
>
>


### <a name="proxy-server-considerations"></a>Zagadnienia dotyczące serwera proxy
Jeśli środowisko sieci firmowej używa serwera proxy serwera tooaccess hello internet, skonfigurować danych zarządzania bramy toouse odpowiednie ustawienia serwera proxy. W fazie początkowe rejestracyjny hello można ustawić powitania serwera proxy.

![Zestaw proxy podczas rejestracji](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

Brama używa powitania serwera proxy serwera tooconnect toohello chmury usługi. Kliknij przycisk **zmiany** łącze podczas instalacji początkowej. Zobacz hello **ustawienie serwera proxy** okna dialogowego.

![Zestaw serwera proxy przy użyciu Menedżera konfiguracji](media/data-factory-data-management-gateway/SetProxySettings.png)

Dostępne są trzy opcje konfiguracji:

* **Nie używaj serwera proxy**: bramy nie używa jawnie żadnych usług toocloud tooconnect serwera proxy.
* **Użyj serwera proxy systemu**: hello serwera proxy, ustawienie skonfigurowane w diahost.exe.config i diawp.exe.config używa bramy.  Jeśli żadnego serwera proxy jest skonfigurowany w diahost.exe.config i diawp.exe.config, nawiązanie połączenia bramy usługi toocloud bezpośrednio, bez przechodzenia przez serwer proxy.
* **Użyć niestandardowego serwera proxy**: Konfigurowanie toouse ustawienia serwera proxy hello HTTP bramy, zamiast konfiguracje diahost.exe.config i diawp.exe.config.  Wymagane są adres i Port.  Nazwa użytkownika i hasło są opcjonalne, w zależności od ustawienia uwierzytelniania serwer proxy.  Wszystkie ustawienia są zaszyfrowane za pomocą hello certyfikat poświadczeń bramy hello i przechowywane lokalnie na komputerze-hoście hello bramy.

Brama zarządzania danymi Hello usługi hosta do automatycznego uruchomienia po zapisaniu hello zaktualizować ustawienia serwera proxy.

Po brama została pomyślnie zarejestrowana, tooview lub zaktualizować ustawienia serwera proxy, należy użyć Menedżera konfiguracji bramy zarządzania danymi.

1. Uruchom **Menedżera konfiguracji bramy zarządzania danymi**.
2. Przełącz toohello **ustawienia** kartę.
3. Kliknij przycisk **zmiany** łącze w **serwer HTTP Proxy** hello toolaunch sekcji **ustawiony serwer Proxy HTTP** okna dialogowego.  
4. Po kliknięciu hello **dalej** przycisku, zobacz okno dialogowe ostrzeżenia pytania dla użytkownika ustawienia proxy hello toosave uprawnień i uruchom ponownie hello usługa hosta bramy.

Można wyświetlać i aktualizować serwer proxy HTTP za pomocą narzędzia Configuration Manager.

![Zestaw serwera proxy przy użyciu Menedżera konfiguracji](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> Jeśli skonfigurowano serwer proxy z uwierzytelnianiem NTLM usługa hosta bramy jest uruchamiana hello konta domeny. Jeśli zmienisz hasło konta domeny hello później hello, pamiętaj tooupdate ustawienia konfiguracji dla usługi hello i odpowiednio uruchom go ponownie. Ze względu na wymagania toothis zaleca się, że używasz domeny dedykowanego konta tooaccess powitania serwera proxy, który nie jest wymagane hasło hello tooupdate często.
>
>

### <a name="configure-proxy-server-settings"></a>Skonfiguruj ustawienia serwera proxy
W przypadku wybrania **użycia serwera proxy systemu** ustawienie serwera proxy hello HTTP, brama używa hello ustawienie serwera proxy w diahost.exe.config i diawp.exe.config.  Jeśli w diahost.exe.config i diawp.exe.config określono żadnego serwera proxy, nawiązanie połączenia bramy usługi toocloud bezpośrednio, bez przechodzenia przez serwer proxy. Witaj Poniższa procedura zawiera instrukcje dotyczące aktualizacji hello diahost.exe.config pliku.  

1. W Eksploratorze plików tworzą kopię bezpieczne tooback C:\Program Files\Microsoft danych zarządzania Gateway\2.0\Shared\diahost.exe.config hello oryginalnego pliku.
2. Uruchamianie Notepad.exe uruchomioną jako administrator, a następnie otwórz plik tekstowy "C:\Program Files\Microsoft danych zarządzania Gateway\2.0\Shared\diahost.exe.config. Hello domyślny znacznik można znaleźć system.net pokazane na powitania następującego kodu:

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   Następnie można dodać szczegóły serwera proxy, jak pokazano w hello poniższy przykład:

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   Dodatkowe właściwości są dozwolone wewnątrz hello proxy tag toospecify hello wymagane ustawienia, takie jak scriptLocation. Odwołuje się zbyt[serwera proxy elementu (ustawienia sieciowe)](https://msdn.microsoft.com/library/sa91de1e.aspx) na składni.

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Zapisanie pliku konfiguracyjnego hello w hello oryginalnej lokalizacji, a następnie uruchom ponownie hello usługi hosta bramy zarządzania danymi, które przejmuje hello zmiany. Usługa hello toorestart: użyj apletu usługi w Panelu sterowania hello, lub z hello **Menedżera konfiguracji bramy zarządzania danymi** > kliknij hello **Zatrzymaj usługę** przycisk, a następnie kliknij przycisk hello **Uruchomić usługę**. Jeśli hello usługa nie zostanie uruchomiona, istnieje prawdopodobieństwo, że dodano niepoprawną składnię tagu XML w pliku konfiguracyjnym aplikacji hello, który był edytowany.

> [!IMPORTANT]
> Nie zapomnij tooupdate **zarówno** diahost.exe.config i diawp.exe.config.  


Ponadto punkty toothese, należy również toomake się, że w dozwolonych w firmie Microsoft Azure. Witaj listę prawidłowych adresów IP firmy Microsoft Azure można pobrać z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>Symptomów zapory i serwera proxy problemów związanych z serwerami
Jeśli wystąpią toohello podobne błędy po takich, które prawdopodobnie ukończenia konfiguracji tooimproper hello zapory lub serwera proxy, która blokuje bramy z łączącego tooauthenticate fabryki tooData sam. Zobacz tooensure sekcji tooprevious Serwer zapory i serwera proxy są poprawnie skonfigurowane.

1. Podczas próby tooregister hello bramy otrzymasz hello następujący błąd: "klucz bramy hello tooregister nie powiodło się. Przed podjęciem ponownej próby klucz bramy hello tooregister, upewnij się, że powitalne brama zarządzania danymi jest w stanie połączenia i hello usługa hosta bramy zarządzania danymi została uruchomiona."
2. Po otwarciu Menedżera konfiguracji zostanie wyświetlony stan jako "Rozłączono" lub "Łączenie." Podczas przeglądania dzienników zdarzeń systemu Windows, w obszarze "Podglądu zdarzeń" > "I usługi Dzienniki aplikacji" > "Brama zarządzania danymi", można wyświetlić komunikaty o błędach, takich jak hello następujący błąd:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>Otwórz port 8050 na potrzeby szyfrowania poświadczeń
Hello **ustawienie poświadczeń** zastosowań aplikacji hello portu wejściowego **8050** toorelay poświadczenia toohello bramy podczas konfigurowania lokalnego połączonej usługi w hello portalu Azure. Podczas instalacji bramy domyślnie instalacja bramy hello powoduje otwarcie go na komputerze bramy hello.

Jeśli używasz zapory innych firm, można ręcznie otwórz hello port 8050. Jeśli napotkasz problem zapory podczas instalacji bramy można spróbować użyć następującego polecenia tooinstall hello bramy bez konfigurowania zapory hello hello.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Jeśli wybierzesz nie tooopen hello portu 8050 na komputerze bramy hello używa mechanizmów innych niż z użyciem hello **ustawienie poświadczeń** poświadczeń magazynu danych tooconfigure aplikacji. Na przykład można użyć [AzureRmDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/mt603802.aspx) polecenia cmdlet programu PowerShell. Zobacz [ustawienie poświadczeń i zabezpieczeń](#set-credentials-and-securityy) sekcję na temat sposobu poświadczeń magazynu danych można ustawić.

## <a name="update"></a>Aktualizacja
Domyślnie gdy dostępna jest nowsza wersja bramy hello brama zarządzania danymi jest automatycznie aktualizowany. Hello bramy nie jest aktualizowana, aż wszystkie hello zaplanowane zadania są wykonywane. Kolejne zadania są przetwarzane przez bramę hello aż do zakończenia operacji aktualizacji hello. W przypadku niepowodzenia aktualizacji hello bramy jest przywracana toohello starą wersję.

Zostanie wyświetlony hello zaplanowane czas aktualizacji w następujących miejscach hello:

* strony właściwości bramy Hello w hello portalu Azure.
* Strona główna hello Menedżera konfiguracji bramy zarządzania danymi
* Komunikat powiadomienia na pasku zadań systemu.

na karcie Strona główna Hello hello Menedżera konfiguracji bramy zarządzania danymi Wyświetla harmonogram aktualizacji hello i hello ostatni czas hello bramy zostało zainstalowane zaktualizowane.

![Aktualizacje harmonogramu](media/data-factory-data-management-gateway/UpdateSection.png)

Można zainstalować aktualizację powitania od razu lub zaczekaj na powitania bramy toobe automatycznie zaktualizowany w momencie hello zaplanowane. Na przykład powitania po pokazuje obrazu hello komunikatu powiadomienia pokazanym w hello Menedżera konfiguracji bramy wraz z przycisku Aktualizuj powitania kliknij tooinstall go.

![Aktualizacja w DMG programu Configuration Manager](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

Hello komunikatu powiadomienia w hello na pasku zadań będzie wyglądać jak pokazano w powitania po obrazu:

![Komunikat na pasku zadań systemu](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

Możesz wyświetlić stan hello operacji aktualizacji (ręczne lub automatyczne) hello na pasku zadań. Po następnym uruchomieniu Menedżera konfiguracji bramy zostanie wyświetlony komunikat na pasek tej bramy hello powiadomień hello została zaktualizowana wraz z linkiem zbyt[co to jest nowy temat](data-factory-gateway-release-notes.md).

### <a name="toodisableenable-auto-update-feature"></a>Włącz/toodisable funkcji automatycznej aktualizacji
Użytkownik może Włącz/Wyłącz hello funkcja Aktualizacje automatyczne, wykonując następujące kroki hello:

[Dla jednego węzła bramy]
1. Uruchom program Windows PowerShell na komputerze bramy hello.
2. Przełącz folderu C:\Program Files\Microsoft danych zarządzania Gateway\2.0\PowerShellScript toohello.
3. Witaj uruchom następujące polecenie tooturn hello automatycznej aktualizacji funkcji OFF (wyłączone).   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. tooturn je ponownie:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[Wielowęzłowego wysoką dostępność i skalowalność bramy (wersja zapoznawcza)](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Uruchom program Windows PowerShell na komputerze bramy hello.
2. Przełącz folderu C:\Program Files\Microsoft danych zarządzania Gateway\2.0\PowerShellScript toohello.
3. Witaj uruchom następujące polecenie tooturn hello automatycznej aktualizacji funkcji OFF (wyłączone).   

    Bramy o wysokiej dostępności funkcji (wersja zapoznawcza) wymagany jest dodatkowy param AuthKey.
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. tooturn je ponownie:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
Jeśli dostęp do portalu hello na komputerze, który różni się od hello maszyna bramy, należy się upewnić że hello Menedżer poświadczeń aplikacji mogą się łączyć maszyna bramy toohello. Jeśli aplikacja hello można nawiązać połączenia z hello maszyna bramy, jego nie zezwala tooset poświadczeń dla źródła danych hello i źródła danych toohello połączenia tootest.  

Jeśli używasz hello **ustawienie poświadczeń** aplikacji, hello portal szyfruje poświadczenia hello z hello certyfikatu podanego w hello **certyfikatu** kartę hello **bramy Menedżer konfiguracji** na komputerze bramy hello.

Jeśli szukasz oparty na interfejsach API podejście do szyfrowania poświadczeń hello, możesz użyć hello [AzureRmDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/mt603802.aspx) poświadczenia tooencrypt polecenia cmdlet programu PowerShell. polecenie cmdlet Hello używa certyfikatów hello, że brama jest skonfigurowany toouse tooencrypt hello poświadczeń. Dodaj zaszyfrowane poświadczenia toohello **EncryptedCredential** element hello **connectionString** w hello JSON. Użyj hello JSON z hello [AzureRmDataFactoryLinkedService nowy](https://msdn.microsoft.com/library/mt603647.aspx) polecenia cmdlet lub hello Edytor fabryki danych.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

Jest jednym z podejść więcej do ustawiania poświadczeń przy użyciu Edytor fabryki danych. W przypadku utworzenia programu SQL Server połączone usługi za pomocą edytora hello i należy wprowadzić poświadczenia w postaci zwykłego tekstu, hello poświadczenia są szyfrowane za pomocą certyfikatu, który jest właścicielem hello usługi fabryka danych. Nie używa certyfikatów hello, że brama jest skonfigurowany toouse. Takie podejście może być nieco szybsze w niektórych przypadkach, jest mniej bezpieczne. Dlatego zaleca się, należy wykonać takie podejście tylko na potrzeby tworzenia/testowania.

## <a name="powershell-cmdlets"></a>Polecenia cmdlet programu PowerShell
W tej sekcji opisano sposób toocreate i zarejestrować bramę za pomocą poleceń cmdlet programu Azure PowerShell.

1. Uruchom **programu Azure PowerShell** w trybie administratora.
2. Zaloguj się za tooyour konto platformy Azure, uruchamiając hello następujące polecenia i wprowadzić poświadczenia platformy Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Użyj hello **AzureRmDataFactoryGateway nowy** toocreate polecenia cmdlet logicznej bramy w następujący sposób:

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    **Przykład polecenia i dane wyjściowe**:

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. W programie Azure PowerShell przełącznika folderu toohello: **C:\Program Files\Microsoft danych zarządzania Gateway\2.0\PowerShellScript\**. Uruchom **RegisterGateway.ps1** skojarzone ze zmienną lokalne powitania **$Key** pokazane na powitania następujące polecenia. Ten skrypt rejestruje agenta klienta hello zainstalowanej na komputerze z bramą logicznej hello utworzone wcześniej.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    Za pomocą parametru IsRegisterOnRemoteMachine hello można zarejestrować bramy hello na komputerze zdalnym. Przykład:

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. Można użyć hello **Get-AzureRmDataFactoryGateway** polecenia cmdlet tooget hello lista bram w fabryce danych. Gdy hello **stan** pokazuje **online**, oznacza to, brama jest gotowy toouse.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
Można usunąć bramy przy użyciu hello **AzureRmDataFactoryGateway Usuń** opis polecenia cmdlet i aktualizacji bramy przy użyciu hello **AzureRmDataFactoryGateway zestaw** polecenia cmdlet. Składnię i inne szczegółowe informacje o tych poleceniach cmdlet zobacz odwołanie do polecenia Cmdlet fabryki danych.  

### <a name="list-gateways-using-powershell"></a>Lista bram przy użyciu programu PowerShell

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>Usuń bramę przy użyciu programu PowerShell

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>Następne kroki
* Zobacz [przenoszenie danych między lokalnymi i w chmurze magazyny danych](data-factory-move-data-between-onprem-and-cloud.md) artykułu. W przewodniku hello utworzysz potok, który korzysta z danych toomove bramy hello z tooan bazy danych programu SQL Server na lokalnych obiektów blob platformy Azure.  
