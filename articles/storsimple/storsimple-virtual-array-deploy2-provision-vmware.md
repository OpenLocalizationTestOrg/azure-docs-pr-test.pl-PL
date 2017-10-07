---
title: "aaaProvision tablicy wirtualnego StorSimple w środowisku programu VMware | Dokumentacja firmy Microsoft"
description: "W tym samouczku drugi w tablicy wirtualnego StorSimple wdrażania serii obejmuje Inicjowanie obsługi urządzenia wirtualnego w środowisku programu VMware."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a>Wdrażanie tablicy wirtualnego StorSimple - Provision w środowisku programu VMware
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a>Omówienie
Ten przewodnik opisuje sposób tooprovision i połącz tooa tablicy wirtualnego StorSimple na komputerze hosta z systemem VMware ESXi 5.5 lub nowszym. Ten artykuł dotyczy wdrożenia toohello tablic wirtualnego StorSimple w portalu Azure i hello Microsoft Azure dla instytucji rządowych chmury.

Należy tooprovision uprawnienia administratora i połączyć tooa urządzenia wirtualnego. Hello inicjowania obsługi administracyjnej i początkowej konfiguracji może potrwać około 10 minut toocomplete.

## <a name="provisioning-prerequisites"></a>Wymagania wstępne dotyczące inicjowania obsługi administracyjnej
Witaj tooprovision wymagania wstępne urządzenia wirtualnego na komputerze hosta z systemem VMware ESXi 5.5 i powyżej, są następujące.

### <a name="for-hello-storsimple-device-manager-service"></a>Dla hello usługi Menedżer StorSimple urządzenia
Przed rozpoczęciem upewnij się, że:

* Zostały ukończone wszystkie kroki hello [Prepare hello portal dla tablicy wirtualnego StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).
* Pobrano hello obrazu urządzenia wirtualnego dla VMware z hello portalu Azure. Aby uzyskać więcej informacji, zobacz **krok 3: obrazu urządzenia wirtualnego hello pobierania** z [portal hello Prepare przewodnik tablicy wirtualnego StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).

### <a name="for-hello-storsimple-virtual-device"></a>Dla urządzenia wirtualnego StorSimple hello
Przed wdrożeniem urządzenia wirtualnego, upewnij się, że:

* Używany system dostępu tooa hosta funkcji Hyper-V (2008 R2 lub nowszy) czy można być używane tooa udostępnić urządzenia.
* system hosta Hello jest możliwe toodedicate hello następujących zasobów tooprovision urządzenia wirtualnego:

  * Co najmniej 4 rdzenie.
  * Co najmniej 8 GB pamięci RAM. Jeśli planujesz tooconfigure hello wirtualnego tablicy jako serwer plików, 8 GB obsługuje mniej niż 2 miliony plików. Należy 16 GB pamięci RAM toosupport 2-4 miliony plików.
  * Jeden interfejs sieciowy.
  * Dysk wirtualny 500 GB danych systemu.

### <a name="for-hello-network-in-datacenter"></a>Witaj sieci w centrum danych
Przed rozpoczęciem upewnij się, że:

* Należy przejrzeć wymagania dotyczące sieci hello toodeploy urządzenia wirtualnego StorSimple i sieci centrum danych hello skonfigurowane zgodnie z wymaganiami hello. 

## <a name="step-by-step-provisioning"></a>Krok po kroku inicjowania obsługi administracyjnej
tooprovision i podłącz urządzenie wirtualne tooa, należy hello tooperform następujące kroki:

1. Upewnij się, że hello hosta system ma wystarczające zasoby toomeet hello wymagania minimalne urządzenia wirtualnego.
2. Udostępnianie w funkcji hypervisor, Twoje urządzenie wirtualne.
3. Uruchom hello wirtualne urządzenie i uzyskać adres IP hello.

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a>Krok 1: Upewnij się, że system hosta spełnia wymagania minimalne urządzenia wirtualnego
toocreate urządzenie wirtualne, potrzebne są:

* Dostęp tooa hosta z systemem VMware ESXi Server 5.5 lub nowszego.
* VMware vSphere klienta na hoście ESXi hello toomanage systemu.

  * Co najmniej 4 rdzenie.
  * Co najmniej 8 GB pamięci RAM. Jeśli planujesz tooconfigure hello wirtualnego tablicy jako serwer plików, 8 GB obsługuje mniej niż 2 miliony plików. Należy 16 GB pamięci RAM toosupport 2-4 miliony plików.
  * Jeden interfejs sieciowy połączone sieci toohello stanie routingu tooInternet ruchu. Witaj minimalnej przepustowości Internetu powinien być 5 MB/s tooallow optymalną funkcjonowania hello urządzenia.
  * Dysk wirtualny 500 GB danych.

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a>Krok 2: Udostępnianie urządzenie wirtualne w ramach funkcji hypervisor
Wykonaj hello następujące kroki tooprovision w funkcji hypervisor, Twoje urządzenie wirtualne.

