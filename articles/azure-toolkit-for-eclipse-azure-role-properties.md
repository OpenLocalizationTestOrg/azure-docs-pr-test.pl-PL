---
title: "Właściwości roli Azure"
description: "Dowiedz się, jak skonfigurować ustawienia roli platformy Azure przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.openlocfilehash: cd734c64ba6d1394cb261bace92dee9dd579dd08
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-properties"></a>Właściwości roli Azure
W ramach zestawu narzędzi platformy Azure dla programu Eclipse można ustawić różne ustawienia konfiguracji dla roli użytkownika platformy Azure.

## <a name="configuring-azure-role-properties"></a>Konfigurowanie właściwości roli Azure
Konfigurowanie właściwości roli platformy Azure jest realizowane za pomocą okien dialogowych właściwości dla swojej roli procesu roboczego. Otwórz w okienku Eksplorator projektów programu Eclipse w menu kontekstowego dla roli i wybierz **Azure** podmenu. (Jeśli nie widzisz roli w obszarze Eksplorator projektów programu Eclipse, rozwiń węzeł projektu platformy Azure w obszarze Eksplorator projektów).

![][ic789599]

Różne właściwości, które można ustawić z **właściwości** okna dialogowe są opisane w tym temacie. Należy pamiętać, że wiele właściwości są automatycznie wypełniane podczas tworzenia nowego projektu wdrożenia usługi Azure.

Następujące strony właściwości dostępnych dla ról platformy Azure.

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
Otwórz menu kontekstowe dla roli w okienku Eksplorator projektów dla programu Eclipse kliknij **Azure**, a następnie kliknij przycisk **właściwości**, i będzie mieć możliwość zmiany rozmiaru maszyny wirtualnej, a także zmienić numer wystąpień, jak pokazano na poniższej ilustracji.

![][ic719499]

> [!NOTE]
> Tylko w systemie Windows: po ustawieniu liczby wystąpień na wartość większą niż 1, a także skonfigurować serwer aplikacji, zestaw narzędzi zezwala tylko na 1 wystąpienia roli do uruchomienia w emulatorze, niezależnie od tego ustawienia. Pozwoli to uniknąć portu konflikty powiązania między wystąpieniami inny serwer (na przykład wszystkie próby utworzenia powiązania z portu 8080) uruchamianych na tym samym komputerze. Liczba wystąpienia odpowiednie ustawienia zostaną zachowane, ale jest uruchamiana tylko w przypadku wdrażania w chmurze.
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>Właściwości buforowania
Otwórz menu kontekstowe dla roli w okienku Eksplorator projektów dla programu Eclipse kliknij **Azure**, a następnie kliknij przycisk **buforowanie**. W tym oknie dialogowym można włączyć nazwanego wspólnie memcache zgodnego pamięci podręcznych, umożliwiając przyspieszyć aplikacji sieci web.

![][ic719483]

W ramach **buforowanie** strony właściwości można określić następujące ustawienia globalne:

* Określa, czy jest włączone buforowanie wspólnie.
* rozmiar pamięci podręcznej w pamięci w procentach.
* Nazwa konta magazynu do zapisania stanu pamięci podręcznej, gdy aplikacja działa jako usługa w chmurze lub none, jeśli nie chcesz zapisać stan pamięci podręcznej. (Nazwa konta magazynu nie jest używana podczas uruchamiania aplikacji w emulatorze obliczeń.) Jeśli wybrana nazwa konta magazynu **(automatycznie)** (jest to wartość domyślna), konfigurację buforowania będą automatycznie używać tego samego konta magazynu, należy wybrać w **publikowania na platformie Azure** okna dialogowego.

> [!NOTE]
> **(Automatycznie)** ustawienie będzie mieć uwzględnione tylko w przypadku wdrożenia przy użyciu zestawu narzędzi Eclipse Kreator publikowania. Jeśli zamiast tego można opublikować pliku cspkg ręcznie przy użyciu mechanizmu zewnętrznych, takich jak [portalu zarządzania Azure][Azure Management Portal], wdrożenie nie będzie działać prawidłowo.
> 
> 

To okno dialogowe wyświetlane właściwości na potrzeby pamięci podręcznej.

![][ic719501]

* **Nazwa:** nazwę tej samej lokalizacji pamięci podręcznej.
* **Numer portu:** numer portu na potrzeby pamięci podręcznej.
* **Zasady wygasania:** jedną z następujących wartości, które określają, kiedy wygasa klucz w pamięci podręcznej.
  * **Bezwzględna:** klucz wygasa przez określony czas **minut na żywo** zostanie osiągnięty.
  * **NeverExpires:** klucz nie ma czasu wygaśnięcia.
  * **SlidingWindow:** klucz wygasa, jeśli nie była używana przez czas określony przez **minut na żywo**; zawsze jest on dostępny, wygaśnięcia zegar zostanie zresetowana.
* **Minut na żywo:** maksymalna liczba minut dla klucza memcached na żywo może ulec zasady wygasania.
* **Wysoką dostępność z replikowanych kopii zapasowych w różnych wystąpieniach:** włączenie pomaga zapewnić wysokiej dostępności przy użyciu replikowane kopie zapasowe w wystąpieniach ról. Należy pamiętać, że co najmniej dwa wystąpienia roli musi być obowiązywać dla danego wdrożenia, ta funkcja działała.

