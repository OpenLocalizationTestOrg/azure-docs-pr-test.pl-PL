---
title: "problemy z wdrażaniem StorSimple aaaTroubleshoot | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toodiagnose i napraw błędy występujące po najpierw wdrożyć StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f8352eaa-193c-42d1-8818-0b8e02d8485d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 9a31a3cfb3be577500b226c2bc8172dd8664bad9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>Rozwiązywanie problemów dotyczących wdrożenia urządzenia StorSimple
## <a name="overview"></a>Omówienie
Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów przydatne dla danego wdrożenia programu Microsoft Azure StorSimple. Opisuje typowych problemów, możliwe przyczyny i toohelp zalecane kroki rozwiązywania problemów, które mogą wystąpić podczas konfigurowania StorSimple. Te informacje dotyczą urządzenia fizycznego StorSimple lokalnymi tooboth hello i hello urządzenia wirtualnego StorSimple.

> [!NOTE]
> Związane z konfiguracją problemów urządzenia, które mogą się spodziewać, może wystąpić podczas wdrażania urządzenia hello powitania po raz pierwszy, lub mogą one występować później, gdy działa hello urządzenia. Ten artykuł skupia się na temat rozwiązywania problemów dotyczących wdrożenia po raz pierwszy. tootroubleshoot działającego urządzenia, przejdź zbyt[rozwiązywania problemów operacyjnych urządzenie](storsimple-troubleshoot-operational-device.md).
> 
> 

W tym artykule również opisano narzędzia hello Rozwiązywanie problemów z wdrożeniami StorSimple oraz przedstawiono krok po kroku przykład rozwiązywania problemów.

## <a name="first-time-deployment-issues"></a>Problemy z wdrażaniem po raz pierwszy
Jeśli napotkasz problem podczas wdrażania do hello urządzenia po raz pierwszy, należy wziąć pod uwagę następujące hello:

