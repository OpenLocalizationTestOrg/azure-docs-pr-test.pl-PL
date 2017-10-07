---
title: "dostępność aaaHigh z brama zarządzania danymi w fabryce danych Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak można skalować w poziomie bramy zarządzania danymi, dodając więcej węzłów i skalowania w górę zwiększając liczbę współbieżnych zadań, które można uruchomić w węźle."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: abnarain
ms.openlocfilehash: 925f63728e23596bca2655636f6535b509fce0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway---high-availability-and-scalability-preview"></a>Brama zarządzania danymi - wysokiej dostępności i skalowalności (wersja zapoznawcza)
Ten artykuł ułatwia konfigurowanie wysokiej dostępności i skalowalności rozwiązania przy użyciu bramy zarządzania danymi.    

> [!NOTE]
> W tym artykule przyjęto założenie, że znasz już podstawy brama zarządzania danymi. Jeśli nie masz, zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md).

>**Ta funkcja podglądu oficjalnie jest obsługiwana na 2.12.xxxx.x wersja bramy zarządzania danymi i nowszym**. Upewnij się, że używasz wersji 2.12.xxxx.x lub nowszej. Pobierz najnowszą wersję bramy zarządzania danymi hello [tutaj](https://www.microsoft.com/download/details.aspx?id=39717).

## <a name="overview"></a>Omówienie
Można skojarzyć dane zarządzania bram, które są zainstalowane na wielu komputerach lokalnych z pojedynczą bramą logicznych z portalu hello. Te komputery są nazywane **węzłów**. Może zawierać maksymalnie zbyt**czterech węzłów** skojarzone z bramą logiczne. Zalety Hello mające wiele węzłów (lokalnymi maszynami z bramą zainstalowany) dla bramy logiczne to:  

- Poprawianie wydajności przenoszenia danych między lokalnymi i w chmurze magazynów danych.  
- Jeśli jeden z węzłów hello ulegnie awarii jakiegoś powodu inne węzły są nadal dostępne do przenoszenia danych hello. 
- Jeśli potrzebujesz jednego z węzłów hello toobe przełączony w tryb offline w celu przeprowadzenia konserwacji, pozostałe węzły są nadal dostępne do przenoszenia danych hello.

Można również skonfigurować liczbę hello **zadania przepływu danych równoczesnych** który można uruchomić na tooscale węzeł w górę hello możliwość przenoszenia danych między lokalnymi i w chmurze magazynów danych. 

Używając hello portalu Azure, można monitorować stan hello tych węzłów, które ułatwiają określenie, czy tooadd lub usunąć węzeł z hello logicznej bramy. 

## <a name="architecture"></a>Architektura 
Witaj następujący diagram zawiera omówienie architektury hello skalowalności i dostępności funkcji hello brama zarządzania danymi: 

![Brama zarządzania danymi - wysokiej dostępności i skalowalności](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-high-availability-and-scalability.png)

A **logicznej bramy** jest bramą hello Dodaj tooa fabryki danych w hello portalu Azure. Wcześniej można skojarzyć tylko jedną na lokalnej maszynie systemu Windows z zainstalowana brama logicznej bramy zarządzania danymi. To lokalna maszyna bramy jest nazywany węzłem. Teraz można skojarzyć się zbyt**czterech węzłów fizycznych** logicznej bramy. Nosi nazwę logiczną bramy z wielu węzłów **bramy wielowęzłowego**.  

Te węzły są **active**. Wszystkie one może przetwarzać danych toomove zadania przepływu danych między lokalnymi i w chmurze magazynów danych. Jednym z węzłów hello pełnić zarówno dyspozytora i proces roboczy. Inne węzły należące do grup hello są węzłami procesów roboczych. A **dyspozytora** węzeł ściąga przepływ zadań/zadania danych z usługi w chmurze hello i wysyła je węzłów tooworker (w tym sam). A **procesu roboczego** węzeł wykonuje danych toomove zadania przepływu danych między lokalnymi i w chmurze magazynów danych. Wszystkie węzły są pracowników. Tylko jeden węzeł może być zarówno wysyłania i proces roboczy.    

Zazwyczaj można rozpocząć z jednym węzłem i **skalowanie** tooadd więcej węzłów hello istniejących węzłów jest przeciążony z ładowania przepływu danych hello. Możesz również **skalowanie w górę** hello możliwość przenoszenia danych węzła bramy, zwiększając hello liczbę współbieżnych zadań, które mogą toorun w węźle hello. Ta funkcja jest również dostępna przy użyciu bramy jednowęzłowej (nawet jeśli nie włączono funkcji hello skalowalność i dostępność). 

Brama z wielu węzłów przechowuje poświadczeń magazynu danych hello zsynchronizowane we wszystkich węzłach. Jeśli występuje problem łączności między węzłami, hello poświadczenia mogą być zsynchronizowane. Podczas ustawiania poświadczeń na lokalnym magazynem danych, który używa bramy zapisuje poświadczeń na powitania dyspozytora/węzła procesu roboczego. Dyspozytor Hello węzła synchronizacje z innych węzłów procesu roboczego. Ten proces jest nazywany **Poświadczenia synchronizacji**. hello kanał komunikacyjny między węzłami może być **zaszyfrowanych** za pomocą publicznego certyfikatu SSL/TLS. 

## <a name="set-up-a-multi-node-gateway"></a>Skonfiguruj bramę wieloma węzłami.
W tej sekcji założono, mieć przeszli hello następujące dwa artykuły lub masz pojęcia w tych artykułach: 

- [Brama zarządzania danymi](data-factory-data-management-gateway.md) — zawiera szczegółowe omówienie hello bramy.
- [Przenoszenie danych między lokalnymi i w chmurze magazyny danych](data-factory-move-data-between-onprem-and-cloud.md) — zawiera przewodnik krok po kroku instrukcje korzystania z jednego węzła przy użyciu bramy.  

> [!NOTE]
> Przed zainstalowaniem bramy zarządzania danymi na lokalnym komputerze z systemem Windows, zobacz wymagania wstępne wymienione w [hello główny artykuł](data-factory-data-management-gateway.md#prerequisites).

1. W hello [wskazówki](data-factory-move-data-between-onprem-and-cloud.md#create-gateway), podczas tworzenia logicznej bramy, Włącz hello **zapewniające wysoką dostępność i skalowalność** funkcji. 

    ![Brama zarządzania danymi - enable wysokiej dostępności i skalowalności](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-enable-high-availability-scalability.png)
2. W hello **Konfiguruj** albo użyj **Express Instalator** lub **Podręcznika instalacji** link tooinstall bramę na powitania pierwszego węzła (komputer Windows lokalnych).

    ![Brama zarządzania danymi - instalacji ekspresowej, czy ręcznie](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-express-manual-setup.png)

    > [!NOTE]
    > Jeśli używasz opcji instalacji ekspresowej hello komunikacji między węzłami hello odbywa się bez szyfrowania. Nazwa węzła Hello jest taka sama jak nazwa komputera hello. Użyj instalacji ręcznej, jeśli komunikacji węzeł węzeł hello musi toobe zaszyfrowany lub ma toospecify nazwa węzła wybranych przez użytkownika. Nie można później edytować nazwy węzła.
3. Jeśli wybierzesz **instalacji ekspresowej**
    1. Zostanie wyświetlony hello następującą wiadomości, po pomyślnym zainstalowaniu bramy hello:

        ![Brama zarządzania danymi — powodzenie instalacji ekspresowej](media/data-factory-data-management-gateway-high-availability-scalability/express-setup-success.png)
    2. Uruchom Menedżera konfiguracji zarządzania danymi dla bramy hello wykonując [tych instrukcji](data-factory-data-management-gateway.md#configuration-manager). Zostanie wyświetlony hello nazwa bramy, nazwa węzła, stan, itp.

        ![Brama zarządzania danymi - Instalacja powiodła się](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)
4. Jeśli wybierzesz **instalacji ręcznej**:
    1. Aby pobrać pakiet instalacyjny hello z witryny Microsoft Download Center hello, uruchom go tooinstall bramy na tym komputerze.
    2. Użyj hello **klucz uwierzytelniania** z hello **Konfiguruj** strony tooregister hello bramy.
    
        ![Brama zarządzania danymi - Instalacja powiodła się](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-authentication-key.png)
    3. W hello **nowy węzeł bramy** strony, musisz podać niestandardowy **nazwa** toohello węzeł bramy. Domyślnie nazwa węzła jest taka sama jak nazwa komputera hello.    

        ![Brama zarządzania danymi — Określ nazwę](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-name.png)
    4. W następnej strony hello, można wybrać, czy za**włączenie szyfrowania komunikacji między węzłami**. Kliknij przycisk **Pomiń** toodisable szyfrowania (ustawienie domyślne).

        ![Brama zarządzania danymi - Włącz szyfrowanie](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-node-encryption.png)  
    
        > [!NOTE]
        > Zmianę trybu szyfrowania jest obsługiwana tylko, gdy węzeł pojedyncza brama hello logicznej bramy. Program toochange hello szyfrowania tryb bramy ma wiele węzłów hello następujące kroki: Usuń wszystkie węzły hello, z wyjątkiem jednego węzła, Zmień tryb szyfrowania hello, a następnie dodaj węzły hello ponownie.
        > 
        > Zobacz [wymagania dotyczące certyfikatów protokołu TLS/SSL](#tlsssl-certificate-requirements) sekcja zawiera listę wymagań dotyczących korzystania z certyfikatu TLS/SSL. 
    5. Po pomyślnym zainstalowaniu hello bramy, kliknij przycisk Uruchom Menedżera konfiguracji:
    
        ![Instalacji ręcznej — Uruchom Menedżera konfiguracji](media/data-factory-data-management-gateway-high-availability-scalability/manual-setup-launch-configuration-manager.png)   
    6. Menedżer konfiguracji bramy zarządzania danymi zostanie wyświetlony w węźle hello (na lokalnej maszynie z systemem Windows), który wyświetla stan łączności, **nazwa bramy**, i **nazwa węzła**.  

        ![Brama zarządzania danymi - Instalacja powiodła się](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)

        > [!NOTE]
        > W przypadku udostępniania hello bramy na maszynie Wirtualnej platformy Azure, można użyć [tego szablonu usługi Azure Resource Manager w witrynie GitHub](https://github.com/xiaoyingLJ/vms-with-multiple-data-management-gateway). Ten skrypt tworzy logicznej bramy, ustawia maszyn wirtualnych z zainstalowanym oprogramowaniem brama zarządzania danymi i rejestruje hello logicznej bramy. 
6. W portalu Azure, uruchom program hello **bramy** strony: 
    1. Polecenie hello danych fabryki strony głównej w portalu hello, **połączonych usług**.
    
        ![Strona główna fabryki danych](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-home-page.png)
    2. Wybierz hello **bramy** toosee hello **bramy** strony:
    
        ![Strona główna fabryki danych](media/data-factory-data-management-gateway-high-availability-scalability/linked-services-gateway.png)
    4. Zobacz hello **bramy** strony:   

        ![Brama z jednego węzła widoku](media/data-factory-data-management-gateway-high-availability-scalability/gateway-first-node-portal-view.png) 
7. Kliknij przycisk **Dodaj węzeł** na tooadd narzędzi hello bramy logicznej toohello węzła. Jeśli planujesz toouse instalacji ekspresowej, należy wykonać ten krok z hello na lokalnym komputerze, na który zostanie dodany jako węzeł bramy toohello. 

    ![Brama zarządzania danymi — Dodaj menu węzła](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)
8. Kroki są podobne toosetting się hello pierwszy węzeł. Witaj interfejsu użytkownika programu Configuration Manager umożliwia określenie nazwy węzła hello, po wybraniu opcji instalacji ręcznej hello: 

    ![Configuration Manager — instalacji drugiego bramy](media/data-factory-data-management-gateway-high-availability-scalability/install-second-gateway.png)
9. Po bramy hello jest pomyślnie zainstalowane w węźle hello, narzędzie Menedżer konfiguracji hello wyświetla po ekranie powitania:  

    ![Configuration Manager — instalacja bramy drugi powiodło się](media/data-factory-data-management-gateway-high-availability-scalability/second-gateway-installation-successful.png)
10. Po otwarciu hello **bramy** strony w portalu hello można zobaczyć dwa węzły bramy teraz: 

    ![Brama z dwoma węzłami w portalu hello](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)
11. toodelete węzła bramy, kliknij przycisk **usunąć węzeł** na powitania narzędzi, wybierz węzeł hello toodelete, a następnie kliknij przycisk **usunąć** z hello paska narzędzi. Ta akcja spowoduje usunięcie wybranego węzła hello z hello grupy. Należy pamiętać, że ta akcja nie powoduje odinstalowania oprogramowania bramy zarządzania danych hello z węzła hello (komputera lokalnego systemu Windows). Użyj **apletu Dodaj lub usuń programy** w Panelu sterowania na powitania lokalnymi toouninstall hello bramy. Po odinstalowaniu bramy z węzła hello są automatycznie usuwane w portalu hello.   

## <a name="upgrade-an-existing-gateway"></a>Uaktualnij istniejącą bramę
Można uaktualnić istniejącą bramę toouse hello wysokiej dostępności i skalowalności funkcji. Ta funkcja działa tylko w przypadku węzłów posiadających brama zarządzania danymi hello wersji > = 2.12.xxxx. Można znaleźć wersji hello brama zarządzania danymi zainstalowany na komputerze w hello **pomocy** kartę hello Menedżera konfiguracji bramy zarządzania danymi. 

1. Aktualizacja bramy hello hello lokalnej maszyny toohello najnowszej wersji, postępując przez pobieranie i uruchamianie pakiet Instalatora MSI hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717). Zobacz [instalacji](data-factory-data-management-gateway.md#installation) sekcji, aby uzyskać szczegółowe informacje.  
2. Przejdź toohello portalu Azure. Uruchamianie hello **strony fabryki danych** Twojego fabryki danych. Kliknij przycisk połączonej usługi kafelka toolaunch hello **strony połączonych usług**. Wybierz hello bramy toolaunch hello **strony bramy**. Kliknij i włączyć **funkcja w wersji zapoznawczej** pokazane na powitania po obrazu: 

    ![Brama zarządzania danymi - enable funkcja w wersji zapoznawczej](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-existing-gateway-enable-high-availability.png)   
2. Po włączeniu funkcji Podgląd hello w portalu hello Zamknij wszystkie strony. Otwórz ponownie hello **strony bramy** toosee hello nowy interfejs użytkownika w wersji zapoznawczej (UI).
 
    ![Brama zarządzania danymi - Włącz podgląd funkcji Powodzenie](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview-success.png)

    ![Brama zarządzania danymi - preview interfejsu użytkownika](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview.png)

    > [!NOTE]
    > Podczas uaktualniania hello nazwę pierwszego węzła hello jest nazwą hello hello maszyny. 
3. Teraz Dodaj węzeł. W hello **bramy** kliknij przycisk **Dodaj węzeł**.  

    ![Brama zarządzania danymi — Dodaj menu węzła](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)

    Wykonaj instrukcje z hello poprzedniej sekcji tooset się hello węzła. 

### <a name="installation-best-practices"></a>Najlepsze rozwiązania dotyczące instalacji

- Skonfiguruj planu zasilania na komputerze-hoście hello hello bramy, dzięki czemu hello maszyny nie hibernacji. Hibernacja hello komputer hosta, hello bramy nie odpowiada toodata żądań.
- Utwórz kopię zapasową certyfikatu hello skojarzone z bramą hello.
- Upewnij się, że wszystkie węzły są podobne konfiguracji (zalecane) doskonale wydajności. 
- Dodaj co najmniej dwa węzły tooensure wysokiej dostępności.  

### <a name="tlsssl-certificate-requirements"></a>Wymagania dotyczące certyfikatów dla protokołu TLS/SSL
Poniżej przedstawiono wymagania hello hello certyfikatu TLS/SSL, który służy do zabezpieczania komunikacji między węzłami bramy:

- Witaj certyfikat musi być publicznie zaufany X509 certyfikatu w wersji 3.
- Wszystkie węzły bramy musi ufać temu certyfikatowi. 
- Firma Microsoft zaleca, aby używać certyfikatów wystawionych przez publiczny (niezależny) urząd certyfikacji (CA).
- Obsługuje wszystkie rozmiar klucza obsługiwana przez system Windows Server 2012 R2 dla certyfikatów SSL.
- Nie obsługuje certyfikatów, które używają kluczy CNG.
- Certyfikaty — symbol wieloznaczny są obsługiwane. 


## <a name="monitor-a-multi-node-gateway"></a>Monitor bramy wieloma węzłami.
### <a name="multi-node-gateway-monitoring"></a>Monitorowanie bramy z wieloma węzłami.
W portalu Azure hello można wyświetlić migawki czasie niemal rzeczywistym wykorzystania zasobów (procesora CPU, pamięci, network(in/out) itp.) w każdym węźle wraz ze Stanami węzłów bramy. 

![Brama zarządzania danymi - monitorowania wielu węzła](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)

Można włączyć **ustawienia zaawansowane** w hello **bramy** toosee zaawansowane metryk, takich jak strony **sieci**(We/Wy), **stan poświadczeń&roli**, co jest przydatne w debugowaniu problemów bramy i **równoczesnych zadań** (systemem / Limit) który można być zmodyfikowane / odpowiednio zmienione podczas dostrajania wydajności. Witaj Poniższa tabela zawiera opisy kolumn w hello **węzłów bramy** listy:  

Właściwość monitorowania | Opis
:------------------ | :---------- 
Nazwa | Nazwa logicznej bramy hello i skojarzone z bramą hello węzłów.  
Stan | Stan bramy logicznej hello i hello węzłów bramy. Przykład: Online/Offline/Limited/itp. Informacje o tych stanów znajdują się w temacie [stanu bramy](#gateway-status) sekcji. 
Wersja | Zawiera wersję hello hello logicznej bramy i każdy węzeł bramy. Wersja Hello hello logicznej bramy jest określana na podstawie wersji Większość węzłów w grupie hello. W przypadku węzłów z różnych wersji w konfiguracji bramy logicznej hello tylko hello węzły z hello tego samego numeru wersji funkcji logicznej bramy hello poprawnie. Inne są w trybie ograniczonym hello i wymagają toobe ręcznie zaktualizować (tylko w przypadku automatycznej aktualizacji nie powiedzie się). 
Dostępna pamięć | Dostępna pamięć na węzeł bramy. Ta wartość jest blisko migawka w czasie rzeczywistym. 
Użycie procesora CPU | Użycie procesora CPU przez węzeł bramy. Ta wartość jest blisko migawka w czasie rzeczywistym. 
Sieć (We/Wy) | Użycie sieci węzeł bramy. Ta wartość jest blisko migawka w czasie rzeczywistym. 
Równoczesnych zadań (systemem / Limit) | Liczba zadań lub zadania uruchomione w każdym węźle. Ta wartość jest blisko migawka w czasie rzeczywistym. Limit oznacza hello maksymalną współbieżnych zadań dla każdego węzła. Ta wartość jest określona na podstawie rozmiaru maszyny hello. Można zwiększyć hello limit tooscale się wykonywania zadań jednoczesnych w zaawansowanych scenariuszach, gdzie Procesora / pamięci / sieci jest używane w obszarze, ale limit czasu są działania. Ta funkcja jest również dostępna przy użyciu bramy jednowęzłowej (nawet jeśli nie włączono funkcji hello skalowalność i dostępność). Aby uzyskać więcej informacji, zobacz [skalować zagadnienia](#scale-considerations) sekcji. 
Rola | Istnieją dwa typy ról — dyspozytora i proces roboczy. Wszystkie węzły są pracowników, co oznacza, że wszystkie były używane tooexecute zadania. Istnieje tylko jeden węzeł dyspozytora, jest używane toopull zadania/zadań z usługi w chmurze i wysyłania ich węzłów procesu roboczego toodifferent (w tym sam). 

![Brama zarządzania danymi - zaawansowane monitorowanie wielu węzła](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-advanced.png)

### <a name="gateway-status"></a>Stan bramy

Witaj poniższej tabeli przedstawiono możliwe stany **węzeł bramy**: 

Stan  | Komentarz/scenariuszy
:------- | :------------------
Online | Węzeł połączenia usługi fabryki tooData.
W trybie offline | Węzeł jest w trybie offline.
Uaktualnianie | węzeł Hello są aktualizowane automatycznie.
Ograniczone | Ze względu na problem tooConnectivity. Może być spowodowane tooHTTP portu 8050 problem, problem dotyczący łączności magistrali usługi lub problemu z synchronizacją poświadczeń. 
Nieaktywne | Węzeł znajduje się w różnych konfiguracji hello innych węzłów większość konfiguracji.<br/><br/> Węzeł może być nieaktywne, gdy nie można połączyć z tooother węzłów. 


Witaj poniższej tabeli przedstawiono możliwe stany **logicznej bramy**. Stan bramy Hello zależy od stany hello węzłów bramy. 

Stan | Komentarze
:----- | :-------
Wymaga rejestracji | Żaden węzeł nie jest jeszcze zarejestrowany toothis logicznej bramy
Online | Węzły bramy są w trybie online
W trybie offline | Nie węzła w stan online.
Ograniczone | Nie wszystkie węzły w tej bramy są w dobrej kondycji. Ten stan jest ostrzeżenie, że niektóre węzeł może być wyłączony! <br/><br/>Może to być powodu problemu z synchronizacją toocredential w węźle dyspozytora/proces roboczy. 

### <a name="pipeline-activities-monitoring"></a>Potok / działania monitorowania
Hello Azure portal udostępnia potoku monitorowania środowisko z poziomu szczegółów szczegółowego węzła. Na przykład przedstawia działania uruchomionego na wybór węzła. Te informacje mogą być pomocne w opis problemy z wydajnością w określonym węźle, powiedz powodu ograniczania toonetwork. 

![Brama zarządzania danymi - monitorowania dla potoków wiele węzłów](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-pipelines.png)

![Brama zarządzania danymi — szczegóły potoku](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-pipeline-details.png)

## <a name="scale-considerations"></a>Zagadnienia dotyczące skali

### <a name="scale-out"></a>Skalowanie w poziomie
Gdy hello **jest za mało dostępnej pamięci** i hello **użycie procesora CPU jest wysokie**, dodanie nowego węzła pomaga skalowania obciążenia hello na komputerach. Jeśli działania kończą się niepowodzeniem powodu węzła tootime-out lub brama jest w trybie offline, pomaga po dodaniu bramy toohello węzła.
 
### <a name="scale-up"></a>Skalowanie w górę
Gdy hello dostępnej pamięci i Procesora nie są używane również, ale hello pojemność bezczynności wynosi 0, należy skalować w górę zwiększając hello liczbę współbieżnych zadań, które można uruchomić w węźle. Można również tooscale się podczas działania są limit czasu, ponieważ brama hello jest przeciążona. Jak pokazano na powitania po obrazu, może zwiększyć hello maksymalna pojemność węzła. Zalecamy podwojenie go toostart z.  

![Brama zarządzania danymi — zagadnienia dotyczące skali](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-scale-considerations.png)


## <a name="known-issuesbreaking-changes"></a>Znane problemy/najważniejszych zmian

- Obecnie użytkownik może zawierać maksymalnie węzły fizyczne bramy toofour pojedyncza brama logiczne. Jeśli potrzebujesz więcej niż czterech węzłów ze względu na wydajność, Wyślij wiadomość e-mail zbyt[DMGHelp@microsoft.com](mailto:DMGHelp@microsoft.com).
- Nie można ponownie zarejestrować węzeł bramy z kluczem uwierzytelniania hello z innej tooswitch logicznej bramy z bieżącej bramy logicznej hello. toore rejestru odinstalować bramę hello z węzła hello, ponowne zainstalowanie bramy hello i zarejestrowanie go za pomocą klucza uwierzytelniania hello hello innych logicznej bramy. 
- Jeśli serwer proxy HTTP jest wymagane dla wszystkich węzłów bramy, ustaw powitania serwera proxy w diahost.exe.config i diawp.exe.config i użyj powitania serwera Menedżera toomake się, że wszystkie węzły mają hello tych samych diahost.exe.config i diawip.exe.config. Zobacz [Skonfiguruj ustawienia serwera proxy](data-factory-data-management-gateway.md#configure-proxy-server-settings) sekcji, aby uzyskać szczegółowe informacje. 
- toochange tryb szyfrowania komunikacji między węzłami w Menedżerze konfiguracji bramy, Usuń wszystkie węzły hello w portalu hello z wyjątkiem jednego. Następnie należy dodać węzłów, po zmianie trybu szyfrowania hello.
- Po wybraniu kanał komunikacyjny między węzłami hello tooencrypt, należy użyć oficjalnego certyfikatu SSL. Certyfikat z podpisem własnym może spowodować problemy z łącznością jako powitalne tego samego certyfikatu może nie być uważany za zaufany liście urząd certyfikacji na innych komputerach. 
- Nie można zarejestrować brama brama logicznej tooa węzła, podczas hello węzła wersja jest starsza niż wersja bramy logicznej hello. Usuń wszystkie węzły hello logicznej bramy z portalu, tak aby niższe node(downgrade) wersji można zarejestrować go. Po usunięciu wszystkich węzłów bramy logicznej ręcznie zainstaluj i Zarejestruj nowe węzły toothat logicznej bramy. Instalacja ekspresowa nie jest obsługiwana w tym przypadku.
- Nie można użyć instalacji ekspresowej tooinstall węzłów tooan istniejącej logiczne bramy, które nadal korzysta z poświadczeń w chmurze. Możesz sprawdzić, gdzie przechowywane są poświadczenia hello z hello Menedżera konfiguracji bramy na karcie Ustawienia hello.
- Nie można użyć instalacji ekspresowej tooinstall węzłów tooan istniejącej logicznej bramy, który ma włączone szyfrowanie węzła do węzła. Jako ustawienie hello szyfrowania tryb obejmuje ręczne dodanie certyfikaty, instalacja ekspresowa jest nie więcej opcji. 
- Dla kopiowania plików ze środowiska lokalnego, nie należy używać \\nazwy localhost ani C:\files już od hosta lokalnego lub na dysku lokalnym może nie być dostępny za pośrednictwem wszystkich węzłów. Zamiast tego należy użyć \\lokalizacji plików toospecify ServerName\files.


## <a name="rolling-back-from-hello-preview"></a>Wycofywanie z hello podglądu 
tooroll z wersji zapoznawczej hello, Usuń wszystkie węzły oprócz jednego węzła. Nie ma znaczenia, których węzłów, usuwanie, ale upewnij się, że co najmniej jeden węzeł w hello logicznej bramy. Odinstalowanie bramy na maszynie hello lub przy użyciu hello portalu Azure, można usunąć węzła. W portalu Azure w hello hello **fabryki danych** kliknij przycisk połączonej usługi toolaunch hello **połączone usługi** strony. Wybierz hello bramy toolaunch hello **bramy** strony. Na stronie bramy hello widać węzłów hello skojarzone z bramą hello. Strona Hello umożliwia usunięcie węzła z hello bramy.
 
Po usunięciu, kliknij przycisk **funkcji w wersji zapoznawczej** w hello tej samej stronie portalu Azure, a następnie wyłącz hello funkcja w wersji zapoznawczej. Zresetowaniu bramy bramy tooone węzła GA (ogólnej dostępności).


## <a name="next-steps"></a>Następne kroki
Przejrzyj hello następujące artykuły:
- [Brama zarządzania danymi](data-factory-data-management-gateway.md) — zawiera szczegółowe omówienie hello bramy.
- [Przenoszenie danych między lokalnymi i w chmurze magazyny danych](data-factory-move-data-between-onprem-and-cloud.md) — zawiera przewodnik krok po kroku instrukcje korzystania z jednego węzła przy użyciu bramy. 