Aby dodać nową pamięć podręczną, kliknij przycisk **Dodaj** przycisk **buforowanie** strony właściwości oraz **Konfigurowanie pamięci podręcznej o nazwie** będzie można otworzyć okna dialogowego. Podaj wartości dla właściwości, które są opisane powyżej.

Aby zmodyfikować nazwanego pamięci podręcznej, wybierz pamięci podręcznej, a następnie kliknij przycisk **Edytuj** przycisk **buforowanie** strony właściwości. Okno dialogowe zostanie otwarty, co umożliwia modyfikowanie właściwości pamięci podręcznej. Naciśnij klawisz **OK** można zapisać wartości pamięci podręcznej.

Aby usunąć pamięć podręczną, wybierz pamięci podręcznej, a następnie kliknij przycisk **Usuń** przycisk **buforowanie** strony właściwości, a następnie kliknij **tak** aby potwierdzić usunięcie.

Aby uzyskać więcej informacji na temat korzystania z pamięci podręcznej, zobacz [sposobu użycia buforowania Co-located][How to Use Co-located Caching].

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>Właściwości certyfikatów
Otwórz menu kontekstowe dla roli w okienku Eksplorator projektów dla programu Eclipse kliknij **Azure**, a następnie kliknij przycisk **certyfikaty**.

![][ic710964]

W tym oknie dialogowym można dodawać lub Usuń certyfikaty odwołuje się projektu Eclipse. Zauważ, że certyfikaty wymienione w tym miejscu nie są automatycznie przechowywane w dowolnym Java keystore i w związku z tym nie są automatycznie dostępne do użycia z poziomu aplikacji Java. Tylko są zarejestrowane z platformy Azure, dzięki czemu mogą być załadowane w systemie Windows certyfikat przechowywać na maszynach wirtualnych działających wdrożenia i następnie używane przez inne oprogramowanie systemu Windows. Obecnie jedyną funkcją zestawu narzędzi, który używa certyfikatów przywoływany w ten sposób w **certyfikaty** okno dialogowe jest [odciążanie protokołu SSL][SSL Offloading], z powodu jego zależność od Internet Information Services (IIS) i Routing żądań aplikacji (ARR), które wymagają właściwy certyfikat ma zostać udostępniony w ten sposób.

Podczas wdrażania projektu na platformie Azure przy użyciu Kreatora publikowania, pojawi się monit aby wskazywały na plik wymiany informacji osobistych (PFX) odpowiadający tych certyfikatów, wraz z ich hasła, aby automatycznie przekazać je do usługi Azure , ale tylko wtedy, gdy ich nie zostały przekazane istnieje wcześniej.

<a name="components_properties"></a> 

### <a name="components-properties"></a>Właściwości składników
Otwórz menu kontekstowe dla roli w okienku Eksplorator projektów dla programu Eclipse kliknij **Azure**, a następnie kliknij przycisk **składniki**. W tym oknie dialogowym możesz mieć możliwość dodać, zmodyfikować, lub usunąć składniki roli użytkownika, a także zmienić kolejność, w jakiej są przetwarzane.

![][ic719502]

Funkcja składników umożliwia dodawanie zależności do projektu wdrożenia usługi Azure, takich jak projekty aplikacji Java, specjalne pliki i instrukcje pliku wykonywalnego wiersza polecenia, które są wymagane przez wdrożenie.

Dla każdego składnika można określić:

* Krok podejmowane podczas importowania składnika do projektu wdrożenia usługi Azure, gdy jest ona wbudowana.
* Krok do wykonania, kiedy wdrażanie tego składnika w chmurze Azure.

> [!NOTE]
> Podczas określania składnika pliki lub wiersze polecenia, należy pamiętać, że wdrożenia zostaną opublikowane na maszynę wirtualną systemu Windows, wszystkie niestandardowe czynności musi być prawidłowy dla systemu operacyjnego Windows. 
> 
> 

Składniki mają następujące właściwości:

* **Import:** metodę, która wskazuje, jak składnika zostaną zaimportowane do projektu podczas tworzenia projektu. Może to być jedna z następujących wartości:
  * **Kopiuj:** składnik zostanie skopiowana ze ścieżki lokalnej, określony przez **z** właściwości do roli **approot** katalogu.
  * **Wyczyść:** składnika jest archiwum enterprise Java (Wyczyść) zaimportowane z projektu aplikacji przedsiębiorstwa o ścieżce lokalnej określony przez **z** właściwości. (To jest wykrywane automatycznie przez toolkit oparte na rodzaj projektu w tej lokalizacji).
  * **JAR:** składnik to archiwum Java (JAR) i jest importowany z projektu języka Java w lokalnej ścieżce określony przez **z** właściwości. (To jest wykrywane automatycznie przez toolkit oparte na rodzaj projektu w tej lokalizacji).
  * **Brak:** do zaimportowania składnika nie podjęto żadnej akcji. Ma to zastosowanie, gdy składnik zakłada się, że już istnieje w tej roli **approot** katalogu, lub gdy składnik jest jedynie pliku wykonywalnego wiersza polecenia instrukcji, jak określono w **jako** Właściwość podczas **Wdróż** jest metoda **exec**.
  * **WAR:** składnik jest Java archiwum aplikacji sieci web (plik WAR) i jest importowany z dynamiczny projekt sieci Web o ścieżce lokalnej określony przez **z** właściwości. (To jest wykrywane automatycznie przez toolkit oparte na rodzaj projektu w tej lokalizacji).
  * **ZIP:** składnik jest plik zip i zaimportowanych przez pakowanie katalogu lub pliku określonego przez **z** właściwości.
