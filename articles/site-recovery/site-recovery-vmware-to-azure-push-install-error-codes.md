---
title: "Azure Site Recovery Rozwiązywanie problemów z VMware do platformy Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 1e2452ccc6d3f1859a39e1ee09cdde32f53767ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Rozwiązywanie problemów instalacji wypychanej usługi mobilności

Szczegóły tego artykułu typowych problemów, które muszą ponieść podczas próby instalacji usługi mobilności na serwer źródłowy do włączania ochrony.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(Kod błędu 95107) Nie można włączyć ochrony.
**Kod błędu:** | **Możliwe przyczyny** | **Zalecenia dotyczące błędu**
--- | --- | ---
95107 </br>***Komunikat —*** instalacji wypychanej usługi mobilności na maszynie źródłowej nie powiodła się z kodem błędu ***EP0858***. <br> Poświadczenia podane do zainstalowania usługi mobilności jest niepoprawna albo konto użytkownika ma niewystarczające uprawnienia | Poświadczenia użytkownika do zainstalowania usługi mobilności na maszynie źródłowej jest nieprawidłowy | Upewnij się, poświadczenia użytkownika podane dla maszyny źródłowej na serwerze konfiguracji są poprawne. <br> Aby Dodawanie/edytowanie poświadczeń użytkownika: Przejdź do konfiguracji serwera > ikona Cspsconfigtool > Zarządzaj kontem. </br> Ponadto upewnij się, poniżej wymagania wstępne są sprawdzane w celu pomyślnego ukończenia instalacji.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(Kod błędu 95015) Nie można włączyć ochrony.
**Kod błędu:** | **Możliwe przyczyny** | **Zalecenia dotyczące błędu**
--- | --- | ---
95105 </br>***Komunikat —*** instalacji wypychanej usługi mobilności na maszynie źródłowej nie powiodła się z kodem błędu ***EP0856***. <br> "Udostępnianie plików i drukarek" niedozwolony na maszynie źródłowej, albo występują problemy z połączeniem sieciowym między serwerem przetwarzania i komputera źródłowego| Udostępnianie plików i drukarek nie jest włączona. | Zezwalaj na "Udostępnianie plików i drukarek" na maszynie źródłowej w Zaporze systemu Windows, przejdź do maszyny źródłowej > Ustawienia w obszarze Zapory systemu Windows > "Zezwalaj aplikacji lub funkcji przez zaporę" > Wybierz "Udostępnianie plików i drukarek we wszystkich profilach". </br> Ponadto upewnij się, poniżej wymagania wstępne są sprawdzane w celu pomyślnego ukończenia instalacji.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(Kod błędu 95117) Nie można włączyć ochrony.
**Kod błędu:** | **Możliwe przyczyny** | **Zalecenia dotyczące błędu**
--- | --- | ---
95117 </br>***Komunikat —*** instalacji wypychanej usługi mobilności na maszynie źródłowej nie powiodła się z kodem błędu ***EP0865***. <br> Maszyna źródłowa nie jest uruchomiona albo występują problemy z połączeniem sieciowym między serwerem przetwarzania i komputera źródłowego | Połączenie sieciowe między serwerem przetwarzania i serwera źródłowego | Sprawdź łączność między serwerem przetwarzania i serwer źródłowy. </br> Ponadto upewnij się, poniżej wymagania wstępne są sprawdzane w celu pomyślnego ukończenia instalacji.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(Kod błędu 95103) Nie można włączyć ochrony.
**Kod błędu:** | **Możliwe przyczyny** | **Zalecenia dotyczące błędu**
--- | --- | ---
95103 </br>***Komunikat —*** instalacji wypychanej usługi mobilności na maszynie źródłowej nie powiodła się z kodem błędu ***EP0854***. <br> "Zarządzania instrumentacji Windows (WMI)" nie jest dozwolona na maszynie źródłowej, albo występują problemy z połączeniem sieciowym między serwerem przetwarzania i komputera źródłowego| Instrumentacja zarządzania Windows (WMI) jest zablokowana w Zaporze systemu Windows | Zezwalaj na Instrumentacji zarządzania Windows (WMI) w Zaporze systemu Windows. W obszarze Ustawienia Zapory systemu Windows > "Zezwalaj aplikacji lub funkcji przez zaporę" > "Wybierz WMI dla wszystkich profilów". </br> Ponadto upewnij się, poniżej wymagania wstępne są sprawdzane w celu pomyślnego ukończenia instalacji.

## <a name="check-push-install-logs-for-errors"></a>Sprawdź dzienniki instalacji wypychanej błędy

