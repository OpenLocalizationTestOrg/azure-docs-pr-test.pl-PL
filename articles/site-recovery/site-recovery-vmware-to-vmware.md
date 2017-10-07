---
title: "aaaReplicate maszyn wirtualnych VMware lub serwerów fizycznych tooanother lokacji (klasyczny portal Azure) | Dokumentacja firmy Microsoft"
description: "Ten artykuł tooreplicate maszyn wirtualnych VMware lub systemem Windows lub Linux serwerów fizycznych tooa lokacji dodatkowej za pomocą usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: jwhit
editor: 
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 5789ca07f0aa15cf194615fd33103dac930d7b7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-tooa-secondary-site-in-hello-classic-azure-portal"></a>Replikowanie lokalnych maszyn wirtualnych VMware lub serwerów fizycznych tooa lokacji dodatkowej w klasycznym portalu Azure hello

## <a name="overview"></a>Omówienie
InMage Scout w usłudze Azure Site Recovery zapewnia w czasie rzeczywistym replikacji między lokacjami lokalnymi VMware. InMage Scout znajduje się w ramach subskrypcji usługi Azure Site Recovery. 

## <a name="prerequisites"></a>Wymagania wstępne
**Konto platformy Azure**: należy [Microsoft Azure](https://azure.microsoft.com/) konta. Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/site-recovery/) o cenach usługi Site Recovery.

## <a name="step-1-create-a-vault"></a>Krok 1: Tworzenie magazynu
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk Nowy > zarządzania > kopii zapasowych i odzyskiwania lokacji (OMS). Alternatywnie możesz kliknąć przycisk Przeglądaj > magazynu usług odzyskiwania > Dodaj.
3. W **nazwa** Określ przyjazną nazwę tooidentify hello magazynu. Jeśli masz więcej niż jedną subskrypcję, wybierz jedną z nich.
4. W **grupy zasobów** Utwórz nową grupę zasobów lub wybierz istniejący. Określ region platformy Azure toocomplete wymagane pola.
5. W **lokalizacji**, wybierz hello region geograficzny magazynu hello. toocheck obsługiwane regiony, zobacz [cennik usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Jeśli chcesz tooquickly dostępu hello magazynu z hello pulpitu nawigacyjnego kliknij toodashboard numeru Pin, a następnie kliknij przycisk Utwórz.
7. Witaj nowy magazyn będzie wyświetlany na powitania pulpitu nawigacyjnego > wszystkie zasoby i magazyny bloku na powitania głównej usług odzyskiwania.

## <a name="step-2-configure-hello-vault-and-download-inmage-scout-components"></a>Krok 2: Konfigurowanie magazynu hello i pobrać składników InMage Scout
1. W bloku Magazyny usług odzyskiwania hello wybierz magazyn, a następnie kliknij przycisk Ustawienia.
2. W **ustawienia** > **wprowadzenie** kliknij **usługi Site Recovery** > krok 1: **przygotowanie infrastruktury**  >  **Cel ochrony**.
3. W **cel ochrony** wybierz toorecovery lokacji, a następnie wybierz opcję Tak, z programem VMware vSphere Hypervisor. Następnie kliknij przycisk OK.
4. W **Instalatora Scout**, kliknij przycisk pobierania toodownload GA InMage Scout 8.0.1 oprogramowania i klucz rejestracji. pliki instalacyjne Hello wszystkie hello wymaganych składników w pliku zip pobranego hello.

## <a name="step-3-install-component-updates"></a>Krok 3: Instalowanie aktualizacje składników
Przeczytaj informacje o hello najnowszych [aktualizacje](#updates). Zainstaluj hello pliki aktualizacji na serwerach w następującej kolejności hello:

1. Serwer ODBIERANIA, jeśli istnieje
2. Serwery konfiguracji
3. Serwery procesów
4. Głównych serwerów docelowych
5. serwery vContinuum
6. Serwer źródłowy (z systemem Windows i Linux Server)

Zainstaluj aktualizacje hello w następujący sposób:

1. Pobierz hello [aktualizacji](https://aka.ms/asr-scout-update5) pliku zip. Ten plik zip zawiera hello następujące pliki:

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.GZ
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe
   * UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe
   * Usługa bits update4 UA systemem RHEL5 OL5, OL6, SUSE 10, SUSE 11: UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Wyodrębnij pliki z rozszerzeniem .zip hello.<br>
3. **Dla serwera RX hello**: kopiowanie **RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** toohello RX serwera i wyodrębnij go. W hello wyodrębniony folder, uruchom **/Install**.<br>
4. **Witaj konfiguracji serwera/procesu serwera**: kopiowania **CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** toohello konfiguracji serwera i serwera przetwarzania. Kliknij dwukrotnie toorun go.<br>
5. **Dla serwera głównego celu Windows hello**: tooupdate hello unified agent kopiowania **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello główny serwer docelowy. Kliknij go dwukrotnie toorun go. Należy pamiętać, że hello unified agent jest również toohello zastosowania serwera źródłowego, jeśli źródło nie zostanie zaktualizowane do Update4. Należy zainstalować go na serwerze źródłowym hello, jak również, jak zostało to opisane w dalszej części tej listy.<br>
6. **Serwer vContinuum hello**: kopiowanie **vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe** toohello serwer vContinuum.  Upewnij się, zamkniętych hello vContinuum kreatora. Na toorun pliku powitania kliknij go dwukrotnie.<br>
7. **Dla hello Linux główny serwer docelowy**: tooupdate hello unified agent kopiowania **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello głównego serwera docelowego i wyodrębnij go. W hello wyodrębniony folder, uruchom **/Install**.<br>
8. **Dla serwera źródłowego z systemem Windows hello**: nie ma potrzeby tooinstall 5 aktualizacji agenta w źródle, jeśli źródłowych znajduje się już na update4. Jeśli jest mniejszy niż update4, zastosuj hello aktualizacji 5 agenta.
Witaj tooupdate unified agent kopiowania **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello serwera źródłowego. Kliknij go dwukrotnie toorun go. <br>
9. **Dla serwera źródłowego Linux hello**: tooupdate hello unified agent, skopiuj odpowiednią wersję serwera Linux toohello plików UA i wyodrębnij go. W hello wyodrębniony folder, uruchom **/Install**.  Przykład: RHEL 6,7 x 64 serwera, skopiować **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello serwera i wyodrębnij go. W hello wyodrębniony folder, uruchom **/Install**.

## <a name="step-4-set-up-replication"></a>Krok 4: Konfigurowanie replikacji
1. Konfigurowanie replikacji między hello źródłowa i docelowa VMware witryny.
2. Aby uzyskać wskazówki za pomocą hello dokumentacji InMage Scout, który jest pobierany hello produktu. Alternatywnie można uzyskać dostęp do dokumentacji hello w następujący sposób:

   * [Informacje o wersji](https://aka.ms/asr-scout-release-notes)
   * [Macierz zgodności](https://aka.ms/asr-scout-cm)
   * [Podręcznik użytkownika](https://aka.ms/asr-scout-user-guide)
   * [Podręcznik użytkownika RX](https://aka.ms/asr-scout-rx-user-guide)
   * [Przewodnik szybkiego instalacji](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>Aktualizacje
### <a name="azure-site-recovery-scout-801-update-5"></a>Usługi Azure Site Recovery Scout 8.0.1 aktualizacji 5
Aktualizacja Scout 5 jest aktualizacją zbiorczą. Ma ona wszystkie poprawki hello z aktualizację1 do update4 i następujące nowe poprawki i ulepszeń.
Poprawki, które są dodawane z tooupdate5 update4 ASR Scout są składniki tooMaster określonego obiektu docelowego i vContinuum. Jeśli wszystkie źródła serwery, główny cel, konfiguracji serwera, serwer przetwarzania i ODBIERANIA są już na update4 ASR Scout następnie użytkownik musi tooapply aktualizacji 5 tylko na głównym serwerze docelowym. 

**Nowa funkcja obsługi platformy**
* SUSE Linux Enterprise Server 11 z dodatkiem Service Pack 4(SP4)

> [!NOTE]
> SLES 11 z dodatkiem SP4 64 bitowej **InMage_UA_8.0.1.0_SLES11-SP4-64_GA_13Apr2017_release.tar.gz** jest dostarczana z pakietem Scout GA podstawowej **InMage_Scout_Standard_8.0.1 GA.zip**. Pobierz pakiet Scout GA z portalu, jak wspomniano w [krok 1](#step-1-create-a-vault).
>

**Poprawki błędów i rozszerzenia**

* Zwiększyć niezawodność obsługi klastra systemu Windows
    * Niekiedy stałej-także niektóre hello P2V MSCS stają się dysków klastrowych RAW po odzyskaniu
    * Odzyskiwanie klastra Fixed-P2V MSCS zakończy się niepowodzeniem ze względu na niezgodność kolejności toodisk
    * Klastrze Fixed-MSCS dodać dyski, które operacja kończy się niepowodzeniem z niezgodność rozmiaru dysku
    * Klaster MSCS źródła Fixed-z sprawdzanie gotowości mapowania RDM jednostki LUN nie powiedzie się rozmiar weryfikacji
    * Fixed-jednego węzła klastra ochrony kończy się niepowodzeniem ze względu na problem niezgodności tooSCSI 
    * Fixed-ponownego włączenia ochrony serwera klastra P2V Windows hello kończy się niepowodzeniem, jeśli występują dyski klastra docelowego. 
    
* Podczas ochrony powrotu po awarii jeśli nie jest wybrane MT hello tego samego serwera ESXi jako który hello chronione maszyny źródłowej (podczas przekazywania ochrony), a następnie vContinuum przejmuje MT niewłaściwy hello podczas odzyskiwania powrotu po awarii, a następnie operacja odzyskiwania nie powiedzie się.

> [!NOTE]
> 
> * Powyżej P2V klastra poprawki są stosowane tooonly klastra MSCS tych fizycznego, który świeżo są chronione przy użyciu usługi ASR Scout update5. tooavail hello klastra poprawki na powitania już chronione klastrze P2V MSCS w przypadku starszych aktualizacji, należy toofollow hello uaktualnienia kroki opisane w sekcji hello 12, uaktualnienie chronione tooScout klastrze P2V MSCS Update5 z [wersji Scout ASR Informacje o](https://aka.ms/asr-scout-release-notes).
> 
> * Ponownego włączenia ochrony klastra MSCS fizycznych można wykorzystać istniejące dyski docelowe, tylko jeśli w czasie hello ponownego włączenia ochrony, hello tego samego zestawu dysków są aktywne na każdym z węzłów jak podczas pierwotnie chroniony klaster hello. Jeśli nie, nie będą wymagane ręczne wykonanie czynności wymienionych w sekcji 12 [informacje o wersji usługi ASR Scout](https://aka.ms/asr-scout-release-notes) zbyt Przenieś hello docelowej po stronie dysków toohello poprawny magazyn danych ścieżki toore użycia ich podczas ponownego włączenia ochrony. Jeśli Wznów klastrze MSCS hello P2V w trybie bez następujące kroki uaktualniania następnie utworzy nowy dysk na serwerze docelowym, ESXi hello. Należy toomanually delete hello stare dyski z hello magazynu danych.
> 
> * Po każdej zmianie źródła SLES11 lub poprawnego działania ponownego SLES11 z dowolnym serwerem pakiet usługi, a następnie jedną należy ręcznie oznaczyć hello **głównego** dysku pary replikacji do ponownej synchronizacji, ponieważ nie otrzymasz powiadomienie w interfejsie użytkownika CX. W przeciwnym razie "znak hello głównego dysku dla ponownej synchronizacji, mogą pojawić się problemy z integralnością (Podpisane) danych.
> 

### <a name="azure-site-recovery-scout-801-update-4"></a>Usługi Azure Site Recovery Scout 8.0.1 Update 4
Aktualizacja Scout 4 jest aktualizacją zbiorczą. Ma ona wszystkie poprawki hello z aktualizację1 do update3 i następujące nowe poprawki i ulepszeń.

**Nowa funkcja obsługi platformy**

* Dodano obsługę dla vCenter/vSphere w wersji 6.0 i 6.1 6.2
* Dodano obsługę dla następujących systemów operacyjnych Linux
  * Red Hat Enterprise Linux (RHEL) 7.0, 7.1 i 7.2
  * CentOS 7.0, 7.1 i 7.2
  * Red Hat Enterprise Linux (RHEL) 6.8
  * CentOS 6.8

> [!NOTE]
> RHEL/CentOS 7 64-bitowym **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz** jest dostarczana z pakietem Scout GA podstawowej **InMage_Scout_Standard_8.0.1 GA.zip**. Pobierz pakiet Scout GA z portalu, jak wspomniano w [krok 1](#step-1-create-a-vault).
>
>

**Poprawki błędów i rozszerzenia**

* Ulepszone zamykania obsługi dla następujących systemów operacyjnych Linux i tooprevent klony problemów niechciane ponownej synchronizacji.
  * Red Hat Enterprise Linux (RHEL) 6.x
  * Oracle Linux (OL) 6.x
* Dla systemu Linux dostępu do folderu pełną uprawnienia w katalogu instalacji agenta ujednoliconego są teraz ograniczone tylko toohello użytkownika lokalnego.
* W systemie Windows chronometrażu się problem podczas wystawiania wspólnej zakładka spójności rozproszone na silnie załadować aplikacji rozproszonych, takich jak klastry SQL i punktu udziału.
* Dodano dziennika powiązane poprawki w Instalatorze podstawowej CX.
* Link do pobierania vCLI 6.0 VMware jest dodawana tooWindows Instalator podstawowej docelowego elementu głównego.
* Podczas pracy awaryjnej i odzyskiwania po awarii ćwiczenia, należy dodać więcej kontroli i dzienniki, aby zmiany konfiguracji sieci.
* Informacje dotyczące przechowywania pewnym czasie nie jest zgłoszony toohello CX.  
* Dla klastra fizycznego woluminu zmieniać rozmiar operacji za pomocą Kreatora vContinuum kończy się niepowodzeniem podczas zmniejszania rozmiaru woluminu źródłowego się stało.
* Klaster ochrony nie powiodło się z powodu błędu "Podpisu dysku hello toofind nie powiodło się" podczas dysk klastrowy znajduje się dysk PRDM.
* cxps transportu awarii serwera z powodu wyjątku out-of-range.
* Nazwa serwera i IP kolumn są teraz o zmiennym rozmiarze stronie instalacji wypychanej vContinuum kreatora.
* Rozszerzenia interfejsu API ODBIERANIA
  * Zawiera pięć najnowszych dostępnych wspólnej spójności punktów (gwarantowaną jedynie znaczniki).
  * Zawiera szczegóły dotyczące pojemności i wolnego miejsca dla wszystkich hello chronionych urządzeń.
  * Zawiera stan sterownika Scout na serwerze źródłowym.

> [!NOTE]
> * **InMage_Scout_Standard_8.0.1_GA.zip** teraz pakiet podstawowy został zaktualizowany Instalator podstawowej CX **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe** i podstawowej Instalatora Windows główny cel **InMage_Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe**. Nowa instalacja wszystkich nowych CX i docelowego elementu głównego Windows GA usługi bits możesz używać.
> * Aktualizacja 4, które mogą być bezpośrednio stosowane w 8.0.1 po
> * Po są one stosowane w systemie hello nie można obniżyć Hello serwer konfiguracji i ODBIERANIA aktualizacji.
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Usługi Azure Site Recovery Scout 8.0.1 Update 3
Aktualizacja 3 obejmuje następujące hello poprawek i ulepszenia:

* Hello serwer konfiguracji i ODBIERANIA nie magazynu usługi Site Recovery toohello tooregister, gdy są one za powitania serwera proxy.
* Witaj liczbę godzin, które hello cel punktu odzyskiwania (RPO) nie jest spełniony nie są aktualizowane w hello raport o kondycji.
* Serwer konfiguracji Hello nie jest synchronizowany z ODBIERANIA, gdy szczegóły sprzętu ESX hello lub szczegóły sieci zawiera wszystkie znaki UTF-8.
* Kontrolery domeny systemu Windows Server 2008 R2 nie tooboot po odzyskaniu.
* Synchronizacja w trybie offline nie działa zgodnie z oczekiwaniami.
* Po tryb failover maszyny wirtualnej (VM) usunięcie pary replikacji zablokowała w hello CX interfejsu użytkownika przez długi czas i użytkownik nie może ukończyć powitalnych powrotu po awarii i wznowić działanie.
* Ogólne zostały zoptymalizowane migawki operacje, które są wykonywane przez zadanie spójności hello toohelp zmniejszyć aplikacji rozłącza podobnie jak klienci SQL.
* wydajność Hello hello spójności narzędzia (VACP.exe) została zwiększona dzięki zmniejszeniu użycia pamięci hello, który jest wymagany do tworzenia migawek w systemie Windows.
* wypychania Hello zainstalować awarie usługi, gdy hello hasła jest większa niż 16 znaków.
* vContinuum nie jest sprawdzanie i monitowanie o nowe poświadczenia vCenter po zmianie hello poświadczeń.
* W systemie Linux Menedżera pamięci podręcznej głównego celu hello (cachemgr) nie jest pobieranie plików z serwera przetwarzania hello, co powoduje ograniczenie pary replikacji.
* Gdy kolejność dysku klastra (MSCS) fizycznych trybu failover hello jest nie hello takie same na wszystkich węzłach hello, replikacji nie jest ustawiona dla niektórych woluminów klastra hello.
  <br/>Należy pamiętać, że w klastrze hello musi korzystać tootake toobe przełączona do trybu tej poprawki.  
* Funkcje SMTP nie działa zgodnie z oczekiwaniami po uaktualnieniu z tooScout Scout 7.1 8.0.1 ODBIERANIA.
* Statystyka więcej zostały dodane w dzienniku hello raz hello wycofywania operacji tootrack hello trwało toocomplete go.
* Dodano obsługę dla systemów operacyjnych Linux na serwerze źródłowym hello:
  * Red Hat Enterprise Linux (RHEL) 6 aktualizacji 7
  * CentOS 6 aktualizacji 7
* Hello CX i ODBIERANIA interfejsu użytkownika umożliwia teraz wyświetlanie powiadomień hello pary hello, który przechodzi do trybu mapy bitowej.
* Witaj następujące poprawki zabezpieczeń zostały dodane w RX:

| **Opis problemu** | **Procedury implementacji** |
| --- | --- |
| Obejście autoryzacji za pomocą parametru naruszeniu |Ograniczony dostęp do odpowiednich toonon użytkowników. |
| Sfałszowaniem żądań Cross-site |Koncepcja strony token implementowany hello losowo generowany dla każdej strony. <br/>Dzięki temu zostanie wyświetlony: <li> Istnieje tylko jednego logowania wystąpienia dla hello tego samego użytkownika.</li><li>Nie obsługuje odświeżania strony — nastąpi przekierowanie toohello pulpitu nawigacyjnego.</li> |
| Przekazywanie złośliwego pliku |Rozszerzenia toocertain plików o ograniczonym dostępie. Dozwolone są rozszerzenia: 7z, aiff, asf, avi, bmp, csv, doc, docx, fla, flv, gif, gz, gzip, jpeg, jpg, dziennika środek mov, mp3, mp4, mpc, mpeg, mpg, ods odt, pdf, png, ppt, pptx, pxd, qt, pamięci ram, rar, rm, rmi, rmvb, rtf, sdc, sitd, swf, sxc, sxw, tar, tgz, tif, tiff, txt, vsd, wav, wma, wmv, xls, xlsx, xml, a zip. |
| Trwałe skryptów krzyżowych |Dodano wejściowych operacji sprawdzania poprawności. |

> [!NOTE]
> * Wszystkie aktualizacje usługi Site Recovery kumulują się. Aktualizacja 3 ma wszystkie poprawki hello Update 1 i Update 2. Aktualizacja 3, które mogą być bezpośrednio stosowane w 8.0.1 po
> * Po są one stosowane w systemie hello nie można obniżyć Hello serwer konfiguracji i ODBIERANIA aktualizacji.
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Usługi Azure Site Recovery Scout 8.0.1 aktualizacji 2 (aktualizacja, 03 będzie gru 15)
Poprawki w wersji Update 2 obejmują:

* **Serwer konfiguracji**: poprawkę dotyczącą problemu, który uniemożliwił hello 31 dni wolne zliczania funkcja pracy zgodnie z oczekiwaniami, gdy hello serwer konfiguracji został zarejestrowany w usłudze Site Recovery.
* **Unified agent**: poprawkę dotyczącą problemu w programie Update 1, które spowodowały hello aktualizacji nie są instalowane na powitania głównego serwera docelowego podczas został uaktualniony z too8.0.1 wersji 8.0.

### <a name="azure-site-recovery-scout-801-update-1"></a>Usługi Azure Site Recovery Scout 8.0.1 Update 1
Aktualizacja 1 obejmuje następujące hello poprawki i nowe funkcje:

* 31 dni wolne ochrony dla każdego wystąpienia serwera. Dzięki temu możesz tootest funkcji lub ustawić Weryfikacja koncepcji.
  * Wszystkie operacje na powitania serwera, w tym tryb failover i powrotu po awarii, mogą dla hello pierwszy 31 dni, począwszy od czasu hello serwer najpierw jest chroniony za pomocą Scout odzyskiwania lokacji.
  * Z hello 32 dzień roku, każdy chroniony serwer zostanie naliczona opłata szybkością standardowe wystąpienie hello Azure Site Recovery ochrony tooa należące do klienta lokacji.
  * W dowolnym momencie hello liczba chronionych serwerów, które są aktualnie pobieranych jest dostępny na stronie pulpitu nawigacyjnego hello hello magazyn Azure Site Recovery.
* Dodać obsługę vSphere interfejsu wiersza polecenia (vCLI) 5.5 Update 2.
* Dodano systemów operacyjnych Linux na serwerze źródłowym hello obsługę:
  * RHEL 6 aktualizacji 6
  * RHEL 5 zaktualizować 11
  * CentOS 6 aktualizacji 6
  * CentOS 5 aktualizacji 11
* Poprawki błędów hello tooaddress następujące problemy:
  * Rejestracji magazynu nie powiedzie się dla serwera konfiguracji hello lub RX serwera.
  * Wolumin klastra nie są wyświetlane zgodnie z oczekiwaniami, gdy klastrowane maszyny wirtualne są przełączona do trybu podczas one.
  * Powrót po awarii nie powiedzie się, kiedy hello główny serwer docelowy znajduje się na innym serwerze ESXi z maszyn wirtualnych produkcji lokalne powitania.
  * Uprawnienia do pliku konfiguracji są zmieniane po uaktualnieniu too8.0.1, który ma wpływ na operacje i ochrony.
  * Próg ponownej synchronizacji Hello nie są wymuszane zgodnie z oczekiwaniami, która prowadzi tooinconsistent replikacją.
  * Ustawienia odzyskiwania Hello nie są wyświetlane poprawnie w interfejsie serwera konfiguracji hello. wartość danych Hello nieskompresowane niepoprawnie wyświetlana jest wartość hello skompresowane.
  * operacji usuwania Hello nie powoduje usunięcia, zgodnie z oczekiwaniami w Kreatorze vContinuum hello i replikacji nie jest usuwany z hello konfiguracji serwera interfejsu.
  * W Kreatorze vContinuum hello dysku hello jest automatycznie usunięte po kliknięciu **szczegóły** w widoku dysku hello podczas ochrony MSCS maszyn wirtualnych.
  * W scenariuszu fizyczna wirtualna (P2V) hello wymagane usługi HP, takie jak CIMnotify i CqMgHost, nie są toomanual przeniesiony w maszynie wirtualnej odzyskiwania. Powoduje to dodatkowe rozruchu.
  * Ochronę maszyny wirtualnej systemu Linux nie powiedzie się, gdy istnieje więcej niż 26 dysków na powitania główny serwer docelowy.

## <a name="next-steps"></a>Następne kroki
Zadawania pytań, które masz na powitania [forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).