* Są rozwiązywania problemu z urządzenia fizycznego, upewnij się, że sprzęt hello został zainstalowany i skonfigurowany zgodnie z opisem w [zainstalować do urządzenia StorSimple 8100](storsimple-8100-hardware-installation.md) lub [zainstalować do urządzenia StorSimple 8600](storsimple-8600-hardware-installation.md).
* Sprawdź wymagania wstępne dotyczące wdrażania. Upewnij się, że wszystkie informacje hello opisane w hello [Lista kontrolna dotycząca konfiguracji wdrożenia](storsimple-deployment-walkthrough.md#deployment-configuration-checklist).
* Przejrzyj hello toosee wersji StorSimple, jeśli hello problem opisano. Witaj informacje o wersji obejmują rozwiązania problemów z instalacją znane. 

Podczas wdrażania urządzenia hello najbardziej typowych problemów przez użytkowników krój wystąpić po uruchomieniu hello Kreatora instalacji i po ich rejestracji urządzenie hello za pomocą środowiska Windows PowerShell dla urządzenia StorSimple. (Możesz użyć programu Windows PowerShell dla StorSimple tooregister i skonfigurować urządzenie StorSimple. Aby uzyskać więcej informacji o rejestracji urządzenia, zobacz [krok 3: Konfigurowanie i rejestrowanie urządzenia za pośrednictwem programu Windows PowerShell dla StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)).

następujące sekcje Hello może pomóc rozwiązać problemy, które wystąpią podczas konfigurowania urządzenia StorSimple hello na powitania po raz pierwszy.

## <a name="first-time-setup-wizard-process"></a>Proces Kreatora instalacji po raz pierwszy
następujące kroki Hello podsumowanie procesu Kreatora instalacji hello. Szczegółowe informacje, zobacz [wdrażanie lokalnego urządzenia StorSimple](storsimple-deployment-walkthrough.md).

1. Uruchom hello [Invoke HcsSetupWizard](https://technet.microsoft.com/library/dn688135.aspx) Kreator instalacji hello toostart polecenia cmdlet, który poprowadzi Cię przez hello pozostałe kroki. 
2. Skonfiguruj sieć hello: hello Kreator instalacji umożliwia skonfigurowanie ustawień sieci dla interfejsu sieciowego 0 danych hello na urządzeniu StorSimple. Te ustawienia obejmują następujące hello:
   * Wirtualnego adresu IP (VIP), maskę podsieci i bramę — Witaj [HcsNetInterface zestaw](https://technet.microsoft.com/library/dn688161.aspx) polecenia cmdlet są wykonywane w tle hello. Konfiguruje hello adres IP, maski podsieci i bramy dla interfejsu sieciowego 0 danych hello na urządzeniu StorSimple.
   * Podstawowy serwer DNS — Witaj [HcsDnsClientServerAddress zestaw](https://technet.microsoft.com/library/dn688172.aspx) polecenia cmdlet są wykonywane w tle hello. Konfiguruje ustawienia DNS hello rozwiązania StorSimple.
   * Serwer NTP — Witaj [HcsNtpClientServerAddress zestaw](https://technet.microsoft.com/library/dn688138.aspx) polecenia cmdlet są wykonywane w tle hello. Konfiguruje ustawienia serwera NTP powitania dla rozwiązania StorSimple.
   * Opcjonalne serwer proxy sieci web — Witaj [HcsWebProxy zestaw](https://technet.microsoft.com/library/dn688154.aspx) polecenia cmdlet są wykonywane w tle hello. Ustawia, a umożliwia hello konfigurację serwera proxy sieci web dla rozwiązania StorSimple.
3. Ustawianie hasła hello: hello następnym krokiem jest tooset administratora urządzenia i hasło programu StorSimple Snapshot Manager. Jeśli używasz Update 1, następnie nie będzie wymagane tooset hello hasło programu StorSimple Snapshot Manager.
   
   * hasło administratora urządzenia Hello jest używany toolog na urządzeniu tooyour. Witaj domyślne hasło urządzenia to **Password1**.
   * hasło programu StorSimple Snapshot Manager Hello jest wymagany w przypadku skonfigurowania toouse urządzenia StorSimple Snapshot Manager. Potrzebne hasło hello zestaw toofirst hello Kreatora instalacji, a następnie można ustawić i zmienić hello usługi Menedżer StorSimple. To hasło służy do uwierzytelniania urządzenia hello z StorSimple Snapshot Manager.
     
     > [!IMPORTANT]
     > Hasła są zbierane przed rejestracją, ale stosowane tylko po zarejestrowaniu urządzenia hello. Jeśli istnieje tooapply Błąd hasła, będzie toosupply zostanie wyświetlony monit o hasło hello ponownie aż hello wymaganych haseł (spełniających wymagania dotyczące złożoności hello) są zbierane.
     > 
     > 
4. Zarejestruj urządzenie hello: hello ostatnim krokiem jest tooregister hello urządzenia w usłudze Menedżer StorSimple hello działają na platformie Microsoft Azure. Rejestracja Hello wymaga zbyt[pobieranie klucza rejestracji usługi hello](storsimple-manage-service.md#get-the-service-registration-key) z hello klasycznego portalu Azure, a następnie podaj go w Kreatorze instalacji hello. Po pomyślnym zarejestrowaniu urządzenia hello, klucz szyfrowania danych usługi podano tooyou. Upewnij się, że tookeep klucza szyfrowania w bezpiecznej lokalizacji, ponieważ będzie ona wymagana tooregister wszystkich kolejnych urządzeń w usłudze hello.

## <a name="common-errors-during-device-deployment"></a>Typowe błędy podczas wdrażania urządzenia
Witaj następujące tabele listy hello typowe błędy że można napotkać podczas możesz:

* Skonfiguruj ustawienia sieciowe hello wymagane.
* Skonfiguruj ustawienia serwera proxy sieci web opcjonalne hello.
* Konfigurowanie hello administratora urządzenia i hasło programu StorSimple Snapshot Manager. 
* Rejestrowanie hello urządzenia. 

## <a name="errors-during-hello-required-network-settings"></a>Błędy podczas hello wymagane ustawienia sieci
| Nie. | Komunikat o błędzie | Możliwe przyczyny | Zalecane działanie |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: To polecenie można uruchomić tylko na aktywnym kontrolerze hello. |Konfiguracja wykonywana na powitania pasywnym kontrolera. |Uruchom to polecenie hello aktywnym kontrolerze. Aby uzyskać więcej informacji, zobacz [Zidentyfikuj active kontroler na urządzeniu](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device). |
| 2 |Invoke-HcsSetupWizard: Urządzenie nie jest gotowy. |Występują problemy z łącznością sieciową hello na dane 0. |Sprawdź łączność sieci fizycznej hello na dane 0. |
| 3 |Invoke-HcsSetupWizard: Istnieje konflikt adresów IP z innym systemem hello sieci (wyjątek od HRESULT: 0x80070263). |IP Hello dostarczony dla danych 0 już był używany przez inny system. |Podaj nowego adresu IP, który nie jest używany. |
| 4 |Invoke-HcsSetupWizard: Zasób klastra nie powiodło się. (Wyjątek od HRESULT: 0x800713AE). |Zduplikowany adres VIP. dostarczony Hello IP jest już używana. |Podaj nowego adresu IP, który nie jest używany. |
| 5 |Wywołanie HcsSetupWizard: Adres IPv4 nieprawidłowe. |adres IP Hello znajduje się w niepoprawnym formacie. |Sprawdź hello format i ponownie podaj adres IP. Aby uzyskać więcej informacji, zobacz [adresowanie Ipv4][1]. |
| 6 |Wywołanie HcsSetupWizard: Adres IPv6 nieprawidłowe. |adres IP Hello znajduje się w niepoprawnym formacie. |Sprawdź hello format i ponownie podaj adres IP. Aby uzyskać więcej informacji, zobacz [adresowanie Ipv6][2]. |
| 7 |Invoke-HcsSetupWizard: Nie dostępnych więcej punktów końcowych z hello program mapowania punktów końcowych. (Wyjątek od HRESULT: 0x800706D9) |funkcje klastra Hello nie działa. |[Skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) dalsze czynności. |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Błędy podczas hello opcjonalne ustawienia serwera proxy w sieci web
| Nie. | Komunikat o błędzie | Możliwe przyczyny | Zalecane działanie |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: Nieprawidłowy parametr (wyjątek od HRESULT: 0x80070057) |Jeden z parametrów hello podanych ustawień serwera proxy hello jest nieprawidłowy. |nie podano Hello URI hello poprawnego formatu. Witaj Użyj następującego formatu: http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invoke-HcsSetupWizard: Serwer RPC jest niedostępny (wyjątek od HRESULT: 0x800706ba) |Hello główną przyczyną jest jedną z następujących hello:<ol><li>Witaj klaster nie jest w górę.</li><li>Hello pasywnym kontrolera nie może komunikować się z aktywnym kontrolerze hello i hello polecenie jest uruchamiane z pasywnym kontrolera.</li></ol> |W zależności od przyczyny głównej hello:<ol><li>[Skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) toomake się, że ten klaster hello jest uruchomiony.</li><li>Uruchom polecenie hello na aktywnym kontrolerze hello. Jeśli chcesz, aby polecenie hello toorun z kontrolera pasywnym hello, konieczne będzie tooensure tego kontrolera pasywnym hello może komunikować się z aktywnym kontrolerze hello. Konieczne będzie zbyt[skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) Jeżeli to połączenie zostanie przerwane.</li></ol> |
| 3 |Invoke-HcsSetupWizard: Wywołanie RPC nie powiodło się (wyjątek od HRESULT: 0x800706be) |Klaster jest wyłączony. |[Skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) toomake się, że ten klaster hello jest uruchomiony. |
| 4 |Invoke-HcsSetupWizard: Nie można odnaleźć zasobu klastra (wyjątek od HRESULT: 0x8007138f) |Nie można odnaleźć zasobu klastra Hello. Może to być spowodowane hello instalacji nie jest poprawny. |Może być konieczne tooreset hello urządzenia toohello domyślne ustawienia fabryczne. [Skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) toocreate zasobu klastra. |
| 5 |Invoke-HcsSetupWizard: Zasób nie online klastra (wyjątek od HRESULT: 0x8007138c) |Zasoby klastra nie są w trybie online. |[Skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) dalsze czynności. |

## <a name="errors-related-toodevice-administrator-and-storsimple-snapshot-manager-passwords"></a>Błędy związane z toodevice administrator i hasło programu StorSimple Snapshot Manager
Witaj domyślne hasło administratora urządzenia jest **Password1**. To hasło wygasa po pierwszym zalogowaniu hello; w związku z tym należy toochange Kreatora instalacji hello toouse go. Należy podać nowe hasło administratora urządzenia podczas rejestrowania urządzenia hello powitania po raz pierwszy. 

Jeśli używasz oprogramowanie StorSimple Snapshot Manager hello działające na powitania serwera Windows hosta toomanage hello urządzeniu, należy również podać hasło programu StorSimple Snapshot Manager podczas rejestracji po raz pierwszy. 

Upewnij się, że hasła spełniają hello następujące wymagania:

* Hasło administratora urządzenia może zawierać od 8 do 15 znaków.
* Hasło programu StorSimple Snapshot Manager powinien być 14 lub 15 znaków.
* Hasła powinna zawierać 3 hello następujące 4 typów znaków: małe litery, wielkie litery liczbowych i specjalnych. 
* Hasło nie może Witaj, taka sama, jak hello ostatnie 24 haseł.

Ponadto należy pamiętać, że hasła wygasną co roku i można zmienić tylko po zarejestrowaniu urządzenia hello. W przypadku niepowodzenia rejestracji hello jakiegokolwiek powodu hello hasła nie zostaną zmienione. Aby uzyskać więcej informacji o administratora urządzenia i hasło programu StorSimple Snapshot Manager Przejdź zbyt[Użyj hello toochange usługi Menedżer StorSimple haseł StorSimple](storsimple-change-passwords.md).

Mogą wystąpić co najmniej jeden hello następujące błędy podczas konfigurowania hello administratora urządzenia i hasło programu StorSimple Snapshot Manager.

| Nie. | Komunikat o błędzie | Zalecane działanie |
| --- | --- | --- |
| 1 |hasło Hello przekracza maksymalną długość hello. |Użyj hasła, które spełnia następujące wymagania:<ul><li>Hasło administratora urządzenia musi należeć do zakresu od 8 do 15 znaków.</li><li>Hasło programu StorSimple Snapshot Manager musi być 14 lub 15 znaków.</li></ul> |
| 2 |Witaj hasło nie spełnia hello wymagana długość. |Użyj hasła, które spełnia następujące wymagania:<ul><li>Hasło administratora urządzenia musi należeć do zakresu od 8 do 15 znaków.</li><li>Hasło programu StorSimple Snapshot Manager musi być 14 lub 15 znaków.</lu></ul> |
| 3 |Witaj hasło musi zawierać tylko małe litery. |Hasło musi mieć 3 hello następujące 4 typy znaków: małe litery, wielkie litery liczbowych i specjalnych. Upewnij się, że hasło spełnia te wymagania. |
| 4 |Witaj hasło musi zawierać cyfry. |Hasło musi mieć 3 hello następujące 4 typy znaków: małe litery, wielkie litery liczbowych i specjalnych. Upewnij się, że hasło spełnia te wymagania. |
| 5 |Witaj hasło musi zawierać znaki specjalne. |Hasło musi mieć 3 hello następujące 4 typy znaków: małe litery, wielkie litery liczbowych i specjalnych. Upewnij się, że hasło spełnia te wymagania. |
| 6 |Witaj musi zawierać hasło 3 hello następujące 4 typy znaków: wielkie litery, małe litery, liczbowych i specjalnych. |Hasło nie zawiera hello wymaganych typów znaków. Upewnij się, że hasło spełnia te wymagania. |
| 7 |Parametr jest niezgodny z potwierdzeniem. |Upewnij się, że hasło spełnia wszystkie wymagania i że został wprowadzony poprawnie. |
| 8 |Hasło nie może dopasować hello domyślne. |Witaj domyślne hasło jest *Password1*. Należy toochange tego hasła po zalogowaniu do powitania po raz pierwszy. |
| 9 |zostały wprowadzone hasło Hello jest niezgodna z hello hasło urządzenia. Wpisz ponownie hasło hello. |Sprawdź hello hasło, a następnie wpisz je ponownie. |

Hasła są zbierane przed hello urządzenie jest zarejestrowane, ale są stosowane tylko po pomyślnej rejestracji. Witaj hasła odzyskiwania w przepływie pracy wymaga hello toobe urządzenia zarejestrowane. 

> [!IMPORTANT]
> Ogólnie rzecz biorąc Jeśli próba tooapply hasła nie powiedzie się, a następnie oprogramowania hello podejmuje wielokrotne próby toocollect hello hasła przed pomyślnym zakończeniem. W rzadkich przypadkach nie można zastosować hello hasła. W takiej sytuacji można zarejestrować urządzenia hello i przejść, jednak hello hasła nie zostaną zmienione. Otrzymasz nie wskazuje na to, jak toowhich hasło nie zostało zmienione — hasło administratora urządzenia hello lub hello hasło programu StorSimple Snapshot Manager. Jeśli ta sytuacja występuje, zaleca się zmianę oba hasła.
> 
> 

Możesz resetować hasła hello w hello klasycznego portalu Azure za pośrednictwem hello usługi Menedżer StorSimple. Aby uzyskać więcej informacji przejdź do: 

* [Hasło administratora urządzenia hello zmiany](storsimple-change-passwords.md#change-the-device-administrator-password).
* [Zmień hasło programu StorSimple Snapshot Manager hello](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

## <a name="errors-during-device-registration"></a>Błędy podczas rejestracji urządzenia
Możesz użyć usługi Menedżer StorSimple hello uruchomione na urządzeniu hello tooregister Microsoft Azure. Może wystąpić jeden lub więcej hello następujące problemy podczas rejestracji urządzenia.

| Nie. | Komunikat o błędzie | Możliwe przyczyny | Zalecane działanie |
| --- | --- | --- | --- |
| 1 |Błąd 350027: Nie tooregister hello urządzenia z hello Menedżer StorSimple. | |Poczekaj kilka minut, a następnie spróbuj ponowić operację hello. Jeśli hello problem będzie się powtarzać, [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md). |
| 2 |Błąd 350013: Wystąpił błąd w rejestracji urządzenia hello. Może to być spowodowane klucz rejestracji usługi tooincorrect. | |Zarejestruj ponownie hello urządzenia z kluczem rejestracji usługi poprawne hello. Aby uzyskać więcej informacji, zobacz [Pobierz klucz rejestracji usługi hello.](storsimple-manage-service.md#get-the-service-registration-key) |
| 3 |Błąd 350063: TooStorSimple uwierzytelniania usługi Menedżera został przekazany, ale rejestracja nie powiodła się. Ponów operację powitania po pewnym czasie. |Ten błąd wskazuje, że minął uwierzytelniania w usługach ACS, ale hello rejestru wywołania toohello usługi nie powiodło się. Może to być wynikiem usterkę sporadyczne sieci. |Jeśli hello problem będzie się powtarzać, skontaktuj [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md). |
| 4 |Błąd 350049: nie można osiągnąć usługi hello podczas rejestracji. |Witaj wywołanie usługi toohello, odebrano wyjątek sieci web. W niektórych przypadkach może pobrać rozwiązany z ponowną próbą wykonania operacji hello później. |Sprawdź nazwę DNS i adres IP, a następnie ponów operację hello. Jeśli hello problem będzie nadal występował, [skontaktuj się z Microsoft Support.](storsimple-contact-microsoft-support.md) |
| 5 |Błąd 350031: hello urządzenia został już zarejestrowany. | |Nie trzeba nic robić. |
| 6 |Błąd 350016: Rejestracja urządzenia nie powiodła się. | |Upewnij się, że klucz rejestracji hello jest poprawny. |
| 7 |Invoke-HcsSetupWizard: Wystąpił błąd podczas rejestrowania urządzenia; może to być spowodowane tooincorrect adres IP lub nazwę DNS. Sprawdź ustawienia sieciowe i spróbuj ponownie. Jeśli hello problem będzie nadal występował, [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md). (Błąd 350050) |Upewnij się, że urządzenie może wysyłać polecenia ping hello poza siecią. Jeśli nie ma łączności sieciowej toooutside, hello rejestracji może zakończyć się niepowodzeniem z powodu następującego błędu. Ten błąd może być kombinacją co najmniej jeden z następujących hello:<ul><li>Niepoprawne IP</li><li>Niepoprawne podsieci</li><li>Niepoprawne bramy</li><li>Nieprawidłowe ustawienia DNS</li></ul> |Zobacz kroki hello w hello [przykład rozwiązywania problemów krok po kroku](#step-by-step-storsimple-troubleshooting-example). |
| 8 |Invoke-HcsSetupWizard: hello bieżąca operacja nie powiodła z powodu tooan wewnętrznego błędu usługi [0x1FBE2]. Ponów operację powitania po pewnym czasie. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support. |Jest to rodzajowy błąd zgłoszony dla wszystkich użytkowników, niewidoczne błędów z usługi lub agenta. Najczęstszą przyczyną Hello mogą być uwierzytelnianie hello ACS nie powiodło się. Możliwą przyczyną niepowodzenia hello jest występują problemy z konfiguracją serwera NTP hello oraz czas na urządzeniu hello nie została poprawnie ustawiona. |Popraw hello czas (w przypadku problemów), a następnie ponów operację rejestracji hello. Użycie strefy czasowej hello tooadjust hello Set HcsSystem - Timezone polecenia własne w strefie czasowej hello (na przykład "czas pacyficzny").  Jeśli ten problem będzie się powtarzać, [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) dalsze czynności. |
| 9 |Ostrzeżenie: Nie można aktywować hello urządzenia. Nie zmieniono administratora urządzenia i hasło programu StorSimple Snapshot Manager. |W przypadku niepowodzenia rejestracji hello hello administratora urządzenia i hasło programu StorSimple Snapshot Manager nie są zmieniane. | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>Narzędzia do rozwiązywania problemów z wdrożeniami StorSimple
StorSimple zawiera kilka narzędzi, których można używać tootroubleshoot rozwiązania StorSimple. Należą do nich:

* Obsługa pakietów i dzienników urządzenia 
* Polecenia cmdlet zaprojektowane specjalnie na potrzeby rozwiązywania problemów 

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>Obsługuje pakiety i urządzenia dzienników dostępnych dla rozwiązywania problemów
Pakiet obsługi zawiera wszystkie dzienniki odpowiednich hello, wspomagające zespołu Microsoft Support hello z rozwiązywania problemów z urządzeniami. Można użyć programu Windows PowerShell dla StorSimple toogenerate pakietu zaszyfrowanych pomocy technicznej, który można następnie udostępnić pomocy technicznej.

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>Dzienniki hello tooview lub hello zawartość pakietu obsługi hello
1. Użyj programu Windows PowerShell dla StorSimple toogenerate pakietu obsługi, zgodnie z opisem w [tworzenie i zarządzanie nimi pakietu obsługi](storsimple-create-manage-support-package.md).
2. Pobierz hello [skryptu odszyfrowywania](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokalnie na komputerze klienckim.
3. Użyj tej [procedury krok po kroku](storsimple-create-manage-support-package.md#edit-a-support-package) pakietu obsługi hello tooopen i odszyfrowywania.
4. Witaj odszyfrować pakietu obsługi, które dzienniki są w formacie etw/etvx. Można wykonać następujące kroki tooview hello tych plików w Podglądzie zdarzeń systemu Windows:
   
   1. Uruchom hello **eventvwr** na kliencie systemu Windows. Spowoduje to uruchomienie hello Podgląd zdarzeń.
   2. W hello **akcje** okienku, kliknij przycisk **Otwórz zapisany dziennik** i pliki dziennika punktu toohello w formacie etvx/etw (pakietu obsługi hello). Możesz teraz przeglądać hello pliku. Po otwarciu pliku hello można kliknij prawym przyciskiem myszy i Zapisz plik hello jako tekst.
      
      > [!IMPORTANT]
      > Można również użyć hello **Get-WinEvent** tooopen polecenia cmdlet tych plików w programie Windows PowerShell. Aby uzyskać więcej informacji, zobacz [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx) w hello dokumentację referencyjną polecenia cmdlet programu Windows PowerShell.
      > 
      > 
5. Po otwarciu hello dzienniki w Podglądzie zdarzeń, poszukaj hello następujące pliki dziennika zawierające problemy związane z toohello konfiguracji urządzenia:
   
   * hcs_pfconfig/Operational dziennika
   * hcs_pfconfig/Config
6. W plikach dziennika hello wyszukiwanie ciągów toohello pokrewne polecenia cmdlet wywoływane przez Kreatora instalacji hello. Zobacz [procesu Kreatora instalacji po raz pierwszy](#first-time-setup-wizard-process) listę tych poleceń cmdlet. 
7. Jeśli nie jest możliwe toofigure limit hello przyczyną problemu hello, możesz [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) dalsze czynności. Użyj hello czynnościach w ramach [Utwórz żądanie obsługi](storsimple-contact-microsoft-support.md#create-a-support-request) po się Support firmy Microsoft, aby uzyskać pomoc.

## <a name="cmdlets-available-for-troubleshooting"></a>Polecenia cmdlet dostępne do rozwiązywania problemów
Użyj hello następujące błędy łączności toodetect poleceń cmdlet programu Windows PowerShell.

* `Get-NetAdapter`: Użyj tego polecenia cmdlet toodetect hello kondycji interfejsów sieciowych. 
* `Test-Connection`: Użyj tego polecenia cmdlet toocheck hello łączność w sieci oraz poza hello.
* `Test-HcsmConnection`: Użyj tego polecenia cmdlet toocheck hello łączności pomyślnie zarejestrowane urządzenia.

Update 1 są uruchomione na urządzeniu StorSimple, hello następującego polecenia cmdlet diagnostycznych są również dostępne.

* `Sync-HcsTime`: Użyj tego polecenia cmdlet toodisplay urządzenia czasu i wymuszanie synchronizacji czasu z powitania serwera NTP.
* `Enable-HcsPing`i `Disable-HcsPing`: używać tych poleceń cmdlet tooallow hello hostów tooping hello interfejsów sieciowych na urządzeniu StorSimple. Domyślnie interfejsy sieciowe StorSimple hello nie odpowiadają tooping żądań.
* `Trace-HcsRoute`: Użyj tego polecenia cmdlet jako narzędziem do śledzenia trasy. Wysyła pakiety tooeach router na powitania sposób tooa przeznaczenia w danym okresie czasu, a następnie oblicza wyniki na podstawie pakietów hello zwrócony z każdym przeskoku. Ponieważ `Trace-HcsRoute` pokazuje hello stopień utraty pakietów na określonym routerze lub łącza, można wyznaczyć które routery lub łącza mogą być przyczyną problemów z siecią. 
* `Get-HcsRoutingTable`: Użyj tego polecenia cmdlet toodisplay hello lokalnej tabeli routingu protokołu IP.

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>Rozwiązywanie problemów za pomocą polecenia cmdlet Get-NetAdapter hello
Po skonfigurowaniu interfejsów sieciowych dla wdrożenia urządzenia po raz pierwszy hello sprzętu stan jest niedostępny w hello usługi Menedżer StorSimple interfejsu użytkownika ponieważ hello urządzenie nie zostało jeszcze zarejestrowane z usługą hello. Ponadto hello stan sprzętu strony może nie zawsze poprawnie odzwierciedlają hello stan urządzenia hello, zwłaszcza, jeśli występują problemy, które mają wpływ na usługi synchronizacji. W takich przypadkach można użyć hello `Get-NetAdapter` toodetermine polecenia cmdlet hello kondycję i stan interfejsów sieciowych.

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>toosee listę wszystkich kart sieciowych hello na urządzeniu
1. Uruchom program Windows PowerShell dla urządzenia StorSimple, a następnie wpisz `Get-NetAdapter`. 
2. Użyj danych wyjściowych hello hello `Get-NetAdapter` polecenia cmdlet i hello następujące wytyczne toounderstand hello stan interfejsu sieciowego.
   
   * W przypadku dobrej kondycji i został włączony interfejs hello hello **ifIndex** stan jest wyświetlany jako **się**.
   * Jeśli interfejs hello jest w dobrej kondycji, ale nie jest fizycznie podłączony (za pomocą kabla sieciowego), hello **ifIndex** jest wyświetlany jako **wyłączone**.
   * W przypadku dobrej kondycji, ale nie jest włączony interfejs hello hello **ifIndex** stan jest wyświetlany jako **NotPresent**.
   * Jeśli interfejs hello nie istnieje, nie ma na liście. Witaj usługi Menedżer StorSimple interfejsu użytkownika będzie widoczna w stanie niepowodzenia tego interfejsu.

Aby uzyskać więcej informacji na temat toouse tego polecenia cmdlet, przejdź zbyt[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) w hello dokumentacji poleceń cmdlet programu Windows PowerShell. 

Witaj poniższych sekcjach przedstawiono przykłady, danych wyjściowych z hello `Get-NetAdapter` polecenia cmdlet. 

 Te przykłady kontrolera 0 został hello pasywnym kontrolera i był skonfigurowany następująco:

* DANE 0, 1 danych, dane 2 i interfejsy znajdował się na urządzeniu hello sieci dane 3.
* DANE 4 i 5 danych karty sieciowe nie były widoczne; nie są one w związku z tym wymienione w danych wyjściowych hello.
* DATA 0 został włączony.

Kontrolera 1 została hello aktywnym kontrolerze i był skonfigurowany następująco:

* DANE 0, danych 1, 2 danych, dane 3, 4 danych i sieci danych 5 interfejsy znajdował się na urządzeniu hello.
* DATA 0 został włączony.

**Przykładowe dane wyjściowe — kontrolera 0**

Hello poniżej przedstawiono dane wyjściowe hello kontrolera 0 (hello kontroler pasywnym). DANE 1, dane 2 i dane 3 nie są połączone. DANE 4 i 5 dane nie są wyświetlane, ponieważ nie są obecne na urządzeniu hello. 

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**Przykładowe dane wyjściowe — kontrolera 1**

Hello poniżej przedstawiono dane wyjściowe hello kontrolera 1 (hello active kontrolera). Tylko hello dane 0 skonfigurowano interfejs sieciowy na powitania urządzenia i czy działa.

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>Rozwiązywanie problemów za pomocą polecenia cmdlet Test-Connection hello
Można użyć hello `Test-Connection` toodetermine polecenia cmdlet czy urządzenia StorSimple można połączyć toohello poza siecią. Jeśli wszystkie parametry sieci hello, w tym hello DNS, są poprawnie skonfigurowane w hello Kreatora instalacji, możesz użyć hello `Test-Connection` tooping polecenia cmdlet znanego adresu poza hello sieci, takich jak outlook.com. 

Problemy z łącznością tootroubleshoot ping z tego polecenia cmdlet należy włączyć, gdy ping jest wyłączona.

Zobacz następujące przykłady, danych wyjściowych z hello hello `Test-Connection` polecenia cmdlet. 

> [!NOTE]
> W pierwszej próbie hello urządzenia hello skonfigurowano niepoprawne DNS. W drugiej próbki hello hello DNS jest poprawna.
> 
> 

**Przykładowe dane wyjściowe — nieprawidłowa DNS**

W następujące przykładowe hello nie ma żadnych danych wyjściowych dla adresów IPV4 i IPV6 hello, co oznacza, że powitalne DNS nie zostanie rozwiązany. Oznacza to, że nie istnieje żadne toohello łączności spoza sieci i poprawne DNS musi toobe dostarczony. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**Przykładowe dane wyjściowe — właściwego systemu DNS**

W następujące przykładowe hello zwraca DNS hello hello adres IPV4, wskazującą tego hello, który serwer DNS jest skonfigurowany prawidłowo. Potwierdza to, że istnieje łączność toohello spoza sieci. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>Rozwiązywanie problemów za pomocą polecenia cmdlet Test-HcsmConnection hello
Użyj hello `Test-HcsmConnection` polecenia cmdlet dla urządzenia, który jest już połączony tooand zarejestrowana przy użyciu usługi Menedżer StorSimple. To polecenie cmdlet pomaga Sprawdź hello łączność między zarejestrowanym urządzeniu i hello odpowiadającego usługi Menedżer StorSimple. To polecenie można uruchomić środowisko Windows PowerShell dla urządzenia StorSimple. 

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>polecenia cmdlet Test-HcsmConnection hello toorun
1. Upewnij się, że urządzenie hello jest zarejestrowany.
2. Sprawdź stan urządzenia hello. Jeśli urządzenie hello jest dezaktywowana w trybie konserwacji, lub w trybie offline, można napotkać hello następujące błędy: 
   
   * ErrorCode.CiSDeviceDecommissioned — to znaczy, że urządzenie hello jest dezaktywowana.
   * ErrorCode.DeviceNotReady — oznacza to, że urządzenie hello jest w trybie konserwacji.
   * ErrorCode.DeviceNotReady — oznacza to, że urządzenie hello nie jest w trybie online.
3. Sprawdź, że hello usługi Menedżer StorSimple działa (Użyj hello [Get-ClusterResource](https://technet.microsoft.com/library/ee461004.aspx) polecenia cmdlet). Jeśli usługa hello nie jest uruchomiona, można napotkać hello następujące błędy:
   
   * ErrorCode.CiSApplianceAgentNotOnline
   * ErrorCode.CisPowershellScriptHcsError — wskazuje, że wystąpił wyjątek po uruchomieniu Get ClusterResource.
4. Sprawdź hello tokenu usługi kontroli dostępu (ACS). Zgłasza wyjątek sieci web, może być wynikiem hello problem bramy, brak uwierzytelnianie serwera proxy, niepoprawny DNS lub wystąpił błąd uwierzytelniania. Może zostać wyświetlony hello następujące błędy:
   
   * ErrorCode.CiSApplianceGateway — wskazuje wyjątek HttpStatusCode.BadGateway: usługa rozpoznawania nazw hello nie można rozpoznać nazwy hosta hello. 
   * ErrorCode.CiSApplianceProxy — wskazuje wyjątek HttpStatusCode.ProxyAuthenticationRequired (kod stanu HTTP 407): nie można uwierzytelnić powitania klienta serwera proxy hello. 
   * ErrorCode.CiSApplianceDNSError — wskazuje wyjątek WebExceptionStatus.NameResolutionFailure: usługa rozpoznawania nazw hello nie można rozpoznać nazwy hosta hello.
   * ErrorCode.CiSApplianceACSError — to wskazuje, że hello Usługa zwróciła błąd uwierzytelniania, ale ma łączności.
     
     Jeśli nie zgłasza wyjątek sieci web, sprawdź ErrorCode.CiSApplianceFailure. Wskazuje urządzenie tym hello nie powiodło się.
5. Sprawdź łączność usługi chmury hello. Jeśli usługa hello zgłasza wyjątek sieci web, mogą pojawić hello następujące błędy:
   
   * ErrorCode.CiSApplianceGateway — wskazuje wyjątek HttpStatusCode.BadGateway: pośredniczącego serwera proxy otrzymał nieprawidłowe żądanie z innego serwera proxy lub hello oryginalny serwer.
   * ErrorCode.CiSApplianceProxy — wskazuje wyjątek HttpStatusCode.ProxyAuthenticationRequired (kod stanu HTTP 407): nie można uwierzytelnić powitania klienta serwera proxy hello. 
   * ErrorCode.CiSApplianceDNSError — wskazuje wyjątek WebExceptionStatus.NameResolutionFailure: usługa rozpoznawania nazw hello nie można rozpoznać nazwy hosta hello.
   * ErrorCode.CiSApplianceACSError — to wskazuje, że hello Usługa zwróciła błąd uwierzytelniania, ale ma łączności.
     
     Jeśli nie zgłasza wyjątek sieci web, sprawdź ErrorCode.CiSApplianceSaasServiceError. Oznacza to problem z hello usługi Menedżer StorSimple.
6. Sprawdź łączność usługi Azure Service Bus. ErrorCode.CiSApplianceServiceBusError wskazuje, że urządzenie tym hello nie może połączyć toohello usługi Service Bus.

Witaj pliki dziennika CiSCommandletLog0Curr.errlog i CiSAgentsvc0Curr.errlog będzie mieć więcej informacji, takich jak Szczegóły wyjątku. 

Aby uzyskać więcej informacji o sposobie toouse hello polecenia cmdlet, przejdź zbyt[Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx) dokumentacji odwoływać się w hello środowiska Windows PowerShell.

> [!IMPORTANT]
> Możesz uruchomić to polecenie cmdlet hello active i hello pasywnym kontrolera. 
> 
> 

Zobacz następujące przykłady, danych wyjściowych z hello hello `Test-HcsmConnection` polecenia cmdlet. 

**Przykładowe dane wyjściowe — pomyślnie zarejestrowane urządzenie z systemem wersji StorSimple (lipca 2014)**

przykład pierwszy Hello jest z urządzenia, który został pomyślnie zarejestrowany hello usługi Menedżer StorSimple i ma problemów z połączeniem. 

     Controller1>Test-HcsmConnection -verbose
     Checking device state  ... Success.
     Device registered successfully
     Checking device authentication.  ... This operation will take few minutes toocomplete....
     Checking device authentication.  ... Success.
     Checking connectivity from device tooStorSimple Manager service.  ... This operation will take few minutes toocomplete....
     Checking connectivity from device tooStorSimple Manager service.  ... Success.
     Checking connectivity from StorSimple Manager service tooStorSimple device. .... Success.
     Controller1>

**Przykładowe dane wyjściowe — pomyślnie zarejestrowane urządzenie z systemem StorSimple Update 1**

Jeśli korzystasz z 1 aktualizacji na urządzeniu StorSimple, nie będzie konieczne toorun go z pełnym przełącznikiem hello.

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**Przykładowe dane wyjściowe — urządzenie w trybie offline z systemem wersji StorSimple (lipca 2014)**

Ten przykład jest z urządzenia, które ma stan **Offline** w hello klasycznego portalu Azure.

     Checking device state: Success 
     Device is registered successfully 
     Checking connectivity from device tooSaaS.. Failure

Witaj urządzenia nie można połączyć za pomocą hello bieżącej konfiguracji serwera proxy sieci web. Może to być problem z konfiguracją serwera proxy sieci web hello lub problem z łącznością sieciową. W takim przypadku należy się upewnić, że ustawienia serwera proxy sieci web są poprawne i serwerów proxy sieci web są w trybie online i jest dostępny. 

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>Rozwiązywanie problemów za pomocą polecenia cmdlet HcsTime synchronizacji hello
Użyj tego polecenia cmdlet toodisplay hello urządzenia czasu. Jeśli godzina na urządzeniu hello przesunięcia z serwera NTP hello, następnie można użyć tego polecenia cmdlet tooforce-synchronizacji czasu powitania serwera NTP. Jeśli przesunięcie hello między urządzeniem hello i serwer NTP jest większa niż 5 minut, zostanie wyświetlone ostrzeżenie. Jeśli hello przesunięcie przekracza 15 minut, następnie hello urządzenia przejdzie w trybie offline. Można nadal używać tego polecenia cmdlet tooforce synchronizacja czasu. Jednak jeśli hello przesunięcie przekracza 15 godzin, nie będzie możliwe synchronizacji tooforce hello czasu i wyświetlany jest komunikat o błędzie.

**Przykładowe dane wyjściowe — synchronizacja czasu wymuszony przy użyciu HcsTime synchronizacji**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>Rozwiązywanie problemów za pomocą polecenia cmdlet Enable-HcsPing i Wyłącz HcsPing hello
Użyj tych poleceń cmdlet tooensure, że interfejsy sieciowe hello na urządzeniu odpowiadać tooICMP żądania ping. Domyślnie interfejsy sieciowe StorSimple hello nie odpowiadają tooping żądań. Za pomocą tego polecenia cmdlet jest hello Najprostszym sposobem tooknow, jeśli urządzenie jest w trybie online i jest dostępny.  

**Przykładowe dane wyjściowe — HcsPing Włączanie i wyłączanie HcsPing**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>Rozwiązywanie problemów za pomocą polecenia cmdlet HcsRoute śledzenia hello
Użyj następującego polecenia cmdlet jako narzędziem do śledzenia trasy. Wysyła pakiety tooeach router na powitania sposób tooa przeznaczenia w danym okresie czasu, a następnie oblicza wyniki na podstawie pakietów hello zwrócony z każdym przeskoku. Ponieważ polecenie cmdlet hello przedstawia hello stopień utraty pakietów na danego routera lub łącza, można wyznaczyć które routery lub łącza mogą być przyczyną problemów z siecią.

**Przykładowe dane wyjściowe przedstawiający sposób tootrace hello trasy pakiet z HcsRoute śledzenia**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>Rozwiązywanie problemów za pomocą polecenia cmdlet Get-HcsRoutingTable hello
Użyj tego polecenia cmdlet tooview hello tabeli routingu dla urządzenia StorSimple. Tabela routingu jest zestaw reguł, które mogą pomóc ustalić, który zostanie skierowany pakiety danych przesyłanych przez sieć protokołu internetowego (IP). 

Witaj tabeli routingu pokazuje hello interfejsy i hello bramy, że trasy hello toohello danych określony sieci. Udostępnia także hello metrykę routingu, czyli hello podejmującą dla tooreach ścieżkę hello danego przeznaczenia. Witaj niższe hello routingu metryki, hello wyższy poziom hello preferencji. 

Na przykład, jeśli masz 2 interfejsy sieciowe dane 2 i dane 3, toohello połączenia internetowego. Jeśli metryka routingu hello dane 2 i dane 3 są odpowiednio 15 i 261, 2 danych z niższym metrykę routingu hello jest hello wybranego interfejsu używanych tooreach hello Internet.

Jeśli używasz Update 1 na urządzeniu StorSimple, interfejsu dane 0 sieci ma hello najwyższą preferencję hello ruchu w chmurze. Oznacza to, że nawet jeśli istnieją inne interfejsy włączoną obsługę chmury, hello chmury ruch będzie kierowany przez dane 0. 

Po uruchomieniu hello `Get-HcsRoutingTable` polecenia cmdlet bez określania parametrów (jako hello po przykładzie), hello polecenia cmdlet dane wyjściowe obejmują tabelach routingu IPv4 i IPv6. Alternatywnie można określić `Get-HcsRoutingTable -IPv4` lub `Get-HcsRoutingTable -IPv6` tooget odpowiedniej tabeli routingu.

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>Krok po kroku StorSimple przykład rozwiązywania problemów
Witaj poniższy przykład przedstawia rozwiązywania problemów krok po kroku wdrożenia StorSimple. W przykładowym scenariuszu hello rejestracji urządzeń kończy się niepowodzeniem z komunikat o błędzie wskazujący, ustawienia sieciowe hello lub nazwa DNS hello jest niepoprawny.

jest zwracany komunikat o błędzie Hello:

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

Błąd Hello może być spowodowane jedną z następujących przyczyn hello:

* Instalacja niepoprawne sprzętu
* Interfejs sieciowy uszkodzony
* Nieprawidłowy adres IP, maski podsieci, bramy, podstawowy serwer DNS lub serwer proxy sieci web
* Klucz rejestracji niepoprawne
* Ustawienia zapory niepoprawne

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>toolocate i napraw problem rejestracji urządzenia hello
1. Sprawdź konfigurację urządzenia: hello active kontrolera, uruchom `Invoke-HcsSetupWizard`.
   
   > [!NOTE]
   > Kreator instalacji Hello należy uruchomić na aktywnym kontrolerze hello. tooverify, które są połączone toohello active kontrolera, przyjrzeć transparent hello przedstawionych w konsoli szeregowej hello. transparent Hello wskazuje są połączone toocontroller 0 i kontrolera 1 i czy kontroler hello jest aktywnych lub pasywnych. Aby uzyskać więcej informacji, przejdź zbyt[Zidentyfikuj active kontroler na urządzeniu](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
   > 
   > 
2. Upewnij się, że urządzenie hello jest poprawnie kablem: Sprawdź sieci hello okablowania na urządzeniu hello płaszczyzny ponownie. okablowanie Hello jest toohello określonego modelu urządzenia. Aby uzyskać więcej informacji, przejdź zbyt[zainstalować do urządzenia StorSimple 8100](storsimple-8100-hardware-installation.md) lub [zainstalować do urządzenia StorSimple 8600](storsimple-8600-hardware-installation.md).
   
   > [!NOTE]
   > Jeśli używasz portów sieciowych 10 GbE, konieczne będzie hello toouse QSFP SFP kart i kable SFP. Aby uzyskać więcej informacji, zobacz hello [lista kabli i przełączników oraz nadawczo-odbiorczych zalecane w przypadku hello 10 GbE porty](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
   > 
   > 
3. Sprawdź kondycję hello hello interfejsu sieciowego:
   
   * Użyj kondycji polecenia cmdlet Get-NetAdapter hello hello toodetect interfejsów sieciowych hello danych 0. 
   * Jeśli hello łącze nie działa, hello **ifindex** pokaże interfejsu hello jest wyłączony. Następnie należy połączenie sieciowe hello toocheck hello portu toohello urządzenia i toohello przełącznika. Należy również toorule się zła kable. 
   * Jeśli podejrzewasz, że hello dane 0 port na aktywnym kontrolerze hello nie powiodło się, można to potwierdzić, łącząc toohello dane 0 port kontrolera 1. tooconfirm, odłączyć kabel sieciowy hello hello obu hello urządzenia z kontrolera 0, Połącz hello kabel toocontroller 1 i następnie ponownie uruchom polecenie cmdlet Get-NetAdapter hello. 
     Jeśli hello dane 0 portu na kontrolerze nie powiedzie się, [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) dalsze czynności. Może być konieczne tooreplace hello kontrolera, w tym systemie.
4. Sprawdź hello łączności toohello przełącznika:
   
   * Upewnij się, że interfejsy sieciowe 0 danych na kontrolera 0 i kontrolera 1 w sieci podstawowej obudowy znajdują się na powitania tej samej podsieci. 
   * Sprawdź Centrum hello lub router. Zazwyczaj należy połączyć oba toohello kontrolerów tego samego Centrum lub router. 
   * Upewnij się, że używasz połączenia hello przełączniki hello dane 0 dla obu kontrolerów w hello tą samą siecią vLAN.
5. Wyeliminować błędy użytkownika:
   
   * Uruchom ponownie Kreatora instalacji hello (Uruchom **Invoke HcsSetupWizard**), a następnie wprowadź hello ponownie wartości toomake się upewnić, że nie ma żadnych błędów. 
   * Weryfikuj rejestrację hello klucz używany. Witaj w tym samym kluczem rejestracji mogą być używane tooconnect wiele urządzeń tooa usługi Menedżer StorSimple. Użyj procedury hello [Pobierz klucz rejestracji usługi hello](storsimple-manage-service.md#get-the-service-registration-key) tooensure, którego używasz hello rejestracji poprawny klucz.
     
     > [!IMPORTANT]
     > Jeśli masz wiele usług uruchomionych, konieczne będzie tooensure tego klucza rejestracji hello odpowiednią usługę hello jest używany tooregister hello urządzenia. Jeśli urządzenia zostały zarejestrowane w usłudze Menedżer StorSimple z niewłaściwego hello, konieczne będzie zbyt[skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) dalsze czynności. Masz tooperform resetowania do ustawień fabrycznych (co może doprowadzić do utraty danych) urządzeń hello toothen połączenia usługi toohello przeznaczone.
     > 
     > 
6. Użyj tooverify polecenia cmdlet Test-Connection hello czy masz połączenie toohello spoza sieci. Aby uzyskać więcej informacji, przejdź zbyt[Rozwiązywanie problemów za pomocą polecenia cmdlet Test-Connection hello](#troubleshoot-with-the-test-connection-cmdlet).
7. Sprawdź, czy Zapora zakłóceń. Jeśli po sprawdzeniu, że hello wirtualnego ustawienia adresu IP (VIP), podsieć bramy i DNS są wszystkie prawidłowe i również widzieć problemy z łącznością, a następnie jest możliwe, że Zapora blokuje komunikację między urządzeniem a hello spoza sieci. Należy tooensure, że porty 80 i 443 są dostępne na urządzeniu StorSimple dla komunikacji wychodzącej. Aby uzyskać więcej informacji, zobacz [wymagania dotyczące sieci dla urządzenia StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
8. Sprawdź dzienniki hello. Przejdź za[obsługuje pakiety i urządzenia dzienników dostępnych dla rozwiązywania problemów](#support-packages-and-device-logs-available-for-troubleshooting).
9. Jeśli hello powyższych kroków nie rozwiązują problemu hello [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) Aby uzyskać pomoc.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się, jak tootroubleshoot działającego urządzenia](storsimple-troubleshoot-operational-device.md).

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 
