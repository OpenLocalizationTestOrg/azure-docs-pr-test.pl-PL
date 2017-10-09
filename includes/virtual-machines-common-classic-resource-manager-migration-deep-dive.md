## <a name="meaning-of-migration-of-iaas-resources-from-hello-classic-deployment-model-tooresource-manager"></a>Znaczenie migracji zasobów IaaS z hello wdrażania klasycznego modelu tooResource Manager
Przed możemy przejść do szczegółów hello, Przyjrzyjmy się hello różnica między operacjami płaszczyzna danych i zarządzania płaszczyzny hello zasobów IaaS.

* *Zarządzanie i kontrola płaszczyzny* opisuje hello wywołania, które wchodzą w płaszczyźnie zarządzania i kontrola hello lub hello interfejsu API modyfikowania zasobów. Na przykład operacje takie jak tworzenie maszyny Wirtualnej, ponownego uruchamiania maszyny Wirtualnej i aktualizowania nową podsieć sieci wirtualnej zarządzać hello systemem zasobów. Bezpośrednio nie mają wpływu na wystąpień toohello nawiązującego połączenie.
* *Płaszczyzna danych* (aplikacja) opisano środowiska uruchomieniowego hello o sama aplikacja hello i wymaga interakcji z wystąpieniami, które nie korzystają z interfejsu API Azure hello. Uzyskanie dostępu do witryny internetowej lub pobranie danych z uruchomionego wystąpienia programu SQL Server lub serwera MongoDB jest traktowane jako interakcja z płaszczyzną danych lub aplikacją. Kopiowanie obiektu blob z konta magazynu i uzyskiwania dostępu do publicznej tooRDP adres IP lub SSH do maszyny wirtualnej hello są także płaszczyzna danych. Te operacje Zachowaj aplikacji hello uruchamiany obliczeniowych, sieci i magazynu.

Tle hello płaszczyzna danych hello jest hello tego samego między zarówno hello klasycznego modelu wdrożenia i stosu usługi Resource Manager. Podczas procesu migracji możemy tłumaczenie hello reprezentację hello zasobów z hello Classic deployment model toothat w stosie usługi Resource Manager hello. W związku z tym należy toouse nowych narzędzi, interfejsów API, zestawy SDK toomanage zasobów w stosie usługi Resource Manager hello.

![Zrzut ekranu, który ilustruje różnice między płaszczyzną zarządzania/kontroli i płaszczyzną danych](../articles/virtual-machines/media/virtual-machines-windows-migration-classic-resource-manager/data-control-plane.png)


> [!NOTE]
> W niektórych scenariuszach migracji hello platformy Azure zatrzymuje cofa alokację i ponowne uruchomienie maszyn wirtualnych. To wiąże się z krótkim przestojem płaszczyzny danych.
>

## <a name="hello-migration-experience"></a>środowisko migracji Hello
Przed rozpoczęciem obsługi migracji hello zaleca się następujące hello:

* Upewnij się, że hello zasoby, które mają toomigrate nie używaj nieobsługiwanych funkcji ani konfiguracji. Zazwyczaj platformy hello wykrywa te problemy i generuje błąd.
* Jeśli masz maszyny wirtualne, które nie znajdują się w sieci wirtualnej, ich zostanie zatrzymany i alokację jako część hello przygotować operację. Jeśli nie chcesz toolose hello publicznego adresu IP, wygląd do rezerwowania adresów IP hello przed wyzwalania hello przygotować operację. Jednak w przypadku maszyn wirtualnych hello w sieci wirtualnej, są nie zatrzymana i alokację.
* Planowanie migracji podczas tooaccommodate poza godzinami pracy na nieoczekiwane awarie, które mogą wystąpić podczas migracji.
* Pobierz hello bieżącej konfiguracji maszyn wirtualnych przy użyciu programu PowerShell, interfejsu wiersza polecenia (CLI) poleceń lub interfejsów API REST toomake łatwiejsze do sprawdzania poprawności po krok przygotowania hello jest ukończone.
* Aktualizacji modelu wdrażania Menedżera zasobów hello toohandle automatyzacji/operationalization skrypty, przed rozpoczęciem powitalne migracji. Opcjonalnie można wykonać operacji GET, jeśli hello zasoby są w hello przygotowane stanu.
* Należy ocenić hello RBAC zasad, które są skonfigurowane na powitania klasycznych zasobów IaaS i planowanie po zakończeniu migracji hello.

