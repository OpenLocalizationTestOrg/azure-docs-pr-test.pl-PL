---
title: "aaaAzure właściwości roli"
description: "Dowiedz się, jak toouse hello Azure zestawu narzędzi dla ustawień ról platformy Azure tooconfigure Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: d111b4b9e4f12e49f38755bf6c9acc1a1de17a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-properties"></a>Właściwości roli Azure
Można ustawić różne ustawienia konfiguracji dla roli użytkownika usługi Azure w ramach hello zestawu narzędzi platformy Azure dla programu Eclipse.

## <a name="configuring-azure-role-properties"></a>Konfigurowanie właściwości roli Azure
Konfigurowanie właściwości roli platformy Azure jest realizowane za pomocą okien dialogowych właściwości powitania dla swojej roli procesu roboczego. Menu kontekstowe hello otwarte dla roli hello w okienku Eksplorator projektów programu Eclipse na i wybierz hello **Azure** podmenu. (Jeśli nie widzisz hello roli w hello Eksplorator projektów programu Eclipse, rozwiń węzeł projektu platformy Azure w obszarze Eksplorator projektów).

![][ic789599]

Witaj różne właściwości, które można ustawić z hello **właściwości** okna dialogowe są opisane w tym temacie. Należy pamiętać, że wiele właściwości są automatycznie wypełniane podczas tworzenia nowego projektu wdrożenia usługi Azure.

Hello następujące strony właściwości dostępnych dla ról platformy Azure.

