---
title: "aaaConnect zdalnie tooyour urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooconfigure Twojego urządzenia pod kątem zarządzania zdalnego i w jaki sposób tooWindows tooconnect programu PowerShell dla StorSimple za pośrednictwem protokołu HTTP lub HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>Zdalne połączenia urządzenia z serii StorSimple 8000 tooyour

## <a name="overview"></a>Omówienie

Można zdalnie połączyć urządzenie tooyour za pomocą środowiska Windows PowerShell. Po ustanowieniu połączenia w ten sposób nie ma menu. (Możesz zobaczyć menu tylko wtedy, gdy używasz konsoli szeregowej hello na powitania tooconnect urządzenia). Za pomocą komunikacji zdalnej programu Windows PowerShell należy połączyć tooa określonego obszaru działania. Można również określić język wyświetlania hello.

Aby uzyskać więcej informacji o używaniu toomanage komunikacji zdalnej programu Windows PowerShell urządzeniu Przejdź zbyt[Użyj środowiska Windows PowerShell dla StorSimple tooadminister urządzenia StorSimple](storsimple-8000-windows-powershell-administration.md).

Ten samouczek wyjaśnia sposób tooconfigure Twojego urządzenia pod kątem zarządzania zdalnego, a następnie jak tooWindows tooconnect programu PowerShell dla StorSimple. Korzystanie z protokołu HTTP lub HTTPS tooremotely połączenia za pomocą środowiska Windows PowerShell. Jednak podczas decydowania jak tooWindows tooconnect programu PowerShell dla StorSimple, należy wziąć pod uwagę hello następujących informacji:

* Łączenie bezpośrednio toohello konsoli szeregowej urządzenia jest bezpieczne, ale nie jest łączącego konsoli szeregowej toohello za pośrednictwem przełączników sieciowych. Należy uważać na powitania ryzyko związane z zabezpieczeniami podczas łączenia z konsolą szeregową urządzenia toohello za pośrednictwem przełączników sieciowych.
* Łączących się za pośrednictwem sesji HTTP może oferować lepsze bezpieczeństwo niż łączących się za pośrednictwem konsoli szeregowej hello hello sieci. Chociaż nie jest to najbezpieczniejsza metoda hello, jest dopuszczalne w zaufanych sieciach.
* Łączących się za pośrednictwem sesji protokołu HTTPS z certyfikatu z podpisem własnym jest hello najbardziej bezpieczne i hello zalecana opcja.

Możesz połączyć zdalnie toohello interfejsu programu Windows PowerShell. Jednak urządzenia StorSimple tooyour dostępu zdalnego za pośrednictwem interfejsu programu Windows PowerShell hello nie jest włączona domyślnie. Należy najpierw włączyć zdalne zarządzanie na urządzeniu hello, a następnie na hello klienta, który jest używany tooaccess urządzenia.

Witaj opisane w tym artykule wykonano na komputerze hosta z systemem Windows Server 2012 R2.

## <a name="connect-through-http"></a>Łączenie się za pośrednictwem protokołu HTTP

Łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem sesji HTTP oferuje lepsze zabezpieczenia niż łączących się za pośrednictwem konsoli szeregowej hello urządzenia StorSimple. Chociaż nie jest to najbezpieczniejsza metoda hello, jest dopuszczalne w zaufanych sieciach.

Możesz użyć albo hello Azure portalu lub hello konsoli szeregowej tooconfigure zdalnego zarządzania. Wybierz jedną z procedur przedstawionych hello:

