---
title: "aaaConfigure wielościeżkowego We/Wy na hoście połączone tooStorSimple tablicy wirtualnej | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooconfigure wielościeżkowego We/Wy (MPIO) dla macierzy wirtualnego StorSimple połączenia tooa hosta z systemem Windows Server 2012 R2."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a>Konfigurowanie wielościeżkowego We/Wy na hoście systemu Windows Server dla hello tablicy wirtualnego StorSimple
## <a name="overview"></a>Omówienie
W tym artykule opisano sposób zastosowania określonych ustawień konfiguracyjnych dla woluminów StorSimple — tylko do tooinstall funkcja wielościeżkowego wejścia/wyjścia (MPIO) na hoście z systemem Windows Server, a następnie sprawdź wielościeżkowego wejścia/wyjścia dla woluminów StorSimple. procedury Hello zakłada, że tablica wirtualnego StorSimple 1200 z dwoma interfejsami sieciowymi hosta systemu Windows Server tooa połączonych z dwoma interfejsami sieciowymi. Hello informacje zawarte w tym artykule dotyczą tylko toohello wirtualnego tablicy. Informacji dotyczących urządzeń z serii StorSimple 8000 można przejść za[konfigurowanie wielościeżkowego wejścia/wyjścia dla hosta StorSimple](storsimple-configure-mpio-windows-server.md). 