* [Właściwości maszyny wirtualnej](#virtual_machine_properties)
* [Właściwości buforowania](#caching_properties)
* [Właściwości certyfikatów](#certificates_properties)
* [Właściwości składników](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [Właściwości punktów końcowych](#endpoints_properties)
* [Właściwości zmiennych środowiskowych](#environment_variables_properties)
* [Równoważenie obciążenia / właściwości sesji koligacji (nazywane również "trwałe sesje")](#session_affinity_properties)
* [Lokalny magazyn właściwości](#local_storage_properties)
* [Właściwości konfiguracji serwera](#server_configuration_properties)
* [Odciążanie właściwości protokołu SSL](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a>Właściwości maszyny wirtualnej
Otwórz menu kontekstowe hello hello roli w okienku Eksplorator projektów w środowisku Eclipse, kliknij pozycję **Azure**, a następnie kliknij przycisk **właściwości**, i będzie mieć rozmiar maszyny wirtualnej hello toochange możliwości hello, a także zmienić Hello liczba wystąpień, jak pokazano w powitania po obrazu.

![][ic719499]

> [!NOTE]
> Tylko w systemie Windows: po ustawieniu hello liczbę wystąpień tooa wartość większą niż 1, a także skonfigurować serwer aplikacji, hello toolkit zezwala tylko na 1 toorun wystąpienie roli w emulatorze hello, niezależnie od tego ustawienia. Jest to tooavoid portu powiązanie konfliktów między hello wystąpienia inny serwer (na przykład wszystkie w trakcie toobind tooport 8080) po uruchomieniu na powitania tym samym komputerze. Liczba wystąpienia odpowiednie ustawienia zostaną zachowane, ale jest uruchamiana tylko w przypadku wdrażania toohello chmury.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Właściwości buforowania
Otwórz menu kontekstowe hello hello roli w okienku Eksplorator projektów w środowisku Eclipse, kliknij pozycję **Azure**, a następnie kliknij przycisk **buforowanie**. W tym oknie dialogowym można włączyć nazwanego wspólnie memcache zgodnego pamięci podręcznych, umożliwiając szybkości toohelp zapasowej aplikacji sieci web.

![][ic719483]

W ramach hello **buforowanie** strony właściwości można określić hello następujące ustawienia globalne:

* Określa, czy jest włączone buforowanie wspólnie.
* rozmiar pamięci podręcznej Hello pamięci w procentach.
* Nazwa konta magazynu Hello zapisywania hello pamięci podręcznej stanu, gdy aplikacja działa jako usługa w chmurze lub none, jeśli nie chcesz, aby toosave hello pamięci podręcznej stanu. (nazwa konta magazynu hello nie jest używana podczas uruchamiania aplikacji w emulatorze obliczeń hello.) Jeśli zostanie ustawiona zbyt nazwy konta magazynu hello**(automatycznie)** (który jest domyślnym hello), konfigurację buforowania będą automatycznie używać hello tego samego konta magazynu, zgodnie z jedną wybierz hello hello **publikowania tooAzure**okna dialogowego.

> [!NOTE]
> Witaj **(automatycznie)** ustawienie będzie miało wpływu hello konieczne tylko w przypadku wdrożenia przy użyciu narzędzi Eclipse hello Kreator publikowania. Jeśli zamiast tego podczas publikowania pliku cspkg hello ręcznie przy użyciu mechanizmu zewnętrznego, takiego jak hello [portalu zarządzania Azure][Azure Management Portal], hello wdrożenia nie będą działać poprawnie.
> 
> 

następujące okna dialogowego Hello są wyświetlane właściwości hello na potrzeby pamięci podręcznej.

![][ic719501]

* **Nazwa:** nazwę hello hello wspólną lokalizację pamięci podręcznej.
* **Numer portu:** hello toouse numer portu hello pamięci podręcznej.
* **Zasady wygasania:** jedną hello następujące wartości, który określa, kiedy wygasa klucz w pamięci podręcznej hello.
  * **Bezwzględna:** klucza hello wygasa po hello czasu określony przez **minut toolive** zostanie osiągnięty.
  * **NeverExpires:** hello klucza nie ma czasu wygaśnięcia.
  * **SlidingWindow:** klucza hello wygasa, jeśli nie była używana przez hello czas określony przez **minut toolive**; zawsze jest on dostępny, hello wygaśnięcia zegar zostanie zresetowana.
* **Minut toolive:** maksymalna liczba minut dla klucza memcached toolive, podmiotu toohello zasady wygasania.
* **Wysoką dostępność z replikowanych kopii zapasowych w różnych wystąpieniach:** włączenie pomaga zapewnić wysokiej dostępności przy użyciu replikowane kopie zapasowe w wystąpieniach ról. Należy pamiętać, że co najmniej dwa wystąpienia roli musi być w celu wdrożenia dla tej funkcji toowork.

tooadd nową pamięć podręczną, kliknij przycisk hello **Dodaj** przycisku na powitania **buforowanie** strony właściwości oraz **Konfigurowanie pamięci podręcznej o nazwie** będzie można otworzyć okna dialogowego. Podaj wartości dla właściwości hello, które zostały opisane powyżej.

toomodify nazwanego pamięci podręcznej, wybierz hello pamięci podręcznej i kliknij przycisk hello **Edytuj** przycisku na powitania **buforowanie** strony właściwości. Okno dialogowe zostanie otwarty dzięki czemu możesz toomodify hello właściwości pamięci podręcznej. Naciśnij klawisz **OK** toosave hello pamięci podręcznej wartości.

toodelete pamięci podręcznej, wybierz hello pamięci podręcznej i kliknij przycisk hello **Usuń** przycisku na powitania **buforowanie** strony właściwości, a następnie kliknij przycisk **tak** tooconfirm hello usunięcia.

Aby uzyskać więcej informacji na temat toouse buforowania, zobacz [jak wspólnie tooUse buforowanie][How tooUse Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Właściwości certyfikatów
Otwórz menu kontekstowe hello hello roli w okienku Eksplorator projektów w środowisku Eclipse, kliknij pozycję **Azure**, a następnie kliknij przycisk **certyfikaty**.

![][ic710964]

W tym oknie dialogowym można dodawać lub Usuń certyfikaty odwołuje się projektu Eclipse. Zauważ, że certyfikaty hello wymienione w tym miejscu nie są automatycznie przechowywane w dowolnym Java keystore i w związku z tym nie są automatycznie dostępne do użycia z poziomu aplikacji Java. Są one tylko zarejestrowana z platformy Azure, dzięki czemu może być załadowane do hello Windows certyfikat przechowywać na maszynach wirtualnych hello z wdrożenia i następnie używane przez inne oprogramowanie Windows. Obecnie hello tylko funkcja toolkit hello, który korzysta z certyfikatów hello przywoływany w ten sposób w hello **certyfikaty** okno dialogowe jest [odciążanie protokołu SSL][SSL Offloading], z powodu tooits zależność od usługi Internet Information Services (IIS) i Routing żądań aplikacji (ARR), które wymagają hello udostępniona w ten sposób toobe właściwy certyfikat.

Podczas wdrażania sieci tooAzure projektu za pomocą Kreatora publikowania hello będzie zostanie wyświetlony monit o toopoint na powitania wymiany informacji osobistych (PFX) plików odpowiednie certyfikaty toothese, wraz z ich haseł w kolejności tooautomatically przekazać je toohello Usługa Azure, ale tylko wtedy, jeśli ich nie zostały przekazane wcześniej.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Właściwości składników
Otwórz menu kontekstowe hello hello roli w okienku Eksplorator projektów w środowisku Eclipse, kliknij pozycję **Azure**, a następnie kliknij przycisk **składniki**. W tym oknie dialogowym możesz mieć tooadd możliwości hello, zmodyfikować, lub usunąć składniki hello swojej roli, a także zmienić kolejność hello, w którym są przetwarzane.

![][ic719502]

Funkcja składniki Hello pozwala tooadd zależności tooyour projektu wdrożenia usługi Azure, takich jak projekty aplikacji Java, specjalne pliki i instrukcje pliku wykonywalnego wiersza polecenia, które są wymagane przez wdrożenie.

Dla każdego składnika można określić:

* toobe krok Hello wykonane podczas importowania hello składników do projektu wdrożenia usługi Azure, gdy jest ona wbudowana.
* toobe krok Hello wykonane podczas wdrażania tego składnika w hello chmury Azure.

> [!NOTE]
> Podczas określania składnika pliki lub wiersze polecenia, należy pamiętać wdrożenia będzie opublikowanych tooa maszyny wirtualnej systemu Windows, więc wszystkie czynności dotyczące niestandardowych muszą być prawidłowe dla systemu operacyjnego Windows. 
> 
> 

Składniki mają hello następujące właściwości:

* **Import:** metodę, która wskazuje, jak składnika hello zostaną zaimportowane do projektu powitania po utworzeniu projektu hello. Może to być jeden z hello następujące wartości:
  * **Kopiuj:** składnika hello zostanie skopiowana ze ścieżki lokalnej hello określony przez hello **z** właściwości do roli hello **approot** katalogu.
  * **Wyczyść:** składnik hello jest zaimportowany z projektu aplikacji przedsiębiorstwa o ścieżce lokalnej hello określony przez hello archiwum przedsiębiorstwa (Wyczyść) Java **z** właściwości. (To jest wykrywane automatycznie przez toolkit hello oparte na powitania rodzaj projektu hello w tej lokalizacji).
  * **JAR:** składnik hello archiwum Java (JAR) i jest importowany z projektu języka Java w ścieżce lokalnej hello określony przez hello **z** właściwości. (To jest wykrywane automatycznie przez toolkit hello oparte na powitania rodzaj projektu hello w tej lokalizacji).
  * **Brak:** tooimport hello składnika nie podjęto żadnej akcji. Ma to zastosowanie, gdy przyjęto, że składnik hello tooalready znajdować się w roli hello **approot** katalogu, lub gdy składnik hello jest jedynie pliku wykonywalnego wiersza polecenia instrukcji, jako hello określony w **jako**właściwość podczas hello **Wdróż** jest metoda **exec**.
  * **WAR:** składnik hello Java archiwum aplikacji sieci web (plik WAR) i jest importowany z dynamiczny projekt sieci Web o ścieżce lokalnej hello określony przez hello **z** właściwości. (To jest wykrywane automatycznie przez toolkit hello oparte na powitania rodzaj projektu hello w tej lokalizacji).
  * **ZIP:** składnik hello jest plik zip i zaimportowanych przez kompresja hello katalogu lub pliku określonego przez hello **z** właściwości.
* **Od:** ścieżki źródłowej na komputer lokalny toohello folder lub plik, który reprezentuje hello elementów tooimport tooyour wdrożenia. Zmiennych środowiskowych systemu Windows można użyć w tej właściwości. Wszystkie składniki importowane zostaną zaimportowane do roli hello **approot** katalogu po utworzeniu projektu hello.
  
    Należy zauważyć, że możesz toodeploy możliwości hello składnika pobierać podczas wdrażania chmury toohello (nie emulatora obliczeń hello). Zobacz poniższe pokrewne informacje dotyczące dodawania składnika.    
* **Jak:** nazwę pliku, w którym hello składnika zostaną zaimportowane do roli hello **approot** katalogu i ostatecznie wdrożonej w hello chmury Azure. Pozostaw nazwę hello jest tak samo jak na komputerze lokalnym hello hello tookeep puste tej właściwości. (Dla pliku wykonywalnego składników, czyli tych, których **Wdróż** metody ustawiono zbyt**exec**, może to być instrukcji dowolnego wiersza polecenia systemu Windows.)
  
  > [!IMPORTANT]
  > Jeśli używasz znaków spacji dla tej wartości, ich obsługi inaczej w zależności od hello wdrożenia metody. Metody wdrażania hello jest **exec**, spacje zostanie potraktowany jako separatory argumentów wiersza polecenia, a nie jako część hello nazwy pliku. Dla wszystkich innych wdrażania metod, spacje zostanie potraktowany jako część hello nazwy pliku.
  > 
  > 
* **Wdróż:** metodę, która wskazuje akcji hello stosowane toohello składnika, po uruchomieniu wdrożenia hello. Może to być jeden z hello następujące wartości:
  
  * **Kopiuj:** składnik hello jest skopiowany toohello docelowego ścieżka określona przez hello **do** właściwości.
  * **exec:** składnik hello jest instrukcji pliku wykonywalnego wiersza polecenia systemu Windows wykonywane w kontekście hello hello ścieżka określona przez hello **do** właściwości w czasie hello uruchamia hello wdrożenia.
  * **Brak:** nie jest żadna akcja składnika toohello stosowane podczas uruchamiania hello wdrożenia.
  * **ZIP:** składnik hello jest ścieżka docelowa rozpakowane toohello określony przez hello **do** właściwości. Ta metoda jest dostępna tylko wtedy, gdy hello **importu** właściwość jest **zip**.
* **Do:** ścieżkę docelową na maszynie wirtualnej hello wdrożonym hello składnika. Zmiennych środowiskowych systemu Windows mogą być używane w tej właściwości, a ścieżki plików są zbyt względną**approot**.

tooadd nowy składnik, kliknij przycisk hello **Dodaj** przycisku na powitania **składniki** stronę właściwości i **Azure roli składnika** będzie można otworzyć okna dialogowego. Podaj wartości dla właściwości hello, które zostały opisane powyżej. 

Hello poniżej przedstawiono przykład do dodawania nowego składnika WAR.

![][ic719503]

Podczas wdrażania chmury toohello (nie emulatora obliczeń hello), jeśli chcesz, aby składnik hello toodeploy pobierać, upewnij się, że **w chmurze zamiast w pakiecie hello, w tym wdrażanie z** jest zaznaczony. Chcąc toodownload z kontem magazynu platformy Azure, wybierz konto magazynu hello z hello **konta magazynu** listy rozwijanej (możesz kliknąć hello **kont** link toomodify co to jest na liście hello), które częściowo wypełni hello **adres URL** pola, a następnie wypełnij hello pozostała część hello adresu URL. Jeśli nie chcesz, aby toouse magazynu Azure, wybierz **(Brak)** z hello **konta magazynu** listy rozwijanej liście, a następnie wprowadź hello adresu URL tooyour składnika w hello **adres URL** pola. Określ jedną z następujących metod hello:

* **Kopiuj:** składnik pobierania hello jest skopiowany toohello docelowego ścieżka określona przez hello **tooDirectory** ścieżki.
* **tym samym:** hello tej samej metody używane do **Wdróż z pobierania** jak w przypadku **Wdróż z pakietu**.
* **ZIP:** składnik pobierania hello jest ścieżka docelowa rozpakowane toohello określony przez hello **tooDirectory** ścieżki.

toomodify hello hello składnika, wybierz składnik i kliknij przycisk **Edytuj** przycisku na powitania **składniki** strony właściwości. Okno dialogowe zostanie otwarty dzięki czemu możesz toomodify hello właściwości składnika. Naciśnij klawisz **OK** toosave hello składnika wartości.

toodelete hello hello składnika, wybierz składnik i kliknij przycisk **Usuń** przycisku na powitania **składniki** strony właściwości, a następnie kliknij przycisk **tak** tooconfirm hello usunięcia.

Składniki są przetwarzane w kolejności hello. Użyj hello **Przenieś w górę** i **Przenieś w dół** przyciski tooarrange hello kolejności.

> [!NOTE]
> Funkcja konfiguracji serwera Hello zależy od komponentów oraz. Te składniki nie można usunąć ani edytować bez usuwania hello odpowiedniej konfiguracji serwera. Zostanie wyświetlony monit o tym, że podczas próby toomake zmiany toosuch składników.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have hello ability tooenable or disable remote debugging, as well as create debug configurations, as shown in hello following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Właściwości punktów końcowych
Otwórz menu kontekstowe hello hello roli w okienku Eksplorator projektów w środowisku Eclipse, kliknij pozycję **Azure**, a następnie kliknij przycisk **punkty końcowe**. W tym oknie dialogowym ma hello możliwości toocreate punktu końcowego, a także Edytuj lub Usuń punkt końcowy, pokazane na powitania po obrazu.

![][ic719505]

tooadd jako punktu końcowego, kliknij przycisk hello **Dodaj** przycisku na powitania **punkty końcowe** stronę właściwości i **Dodawanie punktu końcowego** będzie można otworzyć okna dialogowego.

![][ic710897]

Wprowadź nazwę dla punktu końcowego hello, wybierz typ hello (albo **dane wejściowe**, **wewnętrzne**, lub **InstanceInput**) i określić port publiczny i prywatny hello. Naciśnij klawisz **OK** toosave hello nowe wartości punktu końcowego.

W zależności od typu hello punktu końcowego może używać zakresów portów w następujący sposób:

* Dla punktu końcowego wystąpienia wejściowych port publiczny hello może być zakresu portów (na przykład **2000 2010**) i port prywatny hello jest wartością stałą.
* Dla wewnętrzny punkt końcowy nie jest używany port publiczny hello i port prywatny hello może być zakresem, lub pozostać pusty lub zestawu tooan gwiazdki tooindicate, automatycznie zostaje ustawiona przez platformę Azure.
* Dla wejściowych punktów końcowych port publiczny hello tylko może być wartością stałą, a port prywatny hello może być wartością stałą lub pozostać pusty lub zestawu tooan gwiazdki tooindicate, automatycznie zostaje ustawiona przez platformę Azure.

Jeśli chcesz toouse numer pojedynczego portu zamiast zakresu, pozostaw puste pole tekstowe hello hello koniec zakresu hello.

Dla portów, które są tooautomatic zestawu, jeśli potrzebujesz toodetermine port, który będzie faktycznie używana w czasie wykonywania, aplikacja może używać hello środowisko uruchomieniowe interfejsu API usługi Azure, które opisano w hello [com.microsoft.windowsazure.serviceruntime pakietu Podsumowanie][com.microsoft.windowsazure.serviceruntime package summary].

<!-- toosee how instance input endpoints can be used toohelp with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

toomodify jako punkt końcowy, wybierz punkt końcowy hello i kliknij przycisk hello **Edytuj** przycisku na powitania **punkty końcowe** strony właściwości. Okno dialogowe zostanie otwarty, umożliwiając Nazwa punktu końcowego hello toomodify, typ i portów publicznego i prywatnego. Naciśnij klawisz **OK** toosave hello modyfikować wartości punktu końcowego.

toodelete jako punkt końcowy, wybierz punkt końcowy hello i kliknij przycisk hello **Usuń** przycisku na powitania **punkty końcowe** strony właściwości, a następnie kliknij przycisk **tak** tooconfirm hello usunięcia.

W kolejności tooproperly skonfigurować niektóre funkcje hello (takich jak buforowanie, koligacji sesji lub SSL Odciążanie) włączenia przez użytkownika hello roli, hello toolkit mogą automatycznie konfigurować specjalne punkty końcowe, które zostaną wyświetlone wraz z końcowych zdefiniowanych przez użytkownika. Hello toolkit uniemożliwi użytkownikowi hello edytowanie lub usuwanie takich automatycznie generowanych punkty końcowe tak długo, jak hello skojarzona funkcja jest włączona.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Właściwości zmiennych środowiskowych
Otwórz menu kontekstowe hello hello roli w okienku Eksplorator projektów w środowisku Eclipse, kliknij pozycję **Azure**, a następnie kliknij przycisk **zmiennych środowiskowych**. W tym oknie dialogowym ma toocreate możliwości hello zmiennej środowiskowej, a także modyfikację lub usunięcie zmiennej środowiskowej, jak pokazano w powitania po obrazu.

![][ic719506]

Zmienne środowiskowe są dostępne tooyour uruchamiania skryptów podczas uruchamiania hello roli.

> [!NOTE]
> W przypadku określania zmiennych środowiskowych, należy pamiętać wdrożenia będzie opublikowanych tooa maszyny wirtualnej systemu Windows, więc zmienne środowiskowe musi być prawidłowy dla systemu operacyjnego Windows.
> 
> 

Na przykład zmienna środowiskowa jest dostępne po uruchomieniu roli hello utworzyć nową zmienną środowiskową, klikając hello **Dodaj** przycisku. Witaj poniżej pokazano zmienną środowiskową o nazwie **MyRoleVersion** utworzyć i przypisać wartości hello **1.0**.

![][ic659268]

W kodzie jsp można wyświetlić przy użyciu hello wartość hello `System.getenv` metody:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Spowodować, że te dane wyjściowe po uruchomieniu aplikacji:

![][ic552233]

Wybierz zmienną środowiskową hello toomodify zmienną środowiskową i kliknij przycisk hello **Edytuj** przycisku na powitania **zmiennych środowiskowych** strony właściwości. Okno dialogowe zostanie otwarty dzięki czemu możesz toomodify hello środowiska zmiennej właściwości. Naciśnij klawisz **OK** wartości zmiennych środowiskowych hello toosave.

Wybierz zmienną środowiskową hello toodelete zmienną środowiskową i kliknij przycisk hello **Usuń** przycisku na powitania **zmiennych środowiskowych** strony właściwości, a następnie kliknij **tak**tooconfirm hello usunięcia.

W kolejności tooproperly konfiguracji niektóre funkcje hello (np. Konfiguracja serwera zdalnego debugowania lub lokalnego magazynu) włączenia przez użytkownika hello roli, hello toolkit mogą automatycznie konfigurować zmienne środowiskowe specjalne, które zostaną wyświetlone wraz z programem zmienne środowiskowe zdefiniowane przez użytkownika. Hello toolkit uniemożliwi użytkownikowi hello edytowanie lub usuwanie zmiennych środowiskowych automatycznie wygenerowaną, takich jak hello skojarzone funkcji jest włączona.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Równoważenie obciążenia / właściwości sesji koligacji (nazywane również "trwałe sesje")
Otwórz menu kontekstowe hello hello roli w okienku Eksplorator projektów w środowisku Eclipse, kliknij pozycję **Azure**, a następnie kliknij przycisk **równoważenia obciążenia**. W tym oknie dialogowym masz tooenable możliwości hello lub wyłącz koligacji sesji, jak pokazano w powitania po obrazu.

![][ic719492]

Aby uzyskać odpowiednie informacje, zobacz [koligacji sesji][Session Affinity]. Zauważ również, działanie tej funkcji w kontekście hello odciążanie protokołu SSL, zgodnie z opisem w [odciążanie protokołu SSL][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Lokalny magazyn właściwości
Otwórz menu kontekstowe hello hello roli w okienku Eksplorator projektów w środowisku Eclipse, kliknij pozycję **Azure**, a następnie kliknij przycisk **Magazyn lokalny**. W tym oknie dialogowym ma toocreate możliwości hello, zmodyfikować lub usunąć tymczasowe przechowywanie lokalne powitania maszyny wirtualnej, która jest uruchomiona aplikacja. Określone wartości można ustawić dla rozmiaru hello hello magazynu lokalnego, a także czy zawartość hello są zachowywane podczas roli hello odtwarzania, jak pokazano w powitania po obrazu.

![][ic719508]

Również Opcjonalnie możesz określić zmienną środowiskową odpowiadający toohello magazynu lokalnego.

Domyślnie wszystkie czynności, które można wdrożyć na platformie Azure jest umieszczony (i rozpakowane) w hello **approot** folderu hello wystąpienia roli. Gdy zmieści większości wdrożeń proste nawet po rozpakować hello miejsca przydzielonego na powitania **approot** katalog jest ograniczona i nie jest dobrze zdefiniowany (mniej niż 1 GB jest uzasadnione zasadą). W związku z tym tooensure Azure przydziela miejsce na dysku w przypadku większych wdrożeń, które może się nie zmieścić w hello **approot** folderu, należy skonfigurować zasobu magazynu lokalnego przy użyciu hello **Magazyn lokalny** okno dialogowe. Dla toodo łatwy sposób tego, zobacz [wdrażanie dużych wdrożeniach][Deploying Large Deployments].

Możesz łatwo odwoływać się do zasobów magazynu hello ze skryptami uruchamiania (na przykład z **startup.cmd**) przy użyciu zmiennej środowiskowej hello automatycznie skojarzona przez zestaw narzędzi Eclipse hello hello zasobów, jak pokazano w hello  **Lokalny magazyn** okna dialogowego. Tej zmiennej środowiskowej będzie zawierać pełną ścieżkę hello hello zasób lokalny, skonfigurowanego w czasie hello uruchamiania skrypt jest wykonywany. 

toomodify zasobów magazynu lokalnego, wybierz zasób lokalny magazyn hello i kliknij hello **Edytuj** przycisku na powitania **Magazyn lokalny** strony właściwości. Okno dialogowe zostanie otwarty dzięki czemu możesz toomodify hello Magazyn lokalny właściwości zasobów. Naciśnij klawisz **OK** wartości zasobów magazynu lokalnego hello toosave.

toodelete zasobów magazynu lokalnego, wybierz zasób lokalny magazyn hello i kliknij hello **Usuń** przycisku na powitania **Magazyn lokalny** strony właściwości, a następnie kliknij przycisk **tak** Usuwanie hello tooconfirm.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Właściwości konfiguracji serwera
Otwórz menu kontekstowe hello hello roli w okienku Eksplorator projektów w środowisku Eclipse, kliknij pozycję **Azure**, a następnie kliknij przycisk **konfiguracji serwera**. W tym oknie dialogowym masz hello możliwości tooadd, usunąć i zmodyfikować hello JDK i serwera aplikacji Java używany przez wdrożenie, a także dodawanie lub usuwanie aplikacji hello (na przykład plik WAR, JAR lub wyczyść) używanych przez wdrożenie.

### <a name="jdk-configuration"></a>Konfiguracja JDK
To okno dialogowe umożliwia toospecify hello JDK pakietu toouse dla danego wdrożenia. Jeśli używasz programu Eclipse w systemie Windows, można określić hello JDK pakietu toouse lokalnie podczas uruchamiania w hello Azure emulator i masz hello opcja toodeploy tooAzure tej instalacji lokalnej. W systemach operacyjnych innych niż Windows hello emulatora JDK ustawienie nie ma zastosowania i nie można wdrożyć hello lokalnie zainstalowane JDK, ponieważ nie jest zgodny z systemem Windows. Jednak niezależnie od systemu operacyjnego hello są używane, zawsze można zainstalować hello 3 strona JDK pakiety toodeploy tooAzure lub wskaż pakiet JDK zgodne z systemem Windows z lokalizacji alternatywnej.

Hello poniżej znajduje się przykład sposobu JDK można określić w systemie Windows:

![][ic780647]

Jeśli używasz programu Eclipse w systemie Windows, można określić toouse JDK, z hello obliczeniowe emulatora; toodo tak, upewnij się, **Użyj hello JDK z podanej ścieżki pliku do testowania lokalnie** zaewidencjonowania hello **wdrożenia urządzenia emulatora** sekcji. Następnie określ tooyour ścieżki lokalne powitania JDK; istnieje możliwość przeglądania toodifferent JDK hello co chcesz toouse nie jest zaznaczona automatycznie. Masz również hello opcja toodeploy Twojego tooyour JDK usługi w chmurze Azure; toodo należy wybrać hello **wdrażanie Moje JDK lokalnego (magazyn toocloud automatycznego przekazywania)** opcję hello **wdrożenie w chmurze** sekcji.

Uwaga: W systemach operacyjnych innych niż Windows hello **wdrożenia urządzenia emulatora** ustawienia i hello **wdrażanie Moje lokalnego JDK** opcji nie są dostępne. Witaj poniższy przykład przedstawia określenie JDK na komputerze Mac lub innych obsługiwany system operacyjny z systemem innym niż Windows:

![][ic789643]

Niezależnie od systemu operacyjnego hello na, masz następujące dwa hello **wdrożenie w chmurze** opcje hello źródła i typ pakietu JDK:

* **Wdrożenia dostępnych na platformie Azure pakietu JDK 3 stron** 
* **Wdrażanie z pobierania niestandardowych** 

Jeśli używasz hello **wdrożenia dostępnej w sklepie Azure pakietu JDK 3 strona** opcji:

1. Zaznacz pole wyboru hello o nazwie **wdrożenia dostępnej w sklepie Azure pakietu JDK 3 strona**.
2. Z listy rozwijanej hello wybierz hello 3 strona JDK pakiet, który jest dostępny na platformie Azure.
3. Twoje **JDK** kartę będzie wyglądać podobnie następujące toohello w systemie Windows: ![][ic780648] i będzie wyglądać podobnie następujące toohello w systemie Mac OS lub innych obsługiwanych systemach operacyjnych innych niż Windows:![][ic789643]
4. Kliknij przycisk **OK** toosave zmiany.
5. Gdy zostanie wyświetlony monit o tooaccept hello umowę licencyjną z hello 3 JDK pakietu dostawców, przejrzyj postanowienia licencyjne hello. Zakładając, że akceptujesz postanowienia powitania kliknij **tak** tooclose hello **zaakceptować umowę licencyjną** okna dialogowego.
    Należy pamiętać, że hello podstawowej logiki, dla którego elementy są wyświetlane na liście rozwijanej hello dla hello **wdrożenia dostępnej w sklepie Azure pakietu JDK 3 strona** opcji można dostosować. toocustomize hello elementów w hello **JDK** okna dialogowego, kliknij przycisk hello **Dostosuj** łącza. Spowoduje to zamknięcie hello **JDK** stronę właściwości i otwórz hello **componentsets.xml** plików w środowisku Eclipse, które następnie można zmodyfikować zgodnie z potrzebami. Dokumentacja **componentsets.xml** znajduje się w hello **componentsets.xml** samym pliku.

Jeśli używasz hello **wdrażanie JDK niestandardowych pobierać** opcji:

1. Utwórz ZIP katalogu instalacji JDK zapewnienie, że ten sam węzeł katalogu hello jest podrzędnym hello hello ZIP struktury i nie jego zawartość. Zwróć uwagę na powitania nazwę katalogu hello, będzie on potrzebny później i pamiętać o tym JDK instalacji będzie maszyny wirtualnej wdrożonej tooa systemu Windows.
2. Przekaż hello ZIP na koncie magazynu Azure jako obiektu blob. Można to zrobić za pomocą zewnętrznie dostępne narzędzia do przekazywania magazynu tooAzure obiektów blob. Jest zalecana toouse prywatnego obiektu blob. Zanotuj adres URL obiektu blob hello hello ZIP zawartość.
3. Zaznacz pole wyboru hello o nazwie **wdrażanie JDK niestandardowych pobierać**.
    Chcąc toodownload z kontem magazynu platformy Azure, wybierz konto magazynu hello z hello **konta magazynu** listy rozwijanej (możesz kliknąć hello **kont** link toomodify co to jest na liście hello), które częściowo wypełni hello **adres URL** pola, a następnie wypełnij hello pozostała część hello adresu URL. Jeśli nie chcesz, aby toouse magazynu Azure, wybierz **(Brak)** z hello **konta magazynu** listy rozwijanej liście, a następnie wprowadź hello tooyour adresu URL pobierania JDK w hello **adres URL** pola. Jeśli używasz usługi Azure storage, nazwy obiektów blob w adresie URL hello musi być mała.
4. Upewnij się, że hello **JAVA_HOME** toohello poprawny katalog nazwa odwołuje się pole tekstowe. Domyślnie będą się odwoływać hello tej samej nazwy katalogu JDK jako wartość hello wybrana do użycia lokalnego. Ale jeśli katalog hello zawarte w hello ZIP ma inną nazwę (na przykład z powodu toousing innej wersji), nazwę katalogu hello aktualizacji w hello **JAVA_HOME** textbox w związku z tym, ponieważ to ustawienie, które będą używane w hello chmury () nie w emulatorze obliczeń hello).
5. Kliknij przycisk **OK** toosave zmiany.

To już wszystko. Teraz podczas tworzenia chmury hello zauważysz będzie znacznie mniejszy rozmiar pakietu hello, proces kompilacji hello zazwyczaj powinno zająć mniej czasu i wdrożenia hello, sam podczas publikowania chmury toohello również powinno zająć mniej czasu. Należy pamiętać, że hello **wdrażanie Moje JDK lokalnego (magazyn toocloud automatycznego przekazywania)** lub **wdrażanie JDK niestandardowych pobierać** obowiązują tylko podczas wdrażania aplikacji w chmurze hello są opcje. Nie mają wpływu na środowiska emulatora obliczeń; lokalna wersja składników hello Hello nadal będzie używany, podczas wdrażania toohello emulatora obliczeń. 

### <a name="server-configuration"></a>Konfiguracja serwera
Witaj poniżej znajduje się przykład sposobu można określić serwer aplikacji.

![][ic796926]

Sprawdź, że hello **wdrożenie serwera tego typu** pole wyboru jest zaznaczone, a następnie wybierz typ powitania serwera aplikacji ma toouse.

Do określenia toouse serwera, do wdrożenia w chmurze, można korzystać z hello następujące opcje:

1. **Wdrażanie serwera strona 3 dostępnych na platformie Azure** — szczególnie stosować w scenariusze tworzenia/testowania, gdy proces wdrażania i prostota jest priorytet i hello serwer nie wymaga konfiguracji niestandardowej. Lub gdy ma toouse jednego z tych serwerów jako punkt początkowy hello, ale zawiera dostosowania odpowiedni serwer kroków w danym wdrożeniu Logika uruchamiania.
2. **Wdrażanie niestandardowych pobierać** — jest to szczególnie odpowiednie w scenariuszach produkcji, gdy serwer specjalnie przygotowany i jest skonfigurowany, które mają toouse w chmurze hello.
3. **Wdrażanie instalacji Mój serwer lokalny** — szczególnie stosować w, jeśli instalacja lokalny serwer już jest konfigurowane do użycia. Jeśli wybierzesz tę opcję, należy również określić ścieżkę serwera lokalnego w hello **ścieżki serwera lokalnego** poniżej pola tekstowego.

Jeśli używasz hello **wdrożenia serwera strona 3 dostępnych na platformie Azure** opcji:

1. Zaznacz pole wyboru hello o nazwie **wdrożenia serwera strona 3 dostępnych na platformie Azure**.
2. Z menu rozwijanego hello, wybierz hello żądanego serwera oprogramowania toouse z wdrożeniem w chmurze hello. Uwaga: Jeśli już określony typ serwera toouse wcześniej, będzie ograniczona toochoosing tylko serwer chmury w hello tej samej rodziny jako typu serwera. Jednak jeśli nie wybrano typu serwera, możesz wybrać spośród wszystkich serwerów hello, które są obecnie dostępne w systemie Azure i typ serwera hello zostanie automatycznie wybrana automatycznie.
3. Kliknij przycisk **OK** toosave zmiany.

Jeśli przy użyciu hello **wdrażanie niestandardowych pobierać** opcji:

1. Upewnij się, wybrał typ serwera, zgodnie z toohello w poprzednich krokach. Informuje wtyczki hello jak toodeploy powitania serwera z niestandardowych pobierania, ponieważ musi pochodzić z hello tej samej rodziny jako typ wybranego serwera.
2. Zaznacz pole wyboru hello o nazwie **Wdróż z niestandardowych pobierania**.
    Chcąc toodownload z kontem magazynu platformy Azure, wybierz konto magazynu hello z hello **konta magazynu** listy rozwijanej (możesz kliknąć hello **kont** link toomodify co to jest na liście hello), które częściowo wypełni hello **adres URL** pola, a następnie wypełnij hello pozostała część hello adres URL serwera tooyour Pobierz ZIP (Jeśli za pomocą usługi Azure storage, nazwy obiektów blob w adresie URL hello muszą być małymi literami). Jeśli nie chcesz, aby toouse magazynu Azure, wybierz **(Brak)** z hello **konta magazynu** listy rozwijanej liście, a następnie wprowadź hello adresu URL tooyour serwera pobierania ZIP w hello **adres URL** pola. Witaj ZIP zawiera folder podrzędny reprezentujący katalogu instalacji serwera aplikacji. Na przykład, jeśli używasz zip dla Apache Tomcat 7.0.35, w hello zip będzie hello podrzędnych folderu reprezentująca hello katalog instalacyjny, takich jak **apache-tomcat-7.0.35**. 
3. Określ wartość zmiennej środowiskowej katalogu macierzystego hello hello. Domyślnie zostanie użyta wartość toohello używane dla lokalnych aplikacji serwera, jeśli istnieje, ale można określić inną wartość, jeśli serwer aplikacji w chmurze różni się od serwera lokalnego aplikacji. Jednak należy się, że serwer aplikacji w chmurze jest hello toomake tej samej rodziny jako typ serwera hello wybranymi wcześniej.
    Po zaktualizowaniu chmury pocztowy serwera aplikacji w przyszłości hello ręcznie zmienić ustawienie katalogu macierzystego hello lub toohave ponownie zgodne z lokalnym ustawienie (serwer aplikacji lokalnych jest zmieniony zbyt).
4. Kliknij przycisk **OK** toosave zmiany.

Witaj podstawowej logiki, dla którego elementy są wyświetlane w hello **serwera** kartę hello **konfiguracji serwera** strony właściwości można dostosować. Jest to zaawansowana funkcja, która może być konieczne, jeśli potrzeb wykraczają poza wartości domyślne hello, lub jeśli użytkownik chce tooadd innych serwerów. logikę hello toocustomize, hello **serwera** okna dialogowego, kliknij przycisk hello **Dostosuj** łącza. Spowoduje to zamknięcie hello **konfiguracji serwera** stronę właściwości i otwórz hello **componentsets.xml** plików w środowisku Eclipse, którą można następnie zmienić jako wymagane tooextend powitania serwera konfiguracji szablonu. Dokumentacja **componentsets.xml** znajduje się w hello **componentsets.xml** samym pliku.

Jeśli używasz hello **wdrożyć serwer lokalny (magazyn toocloud automatycznego przekazywania)** opcji:

1. Zaznacz pole wyboru hello o nazwie **wdrożyć serwer lokalny (magazyn toocloud automatycznego przekazywania)**.
2. Przy użyciu hello **konta magazynu** listy rozwijanej wybierz **(automatycznie)**. Jeśli określisz **(automatycznie)** w tym miejscu hello użyje zestawu narzędzi Eclipse hello tego samego konta magazynu dla serwera jako hello jedną wybierzesz do wdrożenia w hello **publikowania tooAzure** okna dialogowego.
3. Kliknij przycisk **OK** toosave zmiany.

Wybierz ścieżkę instalacji serwera na komputerze w hello **ścieżki serwera lokalnego** pole tekstowe, jeśli spełnione są dowolne hello następujące warunki:

* Ma tootest wdrożenia w emulatorze hello (dotyczy tylko tooWindows).
* Ma toodeploy chmury toohello lokalnie zainstalowanego serwera.
* Mają toouse pobieranie użytkownika w chmurze hello, w którym to przypadku niestandardowego serwera, upewnij się również hello **wdrożyć serwer lokalny (magazyn toocloud automatycznego przekazywania)** powyżej wybrano opcję.

Jeśli żaden z hello poprzedzających opcje tooyour sytuacji, ustawienie serwera lokalnego hello jest opcjonalne.

### <a name="applications-configuration"></a>Konfiguracja aplikacji
Witaj poniżej znajduje się przykład określania aplikacji.

![][ic719512]

Kliknij przycisk **Dodaj** tooadd inna aplikacja lub **Usuń** tooremove aplikacji. Ze względów wydajności toouse pobieranie źródła hello aplikacji podczas wdrażania chmury toohello, należy użyć hello [właściwości składników](#components_properties) toospecify na adres URL konta magazynu, itd. 

Począwszy od hello kwietnia 2014 roku, aplikacje automatycznie są przekazywane do hello tego samego konta magazynu (w obszarze hello **eclipsedeploy** kontenera) jako hello wybranej do wdrożenia. Logika uruchamiania Hello wdrożenia zawiera krok, który najpierw pobiera tych aplikacji z tego konta magazynu. To oznacza, że może uaktualniania aplikacji w danym wdrożeniu bez konieczności toorebuild i ponownie wdrożyć hello całego pakietu, przekazując ręcznie nowszej wersji aplikacji hello bezpośrednio do tego konta magazynu (na przykład przy użyciu hello portalu Azure) , pierwotnie zastępowania plików WAR hello przekazany przez hello toolkit. Następnie po prostu zainicjować hello odtwarzania z tych wystąpień roli za pomocą portalu zarządzania platformy Azure, ponownie, lub za pomocą narzędzia wiersza polecenia. (Wyzwalanie roli odtwarzania bezpośrednio w ramach zestawu narzędzi Eclipse hello nie jest obecnie obsługiwana.)

### <a name="notes-about-server-configuration"></a>Uwagi dotyczące konfiguracji serwera
Zmiany wprowadzane za pośrednictwem hello **konfiguracji serwera** strony właściwości są uwzględniane w hello `<component>` elementy hello plik package.xml pliku.

Jeśli używasz hello **automatyczne przekazywanie...**  lub **Wdróż z pobierania...**  opcje hello JDK lub serwera aplikacji i możesz budowania hello chmury (nie emulatora obliczeń hello) i są połączone toohello sieci, mogą pojawić się tworzenia komunikaty, takie jak następujące hello w danych wyjściowych konsoli hello hello narzędzia Ant Konstruktor sprawdza dostępność hello pobierania:

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

W przypadku wybrania hello **Wdróż z pobierania...**  opcja, mogą zostać wyświetlone następujące ostrzeżenie hello, ale będzie hello kompilacji:

`[windowsazurepackage] warning: Failed tooconfirm blob availability! Make sure hello URL and/or hello access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

To ostrzeżenie jest hello jedyną reakcją, jaką hello dostępności na pobieranie nie zostało zweryfikowane. Dlatego w przypadku niepowodzenia wdrożenia w chmurze hello jakiegoś powodu Sprawdź toosee, w przypadku otrzymania tego ostrzeżenia.

Jeśli chcesz toodisable hello pobierania weryfikacji (na przykład, jeśli uważasz, że jej niepotrzebnie spowalnia hello kompilacji) Ustaw hello `verifydownloads` atrybutu zbyt`false` w hello `<windowsazurepackage>` elementu plik package.xml: 

`<windowsazurepackage verifydownloads="false" ...>` 

W przypadku wybrania hello **automatyczne przekazywanie...**  opcji, a następnie w oknie konsoli hello pojawi się kompilacji wiadomości raportowania postępu przekazywania hello co 5 sekund, gdy konieczne jest przekazanie hello.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>Odciążanie właściwości protokołu SSL
Otwórz menu kontekstowe hello hello roli w okienku Eksplorator projektów w środowisku Eclipse, kliknij pozycję **Azure**, a następnie kliknij przycisk **odciążanie protokołu SSL**. 

![][ic719481]

W tym oknie dialogowym można włączyć protokołu SSL Odciążanie, co pozwala enable tooeasily, obsługiwanych przez Hypertext Transfer Protocol Secure (HTTPS) w danym wdrożeniu Java na platformie Azure, bez konieczności tooconfigure SSL na serwerze aplikacji Java. Aby uzyskać więcej informacji, zobacz [odciążanie protokołu SSL] [ SSL Offloading] i [jak tooUse odciążanie protokołu SSL][How tooUse SSL Offloading].

## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse]

[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Właściwości projektu platformy Azure][Azure Project Properties]

[Lista kont magazynu Azure][Azure Storage Account List]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How tooUse Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How tooUse SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