* **Od:** ścieżki źródłowej na komputerze lokalnym do folderu lub pliku, który reprezentuje elementy, aby je zaimportować do wdrożenia. Zmiennych środowiskowych systemu Windows można użyć w tej właściwości. Wszystkie składniki importowane zostaną zaimportowane do roli **approot** katalogu podczas tworzenia projektu.
  
    Należy pamiętać, że masz możliwość wdrażania składnika pobierać podczas wdrażania w chmurze (nie emulatora obliczeń). Zobacz poniższe pokrewne informacje dotyczące dodawania składnika.    
* **Jak:** nazwę pliku, w którym składnik zostaną zaimportowane do roli **approot** katalogu i ostatecznie wdrożonych w chmurze Azure. Ta właściwość pozostaw puste, aby zachować tę nazwę takie same jak na komputerze lokalnym. (Dla pliku wykonywalnego składników, czyli tych, których **Wdróż** metoda jest ustawiona na **exec**, może to być instrukcji dowolnego wiersza polecenia systemu Windows.)
  
  > [!IMPORTANT]
  > Jeśli używasz znaków spacji dla tej wartości, ich obsługi inaczej w zależności od metody wdrażania. Jeśli metoda wdrażania jest **exec**, spacje zostanie potraktowany jako separatory argumentów wiersza polecenia, a nie jako część nazwy pliku. Dla wszystkich innych wdrażania metod, spacje, które będą interpretowane jako część nazwy pliku.
  > 
  > 
* **Wdróż:** metodę, która wskazuje akcję zastosować do składnika, po uruchomieniu wdrożenia. Może to być jedna z następujących wartości:
  
  * **Kopiuj:** składnik jest kopiowany do ścieżki docelowej, określone przez **do** właściwości.
  * **exec:** składnika jest instrukcji pliku wykonywalnego wiersza polecenia systemu Windows wykonywana w kontekście ścieżka określona przez **do** właściwości w momencie uruchamiania wdrożenia.
  * **Brak:** żadna akcja ze strony jest stosowany do składnika, po uruchomieniu wdrożenia.
  * **ZIP:** składnika jest rozpakowane w ścieżce docelowej, określone przez **do** właściwości. Ta metoda jest dostępna tylko wtedy, gdy **importu** właściwość jest **zip**.
* **Do:** ścieżkę docelową na maszynie wirtualnej, w którym zostanie wdrożony składnik. Zmiennych środowiskowych systemu Windows mogą być używane w tej właściwości, a ścieżki plików są względem **approot**.

Aby dodać nowy składnik, kliknij przycisk **Dodaj** przycisk **składniki** stronę właściwości i **składnika roli Azure** będzie można otworzyć okna dialogowego. Podaj wartości dla właściwości, które są opisane powyżej. 

Poniżej przedstawiono przykład do dodawania nowego składnika WAR.

![][ic719503]

Podczas wdrażania w chmurze (nie emulatora obliczeń), jeśli chcesz wdrożyć składnik pobierać, upewnij się, że **w chmurze zamiast w pakiecie, w tym wdrażanie z** jest zaznaczony. Jeśli chcesz pobrać z kontem magazynu platformy Azure, wybierz konto magazynu z **konta magazynu** listy rozwijanej (możesz kliknąć **kont** łącze, aby zmodyfikować co znajduje się na liście), który będzie częściowo wypełnić **adres URL** pola, a następnie wprowadź pozostałą część adresu URL. Jeśli nie chcesz używać usługi Azure storage, wybierz **(Brak)** z **konta magazynu** listy rozwijanej liście, a następnie wprowadź adres URL do składnika w **adres URL** pola. Określ jedną z następujących metod:

* **Kopiuj:** składnika pobierania jest kopiowany do ścieżki docelowej, określone przez **do katalogu** ścieżki.
* **tym samym:** tej samej metody używane do **Wdróż z pobierania** jak w przypadku **Wdróż z pakietu**.
* **ZIP:** składnik pobierania jest rozpakowane w ścieżce docelowej, określone przez **do katalogu** ścieżki.

Aby zmodyfikować składnikiem, wybierz składnik, a następnie kliknij przycisk **Edytuj** przycisk **składniki** strony właściwości. Okno dialogowe zostanie otwarty, co umożliwia modyfikowanie właściwości składnika. Naciśnij klawisz **OK** można zapisać wartości składnika.

Aby usunąć składnikiem, wybierz składnik, a następnie kliknij przycisk **Usuń** przycisk **składniki** strony właściwości, a następnie kliknij przycisk **tak** o potwierdzenie usunięcia.

Składniki są przetwarzane w podanej kolejności. Użyj **Przenieś w górę** i **Przenieś w dół** przycisków, aby określić kolejność.

> [!NOTE]
> Funkcja konfiguracji serwera zależy od również składników. Te składniki nie można usunąć ani edytować bez usuwania odpowiednich konfiguracji serwera. Zostanie wyświetlony monit o tym, że podczas próby wprowadzenia zmian w tych składnikach.
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have the ability to enable or disable remote debugging, as well as create debug configurations, as shown in the following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>Właściwości punktów końcowych
Otwórz menu kontekstowe dla roli w okienku Eksplorator projektów dla programu Eclipse kliknij **Azure**, a następnie kliknij przycisk **punkty końcowe**. W tym oknie dialogowym możesz mieć możliwość tworzenie punktu końcowego, a także edytować lub usunąć punkt końcowy, jak pokazano na poniższej ilustracji.

