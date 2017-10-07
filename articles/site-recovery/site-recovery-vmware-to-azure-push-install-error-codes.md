---
title: "aaaAzure usługi Site Recovery Rozwiązywanie problemów z VMware tooAzure | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z błędami podczas replikowania maszyn wirtualnych platformy Azure"
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Rozwiązywanie problemów instalacji wypychanej usługi mobilności

W tym artykule szczegółowo hello typowych problemów, które muszą ponieść podczas próby tooinstall hello usługi mobilności na serwerze toosource potrzeby włączania ochrony.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(Kod błędu 95107) Nie można włączyć ochrony.
**Kod błędu:** | **Możliwe przyczyny** | **Zalecenia dotyczące błędu**
--- | --- | ---
95107 </br>***Komunikat —*** instalacji wypychanej maszyny źródłowej toohello usługi mobilności hello nie powiodło się z kodem błędu ***EP0858***. <br> Czy hello poświadczenia podane tooinstall usługi mobilności jest niepoprawna albo hello konto użytkownika ma niewystarczające uprawnienia | Poświadczenia użytkownika pod warunkiem, że tooinstall usługi mobilności na maszynie źródłowej jest nieprawidłowy | Upewnij się, hello poświadczenia użytkownika podane dla maszyny źródłowej hello na serwerze konfiguracji są poprawne. <br> poświadczenia użytkownika tooadd i edytowanie: Przejdź tooconfiguration serwera > ikona Cspsconfigtool > Zarządzaj kontem. </br> Ponadto upewnij się, poniżej wymagania wstępne są zaznaczone toosuccessfully pełną instalację wypychaną.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(Kod błędu 95015) Nie można włączyć ochrony.
**Kod błędu:** | **Możliwe przyczyny** | **Zalecenia dotyczące błędu**
--- | --- | ---
95105 </br>***Komunikat —*** instalacji wypychanej maszyny źródłowej toohello usługi mobilności hello nie powiodło się z kodem błędu ***EP0856***. <br> "Udostępnianie plików i drukarek" niedozwolony na maszynie źródłowej hello albo występują problemy z połączeniem sieciowym między serwerem przetwarzania hello i hello maszyny źródłowej| Udostępnianie plików i drukarek nie jest włączona. | Zezwalaj na "Udostępnianie plików i drukarek" na maszynie źródłowej hello na powitania zapory systemu Windows, komputer źródłowy toohello Przejdź > Ustawienia w obszarze Zapory systemu Windows > "Zezwalaj aplikacji lub funkcji przez zaporę" > Wybierz "Udostępnianie plików i drukarek we wszystkich profilach". </br> Ponadto upewnij się, poniżej wymagania wstępne są zaznaczone toosuccessfully pełną instalację wypychaną.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(Kod błędu 95117) Nie można włączyć ochrony.
**Kod błędu:** | **Możliwe przyczyny** | **Zalecenia dotyczące błędu**
--- | --- | ---
95117 </br>***Komunikat —*** instalacji wypychanej maszyny źródłowej toohello usługi mobilności hello nie powiodło się z kodem błędu ***EP0865***. <br> Witaj maszyny źródłowej nie jest uruchomiona albo występują problemy z połączeniem sieciowym między serwerem przetwarzania hello i hello maszyny źródłowej | Połączenie sieciowe między serwerem przetwarzania i serwera źródłowego | Sprawdź łączność między serwerem przetwarzania i serwer źródłowy. </br> Ponadto upewnij się, poniżej wymagania wstępne są zaznaczone toosuccessfully pełną instalację wypychaną.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(Kod błędu 95103) Nie można włączyć ochrony.
**Kod błędu:** | **Możliwe przyczyny** | **Zalecenia dotyczące błędu**
--- | --- | ---
95103 </br>***Komunikat —*** instalacji wypychanej maszyny źródłowej toohello usługi mobilności hello nie powiodło się z kodem błędu ***EP0854***. <br> "Zarządzania instrumentacji Windows (WMI)" nie jest dozwolona na maszynie źródłowej hello albo występują problemy z połączeniem sieciowym między serwerem przetwarzania hello i hello maszyny źródłowej| Instrumentacja zarządzania Windows (WMI) zablokowane w hello zapory systemu Windows | Zezwalaj na Instrumentacji zarządzania Windows (WMI) na powitania zapory systemu Windows. W obszarze Ustawienia Zapory systemu Windows > "Zezwalaj aplikacji lub funkcji przez zaporę" > "Wybierz WMI dla wszystkich profilów". </br> Ponadto upewnij się, poniżej wymagania wstępne są zaznaczone toosuccessfully pełną instalację wypychaną.

## <a name="check-push-install-logs-for-errors"></a>Sprawdź dzienniki instalacji wypychanej błędy

