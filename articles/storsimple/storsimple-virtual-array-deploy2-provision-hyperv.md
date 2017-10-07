---
title: Tablica wirtualnego StorSimple w funkcji Hyper-V aaaProvision | Dokumentacja firmy Microsoft
description: "W tym samouczku drugi we wdrożeniu tablicy wirtualnego StorSimple obejmuje udostępniania wirtualnego tablicy w funkcji Hyper-V."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a>Wdrażanie tablicy wirtualnego StorSimple - Provision w funkcji Hyper-V
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a>Omówienie
W tym samouczku opisano, jak tooprovision wirtualne StorSimple tablicy na komputerze hosta z funkcją Hyper-V w systemie Windows Server 2012 R2, Windows Server 2012 lub Windows Server 2008 R2. Ten artykuł dotyczy wdrożenia toohello tablic wirtualnego StorSimple w portalu Azure i Microsoft Azure dla instytucji rządowych chmury.

Należy tooprovision uprawnienia administratora i konfigurowanie wirtualnego tablicy. Hello inicjowania obsługi administracyjnej i początkowej konfiguracji może potrwać około 10 minut toocomplete.

## <a name="provisioning-prerequisites"></a>Wymagania wstępne dotyczące inicjowania obsługi administracyjnej
Tutaj znajdziesz tooprovision wymagania wstępne hello wirtualnego tablicy na komputerze hosta z funkcją Hyper-V w systemie Windows Server 2012 R2, Windows Server 2012 lub Windows Server 2008 R2.

### <a name="for-hello-storsimple-device-manager-service"></a>Dla hello usługi Menedżer StorSimple urządzenia
Przed rozpoczęciem upewnij się, że:

* Zostały ukończone wszystkie kroki hello [Prepare hello portal dla tablicy wirtualnego StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).
* Obraz wirtualnego tablicy hello zostały pobrane dla funkcji Hyper-V z hello portalu Azure. Aby uzyskać więcej informacji, zobacz **krok 3: obraz wirtualnego tablicy hello pobrania** z [portal hello Prepare przewodnik tablicy wirtualnego StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).

  > [!IMPORTANT]
  > oprogramowanie Hello hello tablicy wirtualnego StorSimple można używać tylko z hello usługi Menedżer StorSimple urządzenia.
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a>Dla hello tablicy wirtualnego StorSimple
Przed wdrożeniem wirtualnego tablicy, upewnij się, że:

* Używany system dostępu tooa hosta funkcji Hyper-V w systemie Windows Server 2008 R2 lub nowszym, że może być tooa używane alokowanie urządzenia.
* system hosta Hello jest możliwe toodedicate hello następujących zasobów tooprovision tablica wirtualnego:

  * Co najmniej 4 rdzenie.
  * Co najmniej 8 GB pamięci RAM. Jeśli planujesz tooconfigure hello wirtualnego tablicy jako serwer plików, 8 GB obsługuje mniej niż 2 miliony plików. Należy 16 GB pamięci RAM toosupport 2-4 miliony plików.
  * Jeden interfejs sieciowy.
  * Dysk wirtualny 500 GB danych.