![][ic719505]

Dodawanie punktu końcowego, kliknij przycisk **Dodaj** przycisk **punkty końcowe** stronę właściwości i **Dodawanie punktu końcowego** będzie można otworzyć okna dialogowego.

![][ic710897]

Wprowadź nazwę dla punktu końcowego, wybierz typ (albo **dane wejściowe**, **wewnętrzne**, lub **InstanceInput**) i określić port publiczny i prywatny. Naciśnij klawisz **OK** zapisać nowe wartości punktu końcowego.

W zależności od typu punktu końcowego może używać zakresów portów w następujący sposób:

* Dla punktu końcowego wystąpienia wejściowych port publiczny może być zakresu portów (na przykład **2000 2010**) i port prywatny jest wartością stałą.
* Wewnętrznego punktu końcowego port publiczny nie jest używana i port prywatny może być zakresem lub pozostanie puste lub ustaw wartość gwiazdkę, aby określić, że zostanie automatycznie ustawione przez platformę Azure.
* Dla wejściowych punktów końcowych port publiczny tylko może być wartością stałą, a port prywatny może być wartością stałą lub pozostanie puste lub ustawić gwiazdkę wskazująca, że ta jest automatycznie ustawiana na platformie Azure.

Jeśli chcesz użyć numer pojedynczego portu zamiast zakresu, pozostaw pole tekstowe dla elementu end pusty zakres.

Dla portów, które są ustawione na automatyczne, jeśli trzeba określić port, który będzie faktycznie używana w czasie wykonywania, aplikacja może używać interfejsu API środowiska uruchomieniowego usługi Azure, w którym opisano w [pakietu com.microsoft.windowsazure.serviceruntime podsumowania ][com.microsoft.windowsazure.serviceruntime package summary].

<!-- To see how instance input endpoints can be used to help with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

Aby zmodyfikować punkt końcowy, wybierz punkt końcowy, a następnie kliknij przycisk **Edytuj** przycisk **punkty końcowe** strony właściwości. Okno dialogowe zostanie otwarty, umożliwiając zmodyfikować nazwę punktu końcowego, typ i portów publicznego i prywatnego. Naciśnij klawisz **OK** można zapisać wartości zmodyfikowanej punktu końcowego.

Aby usunąć punkt końcowy, wybierz punkt końcowy, a następnie kliknij przycisk **Usuń** przycisk **punktów końcowych** strony właściwości, a następnie kliknij przycisk **tak** o potwierdzenie usunięcia.

Aby poprawnie skonfigurować funkcji (takich jak buforowanie, koligacji sesji lub SSL Odciążanie) włączenia przez użytkownika w roli, zestawu narzędzi mogą automatycznie konfigurować specjalne punkty końcowe, które zostaną wyświetlone wraz z zdefiniowane przez użytkownika punktów końcowych. Zestaw narzędzi uniemożliwia użytkownikowi edytowanie lub usuwanie takie automatycznie wygenerowany punkty końcowe tak długo, jak skojarzona funkcja jest włączona.

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>Właściwości zmiennych środowiskowych
Otwórz menu kontekstowe dla roli w okienku Eksplorator projektów dla programu Eclipse kliknij **Azure**, a następnie kliknij przycisk **zmiennych środowiskowych**. W tym oknie dialogowym możesz mieć możliwość tworzenia zmiennej środowiskowej, a także zmodyfikować lub usunąć zmienną środowiskową jak pokazano na poniższej ilustracji.

![][ic719506]

Zmienne środowiskowe są dostępne do uruchomienia skryptu, podczas uruchamiania roli.

> [!NOTE]
> W przypadku określania zmiennych środowiskowych, należy pamiętać, że wdrożenia zostaną opublikowane na maszynę wirtualną systemu Windows, zmienne środowiskowe musi być prawidłowy dla systemu operacyjnego Windows.
> 
> 

Jako przykład zmiennej środowiskowej, są dostępne po uruchomieniu roli, utworzyć nową zmienną środowiskową, klikając **Dodaj** przycisku. Poniżej pokazano zmienną środowiskową o nazwie **MyRoleVersion** są tworzone i ma przypisaną wartość **1.0**.

![][ic659268]

W kodzie jsp można wyświetlić przy użyciu wartości `System.getenv` metody:

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

Spowodować, że te dane wyjściowe po uruchomieniu aplikacji:

![][ic552233]

Aby zmodyfikować wartość zmiennej środowiskowej, wybierz zmiennej środowiskowej, a następnie kliknij przycisk **Edytuj** przycisk **zmiennych środowiskowych** strony właściwości. Okno dialogowe zostanie otwarty, co umożliwia modyfikowanie właściwości zmiennej środowiskowej. Naciśnij klawisz **OK** można zapisać wartości zmiennych środowiska.

Aby usunąć zmienną środowiskową, wybierz zmiennej środowiskowej, a następnie kliknij przycisk **Usuń** przycisk **zmiennych środowiskowych** strony właściwości, a następnie kliknij przycisk **tak** do potwierdzenie usunięcia.