przepływ pracy migracji Hello jest następujący

![Zrzut ekranu pokazujący hello przebieg migracji](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-workflow.png)

> [!NOTE]
> Wszystkie operacje hello opisanego w hello następujące sekcje są idempotentności. Jeśli masz problem niż nieobsługiwanej funkcji lub błąd konfiguracji, zaleca się możesz ponowić próbę hello przygotowanie, przerwania lub przekazania operacji. Witaj platformy Azure próbuje hello akcję ponownie.
>
>

### <a name="validate"></a>Walidacja
Operacja sprawdzania poprawności Hello jest hello pierwszym krokiem w procesie migracji hello. Witaj celem tego kroku jest stan hello tooanalyze hello zasobów ma toomigrate w hello klasycznego modelu wdrażania i zwraca powodzeń/niepowodzeń, jeśli hello zasoby są w stanie migracji.

Wybraniu hello sieci wirtualnej lub usługi w chmurze (Jeśli nie znajduje się w sieci wirtualnej) mają toovalidate do migracji.

* Hello zasobu nie jest zdolny do migracji, dlaczego nie jest obsługiwane przez migrację wszystkich przyczyny hello Wyświetla hello platformy Azure.

#### <a name="checks-not-done-in-validate"></a>Testy nie wykonane w weryfikacji

Sprawdź poprawność operacji tylko analizuje stan hello hello zasobów w hello klasycznego modelu wdrażania. Może ono sprawdzić wszystkie błędy i nieobsługiwane scenariusze ukończenia konfiguracji toovarious hello klasycznego modelu wdrażania. Nie jest możliwe toocheck dotyczące wszystkich problemów z hello stosu mogą nakładać się na powitania zasobów podczas migracji Menedżera zasobów Azure. Te problemy tylko są sprawdzane, jeśli zasoby hello poddaje transformacji w następnym kroku hello migracji, to znaczy Prepare. Hello w poniższej tabeli wymieniono wszystkie problemy hello nie zaewidencjonowano weryfikacji.


|Sprawdzanie sieci nie znajduje się w weryfikacji|
|-|
|Posiadanie zarówno ER, jak i sieci VPN bramy sieci wirtualnej|
|Połączenie bramy sieci wirtualnej w rozłączyć stanu|
|Wszystkie łącza ER są wstępnie migrowane tooAzure stosu usługi Resource Manager|
|Przydziału Menedżera zasobów Azure sprawdza, czy zasoby sieciowe, oznacza to, statycznego publicznego adresu IP, dynamiczne publiczne adresy IP, usługi równoważenia obciążenia, grup zabezpieczeń sieci, tabele tras, interfejsy sieciowe |
| Sprawdź, czy wszystkie reguły modułu równoważenia obciążenia są prawidłowe między wdrożenia/sieci Wirtualnej |
| Sprawdź, czy powodujące konflikt prywatnych adresów IP między alokację zatrzymania maszyny wirtualne w hello sam sieci Wirtualnej |

### <a name="prepare"></a>Przygotowanie
Witaj przygotowanie operacji jest hello drugim krokiem w procesie migracji hello. Hello celem tego kroku jest toosimulate transformacji hello hello zasobów IaaS z wdrażania klasycznego modelu tooResource Menedżera zasobów i stanowi to obok siebie dla Ciebie toovisualize.

> [!NOTE] 
> Klasycznym zasobów nie są modyfikowane w tym kroku. Dlatego jest toorun bezpieczne krok Jeśli zastanawiasz się migracji. 

Wybrania hello wirtualnych sieci lub hello usługi w chmurze (Jeśli nie jest sieć wirtualną) mają tooprepare do migracji.

