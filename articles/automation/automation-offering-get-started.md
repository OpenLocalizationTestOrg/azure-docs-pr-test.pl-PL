---
title: "AAA wprowadzenie do usługi Automatyzacja Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie usługi Automatyzacja Azure, sprawdzając szczegóły projekt i implementację hello w hello tooonboard przygotowania oferty z portalu Azure Marketplace."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 434e8ea28c55ff9bda1d2e46a7a6b8378a3baa0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation"></a>Rozpoczynanie pracy z usługą Azure Automation

Ta pobierania przewodnika wprowadzono podstawowe pojęcia pokrewne toohello wdrożenie usługi Automatyzacja Azure. Jeśli tooAutomation nowego na platformie Azure lub nie mają doświadczenia w automatyzacji oprogramowanie przepływu pracy, takie jak System Center Orchestrator, ten przewodnik pomaga zrozumieć sposób tooprepare i dołączyć automatyzacji.  Następnie można będzie gotowa toobegin tworzenia elementów runbook, w związku z Twoim potrzebom automatyzacji procesu. 


## <a name="automation-architecture-overview"></a>Omówienie architektury usługi Automation

![Omówienie usługi Azure Automation](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Automatyzacja Azure to oprogramowanie jako aplikacja usługi (SaaS), która zapewnia wielodostępne skalowalne i niezawodne, tooautomate środowiska przetwarza z elementami runbook i zarządzanie tooWindows zmian konfiguracji i systemu Linux przy użyciu konfiguracji żądanego stanu (DSC) w usługi w chmurze platformy Azure, inne lub lokalnie. Jednostki zawarte na Twoim koncie usługi Automation, takie jak elementy Runbook, zasoby, konta Uruchom jako, są izolowane od innych kont usługi Automation w ramach Twojej subskrypcji i innych subskrypcji.  

Elementy Runbook, które uruchamiasz na platformie Azure, są wykonywane w piaskownicach usługi Automation hostowanych na platformie Azure w postaci platformy jako usługi (PaaS) dla maszyn wirtualnych.  Piaskownice usługi Automation zapewniają izolację dzierżawy dla wszystkich aspektów wykonywania elementów Runbook — modułów, magazynu, pamięci, komunikacji sieciowej, strumieni zadań itd. Ta rola jest zarządzane przez usługę hello i nie jest dostępny z konta Azure lub usługi Automatyzacja Azure dla toocontrol użytkownik.         

tooautomate hello wdrażania i zarządzania zasobami w lokalnym centrum danych lub innych usług w chmurze, po utworzeniu konta automatyzacji można wyznaczyć co najmniej jeden hello toorun maszyny [hybrydowego procesu roboczego elementu Runbook (HRW)](automation-hybrid-runbook-worker.md) roli.  Każdy HRW wymaga hello agenta Microsoft Management Agent z obszaru roboczego analizy dzienników tooa połączenia i konto usługi Automatyzacja.  Analiza dzienników jest używane toobootstrap hello instalacji, obsługa hello agenta Microsoft Management Agent i monitorowanie hello funkcjonalność hello HRW.  dostarczanie Hello elementów runbook i hello toorun instrukcji, które je są wykonywane przez usługi Automatyzacja Azure.

Można wdrożenie wielu HRW tooprovide wysokiej dostępności dla elementy runbook, zadania elementów runbook Równoważenie obciążenia i w niektórych przypadkach należy przeznaczyć je dla konkretnego obciążeń lub środowisk.  Witaj Microsoft Monitoring Agent na powitania HRW inicjuje komunikację z hello usługi Automatyzacja za pośrednictwem portu TCP 443 i nie ma żadnych wymagań dotyczących zapory dla ruchu przychodzącego.  Po masz runbook uruchomionych na HRW w środowisku hello i mają hello runbook tooperform zadania związane z zarządzaniem przed innymi maszyny lub usługi, w tym środowisku, mogą być inne porty, które hello elementu runbook musi mieć dostęp do.  Jeśli zasady zabezpieczeń IT nie zezwalają na toohello tooconnect Twojego sieci Internet komputerów, przejrzyj artykuł hello [OMS bramy](../log-analytics/log-analytics-oms-gateway.md), który działa jako serwer proxy dla hello HRW toocollect stan zadania i odbierać informacje o konfiguracji z Twoje konto usługi Automatyzacja.

Elementów Runbook uruchomionych na HRW uruchomienie w kontekście hello hello lokalnego konta systemowego na komputerze hello, który jest hello zalecane kontekstu zabezpieczeń podczas wykonywania czynności administracyjnych na komputerze z systemem Windows hello. Jeśli chcesz hello runbook toorun zadania względem zasobów poza hello komputera lokalnego, może być konieczne toodefine trwałe bezpiecznych poświadczeń z hello konta automatyzacji można uzyskać dostępu do elementu runbook hello i tooauthenticate za pomocą zewnętrznego zasobu hello. Można użyć [poświadczeń](automation-credentials.md), [certyfikatu](automation-certificates.md), i [połączenia](automation-connections.md) zasoby w elemencie runbook za pomocą poleceń cmdlet, które pozwalają toospecify poświadczeń, można uwierzytelniać.

Konfiguracji DSC przechowywane w automatyzacji Azure mogą być bezpośrednio zastosowane tooAzure maszyn wirtualnych. Konfiguracje mogą żądać innych fizycznych i maszyn wirtualnych z serwera ściągania usługi Konfiguracja DSC automatyzacji Azure hello.  Do zarządzania konfiguracjami lokalnego fizycznych lub wirtualnych Windows i Linux systemów, nie potrzebujesz toodeploy żadnych toosupport hello usługi Konfiguracja DSC automatyzacji ściągania serwer infrastruktury, tylko ruch wychodzący do Internetu z każdej toobe systemu zarządzanych przez usługi Konfiguracja DSC automatyzacji , komunikować się za pośrednictwem protokołu TCP port 443 toohello usługę.   

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="automation-dsc"></a>Usługa Automation DSC
Konfiguracja DSC automatyzacji Azure mogą być używane toomanage różnych komputerów:

* Maszynami wirtualnymi platformy Azure (klasycznymi) z systemem Windows lub Linux
* Maszynami wirtualnymi platformy Azure z systemem Windows lub Linux
* Maszynami wirtualnymi usługi Amazon Web Services (AWS) z systemem Windows lub Linux
* Fizycznymi/wirtualnymi lokalnymi komputerami z systemem Windows lub w chmurze innej niż platformy Azure lub usług AWS
* Fizycznymi/wirtualnymi lokalnymi komputerami z systemem Linux lub w chmurze innej niż platformy Azure lub usług AWS

Najnowsza wersja platformy WMF 5 Hello musi być zainstalowany hello agenta DSC środowiska PowerShell dla Windows toobe stanie toocommunicate w automatyzacji Azure. najnowszą wersję hello Hello [agenta DSC środowiska PowerShell dla systemu Linux](https://www.microsoft.com/en-us/download/details.aspx?id=49150) musi być zainstalowana toocommunicate stanie toobe systemu Linux przy użyciu automatyzacji Azure.

### <a name="hybrid-runbook-worker"></a>Hybrydowy proces roboczy elementu Runbook  
Podczas wyznaczania zadania elementu runbook hybrydowego toorun komputera, ten komputer musi mieć następujące hello:

* Windows Server 2012 lub nowszy
* Windows PowerShell 4.0 lub nowszy.  Zalecane jest zainstalowanie programu Windows PowerShell 5.0 na komputerze hello w celu zwiększenia niezawodności. Witaj nowej wersji można pobrać z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=50395)
* Co najmniej dwa rdzenie
* Co najmniej 4 GB pamięci RAM

### <a name="permissions-required-toocreate-automation-account"></a>Konto automatyzacji toocreate wymagane uprawnienia
toocreate lub aktualizacji konto usługi Automatyzacja, musi mieć powitania po określone uprawnienia i toocomplete wymagane uprawnienia, w tym temacie.   
 
* W kolejności toocreate konto usługi Automatyzacja, Twoje konto użytkownika AD musi toobe tooa dodano rolę z rolę właściciela toohello równoważne uprawnienia Microsoft.Automation zasobów zgodnie z opisem w artykule [kontroli dostępu opartej na rolach w usłudze Automatyzacja Azure ](automation-role-based-access-control.md).  
* Jeśli ustawienie rejestracji aplikacji hello ustawiono zbyt**tak**, użytkownicy inni niż administratorzy w Twojej dzierżawie usługi Azure AD można [rejestrowania aplikacji AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Jeśli ustawienie rejestracji aplikacji hello ustawiono zbyt**nr**, wykonanie tej czynności użytkownika hello musi być administratorem globalnym w usłudze Azure AD. 

Jeśli nie jesteś członkiem wystąpienia usługi Active Directory hello subskrypcji przed dodaniem toohello globalnego administratora/drugi-administrator roli hello subskrypcji, zostaną dodane tooActive katalogu jako Gość. W takiej sytuacji pojawi się "nie ma uprawnień toocreate..." Ostrzeżenie dotyczące hello **Dodaj konto automatyzacji** bloku. Użytkownicy, którzy zostały dodane toohello globalnego administratora/drugi-administrator roli najpierw można usunąć z wystąpienia usługi Active Directory hello subskrypcji i ponownie dodany toomake ich pełną użytkownika w usłudze Active Directory. tooverify takiej sytuacji z hello **usługi Azure Active Directory** okienka w hello portalu Azure, wybierz opcję **użytkowników i grup**, wybierz pozycję **wszyscy użytkownicy** i po wybraniu hello określony użytkownik, wybierz opcję **profilu**. Witaj wartość hello **typ użytkownika** atrybutu na liście profilów użytkowników hello nie powinna być równa **gościa**.

## <a name="authentication-planning"></a>Planowanie uwierzytelniania
Automatyzacja Azure umożliwia tooautomate zadania w odniesieniu do zasobów na platformie Azure i lokalnego i z innych dostawców chmury.  Aby runbook tooperform żądane działania, musi mieć uprawnienia toosecurely dostępu hello zasobów z hello minimalnym poziomem uprawnień wymaganych w ramach subskrypcji hello.  

### <a name="what-is-an-automation-account"></a>Co to jest konto usługi Automation 
Wszystkie zadania automatyzacji hello wykonywać względem zasobów przy użyciu poleceń cmdlet systemu Azure hello automatyzacji Azure uwierzytelniania tooAzure przy użyciu uwierzytelniania opartego na poświadczeń organizacyjnych tożsamości usługi Azure Active Directory.  Konto automatyzacji jest oddzielony od konta hello toosign w portalu tooconfigure toohello i korzystać z zasobów platformy Azure.  Uwzględnione przy użyciu konta zasoby automatyzacji są następujące hello:

* **Certyfikaty** — zawiera certyfikat używany do uwierzytelniania z poziomu elementu runbook lub konfiguracji DSC lub ich dodawania.
* **Połączenia** — zawiera uwierzytelniania i konfiguracji wymaganych informacji tooconnect tooan zewnętrznej usługi lub aplikacji z elementu runbook lub konfiguracji DSC.
* **Poświadczenia** — jest obiekt PSCredential zawierający poświadczenia zabezpieczeń, takie jak nazwa użytkownika i hasło wymagane tooauthenticate z elementu runbook lub konfiguracji DSC.
* **Moduły integracji** — moduły programu PowerShell dołączony z użyciem toomake konto usługi Automatyzacja Azure poleceń cmdlet w elementy runbook i konfiguracji DSC.
* **Harmonogramy** — zawiera harmonogramy, które uruchamiają lub zatrzymują element runbook o określonej godzinie (w tym z częstotliwością cykliczną).
* **Zmienne** — zawiera wartości dostępne z poziomu elementu runbook lub konfiguracji DSC.
* **Konfiguracji DSC** -są skrypty programu PowerShell, które opisano w sposób tooconfigure funkcją systemu operacyjnego lub ustawień lub instalowanie aplikacji na komputerze z systemem Windows lub Linux.  
* **Elementy Runbook** — to zestaw zadań opartych na programie PowerShell wykonujących niektóre zautomatyzowane procesy w usłudze Azure Automation.    

Hello automatyzacji zasobów dla każdego konta automatyzacji skojarzonych z pojedynczym regionie Azure, ale kont automatyzacji mogą zarządzać wszystkie zasoby hello w ramach subskrypcji. Tworzenie kont automatyzacji w różnych regionach, jeśli masz zasady, które wymagają danych i zasobów toobe tooa izolowanego określonego regionu.

> [!NOTE]
> Konta automatyzacji i zasoby hello zawierają, które są tworzone w portalu Azure hello, nie można uzyskać dostępu do hello klasycznego portalu Azure. Jeśli chcesz toomanage te konta lub ich zasobów przy użyciu programu Windows PowerShell, należy użyć hello modułów usługi Azure Resource Manager.
> 

Po utworzeniu konta automatyzacji w portalu Azure hello automatycznie utworzyć dwie jednostki uwierzytelniania:

* Konto Uruchom jako. To konto służy do tworzenia nazwy głównej usługi w usłudze Azure Active Directory (Azure AD) oraz certyfikatu. Przypisuje hello współautora opartej na rolach kontroli dostępu (RBAC), która zarządza zasoby usługi Resource Manager za pomocą elementów runbook.
* Klasyczne konto Uruchom jako. To konto będzie przekazywać certyfikat zarządzania, który jest używany toomanage zasoby klasyczne za pomocą elementów runbook.

Kontrola dostępu oparta na rolach jest dostępna z usługi Azure Resource Manager toogrant dozwolone konto użytkownika usługi Azure AD tooan akcje i konta Uruchom jako, a uwierzytelniania tej nazwy głównej usługi.  Odczyt [kontroli dostępu opartej na rolach w artykule usługi Automatyzacja Azure](automation-role-based-access-control.md) dalsze informacje toohelp opracować modelu do zarządzania uprawnieniami automatyzacji.  

#### <a name="authentication-methods"></a>Metody uwierzytelniania
Witaj Poniższa tabela zawiera podsumowanie hello różnych metod uwierzytelniania dla każdego środowiska obsługiwane przez usługi Automatyzacja Azure.

| Metoda | Środowisko 
| --- | --- | 
| Konto Uruchom jako platformy Azure i klasyczne konto Uruchom jako |Wdrożenie usługi Azure Resource Manager i klasycznej platformy Azure |  
| Konto użytkownika usługi Azure AD |Wdrożenie usługi Azure Resource Manager i klasycznej platformy Azure |  
| Uwierzytelnianie systemu Windows |Lokalnym centrum danych lub innych dostawcy chmury przy użyciu hello hybrydowy proces roboczy elementu Runbook |  
| Poświadczenia AWS |Amazon Web Services |  

W obszarze hello **jak to\Authentication i zabezpieczeń** sekcji, są obsługiwane artykuły etapy Przegląd i implementacja tooconfigure uwierzytelniania w przypadku tych środowisk z istniejącym lub nowe konto ma przeznaczona dla tego środowiska.  Hello Uruchom jako platformy Azure i klasycznego Uruchom jako konta hello tematu [aktualizacji automatyzacji Uruchom jako konta](automation-create-runas-account.md) w tym artykule opisano, jak tooupdate istniejącego konta automatyzacji o hello Uruchom jako konta z hello portalu lub przy użyciu programu PowerShell, jeśli nie było wcześniej skonfigurowana przy użyciu konta Uruchom jako lub klasycznego Uruchom jako. Jeśli chcesz toocreate Uruchom jako i konto klasycznego Uruchom jako z certyfikat wystawiony przez urząd certyfikacji (CA) przedsiębiorstwa, przejrzyj toolearn tego artykułu, jak toocreate hello kont przy użyciu narzędzia tej konfiguracji.     
 
## <a name="network-planning"></a>Planowanie sieci
Dla hello rejestru tooand tooconnect hybrydowy proces roboczy elementu Runbook z Microsoft Operations Management Suite (OMS) musi mieć numer portu toohello dostępu i adresy URL hello opisane poniżej.  Ponadto jest toohello [porty i adresy URL wymagane dla programu Microsoft Monitoring Agent hello](../log-analytics/log-analytics-windows-agents.md#network) tooconnect tooOMS. Jeśli używasz serwera proxy do komunikacji między agentem hello i hello usługę, należy tooensure czy hello odpowiednie zasoby są dostępne. Jeśli używasz zapory toohello dostępu toorestrict Internet, należy tooconfigure dostęp toopermit zapory.

Witaj informacje poniżej listy hello portów i adresów URL, które są wymagane dla hello toocommunicate hybrydowy proces roboczy elementu Runbook automatyzacji.

* Port: Dla wychodzącego dostępu do Internetu wymagany jest tylko port 443 protokołu TCP
* Globalny adres URL: *.azure-automation.net

Jeśli masz konto usługi Automatyzacja zdefiniowane dla konkretnego regionu i chcesz toorestrict komunikacji z tym centrum danych regionalnych, hello Poniższa tabela zawiera hello rekordu DNS dla każdego regionu.

| **Region** | **Rekord DNS** |
| --- | --- |
| Środkowo-południowe stany USA |scus-jobruntimedata-prod-su1.azure-automation.net |
| Wschodnie stany USA 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Środkowo-zachodnie stany USA | wcus-jobruntimedata-prod-su1.azure-automation.net |
| Europa Zachodnia |we-jobruntimedata-prod-su1.azure-automation.net |
| Europa Północna |ne-jobruntimedata-prod-su1.azure-automation.net |
| Kanada Środkowa |cc-jobruntimedata-prod-su1.azure-automation.net |
| Azja Południowo-Wschodnia |sea-jobruntimedata-prod-su1.azure-automation.net |
| Indie Środkowe |cid-jobruntimedata-prod-su1.azure-automation.net |
| Japonia Wschodnia |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Australia Południowo-Wschodnia |ase-jobruntimedata-prod-su1.azure-automation.net |
| Południowe Zjednoczone Królestwo | uks-jobruntimedata-prod-su1.azure-automation.net |
| Administracja USA — Wirginia | usge-jobruntimedata-prod-su1.azure-automation.us |

Lista adresów IP zamiast nazwy, pobieranie i przejrzyj hello [adres IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653) pliku xml z hello Microsoft Download Center. 

> [!NOTE]
> Ten plik zawiera hello zakresów adresów IP (w tym zakresy obliczeniowych, SQL i magazyn) używanych w hello centrach danych firmy Microsoft Azure. Zaktualizowany plik jest wysyłany co tydzień co odzwierciedla hello obecnie wdrożona zakresy i wszystkie zakresy IP toohello nadchodzących zmianach. Nowe zakresy znajdujących się w pliku hello nie umożliwi w centrach danych hello co najmniej jeden tydzień. Sprawdź xml nowe hello pobierania pliku co tydzień i wykonywanie hello niezbędne zmiany w witrynie toocorrectly identyfikowania usług działających na platformie Azure. Express Route użytkownicy mogą należy pamiętać, że ten plik używany tooupdate hello anonsu protokołu BGP platformy Azure miejsca w hello pierwszy tydzień co miesiąc. 
> 

## <a name="creating-an-automation-account"></a>Tworzenie konta usługi Automation

Istnieją różne sposoby, możesz utworzyć konto usługi Automatyzacja w hello portalu Azure.  Hello w poniższej tabeli przedstawiono każdy typ środowisko wdrażania i różnice między nimi.  

|Metoda | Opis |
|-------|-------------|
| Wybierz automatyzacji i kontrolek z hello Marketplace | Oferty, która tworzy zarówno konto automatyzacji, jak i z obszarem roboczym pakietu OMS połączone tooone hello inną w tej samej grupie zasobów i region.  Integracja z usługą OMS również obejmuje hello korzyścią z używania toomonitor analizy dzienników i analizować strumienie stanu i zadania zadania elementu runbook wraz z upływem czasu i korzystać z zaawansowanych funkcji tooescalate lub badania problemów. Witaj oferty również wdraża rozwiązania hello śledzenia zmian i zarządzania aktualizacjami, które są domyślnie włączone. |
| Wybierz automatyzacji z hello Marketplace | Tworzy konto usługi Automatyzacja w grupie nowy lub istniejący zasób, który nie jest połączony tooan obszarem roboczym pakietu OMS i nie ma żadnych dostępnych rozwiązań z oferty usługi Automatyzacja i kontrola hello. To jest podstawową konfigurację wprowadzającej tooAutomation i mogą pomóc w Dowiedz się, jak możliwości usługi hello hello toowrite elementów runbook, konfiguracji DSC i użycia. |
| Wybrane rozwiązania do zarządzania | W przypadku wybrania rozwiązanie —  **[zarządzania aktualizacjami](../operations-management-suite/oms-solution-update-management.md)**,  **[uruchamiania/zatrzymywania maszyn wirtualnych podczas poza godzinami pracy](automation-solution-vm-management.md)**, lub  **[ Śledzenie zmian](../log-analytics/log-analytics-change-tracking.md)**  monit tooselect istniejącej automatyzacji i obszarem roboczym pakietu OMS lub oferują hello toocreate opcji jako wymagane dla toobe rozwiązania hello wdrożone w ramach subskrypcji. |

Ten temat przeprowadzi Cię przez proces tworzenia konta automatyzacji i obszarem roboczym pakietu OMS przez oferty usługi Automatyzacja i kontrola hello dołączania.  toocreate autonomiczny konto automatyzacji dla usługi hello testowania lub toopreview, przejrzyj hello poniższego artykułu [tworzenia konta automatyzacji autonomiczny](automation-create-standalone-account.md).  

### <a name="create-automation-account-integrated-with-oms"></a>Tworzenie konta usługi Automation zintegrowanego z pakietem OMS
Hello zalecana metoda tooonboard, automatyzacji to, wybierając oferty usługi Automatyzacja i kontrola hello z hello Marketplace.  Tworzy konto usługi Automatyzacja i ustanawia hello integracji z obszarem roboczym pakietu OMS tym hello opcja tooinstall hello rozwiązań do zarządzania, które są dostępne z ofertą hello.  

1. Zaloguj się toohello portalu Azure przy użyciu konta, które jest członkiem roli Administratorzy subskrypcji hello i współadministratorem subskrypcji hello.

2. Kliknij przycisk **Nowy**.<br><br> ![Wybieranie opcji Nowy w witrynie Azure Portal](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. Wyszukaj **automatyzacji** , a następnie w hello w wynikach wyszukiwania wybierz **Automatyzacja i kontrola***.<br><br> ![Na platformie Marketplace wyszukaj i wybierz pozycję Automatyzacja i kontrola](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. Po przeczytaniu opisu hello hello oferty, kliknij przycisk **Utwórz**.  

5. Na powitania **Automatyzacja i kontrola** bloku ustawienia, wybierz opcję **obszarem roboczym pakietu OMS**.  Na powitania **obszarów roboczych OMS** bloku, wybierz toohello połączone obszar roboczy OMS znajduje się w tej samej subskrypcji Azure, która hello konta automatyzacji lub Utwórz obszar roboczy OMS.  Jeśli nie masz obszar roboczy OMS, wybierz **Utwórz nowy obszar roboczy** i na powitania **obszarem roboczym pakietu OMS** blok, wykonaj następujące hello: 
   - Określ nazwę nowej hello **obszarem roboczym pakietu OMS**.
   - Wybierz **subskrypcji** toolink tooby wybierając z listy rozwijanej hello Jeśli hello domyślne nie jest odpowiedni.
   - W pozycji **Grupa zasobów** możesz utworzyć grupę zasobów lub wybrać istniejącą grupę zasobów.  
   - Wybierz **lokalizację**.  Obecnie hello jedynymi lokalizacjami, dostępne są **południowo-wschodnia Australia**, **wschodnie stany USA**, **Azja południowo-wschodnia**, **zachodnie centralnej nam**i  **Europa Zachodnia**.
   - Wybierz **warstwę cenową**.  rozwiązanie Hello jest oferowany dwóch warstw: Zwolnij i warstwy na węzeł (OMS).  Witaj warstwa bezpłatna ma ograniczenie na powitania ilość danych zbieranych dziennie, okres przechowywania i minut czasu wykonywania zadania elementu runbook.  Hello warstwy na węzeł (OMS) nie ma limitu na powitania ilość danych zbieranych dziennie.  
   - Wybierz pozycję **Konto usługi Automation**.  Jeśli tworzysz nowy obszar roboczy OMS są wymagane tooalso Utwórz konto automatyzacji, który jest skojarzony z hello nowy obszar roboczy OMS określony wcześniej, łącznie z Twojej subskrypcji platformy Azure, grupy zasobów i region.  Możesz wybrać **utworzyć konto usługi automatyzacja** i na powitania **konto automatyzacji** bloku, podaj poniżej hello: 
  - W hello **nazwa** wprowadź nazwę hello hello konta automatyzacji.

    Wszystkie inne opcje są wypełniane automatycznie na podstawie na wybrany obszar roboczy OMS hello i nie można zmodyfikować te opcje.  Konto Uruchom jako platformy Azure jest domyślną metodą uwierzytelniania dla oferty hello hello.  Po kliknięciu **OK**, opcje konfiguracji hello są weryfikowane i utworzeniu hello konta automatyzacji.  Można śledzić postęp w obszarze **powiadomienia** hello menu. 

    W przeciwnym razie wybierz istniejące konto Uruchom jako usługi Automation.  Konto Hello, którą wybierzesz już nie może być połączone tooanother obszarem roboczym pakietu OMS, w przeciwnym razie komunikatu powiadomienia są prezentowane w bloku hello.  Jeśli jest już połączony, należy tooselect innego konta Uruchom jako automatyzacji lub utworzyć.

    Po zakończeniu hello informacje wymagane, kliknij przycisk **Utwórz**.  informacje o Hello jest weryfikowany i hello konta automatyzacji i Uruchom jako konta są tworzone.  Zwracane są toohello **obszarem roboczym pakietu OMS** bloku automatycznie.  

6. Po podaniu informacji hello wymagane na powitania **obszarem roboczym pakietu OMS** bloku, kliknij przycisk **Utwórz**.  Informacje hello jest weryfikowany i utworzeniu hello obszaru roboczego, można śledzić postęp w obszarze **powiadomienia** hello menu.  Zwracane są toohello **Dodaj rozwiązanie** bloku.  

7. Na powitania **Automatyzacja i kontrola** bloku ustawienia potwierdzenie tooinstall hello zalecane rozwiązania wstępnie wybrane. Jeśli usuniesz wybór któregokolwiek z nich, możesz zainstalować je oddzielnie później.  

8. Kliknij przycisk **Utwórz** tooproceed z obszarem roboczym pakietu OMS i dołączaniu automatyzacji. Wszystkie ustawienia są prawidłowe, a następnie go próbuje hello toodeploy oferty w ramach subskrypcji.  Ten proces może potrwać kilka sekund toocomplete i można śledzić postęp w obszarze **powiadomienia** hello menu. 

Oferty powitania po został załadowany, możesz rozpocząć tworzenie elementów runbook, Praca z hello rozwiązania do zarządzania są włączone, wdrażanie [procesu roboczego elementu Runbook hybrydowego](automation-hybrid-runbook-worker.md) roli lub rozpocząć pracę z [analizy dzienników](https://docs.microsoft.com/azure/log-analytics) dane toocollect wygenerowane przez zasobów w chmurze lub lokalnym środowisku.   

## <a name="next-steps"></a>Następne kroki
* Możesz potwierdzić, że Twoje nowe konto usługi Automation może uwierzytelniać względem zasobów platformy Azure, sprawdzając [test uwierzytelniania konta Uruchom jako usługi Azure Automation](automation-verify-runas-authentication.md).
* wprowadzenie do tworzenia elementów runbook tooget, najpierw należy przejrzeć hello [typy elementu runbook automatyzacji](automation-runbook-types.md) obsługiwane i powiązane zagadnienia, przed rozpoczęciem tworzenia.


