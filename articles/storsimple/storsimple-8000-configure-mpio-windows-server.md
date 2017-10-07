---
title: "aaaConfigure wielościeżkowego wejścia/wyjścia dla urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooconfigure wielościeżkowego wejścia/wyjścia (MPIO) dla urządzenia StorSimple połączenia tooa hosta z systemem Windows Server 2012 R2."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7796524edc739826ba1e977161fc9988c6d316e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-for-your-storsimple-device"></a>Konfigurowanie wielościeżkowego wejścia/wyjścia dla urządzenia StorSimple

W tym samouczku opisano hello kroki należy wykonać tooinstall i użyć hello funkcja wielościeżkowego wejścia/wyjścia (MPIO) na hoście z systemem Windows Server 2012 R2 i tooa podłączonego urządzenia fizycznego StorSimple. wskazówki Hello w tym artykule dotyczą tooStorSimple 8000 fizycznych urządzeń z serii tylko. Wielościeżkowe wejście/wyjście nie jest obecnie obsługiwane na urządzeniu z StorSimple w chmurze.

Wbudowana obsługa funkcji wielościeżkowego wejścia/wyjścia (MPIO) hello w toohelp systemu Windows Server Microsoft kompilacji wysokiej dostępności, odpornej na uszkodzenia konfiguracji sieci SAN. Wielościeżkowe wejście/wyjście używa nadmiarowych składników ścieżki fizycznej — kart, kabli i przełączników — toocreate ścieżek logicznych między serwerem hello i hello urządzenia magazynującego. W przypadku awarii składnika, powodując toofail Ścieżka logiczna, logika wielościeżkowa używa ścieżki alternatywnej dla operacji We/Wy, dzięki czemu aplikacje mogą nadal uzyskiwać dostępu do danych. Ponadto w zależności od konfiguracji wielościeżkowego wejścia/wyjścia mogą także podnieść wydajność przez ponowne równoważenie obciążenia hello we wszystkich tych ścieżek. Aby uzyskać więcej informacji, zobacz [Omówienie wielościeżkowego wejścia/wyjścia](https://technet.microsoft.com/library/cc725907.aspx "wielościeżkowego wejścia/wyjścia Przegląd oraz funkcje").

Aby hello wysokiej dostępności rozwiązania StorSimple należy skonfigurować wielościeżkowego wejścia/wyjścia na urządzeniu StorSimple. Po zainstalowaniu wielościeżkowego wejścia/wyjścia na serwerach hosta z systemem Windows Server 2012 R2 serwery hello następnie może tolerować łącza, sieci lub interfejsu.

## <a name="mpio-configuration-summary"></a>Podsumowanie konfiguracji wielościeżkowego wejścia/wyjścia

Wielościeżkowego wejścia/wyjścia jest opcjonalna funkcja w systemie Windows Server i nie jest instalowany domyślnie. Powinno być instalowane jako funkcja za pomocą Menedżera serwera.

Wykonaj te kroki tooconfigure wielościeżkowego wejścia/wyjścia na urządzeniu StorSimple:

* Krok 1: Instalacja wielościeżkowego We/Wy na hoście systemu Windows Server hello
* Krok 2: Konfigurowanie wielościeżkowego wejścia/wyjścia dla woluminów StorSimple
* Krok 3: Woluminów StorSimple instalacji na hoście hello
* Krok 4: Konfigurowanie wielościeżkowego wejścia/wyjścia wysokiej dostępności i równoważenia obciążenia

Każdy hello w poprzednich krokach opisano w hello następujące sekcje.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Krok 1: Instalacja wielościeżkowego We/Wy na hoście systemu Windows Server hello

ukończenie tej funkcji na hoście z systemem Windows Server, tooinstall hello następujące procedury.

#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall wielościeżkowego We/Wy na hoście hello

1. Otwórz Menedżera serwera na hoście z systemem Windows Server. Domyślnie Menedżer serwera rozpoczyna się, gdy członek grupy Administratorzy hello loguje tooa komputerem z systemem Windows Server 2012 R2 lub Windows Server 2012. Jeśli hello Menedżera serwera nie jest jeszcze otwarty, kliknij przycisk **Start > Menedżera serwera**.
   
   ![Menedżer serwera](./media/storsimple-configure-mpio-windows-server/IC740997.png)

2. Kliknij przycisk **Menedżera serwera > pulpit nawigacyjny > Dodaj role i funkcje**. Spowoduje to uruchomienie hello **Dodaj role i funkcje** kreatora.
   
   ![Dodawanie ról i funkcji — Kreator 1](./media/storsimple-configure-mpio-windows-server/IC740998.png)
3. W hello **Dodaj role i funkcje** kreatora, wykonaj następujące kroki hello:
   
   1. Na powitania **przed rozpoczęciem** kliknij przycisk **dalej**.
   2. Na powitania **Wybieranie typu instalacji** Zaakceptuj domyślne ustawienie hello **rolach lub oparta na funkcjach** instalacji. Kliknij przycisk **Dalej**.
   
       ![Dodawanie ról i funkcji — Kreator 2](./media/storsimple-configure-mpio-windows-server/IC740999.png)
   3. Na powitania **serwera docelowego wybierz** wybierz pozycję **wybierz serwer z puli serwerów hello**. Serwer hosta powinien być wykrywane automatycznie. Kliknij przycisk **Dalej**.
   4. Na powitania **Wybieranie ról serwera** kliknij przycisk **dalej**.
   5. Na powitania **wybierz funkcje** wybierz **wielościeżkowego We/Wy**i kliknij przycisk **dalej**.
   
       ![Dodawanie ról i funkcji — Kreator 5](./media/storsimple-configure-mpio-windows-server/IC741000.png)
   6. Na powitania **Potwierdź wybrane opcje instalacji** , potwierdź wybór hello, a następnie wybierz **ponowne uruchomienie serwera docelowego hello automatycznie w razie potrzeby**, jak pokazano poniżej. Kliknij pozycję **Zainstaluj**.
   
       ![Dodawanie ról i funkcji — Kreator 8](./media/storsimple-configure-mpio-windows-server/IC741001.png)
   7. Użytkownik jest powiadamiany o hello instalacja została zakończona. Kliknij przycisk **Zamknij** tooclose hello kreatora.
   
       ![Dodawanie ról i funkcji — Kreator 9](./media/storsimple-configure-mpio-windows-server/IC741002.png)

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Krok 2: Konfigurowanie wielościeżkowego wejścia/wyjścia dla woluminów StorSimple

Wielościeżkowego wejścia/wyjścia musi być skonfigurowany tooidentify woluminów StorSimple. tooconfigure woluminów StorSimple toorecognize wielościeżkowego wejścia/wyjścia, wykonaj hello następujące kroki.

#### <a name="tooconfigure-mpio-for-storsimple-volumes"></a>tooconfigure wielościeżkowego wejścia/wyjścia dla woluminów StorSimple

1. Otwórz hello **Konfiguracja MPIO**. Kliknij przycisk **Menedżera serwera > pulpit nawigacyjny > Narzędzia > wielościeżkowego wejścia/wyjścia**.
2. W hello **Właściwości wielościeżkowego wejścia/wyjścia** okno dialogowe, wybierz opcję hello **wykrywanie obsługi wielu ścieżek** kartę.
3. Wybierz **dodać obsługę urządzeń iSCSI**, a następnie kliknij przycisk **Dodaj**.  
   ![Właściwości wielościeżkowego wejścia/wyjścia odnajdywanie wielu ścieżek](./media/storsimple-configure-mpio-windows-server/IC741003.png)
4. Uruchom ponownie serwer powitania po wyświetleniu monitu.
5. W hello **Właściwości wielościeżkowego wejścia/wyjścia** okna dialogowego kliknij hello **urządzeń wielościeżkowego wejścia/wyjścia** kartę. Kliknij pozycję **Dodaj**.
    </br>![Wielościeżkowe wejście/wyjście Właściwości wielościeżkowego We/Wy urządzenia](./media/storsimple-configure-mpio-windows-server/IC741004.png)
6. W hello **Dodawanie obsługi wielościeżkowego wejścia/wyjścia** okna dialogowego, w obszarze **identyfikator urządzenia sprzętowego**, wprowadź numer seryjny urządzenia. tooget hello serial number, uzyskiwania dostępu do urządzenia usługi Menedżer StorSimple urządzenia. Przejdź za**urządzenia > pulpit nawigacyjny**. numer seryjny urządzenia Hello jest wyświetlany w prawej hello **szybki przegląd** okienku hello urządzenia z pulpitu nawigacyjnego.
    </br>
    ![Dodawanie obsługi wielościeżkowego wejścia/wyjścia](./media/storsimple-configure-mpio-windows-server/IC741005.png)
7. Uruchom ponownie serwer powitania po wyświetleniu monitu.

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Krok 3: Woluminów StorSimple instalacji na hoście hello

Po skonfigurowaniu wielościeżkowego wejścia/wyjścia w systemie Windows Server woluminy utworzone na urządzeniu StorSimple hello może być instalowany i następnie skorzystać z funkcji MPIO nadmiarowości. toomount woluminu, wykonywanie hello następujące kroki.

#### <a name="toomount-volumes-on-hello-host"></a>toomount woluminy na hoście hello

1. Otwórz hello **właściwości inicjatora iSCSI** okna na hoście serwera Windows hello. Kliknij przycisk **Menedżera serwera > pulpit nawigacyjny > Narzędzia > inicjatora iSCSI**.
2. W hello **właściwości inicjatora iSCSI** okno dialogowe, kliknij kartę odnajdywania hello, a następnie kliknij przycisk **odnajdowanie portalu obiektu docelowego**.
3. W hello **odnajdowanie portalu obiektu docelowego** okna dialogowego wykonaj hello następujące kroki:
   
   1. Wprowadź adres IP hello hello port danych urządzenia StorSimple (na przykład wprowadzić dane 0).
   2. Kliknij przycisk **OK** tooreturn toohello **właściwości inicjatora iSCSI** okno dialogowe.
     
     > [!IMPORTANT]
     > **Jeśli używasz sieci prywatnej dla połączenia iSCSI, wprowadź adres IP hello hello danych portu, który jest połączony toohello sieci prywatnej.**
    
4. Powtórz kroki 2 i 3 dla drugiego interfejsu sieciowego (na przykład 1 danych) na urządzeniu. Należy pamiętać, że te interfejsy powinno być włączone dla interfejsu iSCSI. Aby uzyskać więcej informacji, zobacz [zmodyfikować interfejsów sieciowych](storsimple-8000-modify-device-config.md#modify-network-interfaces).
5. Wybierz hello **celów** kartę w hello **właściwości inicjatora iSCSI** okno dialogowe. Powinny pojawić się urządzenia StorSimple hello target IQN w obszarze **wykryte obiekty docelowe**.

   ![Karta elementy docelowe właściwości inicjatora iSCSI](./media/storsimple-configure-mpio-windows-server/IC741007.png)
   
6. Kliknij przycisk **Connect** tooestablish jako sesji iSCSI przy użyciu swojego urządzenia StorSimple. A **połączyć tooTarget** zostanie wyświetlone okno dialogowe.
7. W hello **połączyć tooTarget** okno dialogowe, wybierz opcję hello **Włącz wielościeżkowe** pole wyboru. Kliknij przycisk **zaawansowane**.
8. W hello **Zaawansowane ustawienia** okna dialogowego wykonaj hello następujące kroki:
   
   1. Na powitania **karty lokalnej** listy rozwijanej wybierz **inicjatora iSCSI firmy Microsoft**.
   2. Na powitania **IP inicjatora** listy rozwijanej, wybierz hello adres IP hosta hello.
   3. Na powitania **portalu obiektu docelowego** IP listy rozwijanej, wybierz hello IP interfejsu urządzenia.
   4. Kliknij przycisk **OK** tooreturn toohello **właściwości inicjatora iSCSI** okno dialogowe.
9. Kliknij pozycję **Właściwości**. W hello **właściwości** okno dialogowe, kliknij przycisk **dodać sesji**.
10. W hello **połączyć tooTarget** okno dialogowe, wybierz opcję hello **Włącz wielościeżkowe** pole wyboru. Kliknij przycisk **zaawansowane**.
11. W hello **Zaawansowane ustawienia** okno dialogowe:

    1. Na powitania **karty lokalnej** listy rozwijanej, wybierz inicjatora iSCSI firmy Microsoft.
    2. Na powitania **IP inicjatora** listy rozwijanej, wybierz hello IP adres odpowiedniego toohello hosta. W takim przypadku jest nawiązywane na powitania urządzenia tooa jeden interfejs sieci na hoście hello dwa interfejsy sieciowe. W związku z tym ten interfejs jest hello taki sam jak przewidzianego hello pierwszą sesję.
    3. Na powitania **docelowy adres IP portalu** listy rozwijanej, adresu IP wybierz hello hello włączone na urządzeniu hello drugi interfejs danych.
    4. Kliknij przycisk **OK** okno dialogowe właściwości inicjatora iSCSI toohello tooreturn. Dodano drugi docelowej toohello sesji.
12. Otwórz **Zarządzanie komputerem** przechodząc zbyt**Menedżera serwera > pulpit nawigacyjny > Zarządzanie komputerem**. W okienku po lewej stronie powitania kliknij **magazynu > Zarządzanie dyskami**. wolumin Hello utworzony na urządzeniu StorSimple hello, które są widoczne toothis host jest wyświetlany w obszarze **Zarządzanie dyskami** jako nowe dyski.
13. Inicjowanie dysku hello i Utwórz nowy wolumin. W trakcie format hello Wybierz blok o rozmiarze 64 KB.
    
    ![Zarządzanie dyskami](./media/storsimple-configure-mpio-windows-server/IC741008.png)
14. W obszarze **Zarządzanie dyskami**, kliknij prawym przyciskiem myszy hello **dysku** i wybierz **właściwości**.
15. W modelu StorSimple hello ### **właściwości urządzenia dysku wielościeżkowe** okna dialogowego kliknij hello **wielościeżkowego wejścia/wyjścia** kartę.
    
    ![StorSimple 8100 DeviceProp wielościeżkowe dysku.](./media/storsimple-configure-mpio-windows-server/IC741009.png)
16. W hello **Nazwa DSM** , kliknij przycisk **szczegóły** i sprawdź, czy parametry hello są toohello parametrów domyślnych. Parametry domyślne Hello są:
    
    * Ścieżka upewnij się, okres = 30
    * Liczba ponownych prób = 3
    * PDO Usuń okres = 20
    * Interwał ponawiania prób = 1
    * Sprawdź ścieżkę włączone = niezaznaczone.

> [!NOTE]
> **Nie należy modyfikować hello parametrów domyślnych.**


## <a name="step-4-configure-mpio-for-high-availability-and-load-balancing"></a>Krok 4: Konfigurowanie wielościeżkowego wejścia/wyjścia wysokiej dostępności i równoważenia obciążenia

Dla wielu ścieżki na podstawie wysoką dostępność i równoważenie obciążenia, wiele sesji należy ręcznie dodać toodeclare hello różne ścieżki dostępne. Na przykład jeśli hello host ma dwa interfejsy połączone tooSAN i hello urządzenie ma dwa interfejsy połączonych tooSAN, potrzebny cztery sesji skonfigurowane z odpowiednią ścieżką permutacji (tylko dwóch sesji będzie wymagane w przypadku każdego danych i interfejsem hosta w innej podsieci IP i nie podlega routingowi).

**Zaleca się, że masz co najmniej 8 aktywnych sesji równoległych między hello urządzeń i aplikacji hosta.** Można to osiągnąć przez włączenie 4 interfejsów sieciowych w systemie Windows Server. Użyj sieci fizycznej lub wirtualnej interfejsów za pomocą technologii wirtualizacji sieci na poziomie sprzętu lub systemu operacyjnego hello na hoście z systemem Windows Server. Z hello dwa interfejsy sieci na urządzeniu hello ta konfiguracja spowoduje 8 aktywnych sesji. Taka konfiguracja pozwala zoptymalizować przepływność hello urządzenia i w chmurze.

> [!IMPORTANT]
> **Zaleca się, że niemieszanie 1 GbE i interfejsów sieciowych usługi 10 GbE. Jeśli używasz dwa interfejsy sieci dotyczą obu interfejsów powinna być typu identyczne hello.**

Witaj Poniższa procedura opisuje sposób sesji tooadd, gdy urządzenie StorSimple z dwoma interfejsami sieciowymi jest połączonych tooa hosta z dwoma interfejsami sieciowymi. Dzięki temu tylko 4 sesji. Zastosuj tę samą procedurę z urządzeniem StorSimple z dwóch sieci interfejsy połączonych tooa hosta z czterech interfejsami sieciowymi. Konieczne będzie tooconfigure 8 zamiast hello 4 sesji opisane w tym miejscu.

### <a name="tooconfigure-mpio-for-high-availability-and-load-balancing"></a>tooconfigure wielościeżkowego wejścia/wyjścia wysokiej dostępności i równoważenia obciążenia

1. Odnajdź docelowy hello: w hello **właściwości inicjatora iSCSI** okno dialogowe na powitania **odnajdywania** , kliknij pozycję **odnajdź Portal**.
2. W hello **połączyć tooTarget** okna dialogowego wprowadź adres IP hello jednego z interfejsów sieciowych hello urządzenia.
3. Kliknij przycisk **OK** tooreturn toohello **właściwości inicjatora iSCSI** okno dialogowe.
4. W hello **właściwości inicjatora iSCSI** okno dialogowe, wybierz opcję hello **celów** , zaznacz hello odnalezione docelowego, a następnie kliknij **Connect**. Witaj **połączyć tooTarget** zostanie wyświetlone okno dialogowe.
5. W hello **połączyć tooTarget** okno dialogowe:
   
   1. Pozostaw domyślne hello wybrane ustawienie docelowej dla **dodania tego połączenia** toohello listy ulubionych elementów docelowych. Dzięki temu urządzeniu hello automatycznie próbę połączenia hello toorestart za każdym razem, gdy ten komputer zostanie uruchomiony ponownie.
   2. Wybierz hello **Włącz wielościeżkowe** pole wyboru.
   3. Kliknij przycisk **zaawansowane**.
6. W hello **Zaawansowane ustawienia** okno dialogowe:
   
   1. Na powitania **karty lokalnej** listy rozwijanej wybierz **inicjatora iSCSI firmy Microsoft**.
   2. Na powitania **IP inicjatora** listy rozwijanej, wybierz hello adres IP hosta hello.
   3. Na powitania **docelowy adres IP portalu** listy rozwijanej, wybierz hello adres IP interfejsu dane hello włączone na urządzeniu hello.
   4. Kliknij przycisk **OK** okno dialogowe właściwości inicjatora iSCSI toohello tooreturn.
7. Kliknij przycisk **właściwości**i w hello **właściwości** okno dialogowe, kliknij przycisk **dodać sesji**.
8. W hello **połączyć tooTarget** okno dialogowe, wybierz opcję hello **Włącz wielościeżkowe** pole wyboru, a następnie kliknij przycisk **zaawansowane**.
9. W hello **Zaawansowane ustawienia** okno dialogowe:
   
   1. Na powitania **karty lokalnej** listy rozwijanej wybierz **inicjatora iSCSI firmy Microsoft**.
   2. Na powitania **IP inicjatora** listy rozwijanej, wybierz hello adres IP odpowiedni toohello drugi interfejs na hoście hello.
   3. Na powitania **docelowy adres IP portalu** listy rozwijanej, adresu IP wybierz hello hello włączone na urządzeniu hello drugi interfejs danych.
   4. Kliknij przycisk **OK** tooreturn toohello **właściwości inicjatora iSCSI** okno dialogowe. Drugi docelowej toohello sesji zostało dodane.
10. Powtórz kroki od 8-10 tooadd dodatkowych sesji (ścieżki) toohello docelowej. Dwa interfejsy na hoście hello i dwa na powitania urządzenia możesz dodać łącznie cztery sesji.
11. Po dodaniu hello potrzeby sesji (ścieżki) w hello **właściwości inicjatora iSCSI** okno dialogowe, wybierz hello docelowej i kliknij przycisk **właściwości**. Na karcie sesje hello hello **właściwości** okno dialogowe, Uwaga hello cztery sesji identyfikatorów, które odpowiadają toohello możliwych ścieżek permutacji. toocancel sesji, wybierz identyfikator sesji tooa dalej pole wyboru hello, a następnie kliknij przycisk **rozłączenia**.
12. urządzenia tooview przedstawione w sesji, wybierz hello **urządzeń** kartę tooconfigure hello zasady wielościeżkowego wejścia/wyjścia dla wybranego urządzenia, kliknij przycisk **wielościeżkowego wejścia/wyjścia**. Witaj **szczegóły urządzenia** zostanie wyświetlone okno dialogowe. Na powitania **wielościeżkowego wejścia/wyjścia** karcie można wybrać odpowiednie hello **zasady równoważenia obciążenia** ustawienia. Można również wyświetlić hello **Active** lub **wstrzymania** typu ścieżki.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [toomodify usługi Menedżer StorSimple urządzenia przy użyciu hello konfiguracji urządzenia StorSimple](storsimple-8000-modify-device-config.md).

