---
title: Konfiguracja serwera iSCSI tablicy wirtualnych Azure StorSimple aaaMicrosoft | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak zarejestrować serwer iSCSI StorSimple tooperform początkowej konfiguracji i przeprowadzić konfigurację urządzenia."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a>Wdrożenie tablicy wirtualne StorSimple — zestawu się jako serwer iSCSI za pośrednictwem portalu Azure

![przepływ procesu instalacji iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a>Omówienie

W tym samouczku wdrażania stosuje toohello tablicy wirtualne Microsoft Azure StorSimple. W tym samouczku opisano, jak tooperform hello początkowej konfiguracji zarejestrować StorSimple serwer iSCSI hello ukończenia konfiguracji urządzenia i następnie utworzyć, zainstalować, zainicjować i sformatować woluminy StorSimple tablica wirtualny skonfigurowany jako serwer iSCSI. 

Hello procedur opisanych w tym miejscu zająć około 30 minut too1 godzinę toocomplete. informacje Hello opublikowane w tym artykule dotyczą tylko tooStorSimple tablice wirtualnego.

## <a name="setup-prerequisites"></a>Wymagania wstępne instalacji

Przed skonfigurowaniem i konfigurowanie macierzy wirtualnego StorSimple, upewnij się, że:

* Udostępnione wirtualne tablicy i połączone tooit zgodnie z opisem w [wdrażanie StorSimple wirtualnego tablicy - udostępniania wirtualnego tablicy w funkcji Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) lub [wdrażanie StorSimple wirtualnego tablicy - udostępniania wirtualnego tablicy w środowisku programu VMware ](storsimple-virtual-array-deploy2-provision-vmware.md).
* Masz klucz rejestracji usługi hello z hello utworzono toomanage macierze wirtualnego StorSimple usługi Menedżer StorSimple urządzenia. Aby uzyskać więcej informacji, zobacz **krok 2: Pobierz klucz rejestracji usługi hello** w [wdrażanie StorSimple wirtualnego tablicy — przygotowanie portalu hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
* Jeśli jest to hello drugi lub kolejny wirtualnego tablica, która rejestrujesz istniejącą usługę Menedżer urządzeń StorSimple, powinien mieć klucz szyfrowania danych usługi hello. Ten klucz został wygenerowany podczas pierwszego urządzenia hello został pomyślnie zarejestrowany z tą usługą. W przypadku utraty tego klucza, zobacz **klucza szyfrowania danych usługi hello Get** w [Użyj hello tooadminister interfejsu użytkownika sieci Web tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).

## <a name="step-by-step-setup"></a>Krok po kroku instalacji

Użyj hello kontynuacji tooset instrukcje krok po kroku i konfigurowanie macierzy wirtualnego StorSimple:

* [Krok 1: Zakończenie lokalnego hello ustawienia interfejsu użytkownika sieci web i rejestrowanie urządzenia](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [Krok 2: Hello pełną wymagane ustawienia urządzenia](#step-2-complete-the-required-device-setup)
* [Krok 3: Dodawanie woluminu](#step-3-add-a-volume)
* [Krok 4: Instalowanie, inicjowanie i formatowanie woluminu](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Krok 1: Zakończenie lokalnego hello ustawienia interfejsu użytkownika sieci web i rejestrowanie urządzenia

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete hello Instalatora i rejestrowanie urządzenia hello

1. Otwórz okno przeglądarki. tooconnect toohello sieci web typu interfejsu użytkownika:
   
    `https://<ip-address of network interface>`
   
    Użyj adresu URL połączenia hello zanotowanym w poprzednim kroku hello. Zostanie wyświetlony błąd informujący, że występuje problem z certyfikatem zabezpieczeń witryny sieci Web hello. Kliknij przycisk **strony sieci web toothis Kontynuuj**.
   
    ![Błąd certyfikatu zabezpieczeń](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. Interfejs użytkownika z urządzeniem wirtualnym jako sieci web logowania toohello **StorSimpleAdmin**. Wprowadź hasło administratora urządzenia hello, który został zmodyfikowany w kroku 3: hello Start urządzenia wirtualnego w [wdrażanie StorSimple wirtualnego tablicy - Provision urządzenia wirtualnego funkcji Hyper-v](storsimple-virtual-array-deploy2-provision-hyperv.md) lub [wdrażanie StorSimple wirtualnego tablicy - Zapewnij urządzenie wirtualne w środowisku programu VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
    ![Strona logowania](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. Nastąpi przekierowanie toohello **Home** strony. Na tej stronie opisano hello różne ustawienia wymagane tooconfigure i rejestrowanie urządzenia wirtualnego przy użyciu usługi Menedżer StorSimple urządzenia hello hello. Należy pamiętać, że hello **ustawień sieciowych**, **ustawienia serwera proxy w sieci Web**, i **ustawienia** są opcjonalne. Witaj tylko wymagane ustawienia to **ustawienia urządzenia** i **ustawienia funkcji Cloud**.
   
    ![Strona główna](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. Na powitania **ustawień sieciowych** w obszarze **interfejsy sieciowe**, dane 0 zostaną automatycznie skonfigurowane dla Ciebie. Każdy interfejs sieciowy jest ustawiana przez tooget domyślny adres IP automatycznie (DHCP). W związku z tym adres IP, podsieci i brama zostanie automatycznie przypisany (dla protokołów IPv4 i IPv6).
   
    Podczas planowania toodeploy urządzenia iSCSI na serwerze (tooprovision magazynu blokowego), zaleca się wyłączenie hello **uzyskać adres IP automatycznie** opcji i skonfigurować statyczne adresy IP.
   
    ![Strona ustawień sieci](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    Jeśli podczas inicjowania obsługi administracyjnej urządzeniu hello hello dodano więcej niż jeden interfejs sieciowy, można je skonfigurować w tym miejscu. Należy pamiętać, że interfejsu sieciowego można skonfigurować jako IPv4 tylko lub jako protokołów IPv4 i IPv6. Konfiguracje tylko protokół IPv6 nie są obsługiwane.
5. Serwery DNS są wymagane, ponieważ są one używane urządzenia próbujący toocommunicate z dostawców usługi magazynu w chmurze lub tooresolve urządzenia według nazwy, jeśli jest on skonfigurowany jako serwer plików. Na powitania **ustawień sieciowych** w obszarze hello **serwerów DNS**:
   
   1. Podstawowego i pomocniczego serwera DNS zostanie skonfigurowany automatycznie. Jeśli wybierzesz tooconfigure statycznych adresów IP, można określić serwerów DNS. Wysokiej dostępności firma Microsoft zaleca, aby skonfigurować podstawowy i pomocniczy serwer DNS.
   2. Kliknij przycisk **Zastosuj**. To spowoduje zastosowanie i sprawdź poprawność ustawień sieciowych hello.
6. Na powitania **ustawienia urządzenia** strony:
   
   1. Przypisz unikatowy **nazwa** tooyour urządzenia. Ta nazwa może być 1 – 15 znaków i może zawierać litery, cyfry i łączniki.
   2. Kliknij przycisk hello **serwerem** ikona ![ikona serwera iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) dla hello **typu** urządzenia, które tworzysz. Serwer iSCSI pozwoli tooprovision magazynu blokowego.
   3. Określ, czy ten toobe urządzeń przyłączonych do domeny. Jeśli urządzenie jest serwerem, następnie dołączania domeny hello jest opcjonalna. Sprzężenia toonot domenę tooa iSCSI serwera, kliknij **Zastosuj**, poczekaj, aż hello toobe ustawienia zastosowane, a następnie przejdź toohello następnego kroku.
      
       Jeśli chcesz toojoin hello urządzenia tooa domeny. Wprowadź **nazwy domeny**, a następnie kliknij przycisk **Zastosuj**.
      
      > [!NOTE]
      > Jeśli dołączenie domenę tooa serwera iSCSI, upewnij się, że tablica wirtualnej jest w jego własnej jednostce organizacyjnej (OU) dla usługi Microsoft Azure Active Directory, a nie obiekty zasad grupy (GPO) są stosowane tooit.
      > 
      > 
   4. Zostanie wyświetlone okno dialogowe. Wprowadź swoje poświadczenia domeny w określonym formacie hello. Kliknij ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png). poświadczenia domeny Hello zostanie zweryfikowane. Zostanie wyświetlony komunikat o błędzie, jeśli hello poświadczenia są nieprawidłowe.
      
       ![poświadczenia](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. Kliknij przycisk **Zastosuj**. Spowoduje to zastosowanie i sprawdź poprawność ustawień urządzenia hello.
7. (Opcjonalnie) skonfiguruj serwer proxy sieci web. Mimo że konfiguracja serwera proxy sieci web jest opcjonalne, należy pamiętać, że jeśli używasz serwera proxy sieci web, można skonfigurować tylko go tutaj.
   
    ![Skonfiguruj serwer proxy sieci web](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    Na powitania **serwer proxy sieci Web** strony:
   
   1. Podaj hello **adres URL serwera proxy sieci Web** w następującym formacie: *adres http://host-IP* lub *FDQN:Port numer*. Należy pamiętać, że adresy URL HTTPS nie są obsługiwane.
   2. Określ **uwierzytelniania** jako **podstawowe** lub **Brak**.
   3. Jeśli używasz uwierzytelniania, należy również tooprovide **Username** i **hasło**.
   4. Kliknij przycisk **Zastosuj**. Spowoduje to zweryfikować i zastosowania ustawień serwera proxy sieci web hello skonfigurowane.
8. (Opcjonalnie) skonfiguruj ustawienia godziny hello urządzenia, na przykład strefa czasowa i hello podstawowe i pomocnicze serwery NTP. Serwery NTP są wymagane, ponieważ urządzenie musi synchronizować czas, aby zapewnić możliwość uwierzytelnienia z dostawcy usług w chmurze.
   
    ![Ustawienia czasu](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    Na powitania **ustawienia** strony:
   
   1. Z listy rozwijanej hello, wybierz hello **strefy czasowej** oparte na powitania lokalizacji geograficznej, w których hello jest wdrażane urządzenie. Witaj domyślną strefę czasową dla Twojego urządzenia jest PST. Wszystkie zaplanowane operacje urządzenia będą wykonywane w ramach tej strefy czasowej.
   2. Określ **podstawowy serwer NTP** dla urządzenia lub zaakceptuj wartość domyślną hello time.windows.com. Upewnij się, że sieć zezwala toopass ruch NTP z sieci centrum danych toohello Internet.
   3. Opcjonalnie można określić **serwera NTP dodatkowej** dla danego urządzenia.
   4. Kliknij przycisk **Zastosuj**. Spowoduje to zweryfikować i zastosowanie hello skonfigurowane ustawienia czasu.
9. Skonfiguruj ustawienia chmury hello urządzenia. W tym kroku zostanie ukończenie konfiguracji urządzenia lokalne powitania, a następnie zarejestruj urządzenie hello usługi Menedżer StorSimple urządzenia.
   
   1. Wprowadź hello **klucz rejestracji usługi** pochodzący **krok 2: Pobierz klucz rejestracji usługi hello** w [wdrażanie StorSimple wirtualnego tablicy — przygotowanie hello Portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
   2. Jeśli nie jest to pierwsze urządzenie hello, który rejestrujesz się z tą usługą, konieczne będzie tooprovide hello **klucza szyfrowania danych usługi**. Ten klucz jest wymagany w przypadku hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple urządzenia. Aby uzyskać więcej informacji, zobacz zbyt[klucza szyfrowania danych usługi hello Get](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) lokalnej interfejs użytkownika sieci web.
   3. Kliknij przycisk **zarejestrować**. To spowoduje ponowne uruchomienie urządzenia hello. Mogą być potrzebne toowait 2 – 3 minuty przed hello urządzenie zostanie pomyślnie zarejestrowana. Po ponownym uruchomieniu urządzenia hello nastąpi przekierowanie toohello Zaloguj się na stronie.
      
      ![Rejestrowanie urządzenia](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. Zwraca toohello portalu Azure.
11. Przejdź toohello **urządzeń** bloku usługi. Jeśli masz wiele zasobów, kliknij przycisk **wszystkie zasoby**, kliknij nazwę usługi (wyszukaj go w razie potrzeby), a następnie kliknij przycisk **urządzeń**.
12. Na powitania **urządzeń** bloku, sprawdź hello urządzenie pomyślnie nawiązało toohello usługi sprawdzając stan hello. Witaj urządzenie powinno mieć stan **gotowe tooset się**.
    
    ![Rejestrowanie urządzenia](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a>Krok 2: Konfigurowanie urządzenia hello jako serwer iSCSI

Wykonaj następujące kroki w hello konfiguracji urządzenia hello wymagane toocomplete portalu Azure hello.

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a>urządzenia hello tooconfigure jako serwer iSCSI

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie przejść za**zarządzania > urządzenia**. W hello **urządzeń** bloku, urządzenia hello wybierz właśnie utworzony. To urządzenie będzie wyświetlany jako **gotowe tooset się**.
   
    ![Konfigurowanie urządzenia jako serwer iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. Kliknij przycisk hello urządzenia i zostanie wyświetlony komunikat transparentu wskazującą urządzenia hello jest gotowy toosetup.
   
    ![Konfigurowanie urządzenia jako serwer iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. Kliknij przycisk **Konfiguruj** na pasku poleceń hello urządzenia. Spowoduje to otwarcie zapasowej hello **Konfiguruj** bloku. W hello **Konfiguruj** bloku hello następujące:
   
   * Nazwa serwera iSCSI Hello jest wypełniane automatycznie.
   * Upewnij się, że szyfrowanie magazynu w chmurze hello ustawiono zbyt**włączone**. Dzięki temu szyfrowanie danych hello wysyłane z hello urządzenia toohello chmury.
   * Określ klucz szyfrowania 32 znaków i zarejestruj go w aplikacji zarządzania kluczami do użytku w przyszłości.
   * Wybierz toobe konta magazynu, używany do urządzenia. W tej subskrypcji, można wybrać istniejące konto magazynu, lub możesz kliknąć **Dodaj** toochoose konta z innej subskrypcji.
     
     ![Konfigurowanie urządzenia jako serwer iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. Kliknij przycisk **Konfiguruj** toocomplete konfigurowania hello iSCSI serwera.
   
    ![Konfigurowanie urządzenia jako serwer iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. Użytkownik zostanie poinformowany, czy tworzenie serwera iSCSI hello jest w toku. Po pomyślnym utworzeniu serwerem hello hello **urządzeń** bloku są aktualizowane i hello odpowiedni stan urządzenia jest **Online**.
   
    ![Konfigurowanie urządzenia jako serwer iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a>Krok 3: Dodawanie woluminu

1. W hello **urządzeń** bloku, urządzenia wybierz hello właśnie skonfigurowany jako serwer usługi iSCSI. Kliknij przycisk **...**  (można również kliknąć prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego hello **Dodaj wolumin**. Możesz również kliknąć **+ Dodaj wolumin** z hello paska poleceń. Spowoduje to otwarcie zapasowej hello **Dodaj wolumin** bloku.
   
    ![Dodawanie woluminu](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. W hello **Dodaj wolumin** bloku hello następujące:
   
   * W hello **nazwa woluminu** wprowadź unikatową nazwę dla woluminu. Nazwa Hello musi być ciągiem o długości 3 znaków too127.
   * W hello **typu** listy rozwijanej liście, określ, czy toocreate **warstwowego** lub **przypięty lokalnie** woluminu. W przypadku obciążeń, które wymagają lokalnych gwarancji, małych opóźnień i większej wydajności, wybierz **przypięty lokalnie** **woluminu**. Dla wszystkich innych danych wybierz **warstwowego** **woluminu**.
   * W hello **pojemności** Określ rozmiar hello hello woluminu. Wolumin warstwowy musi należeć do zakresu od 500 GB i 5 TB i woluminu przypiętego lokalnie musi należeć do zakresu od 50 GB i 500 GB.
     
     Wolumin przypięty lokalnie jest alokowany nieelastycznie i gwarantuje, że hello danych pierwotnych w woluminie hello pozostaje na urządzeniu hello i nie zostaną przeniesione toohello chmury.
     
     Wolumin warstwowy na powitania jest alokowany elastycznie drugiej strony. Podczas tworzenia woluminu warstwowego około 10% miejsca hello jest inicjowana na warstwie lokalne powitania i 90% miejsca hello jest obsługiwana w chmurze hello. Na przykład jeśli udostępniane wolumin 1 TB, 100 GB będzie znajdować się w lokalnej przestrzeni hello i 900 GB byłoby używanych w chmurze powitania po hello warstwy danych. To z kolei oznacza to, że jeśli na urządzeniu hello zabraknie całe miejsce lokalne powitania nie może obsłużyć warstwowych udziału (ponieważ nie będą dostępne hello 10%).
     
     ![Dodawanie woluminu](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * Kliknij przycisk **połączone hosty**, wybierz dostępu formantu rekordu (ACR) odpowiedniego toohello inicjatora iSCSI mają tooconnect toothis woluminu, a następnie kliknij przycisk **wybierz**. <br><br> 
3. tooadd połączonych nowego hosta, kliknij przycisk **Dodaj nowe**, wprowadź nazwę hosta hello i jego iSCSI kwalifikowana nazwa (IQN), a następnie kliknij przycisk **Dodaj**. Jeśli nie masz hello IQN, przejdź zbyt[dodatek A: uzyskać hello IQN hosta z systemem Windows Server](#appendix-a-get-the-iqn-of-a-windows-server-host).
   
      ![Dodawanie woluminu](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. Po zakończeniu konfigurowania woluminu kliknij **OK**. Wolumin zostanie utworzony z hello określonych ustawień i otrzymają powiadomienie. Domyślnie monitorowania i kopii zapasowej mają zostać włączone dla woluminu hello.
   
     ![Dodawanie woluminu](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. tooconfirm, który hello wolumin został toohello został pomyślnie utworzony, przejdź do pozycji **woluminów** bloku. Powinny pojawić się hello woluminu na liście.
   
   ![Dodawanie woluminu](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a>Krok 4: Instalowanie, inicjowanie i formatowanie woluminu

Hello wykonaj następujące kroki toomount, zainicjować i sformatować woluminy StorSimple na hoście systemu Windows Server.

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, inicjowanie i formatowanie woluminu

1. Otwórz hello **inicjatora iSCSI** aplikacji na odpowiednim serwerze hello.
2. W hello **właściwości inicjatora iSCSI** okna na powitania **odnajdywania** , kliknij pozycję **odnajdź Portal**.
   
    ![Odnajdź portal](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. W hello **odnajdowanie portalu obiektu docelowego** okno dialogowe, podaj hello adres IP interfejsu sieci iSCSI, a następnie kliknij **OK**.
   
    ![Adres IP](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. W hello **właściwości inicjatora iSCSI** okna na powitania **celów** zlokalizuj hello **wykryte obiekty docelowe**. (W poszczególnych woluminów będzie odnalezionych docelowy). Stan urządzenia Hello powinny się wyświetlać jako **nieaktywne**.
   
    ![Wykryte obiekty docelowe](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. Wybierz urządzenie docelowe, a następnie kliknij przycisk **Connect**. Po podłączeniu urządzenia hello hello stan powinien zmienić się zbyt**połączony**. (Aby uzyskać więcej informacji o korzystaniu z inicjatora iSCSI firmy Microsoft hello, zobacz [Instalowanie i konfigurowanie programu Microsoft iSCSI Initiator][1].
   
    ![Wybierz urządzenie docelowe](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. Na hoście z systemem Windows, naciśnij klawisze Windows Logo hello + X, a następnie kliknij przycisk **Uruchom**.
7. W hello **Uruchom** okno dialogowe, typ **Diskmgmt.msc**. Kliknij przycisk **OK**i hello **Zarządzanie dyskami** zostanie wyświetlone okno dialogowe. Witaj prawym okienku zostaną wyświetlone powitalne woluminy na hoście.
8. W hello **Zarządzanie dyskami** oknie hello zostaną wyświetlone zainstalowane woluminy pokazane na następującej ilustracji hello. Kliknij prawym przyciskiem myszy hello odnaleziony wolumin (kliknij nazwę dysku hello), a następnie kliknij przycisk **Online**.
   
    ![Zarządzanie dyskami](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. Kliknij prawym przyciskiem myszy i wybierz **Inicjowanie dysku**.
   
    ![Zainicjuj dysk 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. Okno dialogowe hello, wybierz hello tooinitialize dyski, a następnie kliknij **OK**.
    
    ![Inicjowanie dysku 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. zostanie uruchomiony Kreator nowego woluminu prostego powitania. Wybierz rozmiar dysku, a następnie kliknij przycisk **dalej**.
    
    ![Kreator nowego woluminu 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. Przypisywanie woluminu toohello literę dysku, a następnie kliknij przycisk **dalej**.
    
    ![Kreator nowego woluminu 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. Wprowadź hello parametry tooformat hello woluminu. **W systemie Windows Server jest obsługiwana wyłącznie systemu plików NTFS.** Ustaw too64K rozmiar jednostki alokacji hello. Podaj etykietę woluminu. Jest zalecanym najlepszym rozwiązaniem dla tej nazwy toobe identyczne toohello woluminu nazwy podane w macierzy wirtualne StorSimple. Kliknij przycisk **Dalej**.
    
    ![Kreator nowego woluminu 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. Sprawdź wartości powitania dla woluminu, a następnie kliknij przycisk **Zakończ**.
    
    ![Kreator nowego woluminu 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    woluminy Hello będą wyświetlane jako **Online** na powitania **Zarządzanie dyskami** strony.
    
    ![woluminy w trybie online](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toouse hello lokalnego interfejsu użytkownika sieci web zbyt[administrowania tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a>Dodatek A: Get hello IQN hosta z systemem Windows Server

Wykonaj następujące kroki tooget hello iSCSI hello kwalifikowana nazwa (IQN) hosta z systemem Windows z systemem Windows Server 2012.

#### <a name="tooget-hello-iqn-of-a-windows-host"></a>Witaj tooget IQN hosta z systemem Windows

1. Uruchom inicjatora iSCSI firmy Microsoft hello na hoście z systemem Windows.
2. W hello **właściwości inicjatora iSCSI** okna na powitania **konfiguracji** karcie zaznacz i skopiuj ciąg hello z hello **Nazwa inicjatora** pola.
   
    ![Właściwości inicjatora iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. Zapisz ten ciąg.

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