1. Kopiowanie obrazu urządzenia wirtualnego hello w tym systemie. Możesz pobrać ten obraz wirtualnych za pośrednictwem portalu Azure hello.

   1. Upewnij się, pobrano hello najnowszego pliku obrazu. Jeśli wcześniej pobrano obraz powitania, pobierz go ponownie tooensure masz najnowszą obraz powitania. Obraz najnowsze Hello ma dwa plików (zamiast jeden).
   2. Zanotuj lokalizację hello jest kopiowany obraz powitania korzystania z tego obrazu w dalszej części procedury hello.

2. Zaloguj się za toohello ESXi serwera przy użyciu hello vSphere klienta. Należy toocreate uprawnień administratora toohave maszyny wirtualnej.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. W kliencie vSphere hello, w sekcji spisu hello w okienku po lewej stronie powitania wybierz hello ESXi serwera.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. Przekaż hello VMDK toohello ESXi serwera. Przejdź toohello **konfiguracji** karty w okienku po prawej stronie powitania. W obszarze **sprzętu**, wybierz pozycję **magazynu**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. W hello prawym okienku w obszarze **Datastores**, wybierz hello magazynu danych, w którym ma tooupload hello VMDK. Magazyn danych Hello musi mieć wystarczającą ilość wolnego miejsca dla hello systemu operacyjnego i dysków z danymi.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. Kliknij prawym przyciskiem myszy i wybierz **Przeglądaj Datastore**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. A **przeglądarki Datastore** zostanie wyświetlone okno.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. Na pasku narzędzi hello, kliknij ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) toocreate ikonę Nowy folder. Podaj nazwę folderu hello i zapisz go. Ta nazwa folderu będzie używana później, podczas tworzenia maszyny wirtualnej (najlepsze rozwiązanie zalecane). Kliknij przycisk **OK**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. Witaj zostanie wyświetlony nowy folder w okienku po lewej stronie powitania hello **przeglądarki Datastore**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. Kliknij ikonę przekazywania hello ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) i wybierz **Przekaż plik**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. Przeglądaj i wybierz polecenie pliki VMDK toohello został pobrany. Istnieją dwa pliki. Wybierz tooupload pliku.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. Kliknij przycisk **Otwórz**. przekazywanie Hello toohello pliku VMDK hello określony magazynu danych uruchamia. Może upłynąć kilka minut tooupload pliku hello.
13. Po zakończeniu przekazywania hello znajduje się pliku hello w datastore hello w folderze hello, który został utworzony.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    Teraz Przekaż hello drugi toohello pliku VMDK tego samego magazynu danych.
14. Zwraca toohello vSphere klienta okna. ESXi wybranego serwera, kliknij prawym przyciskiem myszy i wybierz **nowej maszyny wirtualnej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. A **tworzenia nowej maszyny wirtualnej** pojawi się okno. Na powitania **konfiguracji** strona, wybierz hello **niestandardowy** opcji. Kliknij przycisk **Dalej**.
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. Na powitania **nazwy i lokalizacji** Określ hello nazwę maszyny wirtualnej. Ta nazwa powinna być zgodna nazwa folderu hello (zalecane) określone wcześniej w kroku 8.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. Na powitania **magazynu** wybierz magazyn danych ma toouse tooprovision maszyny Wirtualnej.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. Na powitania **wersją maszyny wirtualnej** wybierz pozycję **wersją maszyny wirtualnej: 8**. W wersji 8 too11 są obsługiwane.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. Na powitania **systemu operacyjnego gościa** strona, wybierz hello **systemu operacyjnego gościa** jako **Windows**. Dla **wersji**, wybierz z listy rozwijanej hello **Microsoft Windows Server 2012 (64-bitowy)**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. Na powitania **procesorów** pozycję Dostosuj hello **liczbę gniazd wirtualnego** i **liczba rdzeni na gniazdo wirtualnego** , który hello **łączna liczba rdzeni**4 (lub więcej). Kliknij przycisk **Dalej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. Na powitania **pamięci** Określ 8 GB lub więcej pamięci RAM. Kliknij przycisk **Dalej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. Na powitania **sieci** Określ hello liczba interfejsów sieciowych hello. Witaj, minimalna wymagana wartość to jeden interfejs sieciowy.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. Na powitania **kontroler SCSI** pozycję Zaakceptuj domyślną hello **kontrolera LSI Logic SAS**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. Na powitania **wybierz dysk** wybierz pozycję **Użyj istniejącego dysku wirtualnego**. Kliknij przycisk **Dalej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. Na powitania **wybierz istniejący dysk** w obszarze **ścieżkę pliku dysku**, kliknij przycisk **Przeglądaj**. Spowoduje to otwarcie **Przeglądaj Datastores** okna dialogowego. Przejdź toohello lokalizacji, gdzie przekazać hello VMDK. Teraz widać tylko jeden plik w hello magazynu danych jako hello dwóch plików, które początkowo przekazać zostały scalone. Wybierz plik hello, a następnie kliknij przycisk **OK**. Kliknij przycisk **Dalej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. Na powitania **zaawansowane opcje** , zaakceptuj wartość domyślną hello i kliknij przycisk **dalej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. Na powitania **tooComplete gotowe** Przejrzyj wszystkie ustawienia hello skojarzone z hello nowej maszyny wirtualnej. Sprawdź **edytować ustawienia maszyny wirtualnej hello przed ukończeniem**. Kliknij przycisk **kontynuować**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. Na powitania **właściwości maszyny wirtualnej** strony w hello **sprzętu** zlokalizuj hello urządzeń sprzętowych. Wybierz **nowy dysk twardy**. Kliknij pozycję **Dodaj**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. Zostanie wyświetlony **dodawania sprzętu** okna. Na powitania **typu urządzenia** w obszarze **hello wybierz typ urządzenia mają tooadd**, wybierz pozycję **dysku twardego**i kliknij przycisk **dalej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. Na powitania **wybierz dysk** wybierz pozycję **tworzenia nowego dysku wirtualnego**. Kliknij przycisk **Dalej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. Na powitania **Tworzenie dysku** Zmień hello **rozmiar dysku** too500 GB (lub więcej). Chociaż 500 GB hello minimalne wymaganie, zawsze można udostępnić większy dysk. Należy pamiętać, nie można rozwinąć lub zmniejszania dysku hello raz udostępniane. Aby uzyskać więcej informacji o rozmiar hello tooprovision dysku, zapoznaj się z sekcją zmiany rozmiaru hello w hello [najlepszych praktyk dokumentu](storsimple-ova-best-practices.md). W obszarze **udostępniania dysku**, wybierz pozycję **alokacji elastycznej**. Kliknij przycisk **Dalej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. Na powitania **zaawansowane opcje** pozycję Zaakceptuj domyślną hello.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. Na powitania **tooComplete gotowe** Przejrzyj opcje dysku hello. Kliknij przycisk **Zakończ**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. Zwraca toohello strony właściwości maszyny wirtualnej. Nowy dysk twardy jest dodawana tooyour maszyny wirtualnej. Kliknij przycisk **Zakończ**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. Z maszyny wirtualnej wybrany w okienku po prawej stronie powitania, przejdź toohello **Podsumowanie** kartę. Przejrzyj ustawienia hello maszyny wirtualnej.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