* Witaj zasobu nie jest zdolny do migracji, hello platformy Azure powoduje zatrzymanie procesu migracji hello list lub Przyczyna hello Dlaczego hello przygotowanie operacja nie powiodła się.
* Jeśli zasób hello jest w stanie migracji, hello platformy Azure najpierw blokuje operacje zarządzania płaszczyzny hello hello zasobów w ramach migracji. Na przykład nie jesteś stanie tooadd tooa dysku danych maszyny Wirtualnej w ramach migracji.

Witaj platformy Azure następnie uruchamia migracji hello metadanych z wdrażania klasycznego modelu tooResource Manager dla hello migracji zasobów.

Po przygotowanie hello operacja została zakończona, dostępna opcja hello wizualizacja hello zasobów w klasycznym modelu wdrażania i Menedżera zasobów. Dla każdej usługi w chmurze w hello klasycznego modelu wdrażania hello platforma Azure tworzy nazwę grupy zasobów, które ma wzorzec hello `cloud-service-name>-Migrated`.

> [!NOTE]
> Nie jest możliwe tooselect hello Nazwa grupy zasobów utworzonej dla zmigrowanych zasobów (np. "-migracji"), ale po zakończeniu migracji, można użyć usługi Azure Resource Manager Przenieś funkcji toomove zasobów tooany ma grupy zasobów. więcej informacji na temat tego zobacz tooread [przenieść grupy zasobów toonew zasobów lub subskrypcji](../articles/resource-group-move-resources.md)

Poniżej przedstawiono dwa ekrany, które Pokaż wynik powitania po pomyślnej operacji Prepare. Pierwszy ekran pokazuje grupy zasobów, która zawiera hello oryginalnego usługi w chmurze. Drugi ekran pokazuje nowe hello "-migracji" grupy zasobów zawierającej hello równoważne zasoby usługi Azure Resource Manager.

![Zrzut ekranu przedstawiający klasyczną usługę w chmurze w portalu](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-classic.png)

![Zrzut ekranu przedstawiający zasoby usługi Azure Resource Manager w witrynie Portal w ramach operacji przygotowania](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-arm.png)

Tutaj przedstawiono informacje o wewnętrznych zasobów, po zakończeniu hello w fazie przygotowywania. Zwróć uwagę, że zasób hello płaszczyzna danych hello jest hello tego samego. Jest przedstawiany w płaszczyźnie zarządzania hello (klasycznego modelu wdrażania) i płaszczyzny kontroli hello (Resource Manager).

![Tle hello w fazie przygotowywania](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-prepare.png)

> [!NOTE]
> Maszyny wirtualne, które nie znajdują się w klasycznej sieci wirtualnej są alokację zatrzymana na tym etapie migracji.
>

### <a name="check-manual-or-scripted"></a>Sprawdzenie (ręczne lub za pomocą skryptu)
W kroku wyboru hello można opcjonalnie użyć konfiguracji hello został pobrany wcześniej toovalidate poprawne hello migracji. Alternatywnie można zalogować się toohello portal i miejscu hello właściwości i zasoby toovalidate czy migracja metadanych jest dobra.

Jeśli migrujesz sieć wirtualną, większość konfiguracji maszyn wirtualnych nie zostanie uruchomiona ponownie. W przypadku aplikacji na tych maszynach wirtualnych można sprawdzić, czy aplikacja hello jest nadal uruchomiona.

Można testować monitorowania automatyzacji i toosee operacyjne skrypty hello maszyn wirtualnych pracy zgodnie z oczekiwaniami, a jeśli zaktualizowanych skryptów działa prawidłowo. Tylko operacje GET są obsługiwane, gdy zasoby hello są hello przygotowane stanu.

Nie istnieje żadne zestawu przedział czasu, przed którym należy toocommit hello migracji. Ten stan może trwać tak długo, jak chcesz. Jednak płaszczyzny zarządzania hello jest zablokowana dla tych zasobów, dopóki nie zostanie albo przerwania lub przekazania.