Funkcja wielościeżkowego wejścia/wyjścia Hello w konfiguracji wysokiej dostępności i odporności na uszkodzenia magazynu kompilacji pomaga systemu Windows Server. Wielościeżkowe wejście/wyjście używa nadmiarowych składników ścieżki fizycznej — kart, kabli i przełączników — toocreate ścieżek logicznych między serwerem hello i hello urządzenia magazynującego. W przypadku awarii składnika, powodując toofail Ścieżka logiczna, logika wielościeżkowa używa ścieżki alternatywnej dla operacji We/Wy, dzięki czemu aplikacje mogą nadal uzyskiwać dostępu do danych. Ponadto w zależności od konfiguracji wielościeżkowego wejścia/wyjścia mogą także podnieść wydajność przez ponowne równoważenie obciążenia hello we wszystkich tych ścieżek. Aby uzyskać więcej informacji, zobacz [Omówienie wielościeżkowego wejścia/wyjścia](https://technet.microsoft.com/library/cc725907.aspx "wielościeżkowego wejścia/wyjścia Przegląd oraz funkcje").

W przypadku hello wysokiej dostępności rozwiązania StorSimple należy skonfigurować wielościeżkowego wejścia/wyjścia na powitania połączonych tooyour hostów Windows Server tablicy wirtualnego StorSimple (model 1200). następnie może tolerować Hello Serwery hosta, łącza, sieci lub interfejsu. 

Konieczne będzie toofollow tooconfigure te kroki wielościeżkowego wejścia/wyjścia: 

* Wymagania wstępne dotyczące konfiguracji
* Krok 1: Instalacja wielościeżkowego We/Wy na hoście systemu Windows Server hello
* Krok 2: Konfigurowanie wielościeżkowego wejścia/wyjścia dla woluminów StorSimple
* Krok 3: Woluminów StorSimple instalacji na hoście hello

Każdy z hello powyżej kroki omówione w hello następujące sekcje.

## <a name="prerequisites"></a>Wymagania wstępne
Ta sekcja zawiera szczegóły dotyczące wymagań wstępnych dotyczących hosta serwera Windows hello i wirtualnych tablica hello konfiguracji.

### <a name="on-windows-server-host"></a>Na hoście systemu Windows Server
* Upewnij się, że hoście z systemem Windows Server ma włączone 2 interfejsów sieciowych.

### <a name="on-storsimple-virtual-array"></a>W macierzy wirtualnego StorSimple
* Tablica wirtualnego Hello powinna być skonfigurowana jako serwer iSCSI. toolearn więcej, zobacz [Konfigurowanie wirtualnego tablicy jako serwer iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md). Jeden lub więcej interfejsów sieciowych powinna być włączona na powitania tablicy.   
* Interfejsy sieciowe Hello w sieci wirtualnej macierzy powinny być dostępne z hosta serwera Windows hello.
* Należy utworzyć jeden lub więcej woluminów na tablica wirtualne StorSimple. toolearn więcej, zobacz [Dodaj wolumin](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) na tablica wirtualne StorSimple. W tej procedurze w macierzy wirtualnego hello utworzono 3 (woluminy 1 lokalnie przypięty i 2 warstwowych jak pokazano poniżej).
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>Konfiguracja sprzętu dla tablicy wirtualnego StorSimple
na poniższym rysunku Hello przedstawiono hello konfiguracja sprzętu wysokiej dostępności i równoważenia obciążenia wielu ścieżek dla hostów Windows Server i tablicy wirtualnego StorSimple używane w tej procedurze.

![Konfiguracja sprzętu wielościeżkowego wejścia/wyjścia](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

Jak pokazano w powyższej ilustracji hello:

* Tablica wirtualnego StorSimple udostępniane w ramach funkcji Hyper-V jest urządzeniem active jednego węzła, skonfigurowany jako serwer iSCSI.
* Dwa interfejsy sieci wirtualnej są włączone w macierzy. W hello lokalnego interfejsu użytkownika sieci web macierzy wirtualnego, sprawdź, czy dwa interfejsy sieciowe są włączone przechodząc zbyt**ustawienia sieciowe** w sposób przedstawiony poniżej:
  
    ![Interfejsy sieciowe włączone 1200](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    Adresy hello IPv4 Uwaga hello włączone (Ethernet, Ethernet 2 domyślnie) interfejsy sieciowe i Zapisz do późniejszego użytku na hoście hello.
* Dwa interfejsy sieciowe są włączone na hoście z systemem Windows Server. Jeśli hello interfejsów podłączonego do hosta i tablicy znajdują się na hello tej samej podsieci, a następnie będzie 4 ścieżki dostępna. Było hello w tej procedurze. Jednak w przypadku każdego interfejsu w interfejsie hello tablicy i hosta w innej podsieci IP (i nie wzajemnie obsługują routing), to tylko 2 ścieżki będą dostępne.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Krok 1: Instalacja wielościeżkowego We/Wy na hoście systemu Windows Server hello
Wielościeżkowego wejścia/wyjścia jest opcjonalna funkcja w systemie Windows Server i nie jest instalowany domyślnie. Powinno być instalowane jako funkcja za pomocą Menedżera serwera. ukończenie tej funkcji na hoście z systemem Windows Server, tooinstall hello następujące procedury.

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Krok 2: Konfigurowanie wielościeżkowego wejścia/wyjścia dla woluminów StorSimple
Wielościeżkowe wejście/wyjście musi woluminów StorSimple tooidentify toobe skonfigurowany. tooconfigure woluminów StorSimple toorecognize wielościeżkowego wejścia/wyjścia, wykonaj hello następujące kroki.

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Krok 3: Woluminów StorSimple instalacji na hoście hello
Po skonfigurowaniu wielościeżkowego wejścia/wyjścia w systemie Windows Server woluminy tworzone na powitania StorSimple tablicy może być instalowany i następnie skorzystać z funkcji MPIO nadmiarowości. toomount woluminu, wykonywanie hello następujące kroki.

#### <a name="toomount-volumes-on-hello-host"></a>toomount woluminy na hoście hello
1. Otwórz hello **właściwości inicjatora iSCSI** okna na hoście serwera Windows hello. Przejdź za**Menedżera serwera > pulpit nawigacyjny > Narzędzia > inicjatora iSCSI**.
2. W hello **właściwości inicjatora iSCSI** okno dialogowe, kliknij przycisk **odnajdywania**, a następnie kliknij przycisk **odnajdowanie portalu obiektu docelowego**.
3. W hello **odnajdowanie portalu obiektu docelowego** okna dialogowego pozycję hello następujące:
   
    1. Wprowadź adres IP hello hello pierwszy interfejsu sieci włączone na tablica wirtualne StorSimple. Domyślnie to **Ethernet**. 
    2. Kliknij przycisk **OK** tooreturn toohello **właściwości inicjatora iSCSI** okno dialogowe.
     
    > [!IMPORTANT]
    > Jeśli używasz sieci prywatnej dla połączenia iSCSI, wprowadź adres IP hello hello danych portu, który jest połączony toohello sieci prywatnej.
     
4. Powtórz kroki 2 i 3 dla drugiego interfejsu sieciowego (na przykład, Ethernet 2) w macierzy. 
5. Wybierz hello **celów** kartę w hello **właściwości inicjatora iSCSI** okno dialogowe. Powierzchni każdego woluminu dla wirtualnego macierzy, powinien zostać wyświetlony jako miejsce docelowe w obszarze **wykryte obiekty docelowe**. W takim przypadku spowoduje odnalezienie trzy elementy docelowe (odpowiednich woluminów toothree).
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. Kliknij przycisk **Connect** tooestablish jako sesji iSCSI z macierzy wirtualne StorSimple. A **połączyć tooTarget** zostanie wyświetlone okno dialogowe. Wybierz hello **Włącz wielościeżkowe** pole wyboru. Kliknij przycisk **zaawansowane**.
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. W hello **Zaawansowane ustawienia** okna dialogowego pozycję hello następujące:                                        
   
    1. Na powitania **karty lokalnej** listy rozwijanej wybierz **inicjatora iSCSI firmy Microsoft**.
    2. Na powitania **IP inicjatora** listy rozwijanej, wybierz hello adres IP hosta hello.
    3. Na powitania **portalu obiektu docelowego** IP listy rozwijanej, wybierz hello IP interfejsu tablicy.
    4. Kliknij przycisk **OK** tooreturn toohello **właściwości inicjatora iSCSI** okno dialogowe.
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. Kliknij pozycję **Właściwości**. 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. W hello **właściwości** okno dialogowe, kliknij przycisk **dodać sesji**.
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. W hello **połączyć tooTarget** okno dialogowe, wybierz opcję hello **Włącz wielościeżkowe** pole wyboru. Kliknij przycisk **zaawansowane**.
11. W hello **Zaawansowane ustawienia** okno dialogowe:                                        
    
    1. Na powitania **karty lokalnej** listy rozwijanej, wybierz inicjatora iSCSI firmy Microsoft.

    2. Na powitania **IP inicjatora** listy rozwijanej, wybierz hello IP adres odpowiedniego toohello hosta. W takim przypadku jest nawiązywane na powitania tablicy tooa jeden interfejs sieci na hoście hello dwa interfejsy sieciowe. W związku z tym ten interfejs jest hello taki sam jak przewidzianego hello pierwszą sesję.

    3. Na powitania **docelowy adres IP portalu** listy rozwijanej, adresu IP wybierz hello hello drugi interfejs danych włączone na powitania tablicy.

    4. Kliknij przycisk **OK** okno dialogowe właściwości inicjatora iSCSI toohello tooreturn. Dodano drugi docelowej toohello sesji.
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. Po dodaniu hello potrzeby sesji (ścieżki) w hello **właściwości inicjatora iSCSI** okno dialogowe, wybierz hello docelowej i kliknij przycisk **właściwości**. Na karcie sesje hello hello **właściwości** okno dialogowe, Uwaga hello cztery sesji identyfikatorów, które odpowiadają toohello możliwych ścieżek permutacji. toocancel sesji, wybierz identyfikator sesji tooa dalej pole wyboru hello, a następnie kliknij przycisk **rozłączenia**.

    6. urządzenia tooview przedstawione w sesji, wybierz hello **urządzeń** kartę tooconfigure hello zasady wielościeżkowego wejścia/wyjścia dla wybranego urządzenia, kliknij przycisk **wielościeżkowego wejścia/wyjścia**.

    7. Witaj **szczegóły** zostanie wyświetlone okno dialogowe. Na powitania **wielościeżkowego wejścia/wyjścia** karcie można wybrać odpowiednie hello **zasady równoważenia obciążenia** ustawienia. Można również wyświetlić hello **Active** lub **wstrzymania** typu ścieżki.
12. Powtórz kroki od 8-11 tooadd dodatkowych sesji (ścieżki) toohello docelowej. Dwa interfejsy na hoście hello i dwa na tablicy wirtualnego hello możesz dodać łącznie cztery sesji dla każdego obiektu docelowego. 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. Konieczne będzie toorepeat te kroki dla każdego woluminu (powierzchni jako miejsce docelowe).
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. Otwórz **Zarządzanie komputerem** przechodząc zbyt**Menedżera serwera > pulpit nawigacyjny > Zarządzanie komputerem**. W okienku po lewej stronie powitania kliknij **magazynu > Zarządzanie dyskami**. Witaj woluminy utworzone na powitania tablicy wirtualnego StorSimple, które są widoczne toothis hosta zostanie wyświetlona w obszarze **Zarządzanie dyskami** jako nowe dyski.
15. Inicjowanie dysku hello i Utwórz nowy wolumin. W trakcie format hello wybierz rozmiar jednostki alokacji (AUS) 64 KB. Powtórz kroki powitania dla wszystkich dostępnych woluminów hello.
    
    ![Zarządzanie dyskami](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. W obszarze **Zarządzanie dyskami**, kliknij prawym przyciskiem myszy hello **dysku** i wybierz **właściwości**.
17. W hello **właściwości urządzenia dysku wielościeżkowe** okna dialogowego kliknij hello **wielościeżkowego wejścia/wyjścia** kartę.
    
    ![Właściwości dysku](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. W hello **Nazwa DSM** , kliknij przycisk **szczegóły** i sprawdź, czy parametry hello są toohello parametrów domyślnych. Parametry domyślne Hello są:
    
    * Ścieżka upewnij się, okres = 30
    * Liczba ponownych prób = 3
    * PDO Usuń okres = 20
    * Interwał ponawiania prób = 1
    * Sprawdź ścieżkę włączone = niezaznaczone.
    
    > [!NOTE]
    > **Nie należy modyfikować hello parametrów domyślnych.**
   
## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [przy użyciu hello tooadminister usługi Menedżer StorSimple urządzenia wirtualnego StorSimple tablica](storsimple-virtual-array-manager-service-administration.md).