### <a name="for-hello-network-in-hello-datacenter"></a>Witaj sieci w centrum danych hello
Przed rozpoczęciem należy przejrzeć hello sieci toodeploy wymagania tablicą wirtualnego StorSimple i odpowiednio skonfigurować hello sieci centrum danych. Aby uzyskać więcej informacji, zobacz [tablicy wirtualnego StorSimple wymagań sieciowych](storsimple-ova-system-requirements.md#networking-requirements).

## <a name="step-by-step-provisioning"></a>Krok po kroku inicjowania obsługi administracyjnej
tooprovision i połączenia wirtualnej tablicy tooa, należy hello tooperform następujące kroki:

1. Upewnij się, że hello hosta system ma wystarczające zasoby toomeet hello minimalna tablicy wirtualnego wymagania.
2. Udostępnianie wirtualnych tablicy w Twojej funkcji hypervisor.
3. Uruchom tablicy wirtualnego hello i uzyskać adres IP hello.

Każdy z tych kroków zostało wyjaśnione w dokumencie hello następujące sekcje.

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a>Krok 1: Upewnij się, że systemu hosta hello spełnia wymagania minimalne wirtualnego tablicy
toocreate wirtualnego tablicy, potrzebne są:

* Rola Hello funkcji Hyper-V, w systemie Windows Server 2012 R2, Windows Server 2012 lub Windows Server 2008 R2 z dodatkiem SP1.
* Microsoft Hyper-V Manager na komputerze klienckim Microsoft Windows połączone toohello hosta.

Upewnij się, że w tym hello bazowy sprzętu (w systemie hosta), na którym tworzysz tablicy wirtualnego hello jest hello stanie toodedicate następujące zasoby tooyour wirtualnego tablicy:

* Co najmniej 4 rdzenie.
* Co najmniej 8 GB pamięci RAM. Jeśli planujesz tooconfigure hello wirtualnego tablicy jako serwer plików, 8 GB obsługuje mniej niż 2 miliony plików. Należy 16 GB pamięci RAM toosupport 2-4 miliony plików.
* Jeden interfejs sieciowy.
* Dysk wirtualny 500 GB danych systemu.

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a>Krok 2: Udostępnianie wirtualnych tablicy w funkcji hypervisor
Wykonaj następujące kroki tooprovision urządzenie w Twojej funkcji hypervisor hello.

#### <a name="tooprovision-a-virtual-array"></a>tooprovision wirtualnego tablicy
1. Na hoście z systemem Windows Server skopiuj hello wirtualnego tablicy obrazu tooa dysku. Pobrano tego obrazu (plik VHD lub VHDX) za pośrednictwem hello portalu Azure. Zanotuj lokalizację hello jest kopiowany obraz powitania korzystania z tego obrazu w dalszej części procedury hello.
2. Otwórz **Menedżera serwera**. W hello prawym górnym rogu, kliknij przycisk **narzędzia** i wybierz **Menedżera funkcji Hyper-V**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   Jeśli używasz systemu Windows Server 2008 R2 otwórz hello Menedżera funkcji Hyper-V. W Menedżerze serwera kliknij **ról > funkcji Hyper-V > Menedżera funkcji Hyper-V**.
3. W **Menedżera funkcji Hyper-V**w okienku zakresu hello, kliknij prawym przyciskiem myszy z menu kontekstowego hello tooopen systemu węzeł, a następnie kliknij **nowy** > **maszyny wirtualnej**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. Na powitania **przed rozpoczęciem** strony hello Kreatora nowej maszyny wirtualnej, kliknij przycisk **dalej**.
5. Na powitania **Określ nazwę i lokalizację** podaj **nazwa** dla sieci wirtualnej tablicy. Kliknij przycisk **Dalej**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. Na powitania **określić generację** , wybierz typ obrazu hello urządzenia, a następnie kliknij przycisk **dalej**. Ta strona nie zostanie wyświetlone, jeśli używasz systemu Windows Server 2008 R2.

   * Wybierz **generacji 2** Jeśli pobrany obraz vhdx dla systemu Windows Server 2012 lub nowszego.
   * Wybierz **generacja 1** Jeśli pobrano obrazu vhd systemu Windows Server 2008 R2 lub nowszym.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. Na powitania **przypisanie pamięci** określ **pamięć początkowa** z co najmniej **8192 MB**, nie włączać pamięci dynamicznej, a następnie kliknij przycisk **dalej**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. Na powitania **Konfigurowanie sieci** strony, określ hello przełącznikiem wirtualnym, który jest połączony toohello Internet, a następnie kliknij przycisk **dalej**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. Na powitania **Podłączanie wirtualnego dysku twardego** wybierz pozycję **Użyj istniejącego wirtualnego dysku twardego**, określ lokalizację hello hello wirtualnego tablicy obrazu (vhdx lub VHD), a następnie kliknij przycisk **dalej**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. Przejrzyj hello **Podsumowanie** , a następnie kliknij przycisk **Zakończ** maszyny wirtualnej hello toocreate.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. minimalne wymagania hello toomeet należy 4 rdzenie. tooadd 4 procesory wirtualne, wybierz system hosta w hello **Menedżera funkcji Hyper-V** okna. W hello prawym okienku w obszarze lista hello **maszyn wirtualnych**, odszukaj nowo utworzoną maszynę wirtualną hello. Wybierz i kliknij prawym przyciskiem myszy nazwę maszyny hello i wybierz **ustawienia**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. Na powitania **ustawienia** w lewym okienku hello, kliknij **procesora**. W prawym okienku hello, ustaw **liczba procesorów wirtualnych** too4 (lub więcej). Kliknij przycisk **Zastosuj**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. toomeet hello minimalne wymagania, należy również tooadd dysku wirtualnego danych 500 GB. W hello **ustawienia** strony:

    1. Wybierz w okienku po lewej stronie powitania **kontroler SCSI**.
    2. W okienku po prawej stronie powitania, wybierz **dysk twardy** i kliknij przycisk **Dodaj**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. Na powitania **dysk twardy** strona, wybierz hello **wirtualny dysk twardy** opcję i kliknij przycisk **nowy**. Witaj **Kreatora nowego wirtualnego dysku twardego** uruchamia.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. Na powitania **przed rozpoczęciem** strony hello Kreatora nowego wirtualnego dysku twardego kliknij **dalej**.
16. Na powitania **strona Wybieranie formatu dysku**, zaakceptuj domyślną opcją hello **VHDX** format. Kliknij przycisk **Dalej**. Ten ekran nie jest podana, jeśli system Windows Server 2008 R2.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. Na powitania **stronę Wybieranie typu dysku**, Ustaw typ wirtualnego dysku twardego jako **dynamicznie powiększających się** (zalecane). **Stały rozmiar** dysku będzie działać, ale może być konieczne toowait przez długi czas. Firma Microsoft zaleca, nie używaj hello **Differencing** opcji. Kliknij przycisk **Dalej**. W systemie Windows Server 2012 R2 i Windows Server 2012 **dynamicznie powiększających się** jest opcja domyślna hello w systemie Windows Server 2008 R2, jest domyślną hello **stały rozmiar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. Na powitania **Określanie nazwy i lokalizacji** podaj **nazwa** oraz **lokalizacji** (możesz przeglądać tooone) dla dysku danych hello. Kliknij przycisk **Dalej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. Na powitania **Konfigurowanie dysku** strony opcji wybierz hello **utworzyć nowy pusty wirtualny dysk twardy** i określ rozmiar hello jako **500 GB** (lub więcej). Chociaż 500 GB hello minimalne wymaganie, zawsze można udostępnić większy dysk. Należy pamiętać, nie można rozwinąć lub zmniejszania dysku hello raz udostępniane. Aby uzyskać więcej informacji o rozmiar hello tooprovision dysku, zapoznaj się z sekcją zmiany rozmiaru hello w hello [najlepszych praktyk dokumentu](storsimple-ova-best-practices.md). Kliknij przycisk **Dalej**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. Na powitania **Podsumowanie** , przejrzyj szczegóły hello dysku wirtualnego danych i jeśli spełnione, kliknij przycisk **Zakończ** toocreate hello dysku. Kreator Hello zamyka i wirtualny dysk twardy jest dodawany tooyour maszyny.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. Zwraca toohello **ustawienia** strony. Kliknij przycisk **OK** tooclose hello **ustawienia** strony i powrócić do okna Menedżera tooHyper-V.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a>Krok 3: Uruchom tablicy wirtualnego hello i otrzymać hello adres IP
Wykonaj następujące kroki toostart hello tablica wirtualnego i połącz tooit.

#### <a name="toostart-hello-virtual-array"></a>toostart hello wirtualnego tablicy
1. Uruchom hello wirtualnego tablicy.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. Po uruchomieniu urządzenia hello wybierz hello urządzenie, kliknij prawym przyciskiem myszy, a następnie wybierz **Connect**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. Konieczne może być toowait 5 – 10 minut toobe urządzenia hello jest gotowy. Komunikat o stanie jest wyświetlany na powitania konsoli tooindicate hello postępu. Po hello urządzenie jest gotowe, przejdź zbyt**akcji**. Naciśnij klawisz `Ctrl + Alt + Delete` toolog toohello wirtualnego tablicy. Użytkownik domyślny Hello *StorSimpleAdmin* i hello domyślne hasło jest *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. Ze względów bezpieczeństwa hasło administratora urządzenia hello wygasa przy pierwszym logowaniu hello. Jesteś toochange zostanie wyświetlony monit o hasło hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   Wprowadź hasło o długości co najmniej 8 znaków. Witaj hasło musi spełniać wymagania co najmniej 3 poza hello wymogów 4: wielkie litery, małe litery, liczbowego i znaki specjalne. Wprowadź ponownie tooconfirm hasło hello go. Użytkownik jest powiadamiany, że to hasło hello została zmieniona.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. Po pomyślnym zmianie hasła hello hello wirtualnego tablicy może uruchamiać ponownie. Poczekaj na powitania toostart urządzenia.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    Witaj konsoli środowiska Windows PowerShell hello urządzenia zostanie wyświetlona wraz z pasek postępu.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. Kroki od 6 do 8 stosowane tylko wtedy, gdy rozruch w środowisku protokołu DHCP. Jeśli pracujesz w środowisku DHCP, Pomiń te kroki i przejdź toostep 9. Jeśli uruchomiono zapasowych urządzenia w środowisku protokołu DHCP, zostanie wyświetlony po ekranie powitania.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    Skonfiguruj hello sieci.
7. Użyj hello `Get-HcsIpAddress` polecenia interfejsów sieciowych hello toolist włączone tablica wirtualnego. Jeśli urządzenie ma jednym interfejsem sieciowym włączone, jest hello domyślna nazwa przypisana toothis interfejsu `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. Użyj hello `Set-HcsIpAddress` sieci hello tooconfigure polecenia cmdlet. Zobacz poniższy przykład hello:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. Po zakończeniu początkowej konfiguracji hello i urządzenia hello uruchomi się w górę, pojawi się tekst transparentu hello urządzenia. Zanotuj adres IP hello i hello adres URL wyświetlany w hello transparent tekst toomanage hello urządzenia. Użyj tego adresu IP adres tooconnect toohello interfejsu użytkownika sieci web tablicy wirtualnego i instalacji lokalne powitania pełną i rejestracji.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. (Opcjonalnie) Wykonaj ten krok tylko wtedy, gdy wdrażasz urządzenia w hello chmury dla instytucji rządowych. Teraz umożliwi hello tryb Stanów Zjednoczonych informacji przetwarzania Standard FIPS (Federal) na urządzeniu. standard Hello FIPS 140 definiuje zatwierdzone do użycia przez nas federalne systemów komputerowych dla instytucji rządowych hello ochrony danych poufnych algorytmów kryptograficznych.

    1. tooenable hello trybie FIPS, uruchom następujące polecenie cmdlet hello:

        `Enable-HcsFIPSMode`
    2. Po włączeniu trybu FIPS hello tak, aby hello kryptograficzne operacji sprawdzania poprawności zostały zastosowane, należy zrestartować urządzenie.

       > [!NOTE]
       > Można włączyć lub wyłączyć tryb FIPS na urządzeniu. Przemienne urządzenie hello między trybem FIPS i z systemem innym niż FIPS nie jest obsługiwane.
       >
       >

Jeśli urządzenie nie spełnia wymagań minimalnej konfiguracji hello, zobaczysz hello następujący błąd w tekst transparentu hello (pokazana poniżej). Zmodyfikuj konfigurację urządzenia hello, tak, aby hello maszyny toomeet odpowiednie zasoby hello wymagania minimalne. Następnie można ponownie uruchomić i podłącz urządzenie toohello. Zobacz toohello minimalne wymagania dotyczące konfiguracji w [krok 1: Upewnij się, że systemu hosta hello spełnia wymagania minimalne tablicy wirtualnego](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

Jeśli inny błąd czoła podczas konfiguracji początkowej hello przy użyciu lokalne powitania interfejsu użytkownika sieci web, można znaleźć toohello przepływów pracy po:

* Uruchamianie testów diagnostycznych zbyt[Rozwiązywanie problemów z instalacją interfejsu użytkownika sieci web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Generowanie pakietu dziennika i wyświetlanie plików dziennika](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Następne kroki
* [Konfigurowanie tablica wirtualnego StorSimple jako serwer plików](storsimple-virtual-array-deploy3-fs-setup.md)
* [Konfigurowanie tablica wirtualnego StorSimple iSCSI na serwerze](storsimple-virtual-array-deploy3-iscsi-setup.md)