* [Użyj hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTP](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTP](#use-the-serial-console-to-enable-remote-management-over-http)

Po włączeniu zdalnego zarządzania za pomocą hello następujące procedury tooprepare powitania klienta dla połączenia zdalnego.

* [Przygotuj powitania klienta dla połączenia zdalnego](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a>Użyj hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTP

Wykonaj hello, wykonaj następujące kroki w hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTP.

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a>tooenable zarządzanie zdalne za pomocą hello portalu Azure

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple. Wybierz **urządzeń** , a następnie wybierz i kliknij przycisk hello urządzenie tooconfigure do zdalnego zarządzania. Przejdź za**ustawienia urządzenia > zabezpieczeń**.
2. W hello **ustawienia zabezpieczeń** bloku, kliknij przycisk **zdalnego zarządzania**.
3. W hello **zdalnego zarządzania** ustawić bloku **włączyć zdalne zarządzanie** za**tak**.
4. Teraz możesz tooconnect przy użyciu protokołu HTTP. (domyślnie hello jest tooconnect za pośrednictwem protokołu HTTPS). Upewnij się, że wybrano HTTP.
   
   > [!NOTE]
   > Łączenie za pośrednictwem protokołu HTTP jest dopuszczalne tylko w sieciach zaufanych.
   
5. Kliknij przycisk **zapisać** i po wyświetleniu monitu o potwierdzenie, wybierz **tak**.

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTP
Wykonaj następujące kroki na powitania urządzenia konsoli szeregowej tooenable zdalne zarządzanie hello.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>tooenable zdalnego zarządzania za pośrednictwem konsoli szeregowej urządzenia hello
1. Menu konsoli szeregowej hello wybierz opcję 1. Aby uzyskać więcej informacji o używaniu konsoli szeregowej hello na urządzeniu hello Przejdź zbyt[łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem konsoli szeregowej urządzenia](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Witaj, wpisz w wierszu:`Enable-HcsRemoteManagement –AllowHttp`
3. Użytkownik jest powiadamiany o hello luk w zabezpieczeniach systemu przy użyciu protokołu HTTP tooconnect toohello urządzenia. Po wyświetleniu monitu Potwierdź, wpisując **Y**.
4. Sprawdź, czy HTTP jest włączona, wpisując:`Get-HcsSystem`
5. Sprawdź, że hello **RemoteManagementMode** pola pokazuje **HttpsAndHttpEnabled**.hello następującej ilustracji przedstawiono te ustawienia programu PuTTY.
   
     ![Serial HTTPS i HTTP włączone](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>Przygotuj powitania klienta dla połączenia zdalnego
Wykonaj następujące kroki na powitania klienta tooenable zdalne zarządzanie hello.

#### <a name="tooprepare-hello-client-for-remote-connection"></a>tooprepare powitania klienta dla połączenia zdalnego
1. Uruchom sesję programu Windows PowerShell jako administrator.
2. Wpisz hello następującego adresu IP hello tooadd polecenia listy zaufanych hostów hello StorSimple urządzenia toohello klienta:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Zastąp <*device_ip*> o adresie IP hello urządzenia; na przykład: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Następujące polecenie toosave hello urządzenia poświadczeń w zmiennej hello typu: 
   
    ```
    $cred = Get-Credential
    ```
    
4. W hello pojawi się okno dialogowe:
   
   1. Wpisz nazwę użytkownika hello w następującym formacie: *device_ip\SSAdmin*.
   2. Wpisz hasło administratora urządzenia hello, która została ustawiona, gdy urządzenie hello został skonfigurowany z kreatorem hello. Witaj domyślne hasło jest *Password1*.
5. Uruchom sesję programu Windows PowerShell na urządzeniu hello, wpisując polecenie:
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > toocreate sesję programu Windows PowerShell do użytku z urządzenia wirtualnego StorSimple hello, Dołącz hello `–Port` parametru i określ port publiczny hello skonfigurowanego w komunikację zdalną dla urządzenia wirtualnego StorSimple.
   
   
W tym momencie powinien mieć active środowiska Windows PowerShell sesji toohello urządzeniu zdalnym.
   
![Usługi zdalne środowiska PowerShell przy użyciu protokołu HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Łączenie się za pośrednictwem protokołu HTTPS

Łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pomocą sesji protokołu HTTPS jest hello najbardziej bezpieczne i zalecana metoda tooyour zdalnie łączącego się urządzenia Microsoft Azure StorSimple. Hello następujące procedury wyjaśniają, jak tooset się hello serial konsoli i komputerów klienckich, dzięki czemu może używać protokołu HTTPS tooconnect tooWindows programu PowerShell dla urządzenia StorSimple.

Możesz użyć albo hello Azure portalu lub hello konsoli szeregowej tooconfigure zdalnego zarządzania. Wybierz jedną z procedur przedstawionych hello:

* [Użyj hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTPS](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTPS](#use-the-serial-console-to-enable-remote-management-over-https)

Po włączeniu zdalnego zarządzania przy użyciu hello następujące procedury tooprepare hello hosta do zdalnego zarządzania, a następnie podłącz urządzenie toohello z hostem zdalnym hello.

* [Przygotowanie hello hosta do zarządzania zdalnego](#prepare-the-host-for-remote-management)
* [Podłącz urządzenie toohello z hostem zdalnym hello](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a>Użyj hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTPS

Wykonaj hello, wykonaj następujące kroki w hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTPS.

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a>tooenable zdalne zarządzanie przy użyciu protokołu HTTPS z hello portalu Azure

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple. Wybierz **urządzeń** , a następnie wybierz i kliknij przycisk hello urządzenie tooconfigure do zdalnego zarządzania. Przejdź za**ustawienia urządzenia > zabezpieczeń**.
2. W hello **ustawienia zabezpieczeń** bloku, kliknij przycisk **zdalnego zarządzania**.
3. Ustaw **włączyć zdalne zarządzanie** za**tak**.
4. Teraz możesz tooconnect przy użyciu protokołu HTTPS. (domyślnie hello jest tooconnect za pośrednictwem protokołu HTTPS). Upewnij się, że wybrany jest protokół HTTPS.
5. Kliknij przycisk..., a następnie kliknij przycisk **Pobierz certyfikat zdalnego zarządzania**. Określ toosave lokalizację tego pliku. Należy tooinstall ten certyfikat na komputerze klienta lub hosta hello użyje tooconnect toohello urządzenia.
6. Kliknij przycisk **zapisać** , a następnie kliknij przycisk **tak** po wyświetleniu monitu o potwierdzenie.

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTPS

Wykonaj następujące kroki na powitania urządzenia konsoli szeregowej tooenable zdalne zarządzanie hello.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>tooenable zdalnego zarządzania za pośrednictwem konsoli szeregowej urządzenia hello
1. Menu konsoli szeregowej hello wybierz opcję 1. Aby uzyskać więcej informacji o używaniu konsoli szeregowej hello na urządzeniu hello Przejdź zbyt[łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem konsoli szeregowej urządzenia](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Witaj, wpisz w wierszu:
   
     `Enable-HcsRemoteManagement`
   
    To należy włączyć protokół HTTPS na urządzeniu.
3. Sprawdź, czy został włączony protokół HTTPS, wpisując: 
   
     `Get-HcsSystem`
   
    Upewnij się, że hello **RemoteManagementMode** pola pokazuje **HttpsEnabled**.hello następującej ilustracji przedstawiono te ustawienia programu PuTTY.
   
     ![Serial obsługujące protokół HTTPS.](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. Z danych wyjściowych hello `Get-HcsSystem`, skopiuj numer seryjny hello hello urządzenia i zapisz go do późniejszego użycia.
   
   > [!NOTE]
   > numer seryjny Hello mapuje toohello Nazwa CN certyfikatu hello.
   
5. Uzyskaj certyfikat zdalnego zarządzania, wpisując: 
   
     `Get-HcsRemoteManagementCert`
   
    Pojawi się następujący certyfikat z podobnych toohello.
   
    ![Pobierz certyfikat zdalnego zarządzania](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Kopiowanie informacji hello w certyfikacie hello z **---BEGIN CERTIFICATE---** za**---END CERTIFICATE---** do edytora tekstu, takiego jak Notatnik, a następnie zapisz go jako plik cer. (Zostanie skopiowany hosta zdalnego tooyour plików, podczas przygotowywania hosta hello.)
   
   > [!NOTE]
   > toogenerate nowego świadectwa, użyj hello `Set-HcsRemoteManagementCert` polecenia cmdlet.
   
### <a name="prepare-hello-host-for-remote-management"></a>Przygotowanie hello hosta do zarządzania zdalnego

komputer hosta hello tooprepare połączenie zdalnego za pomocą sesji protokołu HTTPS, należy wykonać hello zgodnie z procedurami:

* [Importowanie pliku .cer hello w magazynie głównym hello powitania klienta lub hosta zdalnego](#to-import-the-certificate-on-the-remote-host).
* [Dodawanie pliku hosts toohello numerów seryjnych urządzeń hello na zdalnym hoście](#to-add-device-serial-numbers-to-the-remote-host).

Poniżej opisano każdego hello powyższej procedury.

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>tooimport hello certyfikat na zdalnym hoście hello
1. Kliknij prawym przyciskiem myszy plik cer hello i wybierz **instalacji certyfikatu**. Spowoduje to uruchomienie Kreatora importu certyfikatów hello.
   
    ![Kreator importu certyfikatów 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. Dla **lokalizacji magazynu**, wybierz pozycję **komputera lokalnego**, a następnie kliknij przycisk **dalej**.
3. Wybierz **Umieść wszystkie certyfikaty w powitania po magazynu**, a następnie kliknij przycisk **Przeglądaj**. Przejdź w magazynie głównym toohello dostęp do zdalnego hosta, a następnie kliknij przycisk **dalej**.
   
    ![Kreator importu certyfikatów 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. Kliknij przycisk **Zakończ**. Zostanie wyświetlony komunikat informujący o tym, że hello importowanie zakończyło się pomyślnie.
   
    ![Kreator importu certyfikatów 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>host zdalny numery seryjne toohello tooadd urządzenia
1. Uruchom program Notatnik jako administrator, a następnie otwórz plik hosts hello znajdujący się w \Windows\System32\Drivers\etc.
2. Dodaj następujące trzy pliku hosts tooyour wpisy hello: **adres IP interfejsu dane 0**, **adresu IP stałym kontrolera 0**, i **adres IP stałym kontrolera 1**.
3. Wprowadź numer seryjny urządzenia hello, który został wcześniej zapisany. Ten adres IP toohello mapy, pokazane na powitania po obrazu. Dla kontrolera 0 i kontrolera 1, dołącz **Controller0** i **kontroler1** na końcu hello hello numeru seryjnego (nazwa Pospolita).
   
    ![Dodawanie pliku toohosts nazwa Pospolita](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Plik hosts hello Zapisz.

### <a name="connect-toohello-device-from-hello-remote-host"></a>Podłącz urządzenie toohello z hostem zdalnym hello

Użyj programu Windows PowerShell i protokołu SSL tooenter jako SSAdmin sesję na swoim urządzeniu, z hosta zdalnego lub klienta. Sesja SSAdmin Hello mapuje toooption 1 w hello [konsoli szeregowej](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu urządzenia.

Wykonaj następujące procedury na komputerze hello, z którego mają połączenia zdalnego programu Windows PowerShell hello toomake hello.

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>tooenter jako SSAdmin sesji na urządzeniu hello za pomocą środowiska Windows PowerShell i SSL
1. Uruchom sesję programu Windows PowerShell jako administrator.
2. Dodaj hello urządzenia IP address toohello klienta zaufanych hostów, wpisując:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    Gdzie <*device_ip*> hello adres IP urządzenia, na przykład: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. toocreate nowe poświadczenie, wpisz:
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Gdzie <*IP urządzenie docelowe*> jest adresem IP hello dane 0 dla urządzenia; na przykład **10.126.173.90** pokazane na powitania poprzedzających obrazu pliku hosts hello. Ponadto podaj hello hasło administratora urządzenia.
4. Utwórz sesję, wpisując:
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Dla parametru - ComputerName hello w poleceniu cmdlet hello, podaj hello <*numer seryjny urządzenia docelowego*>. Ten numer seryjny został zamapowany toohello adres IP interfejsu dane 0 w pliku hosts hello na zdalnym hoście; na przykład **SHX0991003G44MT** pokazane na powitania po obrazu.
5. Wpisz:
   
     `Enter-PSSession $session`
6. Należy toowait za kilka minut, a następnie będzie tooyour podłączonego urządzenia za pośrednictwem protokołu HTTPS przy użyciu protokołu SSL. Zostanie wyświetlony komunikat, który wskazuje, że jesteś tooyour podłączonego urządzenia.
   
    ![Usługi zdalne środowiska PowerShell przy użyciu protokołu HTTPS i SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o [przy użyciu programu Windows PowerShell tooadminister urządzenia StorSimple](storsimple-8000-windows-powershell-administration.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