Aby poprawnie skonfigurować niektóre funkcje (np. Konfiguracja serwera zdalnego debugowania lub lokalnego magazynu) włączenia przez użytkownika w roli, zestawu narzędzi mogą automatycznie konfigurować zmienne środowiskowe specjalne, które będą wyświetlane wraz z zdefiniowane przez użytkownika zmienne środowiskowe. Zestaw narzędzi uniemożliwia użytkownikowi edytowanie lub usuwanie takie automatycznie wygenerowany zmiennych środowiskowych tak długo, jak skojarzona funkcja jest włączona.

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>Równoważenie obciążenia / właściwości sesji koligacji (nazywane również "trwałe sesje")
Otwórz menu kontekstowe dla roli w okienku Eksplorator projektów dla programu Eclipse kliknij **Azure**, a następnie kliknij przycisk **równoważenia obciążenia**. W tym oknie dialogowym możesz mieć możliwość włączyć lub wyłączyć koligacji sesji, jak pokazano na poniższej ilustracji.

![][ic719492]

Aby uzyskać odpowiednie informacje, zobacz [koligacji sesji][Session Affinity]. Zauważ również, działanie tej funkcji w kontekście odciążanie protokołu SSL, zgodnie z opisem w [odciążanie protokołu SSL][SSL Offloading].

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>Lokalny magazyn właściwości
Otwórz menu kontekstowe dla roli w okienku Eksplorator projektów dla programu Eclipse kliknij **Azure**, a następnie kliknij przycisk **Magazyn lokalny**. W tym oknie dialogowym możesz mieć możliwość utworzyć, zmodyfikować lub usunąć tymczasowego magazynu lokalnego dla maszyny wirtualnej, która jest uruchomiona aplikacja. Określone wartości można ustawić dla rozmiaru magazynu lokalnego, a także czy zawartość zostaną zachowane, gdy rola jest ponownie przetworzony, jak pokazano na poniższej ilustracji.

![][ic719508]

Również Opcjonalnie możesz określić zmienną środowiskową umożliwiająca magazynu lokalnego.

Domyślnie wszystkie czynności, które można wdrożyć na platformie Azure jest umieszczony (i rozpakowane) w **approot** folderu wystąpienia roli. Podczas gdy większość prostych wdrożeń zmieści się nawet po rozpakować, miejsce przydzielone dla **approot** katalog jest ograniczona i nie jest dobrze zdefiniowany (mniej niż 1 GB jest uzasadnione zasadą). W związku z tym zapewnienie Azure przydziela miejsce na dysku w przypadku większych wdrożeń, które mogą nie mieści się w **approot** folderu, należy skonfigurować zasobów magazynu lokalnego przy użyciu **Magazyn lokalny** okna dialogowego. Aby łatwo to zrobić, zobacz [wdrażanie dużych wdrożeniach][Deploying Large Deployments].

Możesz łatwo odwoływać się do zasobów magazynu ze skryptami uruchamiania (na przykład z **startup.cmd**) przy użyciu zmiennej środowiskowej automatycznie skojarzone przez zestaw narzędzi Eclipse z zasobów, jak pokazano w  **Lokalny magazyn** okna dialogowego. Tej zmiennej środowiskowej będzie zawierać pełną ścieżkę zasób lokalny, skonfigurowanego w momencie uruchamiania skrypt jest wykonywany. 

Aby zmodyfikować zasobów magazynu lokalnego, wybierz zasób lokalny magazyn, a następnie kliknij przycisk **Edytuj** przycisk **Magazyn lokalny** strony właściwości. Okno dialogowe zostanie otwarty, co pozwala modyfikować właściwości zasobu magazynu lokalnego. Naciśnij klawisz **OK** można zapisać wartości zasobów magazynu lokalnego.

Można usunąć zasobu magazynu lokalnego, wybierz zasób lokalny magazyn, a następnie kliknij przycisk **Usuń** przycisk **Magazyn lokalny** strony właściwości, a następnie kliknij przycisk **tak** o potwierdzenie usuwanie.

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>Właściwości konfiguracji serwera
Otwórz menu kontekstowe dla roli w okienku Eksplorator projektów dla programu Eclipse kliknij **Azure**, a następnie kliknij przycisk **konfiguracji serwera**. W tym oknie dialogowym mają możliwość dodawania, usuwania i modyfikowania JDK i Java serwer aplikacji używany przez wdrożenie, a także dodać lub usunąć aplikacji (na przykład plik WAR, JAR lub wyczyść) używanych przez wdrożenie.

### <a name="jdk-configuration"></a>Konfiguracja JDK
To okno dialogowe służy do określenia JDK pakiet do użycia dla danego wdrożenia. Jeśli używasz programu Eclipse w systemie Windows, można określić pakietu JDK, aby uruchamiał lokalnie w emulatorze platformy Azure i mieć możliwość wdrożenia tej instalacji lokalnej do platformy Azure. W systemach operacyjnych innych niż Windows ustawienie JDK emulatora nie ma zastosowania i nie można wdrożyć JDK zainstalowanej lokalnie, ponieważ nie jest zgodny z systemem Windows. Jednak niezależnie od systemu operacyjnego, którego używasz, zawsze można między 3 pakietów JDK stronę wdrażanie na platformie Azure lub wskaż pakiet JDK zgodne z systemem Windows z lokalizacji alternatywnej.

Poniżej przedstawiono przykładowy sposób można określić JDK w systemie Windows:

![][ic780647]

Jeśli używasz programu Eclipse w systemie Windows, można określić JDK do użycia z emulatora obliczeń; Aby to zrobić, upewnij się, **testowania lokalnie na użytek JDK z podanej ścieżki pliku** zaewidencjonowania **wdrożenia urządzenia emulatora** sekcji. Następnie określ ścieżkę lokalną do Twojej JDK; można przejść do różnych JDK, jeśli ten, który chcesz użyć nie zostanie wybrana automatycznie. Masz również możliwość wdrożenia programu JDK do usługi w chmurze Azure; Aby to zrobić, wybierz **wdrażanie Moje JDK lokalnego (auto przekazywania do magazynu w chmurze)** opcji **wdrożenie w chmurze** sekcji.