Maszyna wirtualna jest teraz udostępniony. Witaj, następnym krokiem jest toopower na tym komputerze i uzyskać adres IP hello.

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a>Krok 3: Uruchom urządzenie wirtualne hello i otrzymać hello adres IP
Wykonaj następujące kroki toostart hello urządzenia wirtualnego i połącz tooit.

#### <a name="toostart-hello-virtual-device"></a>Urządzenie wirtualne hello toostart
1. Uruchom hello urządzenia wirtualnego. W vSphere hello programu Configuration Manager w okienku po lewej stronie powitania wybierz urządzenie i kliknij prawym przyciskiem myszy toobring hello menu kontekstowego. Wybierz **zasilania** , a następnie wybierz **włączają**. Powinno to zasilania na maszynie wirtualnej. Stan hello widoczny u dołu hello **ostatnich zadań** okienko hello vSphere klienta.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. zadania konfiguracji Hello potrwa kilka minut toocomplete. Po uruchomieniu urządzenia hello Przejdź toohello **konsoli** kartę. Wyślij toolog Ctrl + Alt + Delete toohello urządzenia. Alternatywnie można punktu kursora hello na powitania okno konsoli i naciśnij klawisze Ctrl + Alt + Insert. Użytkownik domyślny Hello *StorSimpleAdmin* i hello domyślne hasło jest *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. Ze względów bezpieczeństwa hasło administratora urządzenia hello wygasa przy pierwszym logowaniu hello. Jesteś toochange zostanie wyświetlony monit o hasło hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. Wprowadź hasło o długości co najmniej 8 znaków. Witaj hasło musi zawierać 3 z 4 z tych wymagań: wielkie litery, małe litery, liczbowego i znaki specjalne. Wprowadź ponownie tooconfirm hasło hello go. Dowiesz się, że to hasło hello została zmieniona.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. Po pomyślnym zmianie hasła hello hello urządzenie wirtualne może zostać uruchomiony ponownie. Poczekaj na powitania toocomplete ponowne uruchomienie komputera. konsoli programu Windows PowerShell Hello hello urządzenia mogą być wyświetlane wraz z pasek postępu.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. Kroki od 6 do 8 stosowane tylko wtedy, gdy rozruch w środowisku protokołu DHCP. Jeśli pracujesz w środowisku DHCP, Pomiń te kroki i przejdź toostep 9. Jeśli uruchomiono zapasowych urządzenia w środowisku protokołu DHCP, zostanie wyświetlony po ekranie powitania.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   Skonfiguruj hello sieci.
7. Użyj hello `Get-HcsIpAddress` polecenia interfejsów sieciowych hello toolist włączone na urządzeniu wirtualnym. Jeśli urządzenie ma jednym interfejsem sieciowym włączone, jest hello domyślna nazwa przypisana toothis interfejsu `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. Użyj hello `Set-HcsIpAddress` sieci hello tooconfigure polecenia cmdlet. Poniżej przedstawiono przykład:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. Po zakończeniu początkowej konfiguracji hello i urządzenia hello uruchomi się w górę, pojawi się tekst transparentu hello urządzenia. Zanotuj adres IP hello i hello adres URL wyświetlany w hello transparent tekst toomanage hello urządzenia. Użyje tego adresu IP adres tooconnect toohello interfejsu użytkownika sieci web urządzenia wirtualnego i instalacji lokalne powitania pełną i rejestracji.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. (Opcjonalnie) Wykonaj ten krok tylko wtedy, gdy wdrażasz urządzenia w hello chmury dla instytucji rządowych. Teraz umożliwi hello tryb Stanów Zjednoczonych informacji przetwarzania Standard FIPS (Federal) na urządzeniu. standard Hello FIPS 140 definiuje zatwierdzone do użycia przez nas federalne systemów komputerowych dla instytucji rządowych hello ochrony danych poufnych algorytmów kryptograficznych.

    1. tooenable hello trybie FIPS, uruchom następujące polecenie cmdlet hello:

        `Enable-HcsFIPSMode`
    2. Po włączeniu trybu FIPS hello tak, aby hello kryptograficzne operacji sprawdzania poprawności zostały zastosowane, należy zrestartować urządzenie.

       > [!NOTE]
       > Można włączyć lub wyłączyć tryb FIPS na urządzeniu. Przemienne urządzenie hello między trybem FIPS i z systemem innym niż FIPS nie jest obsługiwane.
       >
       >

Jeśli urządzenie nie spełnia wymagań minimalnej konfiguracji hello, zostanie wyświetlony błąd w tekst transparentu hello (pokazana poniżej). Konfiguracja urządzenia hello toomodify należy tak, że ma ona odpowiednie zasoby toomeet hello minimalne wymagania. Następnie można ponownie uruchomić i podłącz urządzenie toohello. Zobacz toohello minimalne wymagania dotyczące konfiguracji w [krok 1: Upewnij się, że system hosta hello spełnia wymagania minimalne urządzenia wirtualnego](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

Jeśli inny błąd czoła podczas konfiguracji początkowej hello przy użyciu lokalne powitania interfejsu użytkownika sieci web, można znaleźć toohello przepływów pracy po:

* Uruchamianie testów diagnostycznych zbyt[Rozwiązywanie problemów z instalacją interfejsu użytkownika sieci web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Generowanie pakietu dziennika i wyświetlanie plików dziennika](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Następne kroki
* [Konfigurowanie tablica wirtualnego StorSimple jako serwer plików](storsimple-virtual-array-deploy3-fs-setup.md)
* [Konfigurowanie tablica wirtualnego StorSimple iSCSI na serwerze](storsimple-virtual-array-deploy3-iscsi-setup.md)