Na serwerze konfiguracji procesu hello Przejdź toofile w lokalizacji "PushinstallService" <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand hello źródło problemu hello i użycia poniżej rozwiązywania problemu hello tooresolve czynności.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Wymagania wstępne instalacji wypychanej dla systemu Windows
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>Upewnij się, że włączono "Udostępnianie plików i drukarek"
Zezwalaj na maszynie źródłowej hello w Zaporze systemu Windows hello "Udostępnianie plików i drukarek" i "Instrumentacji zarządzania Windows" </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Jeśli komputer źródłowy jest przyłączony do domeny: </br>
Skonfiguruj ustawienia zapory przy użyciu konsoli zarządzania zasadami grupy (GPMC).
1. Domeny katalogu tooActive logowania komputerze jako administrator i Otwórz konsolę zarządzania zasadami grupy (GPMC. MSC uruchomienia od początku > Uruchom).</br>
3. Jeśli nie zainstalowano konsoli zarządzania zasadami grupy, łącza hello zbyt[hello instalacji konsoli zarządzania zasadami grupy](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. W drzewie konsoli zarządzania zasadami grupy powitania kliknij dwukrotnie obiekty zasad grupy w hello lasu i domeny, a następnie przejdź zbyt "Domyślne zasady domeny". </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. Kliknij prawym przyciskiem myszy na "Domyślne zasady domeny" > Edytuj > będzie można otworzyć nowe okno "Edytor zarządzania zasadami grupy". </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. W hello Edytor zarządzania zasadami grupy przejdź tooComputer konfiguracji > zasady > Szablony administracyjne > Sieć > połączenia sieciowe > Zapora systemu Windows. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Włącz hello następujące ustawienia dla profilu domeny, a profil standardowy </br>
) kliknij dwukrotnie wyjątek "Zapora systemu Windows: Zezwalaj na udostępnianie wyjątek ruchu przychodzącego plików i drukarek". Wybierz opcję włączone, a następnie kliknij przycisk OK. </br>
(b) kliknij dwukrotnie wyjątek "Zapora systemu Windows: Zezwalaj na wyjątek administracji zdalnej dla ruchu przychodzącego". Wybierz opcję włączone, a następnie kliknij przycisk OK. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Jeśli komputer źródłowy nie jest przyłączony do domeny, jest częścią grupy roboczej </br>
Konfigurowanie ustawień zapory na komputerze zdalnym (do grupy roboczej):
1. Przejdź do maszyny źródłowej toohello,</br>
2. W obszarze Ustawienia Zapory systemu Windows > "Zezwalaj aplikacji lub funkcji przez zaporę" > Wybierz "Udostępnianie plików i drukarek we wszystkich profilach". </br>
3. W obszarze Ustawienia Zapory systemu Windows > "Zezwalaj aplikacji lub funkcji przez zaporę" > "Wybierz WMI dla wszystkich profilów". </br>

#### <a name="disable-remote-user-account-control-uac"></a>Wyłącz zdalnej kontroli konta użytkownika (UAC)
Wyłączanie funkcji Kontrola konta użytkownika przy użyciu usługi mobilności hello toopush klucza rejestru.
1. Kliknij przycisk Start > Uruchom > wpisz regedit > ENTER
2. Zlokalizuj i kliknij powitania po podklucz rejestru: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. Jeśli hello LocalAccountTokenFilterPolicy wpis rejestru nie istnieje, wykonaj następujące kroki:
4. W menu Edycja hello > Nowy > kliknij wartość DWORD.
5. Wpisz LocalAccountTokenFilterPolicy, a następnie naciśnij klawisz ENTER.
6. Kliknij prawym przyciskiem myszy LocalAccountTokenFilterPolicy, a następnie kliknij polecenie Modyfikuj.
7. W polu dane wartości hello wpisz 1, a następnie kliknij przycisk OK.
8. Zamknij Edytor rejestru.


## <a name="push-install-pre-requisites-for-linux"></a>Wypychanie instalacji wymagania wstępne dla systemu Linux:

1. Utwórz użytkownika głównego na serwerze Linux źródłowym hello. (Użyj tego konta tylko dla instalacji wypychanej hello i aktualizacji)</br>
2. Sprawdź ten plik/etc/hosts hello na powitania źródłowy serwer ma wpisów, które mapują hello lokalną nazwą hosta tooIP skojarzonego z wszystkich kart sieciowych w systemie Linux. </br>
3. Upewnij się, że najnowsze pakiety openssh, serwer openssh i biblioteki openssl hello są zainstalowane na serwerze źródłowym Linux. </br>
Sprawdź, czy ssh port 22 jest włączona i uruchomiona. </br>
4. Sprawdź przestarzałych wpisów agentów znajdują się już na serwerze źródłowym hello, odinstaluj agentów starsze hello i uruchom ponownie serwer hello, zainstaluj ponownie agenta. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>Włączanie protokołu SFTP podsystemu i hasło uwierzytelniania w pliku sshd_config hello
1. Na serwerze źródłowym Zaloguj się jako element główny. </br>
2. W pliku /etc/ssh/sshd_config hello,</br> Znajdź wiersz hello, który rozpoczyna się od PasswordAuthentication. </br>
3. d.   Usuń komentarz linii hello i zmień wartość "no" hello zbyt "yes". </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. Znajdź wiersz hello, który rozpoczyna się od "Podsystemu" i Usuń komentarz linii hello. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Zapisz zmiany hello i ponownie uruchom usługę sshd hello. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>Wypchnij kontroli instalacji na serwerze konfiguracji procesu.
#### <a name="validate-credentials-for-discovery-and-installation"></a>Sprawdzanie poprawności poświadczeń do odnajdywania i instalacji

1. Z konfiguracji serwera Uruchom Cspsconfigtool</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Upewnij się, że hello konto używane do ochrony ma uprawnienia administratora na maszynie źródłowej hello. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>Sprawdź łączność między serwerem przetwarzania i serwera źródłowego
1. Upewnij się, że serwer przetwarzania jest połączenie internetowe.
2. Sprawdź połączenie WMI za pomocą wbemtest.exe. </br>
Na serwerze przetwarzania hello, kliknij przycisk Start > Uruchom > wbemtest.exe > będzie można otworzyć okna Tester oprzyrządowania Instrumentacji zarządzania Windows, jak pokazano.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Kliknij pozycję Połącz > Wprowadź adres IP serwera źródłowego hello hello Namespace dane wejściowe użytkownika nazwę i hasło (Jeśli komputer źródłowy jest przyłączony do domeny, podaj hello nazwę domeny oraz nazwy użytkownika jako "nazwa_domeny azwa użytkownika". Jeśli maszyna źródłowa jest w grupie roboczej, podaj nazwę użytkownika tylko hello.) Wybierz poziom uwierzytelniania hello jako prywatność pakietów. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Kliknij przycisk Połącz. Teraz hello WMI połączenie zostanie pomyślnie zakończona z hello dane przekazane i powinny być wyświetlane okna Tester oprzyrządowania Instrumentacji zarządzania Windows hello, jak pokazano poniżej: </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   Jeśli połączenie WMI nie powiedzie, można komunikat o błędzie wyskakujących. Hello poniżej zrzut ekranu przedstawia nieudanej próbie, jeśli WMI/Remote Administration nie jest włączona w Zaporze systemu Windows mogą aplikacji. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Sprawdź stan usługi WMI hello i łączności.</br>
Na serwerze konfiguracji procesu hello </br>
Kliknij przycisk start > Uruchom > wmimgmt.msc > Akcje > więcej akcji > Połącz komputer tooanother (maszyny źródłowej). </br>
Wprowadź hello poświadczeń konta hello użyty do ochrony i wyboru, jeśli połączenie jest poprawne. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Sprawdź udostępnionych folderów sieciowych maszyny źródłowej jest dostępny z serwera przetwarzania (PS) zdalnie przy użyciu określonych poświadczeń.
  1. Otwórz Eksploratora plików w przypadku logowania tooProcess serwera (PS) maszyny > w typie paska adresu hello > "\\\source-machine-ip\C$" > naciśnij klawisz Enter. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. Eksplorator plików wyświetli monit o podanie poświadczeń. Wprowadź hello użytkownika i hasło > kliknij przycisk OK.</br>
   Jeśli komputer źródłowy jest przyłączony do domeny, należy podać nazwę domeny hello wraz z nazwą użytkownika jako "nazwa_domeny azwa użytkownika".</br>
   Jeśli maszyna źródłowa jest w grupie roboczej, należy podać tylko nazwa_użytkownika"hello". </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Jeśli połączenie zostanie nawiązane, możesz wyświetlić folderów hello maszyny źródłowej zdalnie z procesu serwera (PS) </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Jeśli połączenie nie powiedzie się, sprawdź, czy są spełnione wszystkie wymagania wstępne.
>

Jeśli nie chcesz tooopen "Instrumentacji zarządzania Windows", można także zainstalować usługi mobilności ręcznie na maszynie źródłowej hello.</br> [Zainstaluj usługę mobilności ręcznie za pomocą graficznego interfejsu użytkownika](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Instalacja za pomocą wskazówki dotyczące Menedżera konfiguracji](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Następne kroki
- [Włączanie replikacji maszyn wirtualnych VMware](vmware-walkthrough-enable-replication.md)