Na serwerze procesu konfiguracji, przejdź do pliku w lokalizacji "PushinstallService" <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ można określić źródło problemu oraz użycia powyżej kroki rozwiązywania problemów, aby rozwiązać ten problem.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Wymagania wstępne instalacji wypychanej dla systemu Windows
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>Upewnij się, że włączono "Udostępnianie plików i drukarek"
Zezwalaj na "Udostępnianie plików i drukarek" i "Instrumentacji zarządzania Windows" na maszynie źródłowej w Zaporze systemu Windows </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Jeśli komputer źródłowy jest przyłączony do domeny: </br>
Skonfiguruj ustawienia zapory przy użyciu konsoli zarządzania zasadami grupy (GPMC).
1. Zaloguj się do komputera domeny usługi Active directory jako administrator i Otwórz konsolę zarządzania zasadami grupy (GPMC. MSC uruchomienia od początku > Uruchom).</br>
3. Jeśli nie zainstalowano konsoli zarządzania zasadami grupy, kliknij łącze, aby [zainstalować konsolę zarządzania zasadami grupy](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. W drzewie konsoli zarządzania zasadami grupy kliknij dwukrotnie obiekty zasad grupy w lesie i domenie, a następnie przejdź do "Domyślne zasady domeny". </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. Kliknij prawym przyciskiem myszy na "Domyślne zasady domeny" > Edytuj > będzie można otworzyć nowe okno "Edytor zarządzania zasadami grupy". </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. W Edytorze zarządzania zasadami grupy przejdź do pozycji Konfiguracja komputera > zasady > Szablony administracyjne > Sieć > połączenia sieciowe > Zapora systemu Windows. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Włącz następujące ustawienia dla profilu domeny, a profil standardowy </br>
) kliknij dwukrotnie wyjątek "Zapora systemu Windows: Zezwalaj na udostępnianie wyjątek ruchu przychodzącego plików i drukarek". Wybierz opcję włączone, a następnie kliknij przycisk OK. </br>
(b) kliknij dwukrotnie wyjątek "Zapora systemu Windows: Zezwalaj na wyjątek administracji zdalnej dla ruchu przychodzącego". Wybierz opcję włączone, a następnie kliknij przycisk OK. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Jeśli komputer źródłowy nie jest przyłączony do domeny, jest częścią grupy roboczej </br>
Konfigurowanie ustawień zapory na komputerze zdalnym (do grupy roboczej):
1. Przejdź do maszyny źródłowej</br>
2. W obszarze Ustawienia Zapory systemu Windows > "Zezwalaj aplikacji lub funkcji przez zaporę" > Wybierz "Udostępnianie plików i drukarek we wszystkich profilach". </br>
3. W obszarze Ustawienia Zapory systemu Windows > "Zezwalaj aplikacji lub funkcji przez zaporę" > "Wybierz WMI dla wszystkich profilów". </br>

#### <a name="disable-remote-user-account-control-uac"></a>Wyłącz zdalnej kontroli konta użytkownika (UAC)
Wyłączanie funkcji Kontrola konta użytkownika przy użyciu klucza rejestru w celu wypchnięcia usługi mobilności.
1. Kliknij przycisk Start > Uruchom > wpisz regedit > ENTER
2. Zlokalizuj i kliknij następujący podklucz rejestru: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. Jeśli wpis rejestru LocalAccountTokenFilterPolicy nie istnieje, wykonaj następujące kroki:
4. W menu Edycja > Nowy > kliknij wartość DWORD.
5. Wpisz LocalAccountTokenFilterPolicy, a następnie naciśnij klawisz ENTER.
6. Kliknij prawym przyciskiem myszy LocalAccountTokenFilterPolicy, a następnie kliknij polecenie Modyfikuj.
7. W polu dane wartości wpisz 1, a następnie kliknij przycisk OK.
8. Zamknij Edytor rejestru.


## <a name="push-install-pre-requisites-for-linux"></a>Wypychanie instalacji wymagania wstępne dla systemu Linux:

1. Utwórz użytkownika głównego na serwer źródłowy z systemem Linux. (Konto służy tylko do wypychanej instalacji i aktualizacji)</br>
2. Sprawdź, czy plik /etc/hosts na źródłowym serwerze z systemem Linux zawiera wpisy mapujące lokalną nazwę hosta na adres IP skojarzony ze wszystkimi kartami sieciowymi. </br>
3. Upewnij się, że najnowsze pakiety openssh, serwer openssh i biblioteki openssl są zainstalowane na serwerze źródłowym systemu Linux. </br>
Sprawdź, czy ssh port 22 jest włączona i uruchomiona. </br>
4. Sprawdź, jeśli przestarzałych wpisów agentów znajdują się już na serwerze źródłowym, należy odinstalować starsze agentów i uruchom ponownie serwer, zainstaluj ponownie agenta. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-the-sshdconfig-file"></a>Włączanie protokołu SFTP podsystemu i hasło uwierzytelniania w pliku sshd_config
1. Na serwerze źródłowym Zaloguj się jako element główny. </br>
2. W pliku /etc/ssh/sshd_config</br> Znajdź wiersz rozpoczynający się od PasswordAuthentication. </br>
3. d.   Usuń komentarz z linii i zmień wartość "no" na "tak". </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. Znajdź wiersz rozpoczynający się od "Podsystemu" i Usuń komentarz z linii. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Zapisz zmiany i uruchom ponownie usługę sshd. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>Wypchnij kontroli instalacji na serwerze konfiguracji procesu.
#### <a name="validate-credentials-for-discovery-and-installation"></a>Sprawdzanie poprawności poświadczeń do odnajdywania i instalacji

1. Z konfiguracji serwera Uruchom Cspsconfigtool</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Upewnij się, że konto używane do ochrony ma uprawnienia administratora na maszynie źródłowej. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>Sprawdź łączność między serwerem przetwarzania i serwera źródłowego
1. Upewnij się, że serwer przetwarzania jest połączenie internetowe.
2. Sprawdź połączenie WMI za pomocą wbemtest.exe. </br>
Na serwerze przetwarzania, kliknij przycisk Start > Uruchom > wbemtest.exe > będzie można otworzyć okna Tester oprzyrządowania Instrumentacji zarządzania Windows, jak pokazano.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Kliknij pozycję Połącz > Wprowadź adres IP serwera źródłowego w nazwę Namespace danych wejściowych użytkownika i hasło (Jeśli komputer źródłowy jest przyłączony do domeny, podaj nazwę domeny oraz nazwy użytkownika jako "nazwa_domeny azwa użytkownika". Jeśli maszyna źródłowa jest w grupie roboczej, podaj nazwę użytkownika.) Wybierz poziom uwierzytelniania jako prywatność pakietów. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Kliknij przycisk Połącz. Teraz połączenie WMI zostanie pomyślnie zakończona z podanych danych i powinna być wyświetlana okna Tester oprzyrządowania Instrumentacji zarządzania Windows, jak pokazano poniżej: </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   Jeśli połączenie WMI nie powiedzie, można komunikat o błędzie wyskakujących. Poniżej zrzut ekranu pokazuje nieudanej próbie Jeśli WMI/Remote Administration nie jest włączone w Zaporze systemu Windows mogą aplikacji. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Sprawdź stan usługi WMI i łączności.</br>
Na serwerze konfiguracji procesu </br>
Kliknij przycisk start > Uruchom > wmimgmt.msc > Akcje > więcej akcji > nawiązać połączenia z innego komputera (maszyny źródłowej). </br>
Wprowadź poświadczenia konta używanego do ochrony i sprawdź, czy połączenie jest poprawne. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Sprawdź udostępnionych folderów sieciowych maszyny źródłowej jest dostępny z serwera przetwarzania (PS) zdalnie przy użyciu określonych poświadczeń.
  1. Logowanie do procesu serwera (PS) maszyny, otwórz Eksploratora plików > w typie paska adresu > "\\\source-machine-ip\C$" > naciśnij klawisz Enter. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. Eksplorator plików wyświetli monit o podanie poświadczeń. Wprowadź nazwę użytkownika i hasło > kliknij przycisk OK.</br>
   Jeśli komputer źródłowy jest przyłączony do domeny, należy podać nazwę domeny oraz nazwy użytkownika jako "nazwa_domeny azwa użytkownika".</br>
   Jeśli maszyna źródłowa jest w grupie roboczej, należy podać tylko "nazwa_użytkownika". </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Jeśli połączenie zostanie nawiązane, możesz wyświetlić foldery maszyny źródłowej zdalnie z procesu serwera (PS) </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Jeśli połączenie nie powiedzie się, sprawdź, czy są spełnione wszystkie wymagania wstępne.
>

Jeśli nie chcesz otworzyć "Instrumentacji zarządzania Windows", można także zainstalować usługi mobilności ręcznie na maszynie źródłowej.</br> [Zainstaluj usługę mobilności ręcznie za pomocą graficznego interfejsu użytkownika](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Instalacja za pomocą wskazówki dotyczące Menedżera konfiguracji](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Następne kroki
- [Włączanie replikacji maszyn wirtualnych VMware](vmware-walkthrough-enable-replication.md)