Jeśli widzisz wszelkie problemy, zawsze możesz przerwać hello migracji i wrócić do poprzedniej strony toohello klasycznego modelu wdrażania. Po wróć, hello platformy Azure będzie powodować otwarcie operacje zarządzania płaszczyzny hello hello zasobów, dzięki czemu można wznowić wykonywania normalnych operacji na tych maszynach wirtualnych w hello klasycznego modelu wdrażania.

### <a name="abort"></a>Przerwanie
Przerwania jest opcjonalny krok można użyć toorevert Twoje zmiany toohello klasycznego modelu wdrażania i Zatrzymaj hello migracji. Ta operacja powoduje usunięcie hello metadanych Menedżera zasobów dla zasobów utworzonej w poprzednim kroku Prepare hello. 

![Tle hello w fazie przerwania](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-abort.png)


> [!NOTE]
> Nie można wykonać tej operacji, po zostały wyzwolone hello operacji przekazywania.     
>

### <a name="commit"></a>Zatwierdzenie
Po zakończeniu weryfikacji hello można zatwierdzić hello migracji. Zasoby nie są już wyświetlane w klasycznym modelu wdrażania i są dostępne tylko w modelu wdrażania usługi Resource Manager hello. Witaj zmigrowanych zasobów można zarządzać tylko hello nowego portalu.

> [!NOTE]
> Jest to operacja idempotentna. Jeśli nie powiedzie się, zaleca się, ponów próbę wykonania operacji hello. Jeśli nadal toofail, Utwórz bilet pomocy technicznej lub utworzyć forum post z tagiem ClassicIaaSMigration na naszych [forum wirtualna](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).
>
>

![Tle hello w fazie zatwierdzania](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-commit.png)

## <a name="where-toobegin-migration"></a>Gdzie toobegin migracji?

Oto schemat blokowy pokazujący sposób tooproceed z migracją