Uwaga: W systemach operacyjnych innych niż Windows **wdrożenia urządzenia emulatora** ustawienia i **wdrażanie Moje lokalnego JDK** opcji nie są dostępne. Poniższy przykład przedstawia określenie JDK na komputerze Mac lub innego obsługiwanego systemu operacyjnego z systemem innym niż Windows:

![][ic789643]

Niezależnie od systemu operacyjnego znajdują się na, masz następujące dwa **wdrożenie w chmurze** opcje źródłowego i typu pakietu JDK:

* **Wdrożenia dostępnych na platformie Azure pakietu JDK 3 stron** 
* **Wdrażanie z pobierania niestandardowych** 

Jeśli używasz **wdrożenia dostępnej w sklepie Azure pakietu JDK 3 strona** opcji:

1. Zaznacz pole wyboru o nazwie **wdrożenia dostępnej w sklepie Azure pakietu JDK 3 strona**.
2. Z listy rozwijanej wybierz pakiet JDK strona 3, który jest dostępny na platformie Azure.
3. Twoje **JDK** kartę będzie wyglądała podobnie do następującego w systemie Windows: ![][ic780648] i będzie wyglądać podobnie jak poniżej w systemie Mac OS lub innych obsługiwanych systemach operacyjnych innych niż Windows:![][ic789643]
4. Kliknij przycisk **OK**, aby zapisać zmiany.
5. Po wyświetleniu monitu Zaakceptuj Umowę licencyjną z 3 dostawcy pakietu JDK firm Przejrzyj postanowienia licencyjne. Zakładając, że akceptujesz jej warunki, kliknij przycisk **tak** zamknąć **zaakceptować umowę licencyjną** okna dialogowego.
    Należy pamiętać, że logikę podstawowe elementy, które są wyświetlane na liście rozwijanej **wdrożenia dostępnej w sklepie Azure pakietu JDK 3 strona** opcji można dostosować. Do dostosowywania elementów, w **JDK** okna dialogowego, kliknij przycisk **Dostosuj** łącza. Spowoduje to zamknięcie **JDK** stronę właściwości i Otwórz **componentsets.xml** plików w środowisku Eclipse, które następnie można zmodyfikować zgodnie z potrzebami. Dokumentacja **componentsets.xml** znajduje się w **componentsets.xml** samym pliku.

Jeśli używasz **wdrażanie JDK niestandardowych pobierać** opcji:

1. Utwórz ZIP katalogu instalacji JDK zapewnia, że węzeł katalogu jest elementem podrzędnym struktury ZIP, a nie jego zawartość. Zanotuj nazwę katalogu, ponieważ będzie potrzebny później, a pamiętać tej instalacji JDK zostanie wdrożone do maszyny wirtualnej systemu Windows.
2. Przekaż ZIP na koncie magazynu Azure jako obiektu blob. Możesz to zrobić to za pomocą zewnętrznie dostępne narzędzia dla przekazywania obiekty BLOB do magazynu Azure. Zalecane jest Użyj prywatnego obiektu blob. Zanotuj adres URL obiektu blob zawartości ZIP.
3. Zaznacz pole wyboru o nazwie **wdrażanie JDK niestandardowych pobierać**.
    Jeśli chcesz pobrać z kontem magazynu platformy Azure, wybierz konto magazynu z **konta magazynu** listy rozwijanej (możesz kliknąć **kont** łącze, aby zmodyfikować co znajduje się na liście), który będzie częściowo wypełnić **adres URL** pola, a następnie wprowadź pozostałą część adresu URL. Jeśli nie chcesz używać usługi Azure storage, wybierz **(Brak)** z **konta magazynu** listy rozwijanej liście, a następnie wprowadź adres URL do pobierania JDK w **adres URL** pola. Jeśli za pomocą usługi Azure storage, nazwy obiektów blob w adresie URL muszą być małe litery.
4. Upewnij się, że **JAVA_HOME** pole tekstowe odwołuje się do nazwy poprawnym katalogu. Domyślnie odwołania się taką samą nazwę katalogu JDK jak wartość wybrana do użycia lokalnego. Ale jeśli katalog zawarte w ZIP ma inną nazwę (na przykład z powodu przy użyciu innej wersji), zaktualizuj nazwę katalogu w **JAVA_HOME** textbox w związku z tym, ponieważ to ustawienie będzie można używać w chmurze (nie znajduje się w emulator obliczeń).
5. Kliknij przycisk **OK**, aby zapisać zmiany.

To już wszystko. Teraz po utworzeniu chmury można zauważyć będzie znacznie mniejszy rozmiar pakietu, proces kompilacji zazwyczaj powinno zająć mniej czasu i samego w sobie podczas publikowania do chmury wdrażania również powinno zająć mniej czasu. Należy pamiętać, że **wdrażanie Moje JDK lokalnego (auto przekazywania do magazynu w chmurze)** lub **wdrażanie JDK niestandardowych pobierać** są opcje obowiązują tylko podczas wdrażania aplikacji w chmurze. Nie mają wpływu na środowiska emulatora obliczeń; lokalna wersja składników nadal będzie używane, jeśli wdrażasz do emulatora obliczeń. 