![Zrzut ekranu pokazujący hello kroków migracji](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="translation-of-classic-deployment-model-tooazure-resource-manager-resources"></a>Tłumaczenie zasoby usługi Resource Manager tooAzure modelu wdrażania klasycznego
Hello klasycznego modelu wdrażania i Menedżera zasobów reprezentacje hello zasobów można znaleźć w hello w poniższej tabeli. Inne funkcje i zasoby nie są obecnie obsługiwane.

| Reprezentacja klasyczna | Reprezentacja usługi Resource Manager | Szczegółowe uwagi |
| --- | --- | --- |
| Nazwa usługi w chmurze |Nazwa DNS |Podczas migracji, nowej grupy zasobów jest tworzone dla każdej usługi w chmurze z wzorcem nazw hello `<cloudservicename>-migrated`. Ta grupa zasobów zawiera wszystkie zasoby. Nazwa usługi w chmurze Hello staje się nazwy DNS, która jest skojarzona z hello publicznego adresu IP. |
| Maszyna wirtualna |Maszyna wirtualna |Właściwości specyficzne dla maszyny wirtualnej są migrowane bez zmian. Niektóre informacje osProfile, takie jak nazwa komputera nie są przechowywane w hello klasycznego modelu wdrażania i pozostanie pusta, po migracji. |
| Zasoby dysków dołączonych tooVM |Niejawne dysków dołączonych tooVM |Dyski nie są modelowane jako zasoby najwyższego poziomu w modelu wdrażania usługi Resource Manager hello. Są one migracji jako niejawne dyski w obszarze hello maszyny Wirtualnej. Tylko w przypadku dysków, które są dołączone tooa maszyny Wirtualnej są obecnie obsługiwane. Menedżer zasobów maszyn wirtualnych można teraz używać klasycznych kont magazynu, co pozwala łatwo bez żadnych aktualizacji, które zostały zmigrowane hello toobe dysków. |
| Rozszerzenia maszyn wirtualnych |Rozszerzenia maszyn wirtualnych |Wszystkie rozszerzenia zasobu hello, z wyjątkiem rozszerzenia XML są migrowane z hello klasycznego modelu wdrażania. |
| Certyfikaty maszyny wirtualnej |Certyfikaty w usłudze Azure Key Vault |Jeśli usługa w chmurze zawiera certyfikaty usługi, nowego magazynu kluczy Azure dla usługi w chmurze i przenosi hello certyfikatów do magazynu kluczy hello. maszyny wirtualne Hello są zaktualizowane tooreference hello certyfikaty z magazynu kluczy hello. <br><br> **Uwaga:** nie Usuń hello keyvault ponieważ może to spowodować hello toogo maszyny Wirtualnej w stanie awarii. Pracujemy nad poprawy czynności w hello wewnętrznej bazy danych, aby klucz magazynów można bezpiecznie usunąć lub przenieść wraz z hello wirtualna tooa nową subskrypcję. |
| Konfiguracja usługi WinRM |Konfiguracja usługi WinRM w ramach elementu osProfile |Windows Remote Management configuration jest przeniesione bez zmian, w ramach migracji hello. |
| Właściwość Availability-set |Zasób Availability-set | Specyfikacja zestawu dostępności jest właściwość hello maszyny Wirtualnej w hello klasycznego modelu wdrażania. Zestawy dostępności stanie się zasobem najwyższego poziomu w ramach migracji hello. Witaj następujące konfiguracje nie są obsługiwane: wiele zestawy dostępności dla danej usługi chmury, lub zestawy dostępności co najmniej jeden wraz z maszyn wirtualnych, które nie znajdują się w dowolnym zestawem dostępności w usługi w chmurze. |
| Konfiguracja sieci na maszynie wirtualnej |Podstawowy interfejs sieciowy |Konfiguracja sieci na maszynie Wirtualnej jest reprezentowany jako zasobu interfejs sieci podstawowej powitania po migracji. Dla maszyn wirtualnych, które nie znajdują się w sieci wirtualnej hello wewnętrzny adres IP zmienia podczas migracji. |
| Wiele interfejsów sieciowych na maszynie wirtualnej |Interfejsy sieciowe |Jeśli maszyna wirtualna ma wiele interfejsów sieciowych skojarzonych z nim, każdy interfejs sieciowy staje się zasobem najwyższego poziomu w ramach migracji hello w modelu wdrażania usługi Resource Manager hello, wraz ze wszystkich właściwości hello. |
| Zestaw punktów końcowych z równoważeniem obciążenia |Moduł równoważenia obciążenia |Hello klasycznego modelu wdrażania platforma hello przypisać niejawnym modułem równoważenia obciążenia dla każdej usługi w chmurze. Podczas migracji utworzony nowy zasób usługi równoważenia obciążenia, a zestawu punktów końcowych z równoważeniem obciążenia hello staje się reguły modułu równoważenia obciążenia. |
| Reguły NAT dla ruchu przychodzącego |Reguły NAT dla ruchu przychodzącego |Wejściowych punktów końcowych zdefiniowanych w hello maszyny Wirtualnej są reguły tłumaczenia adres sieci przekonwertowanego tooinbound w obszarze hello modułu równoważenia obciążenia podczas migracji hello. |
| Adres VIP |Publiczny adres IP z nazwą DNS |wirtualny adres IP Hello staje się publiczny adres IP i skojarzony z usługą równoważenia obciążenia hello. Wirtualny adres IP można migrować tylko jeśli wejściowy punkt końcowy przypisane tooit. |
| Sieć wirtualna |Sieć wirtualna |sieć wirtualna Hello jest migrowana z wszystkie właściwości, modelu wdrażania usługi Resource Manager toohello. Utworzono nową grupę zasobów o nazwie hello `-migrated`. |
| Zastrzeżone adresy IP |Publiczny adres IP z przydziałem statycznym |Zastrzeżonych adresów IP skojarzone z modułem równoważenia obciążenia hello są migrowane, wraz z migracji hello hello usługi w chmurze lub hello maszyny wirtualnej. Migracja nieskojarzonego zastrzeżonego adresu IP nie jest obecnie obsługiwana. |
| Publiczny adres IP dla maszyny wirtualnej |Publiczny adres IP z przydziałem dynamicznym |Witaj skojarzone z maszyna wirtualna jest konwertowana jako zasób publiczny adres IP, z hello alokacji metody set toostatic powitalne publiczny adres IP. |
| Sieciowe grupy zabezpieczeń |Sieciowe grupy zabezpieczeń |Grup zabezpieczeń sieci skojarzonych z podsieci są klonowane jako część modelu wdrażania usługi Resource Manager toohello migracji hello. Witaj NSG w hello klasycznego modelu wdrażania nie jest usuwany podczas migracji hello. Jednak operacje zarządzania płaszczyzny hello hello NSG są zablokowane, gdy trwa migracja hello. |
| Serwery DNS |Serwery DNS |Serwery DNS skojarzona z siecią wirtualną lub hello maszyny Wirtualnej są migrowane w ramach hello odpowiednich zasobów migracji, wraz ze wszystkich właściwości hello. |
| Trasy zdefiniowane przez użytkownika |Trasy zdefiniowane przez użytkownika |Trasy zdefiniowane przez użytkownika, skojarzone z podsiecią są klonowane jako część modelu wdrażania usługi Resource Manager toohello migracji hello. Witaj przez w hello klasycznego modelu wdrażania nie jest usuwany podczas migracji hello. operacje zarządzania płaszczyzny Hello hello przez są zablokowane, gdy trwa migracja hello. |
| Właściwość przekazywania adresu IP w konfiguracji sieci maszyny wirtualnej |Właściwość hello kart przekazywania pakietów IP |Właściwość przesyłanie dalej IP Hello na maszynie Wirtualnej jest właściwość tooa przekonwertowane na interfejsie sieciowym hello podczas migracji hello. |
| Moduł równoważenia obciążenia z wieloma adresami IP |Moduł równoważenia obciążenia z wieloma zasobami publicznego adresu IP |Co publiczny adres IP skojarzone z modułem równoważenia obciążenia hello jest przekonwertowanego tooa publicznego adresu IP zasobu i skojarzone z modułem równoważenia obciążenia hello po migracji. |
| Wewnętrzny nazw DNS na powitania maszyny Wirtualnej |Wewnętrzny nazw DNS na powitania karty Sieciowej |Podczas migracji hello wewnętrzny sufiksów DNS dla maszyn wirtualnych hello są migrowane tooa tylko do odczytu właściwości o nazwie "Element InternalDomainNameSuffix" na powitania karty sieciowej. sufiks Hello jest zmieniany po migracji i rozpoznawania wirtualna powinno być kontynuowane toowork co poprzednio. |
| Brama sieci wirtualnej |Brama sieci wirtualnej |Właściwości bramy sieci wirtualnej są migrowane bez zmian. Witaj wirtualne adresy IP skojarzone z bramą hello nie zmienia się. |
| Lokacja sieci lokalnej |Brama sieci lokalnej |Właściwości lokacji sieci lokalnej zostały zmigrowane tooa niezmienione nowy zasób o nazwie bramy sieci lokalnej. Reprezentuje on prefiksy adresów lokalnych i adres IP bramy zdalnej. |
| Odwołania połączeń |Połączenie |Odwołania łączności między bramą a lokacją sieci lokalnej w konfiguracji sieci są reprezentowane przez nowo utworzony zasób o nazwie Połączenia w usłudze Resource Manager po migracji. Wszystkie właściwości łączności odwołania w plikach konfiguracji sieci są zasobu połączenia skopiowane bez zmian toohello nowo utworzona. Łączność tooVNet sieć wirtualną w klasycznym jest to osiągane przez utworzenie dwóch tuneli protokołu IPsec Lokacje sieciowe toolocal reprezentujący hello sieci wirtualnych. Jest to połączenie po przekształceniu tooVnet2Vnet typu w modelu Menedżera zasobów bez konieczności bramy sieci lokalnej. |

## <a name="changes-tooyour-automation-and-tooling-after-migration"></a>Automatyzacja tooyour zmian i narzędzi po migracji
W ramach migracji zasobów z wdrożenia klasycznego hello modelu modelu wdrożenia usługi Resource Manager toohello masz tooupdate tooensure narzędzi, że nadal toowork po migracji hello lub z istniejącej automatyzacji.