### <a name="server-configuration"></a>Konfiguracja serwera
Poniżej przedstawiono przykładowy sposób można określić serwer aplikacji.

![][ic796926]

Sprawdź, czy **wdrożenie serwera tego typu** pole wyboru jest zaznaczone, a następnie wybierz typ serwera aplikacji, którego chcesz użyć.

Do określenia serwera do zastosowania podczas wdrażania w chmurze, można skorzystać z następujących opcji:

1. **Wdrażanie serwera strona 3 dostępnych na platformie Azure** — szczególnie stosować w scenariusze tworzenia/testowania, gdy proces wdrażania i prostota jest priorytet i serwer nie wymaga konfiguracji niestandardowej. Lub gdy chcesz używać jednego z tych serwerów jako punkt początkowy, ale możesz uwzględnić odpowiedni serwer dostosowywania kroków w danym wdrożeniu Logika uruchamiania.
2. **Wdrażanie niestandardowych pobierać** — jest to szczególnie odpowiednie w scenariuszach produkcji, gdy masz specjalnie przygotowany i jest skonfigurowany serwer, którego chcesz użyć w chmurze.
3. **Wdrażanie instalacji Mój serwer lokalny** — szczególnie stosować w, jeśli instalacja lokalny serwer już jest konfigurowane do użycia. Jeśli wybierzesz tę opcję, należy również określić ścieżkę serwera lokalnego w **ścieżki serwera lokalnego** poniżej pola tekstowego.

Jeśli używasz **wdrożenia serwera strona 3 dostępnych na platformie Azure** opcji:

1. Zaznacz pole wyboru o nazwie **wdrożenia serwera strona 3 dostępnych na platformie Azure**.
2. Z menu rozwijanego wybierz oprogramowania żądany serwer do wdrożenia w chmurze. Uwaga: Jeśli już określony typ serwera, aby użyć wcześniej, będzie ograniczony do wybierania tylko serwer chmury jest w tej samej rodziny jako typu serwera. Jednak jeśli nie wybrano typu serwera, możesz wybrać spośród wszystkich serwerów, które są obecnie dostępne w systemie Azure i typ serwera zostanie automatycznie wybrana automatycznie.
3. Kliknij przycisk **OK**, aby zapisać zmiany.

Jeśli przy użyciu **wdrażanie niestandardowych pobierać** opcji:

1. Upewnij się, czy już wybrano typ serwera, zgodnie z powyższych kroków. Informuje wtyczki, jak wdrożyć serwer z niestandardowych pobieranie, muszą być w tej samej rodziny jako typ wybranego serwera.
2. Zaznacz pole wyboru o nazwie **Wdróż z niestandardowych pobierania**.
    Jeśli chcesz pobrać z kontem magazynu platformy Azure, wybierz konto magazynu z **konta magazynu** listy rozwijanej (możesz kliknąć **kont** łącze, aby zmodyfikować co znajduje się na liście), który będzie częściowo wypełnić **adres URL** pola, a następnie wypełnij pozostałą część adresu URL do serwera Pobierz ZIP (Jeśli za pomocą usługi Azure storage, nazwy obiektów blob w adresie URL muszą być małymi literami). Jeśli nie chcesz używać usługi Azure storage, wybierz **(Brak)** z **konta magazynu** listy rozwijanej liście, a następnie wprowadź adres URL do serwera Pobierz ZIP w **adres URL** pola. ZIP zawiera folder podrzędny reprezentujący katalogu instalacji serwera aplikacji. Na przykład, jeśli używasz zip dla Apache Tomcat 7.0.35, w zip będzie folder podrzędny reprezentujący katalog instalacyjny, takich jak **apache-tomcat-7.0.35**. 
3. Określ wartość dla zmiennej środowiskowej katalogu macierzystego. Domyślnie zostanie użyta wartość używaną do serwera lokalnego aplikacji, jeśli istnieje, ale można określić inną wartość, jeśli serwer aplikacji w chmurze różni się od serwera lokalnego aplikacji. Jednak należy upewnić się, że serwer aplikacji w chmurze o tej samej rodziny, co serwer wcześniej wybranego typu.
    Po zaktualizowaniu chmury pocztowy serwera aplikacji w przyszłości, możesz ręcznie zmienić ustawienie katalogu macierzystego lub, aby go ponownie zgodne z lokalnym ustawienie (serwer aplikacji lokalnych jest zmieniony zbyt).
4. Kliknij przycisk **OK**, aby zapisać zmiany.

Podstawowej logiki, dla którego elementy są wyświetlane w **serwera** karcie **konfiguracji serwera** strony właściwości można dostosować. Jest to zaawansowana funkcja, która może być konieczne, jeśli potrzeb wykraczają poza wartości domyślne lub jeśli chcesz dodać inne serwery. Aby dostosować logikę w **serwera** okna dialogowego, kliknij przycisk **Dostosuj** łącza. Spowoduje to zamknięcie **konfiguracji serwera** stronę właściwości i Otwórz **componentsets.xml** plików w środowisku Eclipse, które następnie można zmodyfikować zgodnie z potrzebami rozszerzyć serwer konfiguracji szablonu. Dokumentacja **componentsets.xml** znajduje się w **componentsets.xml** samym pliku.

Jeśli używasz **wdrożyć serwer lokalny (auto przekazywania do magazynu w chmurze)** opcji:

1. Zaznacz pole wyboru o nazwie **wdrożyć serwer lokalny (auto przekazywania do magazynu w chmurze)**.
2. Przy użyciu **konta magazynu** listy rozwijanej wybierz **(automatycznie)**. Jeśli określisz **(automatycznie)** w tym miejscu zestawu narzędzi Eclipse użyje tego samego konta magazynu dla serwera, wybierz dla danego wdrożenia w **publikowania na platformie Azure** okna dialogowego.
3. Kliknij przycisk **OK**, aby zapisać zmiany.

Wybierz ścieżkę instalacji serwera na komputerze w **ścieżki serwera lokalnego** pole tekstowe, jeśli spełnione są następujące warunki:

* Użytkownik chce przetestować wdrożenie w emulatorze (dotyczy tylko systemu Windows).
* Chcesz wdrożyć serwer instalowana lokalnie w chmurze.
* Aby użyć niestandardowego serwera pobieranie własne w chmurze, w którego przypadku, upewnij się również **wdrożyć serwer lokalny (auto przekazywania do magazynu w chmurze)** powyżej wybrano opcję.

Jeśli żaden z tych opcji do sytuacji, ustawienie serwer lokalny jest opcjonalne.

### <a name="applications-configuration"></a>Konfiguracja aplikacji
Poniżej przedstawiono przykładowy sposób można określić aplikacji.

![][ic719512]

Kliknij przycisk **Dodaj** Aby dodać inną aplikację, lub **Usuń** do usuwania aplikacji. Do celów wydajność, jeśli chcesz użyć do pobrania źródła aplikacji podczas wdrażania w chmurze, użyj [właściwości składników](#components_properties) Aby określić adres URL, konta magazynu, itp. 

Począwszy od wersji kwietnia 2014 r, aplikacje automatycznie są przekazywane do tego samego konta magazynu (w obszarze **eclipsedeploy** kontenera) jako język wybrany do wdrożenia. Logika uruchamiania wdrożenia zawiera krok, który najpierw pobiera tych aplikacji z tego konta magazynu. Oznacza to, że może uaktualnienie aplikacji w danym wdrożeniu bez konieczności ponowne skompilowanie i wdrożenie całego pakietu, przekazując ręcznie nowszej wersji aplikacji bezpośrednio do tego konta magazynu (na przykład korzystanie z portalu Azure), zastępowanie plików WAR pierwotnie przekazany istnieje przez zestaw narzędzi. Następnie po prostu zainicjować odtwarzania tych wystąpień roli za pomocą portalu zarządzania platformy Azure, ponownie, lub za pomocą narzędzia wiersza polecenia. (Wyzwalanie roli odtwarzania bezpośrednio w zestawie narzędzi programu Eclipse nie jest obecnie obsługiwana.)

### <a name="notes-about-server-configuration"></a>Uwagi dotyczące konfiguracji serwera
Zmiany wprowadzane za pośrednictwem **konfiguracji serwera** strony właściwości są uwzględniane w `<component>` elementy pliku plik package.xml.

Jeśli używasz **automatyczne przekazywanie...**  lub **Wdróż z pobierania...**  opcje zestaw JDK lub serwera aplikacji i możesz tworzenia chmury (nie emulatora obliczeń) i są podłączone do sieci, mogą pojawić się kompilacji komunikaty, takie jak następujące opcje w dane wyjściowe z konsoli zgodnie z konstruktora Ant sprawdza dostępność pobierania:

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

W przypadku wybrania **Wdróż z pobierania...**  opcja, mogą zostać wyświetlone następujące ostrzeżenie, ale będzie kompilacji:

`[windowsazurepackage] warning: Failed to confirm blob availability! Make sure the URL and/or the access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

To ostrzeżenie jest jedyną reakcją dostępności pobierania nie zostało zweryfikowane. Tak w przypadku niepowodzenia wdrożenia w chmurze jakiegoś powodu Sprawdź, czy odebrano to ostrzeżenie.

Jeśli chcesz wyłączyć weryfikację pobierania (na przykład, jeśli uważasz, że jej niepotrzebnie spowalnia kompilacji), ustaw `verifydownloads` atrybutu `false` w `<windowsazurepackage>` elementu plik package.xml: 

`<windowsazurepackage verifydownloads="false" ...>` 

W przypadku wybrania **automatyczne przekazywanie...**  opcji, a następnie w oknie konsoli zostanie wyświetlony kompilacji raportowania postępu przekazywania co 5 sekund, gdy konieczne jest przekazanie wiadomości.

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>Odciążanie właściwości protokołu SSL
Otwórz menu kontekstowe dla roli w okienku Eksplorator projektów dla programu Eclipse kliknij **Azure**, a następnie kliknij przycisk **odciążanie protokołu SSL**. 

![][ic719481]

W tym oknie dialogowym można włączyć odciążanie protokołu SSL, dzięki czemu można łatwo włączyć obsługę Hypertext Transfer Protocol Secure (HTTPS) w danym wdrożeniu Java na platformie Azure, bez konieczności konfigurowania protokołu SSL na serwerze aplikacji Java. Aby uzyskać więcej informacji, zobacz [odciążanie protokołu SSL] [ SSL Offloading] i [sposobu użycia protokołu SSL Odciążanie][How to Use SSL Offloading].

## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse][Installing the Azure Toolkit for Eclipse]

[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Właściwości projektu platformy Azure][Azure Project Properties]

[Lista kont magazynu Azure][Azure Storage Account List]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center][Azure Java Developer Center].

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
[How to Use Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How to Use SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
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
