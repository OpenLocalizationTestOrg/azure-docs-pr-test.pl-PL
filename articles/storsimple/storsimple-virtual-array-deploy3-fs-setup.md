---
title: "aaaSet się StorSimple tablicy wirtualnego jako serwer plików | Dokumentacja firmy Microsoft"
description: "W tym samouczku trzeci we wdrożeniu tablicy wirtualnego StorSimple nakazuje tooset urządzenia wirtualnego jako serwer plików."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: f609f6ff-0927-48bb-a68a-6d8985d2fe34
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89cade37980f342695c0adee42c4ade0e1d53d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---set-up-as-file-server-via-azure-portal"></a>Wdrożenie tablicy wirtualne StorSimple - zestawu się jako serwera plików za pośrednictwem portalu Azure
![](./media/storsimple-virtual-array-deploy3-fs-setup/fileserver4.png)

## <a name="introduction"></a>Wprowadzenie
W tym artykule opisano sposób tooperform początkowej konfiguracji zarejestrować StorSimple serwera plików konfiguracji urządzenia hello pełną i utworzyć i połączyć tooSMB udziałów. To jest artykuł ostatniego hello hello serii samouczków wdrożenia wymagane toocompletely wdrażania wirtualnego tablica jako serwera plików lub serwera iSCSI.

Witaj instalacji i konfiguracji może potrwać około 10 minut toocomplete. Hello informacje w tym artykule dotyczą tylko toohello wdrożenie hello tablicy wirtualne StorSimple. Witaj wdrażania urządzeń z serii StorSimple 8000, przejdź do: [wdrażania urządzenia serii StorSimple 8000 z aktualizacją Update 2](storsimple-deployment-walkthrough-u2.md).

## <a name="setup-prerequisites"></a>Wymagania wstępne instalacji
Przed skonfigurowaniem i konfigurowanie macierzy wirtualnego StorSimple, upewnij się, że:

* Po uprzednim udostępnieniu wirtualnego tablicy i połączone tooit jako hello szczegółowe w [udostępnić tablicą wirtualnego StorSimple w funkcji Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) lub [udostępnić tablicą wirtualnego StorSimple w środowisku programu VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
* Masz hello klucz rejestracji usługi z usługi Menedżer StorSimple urządzenia hello utworzony tablice wirtualnego StorSimple toomanage. Aby uzyskać więcej informacji, zobacz [krok 2: Pobierz klucz rejestracji usługi hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) dla tablicy wirtualne StorSimple.
* Jeśli jest to hello drugi lub kolejny wirtualnego tablica, która rejestrujesz istniejącą usługę Menedżer urządzeń StorSimple, powinien mieć klucz szyfrowania danych usługi hello. Ten klucz został wygenerowany podczas pierwszego urządzenia hello został pomyślnie zarejestrowany z tą usługą. W przypadku utraty tego klucza, zobacz [klucza szyfrowania danych usługi hello Get](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) dla macierzy wirtualne StorSimple.

## <a name="step-by-step-setup"></a>Krok po kroku instalacji
Użyj hello kontynuacji tooset instrukcje krok po kroku i skonfiguruj tablica wirtualne StorSimple.

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Krok 1: Zakończenie lokalnego hello ustawienia interfejsu użytkownika sieci web i rejestrowanie urządzenia
#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete hello Instalatora i rejestrowanie urządzenia hello
1. Otwórz okno przeglądarki i Połącz z lokalnym toohello interfejsu użytkownika sieci web. Wpisz:
   
   `https://<ip-address of network interface>`
   
   Użyj adresu URL połączenia hello zanotowanym w poprzednim kroku hello. Zostanie wyświetlony komunikat o błędzie informujący, że występuje problem z certyfikatem zabezpieczeń witryny sieci Web hello. Kliknij przycisk **kontynuować toothis strony sieci Web**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image2.png)
2. Interfejs użytkownika sieci wirtualnych tablicy jako sieci web logowania toohello **StorSimpleAdmin**. Wprowadź hasło administratora urządzenia hello, który został zmodyfikowany w kroku 3: Start hello wirtualnego tablicy w [udostępnić tablicą wirtualnego StorSimple w funkcji Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) lub [udostępnić tablicą wirtualnego StorSimple w środowisku programu VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image3.png)
3. Podjęto toohello **Home** strony. Na tej stronie opisano hello różne ustawienia wymagane tooconfigure i rejestr wirtualny tablicy przy użyciu usługi Menedżer StorSimple urządzenia hello hello. Witaj **ustawień sieciowych**, **ustawienia serwera proxy w sieci Web**, i **ustawienia** są opcjonalne. Witaj tylko wymagane ustawienia to **ustawienia urządzenia** i **ustawienia funkcji Cloud**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image4.png)
4. W hello **ustawień sieciowych** w obszarze **interfejsy sieciowe**, dane 0 zostaną automatycznie skonfigurowane dla Ciebie. Każdy interfejs sieciowy jest ustawiana przez domyślny adres IP tooget automatycznie (DHCP). W związku z tym adresem IP, podsieci i bramy są automatycznie przypisywane (dla protokołów IPv4 i IPv6).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image5.png)
   
   Jeśli podczas inicjowania obsługi administracyjnej urządzeniu hello hello dodano więcej niż jeden interfejs sieciowy, można je skonfigurować w tym miejscu. Należy pamiętać, że interfejsu sieciowego można skonfigurować jako IPv4 tylko lub jako protokołów IPv4 i IPv6. Konfiguracje tylko protokół IPv6 nie są obsługiwane.
5. Serwery DNS są wymagane, ponieważ są one używane urządzenia próbujący toocommunicate z dostawców usługi magazynu w chmurze lub tooresolve urządzenia według nazwy, gdy jest skonfigurowany jako serwer plików. W hello **ustawień sieciowych** w obszarze hello **serwerów DNS**:
   
   1. Podstawowego i pomocniczego serwera DNS są automatycznie konfigurowane. Jeśli wybierzesz tooconfigure statycznych adresów IP, można określić serwerów DNS. Wysokiej dostępności firma Microsoft zaleca, aby skonfigurować podstawowy i pomocniczy serwer DNS.
   2. Kliknij przycisk **Zastosuj** tooapply i sprawdź poprawność ustawień sieciowych hello.
6. W hello **ustawienia urządzenia** strony:
   
   1. Przypisz unikatowy **nazwa** tooyour urządzenia. Ta nazwa może być 1 – 15 znaków i może zawierać litery, cyfry i łączniki.
   2. Kliknij przycisk hello **serwera plików** ikona ![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png) dla hello **typu** urządzenia, które tworzysz. Serwer plików pozwoli toocreate udostępnione foldery.
   3. Urządzenie jest dostępna na serwerze plików, konieczne będzie toojoin hello urządzenia tooa domeny. Wprowadź **nazwy domeny**.
   4. Kliknij przycisk **Zastosuj**.
7. Zostanie wyświetlone okno dialogowe. Wprowadź swoje poświadczenia domeny w określonym formacie hello. Kliknij ikonę znacznika wyboru hello. poświadczenia domeny Hello są weryfikowane. Zostanie wyświetlony komunikat o błędzie, jeśli hello poświadczenia są nieprawidłowe.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image7.png)
8. Kliknij przycisk **Zastosuj**. Spowoduje to zastosowanie i sprawdź poprawność ustawień urządzenia hello.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image8.png)
   
   > [!NOTE]
   > Sprawdź, czy tablica wirtualnej jest w jego własnej jednostce organizacyjnej (OU) usługi Active Directory i żadne obiekty zasad grupy (GPO) są stosowane tooit lub dziedziczone. Zasad grupy może zainstalować aplikacje, takie jak oprogramowanie antywirusowe na powitania tablicy wirtualne StorSimple. Instalowanie dodatkowego oprogramowania nie jest obsługiwana i może spowodować uszkodzenie toodata. 
   > 
   > 
9. (Opcjonalnie) skonfiguruj serwer proxy sieci web. Mimo że konfiguracja serwera proxy sieci web jest opcjonalne, należy pamiętać, że jeśli używasz serwera proxy sieci web, można skonfigurować tylko go tutaj.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image9.png)
   
   W hello **serwer proxy sieci Web** strony:
   
   1. Podaj hello **adres URL serwera proxy sieci Web** w następującym formacie: *http://&lt;adres IP hosta lub FDQN&gt;: numer portu*. Należy pamiętać, że adresy URL HTTPS nie są obsługiwane.
   2. Określ **uwierzytelniania** jako **podstawowe** lub **Brak**.
   3. Jeśli przy użyciu uwierzytelniania, należy również tooprovide **Username** i **hasło**.
   4. Kliknij przycisk **Zastosuj**. Spowoduje to zweryfikować i zastosowania ustawień serwera proxy sieci web hello skonfigurowane.
10. (Opcjonalnie) skonfiguruj ustawienia godziny hello urządzenia, na przykład strefa czasowa i hello podstawowe i pomocnicze serwery NTP. Serwery NTP są wymagane, ponieważ urządzenie musi synchronizować czas, aby zapewnić możliwość uwierzytelnienia z dostawcy usług w chmurze.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/image10.png)
    
    W hello **ustawienia** strony:
    
    1. Z listy rozwijanej hello, wybierz hello **strefy czasowej** oparte na powitania lokalizacji geograficznej, w których hello jest wdrażane urządzenie. Witaj domyślną strefę czasową dla Twojego urządzenia jest PST. Wszystkie zaplanowane operacje urządzenia będą wykonywane w ramach tej strefy czasowej.
    2. Określ **podstawowy serwer NTP** dla urządzenia lub zaakceptuj wartość domyślną hello time.windows.com. Upewnij się, że sieć zezwala toopass ruch NTP z sieci centrum danych toohello Internet.
    3. Opcjonalnie można określić **serwera NTP dodatkowej** dla danego urządzenia.
    4. Kliknij przycisk **Zastosuj**. Spowoduje to zweryfikować i zastosowanie hello skonfigurowane ustawienia czasu.
11. Skonfiguruj ustawienia chmury hello urządzenia. W tym kroku zostanie ukończenie konfiguracji urządzenia lokalne powitania, a następnie zarejestruj urządzenie hello usługi Menedżer StorSimple urządzenia.
    
    1. Wprowadź hello **klucz rejestracji usługi** pochodzący [krok 2: Pobierz klucz rejestracji usługi hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) dla tablicy wirtualne StorSimple.
    2. Jeśli jest to pierwszy urządzenia rejestrowania za pomocą tej usługi, użytkownik zobaczy hello **klucza szyfrowania danych usługi**. Skopiuj ten klucz i zapisz go w bezpiecznym miejscu. Ten klucz jest wymagany w przypadku hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple urządzenia. 
       
       Jeśli nie jest to pierwsze urządzenie hello, który rejestrujesz się z tą usługą, konieczne będzie klucza szyfrowania danych usługi hello tooprovide. Aby uzyskać więcej informacji, zobacz tooget hello [klucza szyfrowania danych usługi](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) lokalnej interfejs użytkownika sieci web.
    3. Kliknij przycisk **zarejestrować**. To spowoduje ponowne uruchomienie urządzenia hello. Mogą być potrzebne toowait 2 – 3 minuty przed hello urządzenie zostanie pomyślnie zarejestrowana. Po ponownym uruchomieniu urządzenia hello nastąpi przekierowanie toohello Zaloguj się na stronie.
       
       ![](./media/storsimple-virtual-array-deploy3-fs-setup/image13.png)
12. Zwraca toohello portalu Azure. Przejdź za**wszystkie zasoby**, wyszukaj usługi Menedżer StorSimple urządzenia.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/searchdevicemanagerservice1.png) 
13. W hello filtrowane listy, wybierz usługę Menedżer StorSimple urządzenia, a następnie przejdź zbyt**zarządzania > urządzenia**. W hello **urządzeń** bloku, sprawdź urządzenie hello pomyślnie nawiązano połączenie usługi toohello i ma stan hello **gotowe tooset się**.
    
    ![Konfigurowanie serwera plików](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png)

## <a name="step-2-configure-hello-device-as-file-server"></a>Krok 2: Konfigurowanie urządzenia hello jako serwer plików
Wykonaj następujące kroki w hello hello [portalu Azure](https://portal.azure.com/) toocomplete hello wymagane ustawienia urządzenia.

#### <a name="tooconfigure-hello-device-as-file-server"></a>urządzenie hello tooconfigure jako serwer plików
1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie przejść za **zarządzania > urządzenia**. W hello **urządzeń** bloku, urządzenia hello wybierz właśnie utworzony. To urządzenie będzie wyświetlany jako **gotowe tooset się**.
   
   ![Konfigurowanie serwera plików](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png) 
2. Kliknij przycisk hello urządzenia i zostanie wyświetlony komunikat transparentu wskazującą urządzenia hello jest gotowy toosetup.
   
    ![Konfigurowanie serwera plików](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs3m.png)
3. Kliknij przycisk **Konfiguruj** na powitania paska poleceń. Spowoduje to otwarcie zapasowej hello **Konfiguruj** bloku. W hello **Konfiguruj** bloku hello następujące:
   
    1. Nazwa serwera plików Hello jest wypełniane automatycznie.
    
    2. Upewnij się, że szyfrowanie magazynu w chmurze hello ustawiono zbyt**włączone**. Spowoduje to szyfrowanie wszystkich danych hello są wysyłane toohello chmury. 
    
    3. Klucz AES 256-bitowy jest używany z hello zdefiniowane przez użytkownika klucza szyfrowania. Należy określić klucz o długości 32 znaków i ponownie wprowadzić tooconfirm klucza hello go. Rekord hello klucz w aplikacji zarządzania kluczami do użytku w przyszłości.
    
    4. Kliknij przycisk **Skonfiguruj wymagane ustawienia** toospecify konta magazynu poświadczeń toobe używane z urządzeniem. Kliknij przycisk **Dodaj nowe** Jeśli nie istnieją żadne poświadczenia konta magazynu skonfigurowane. **Upewnij się, że hello konto magazynu, którego używasz obsługuje blokowe obiekty BLOB. Stronicowe obiekty BLOB nie są obsługiwane.** Więcej informacji na temat [blokuje obiekty BLOB i stronicowe obiekty BLOB](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).
   
    ![Konfigurowanie serwera plików](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs6m.png) 
4. W hello **dodać poświadczeń konta magazynu** bloku hello następujące: 

    1. Wybierz subskrypcję, jeśli konto magazynu hello jest hello tej samej subskrypcji co hello usługi. Określ inne jest magazynu hello konto znajduje się poza hello subskrypcji usługi. 
    
    2. Z listy rozwijanej hello wybrać istniejące konto magazynu. 
    
    3. Hello lokalizacja zostanie wypełniona automatycznie oparte na powitania określono konto magazynu. 
    
    4. Włącz protokół SSL tooensure sieci bezpieczny kanał komunikacji między urządzeniami hello hello.
    
    5. Kliknij przycisk **Dodaj** tooadd poświadczeń konta tego magazynu. 
   
        ![Konfigurowanie serwera plików](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs8m.png)

5. Po pomyślnym utworzeniu hello poświadczeń dla konta magazynu, hello **Konfiguruj** bloku zostaną zaktualizowane toodisplay hello określone poświadczenia konta magazynu. Kliknij pozycję **Konfiguruj**.
   
   ![Konfigurowanie serwera plików](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs11m.png)
   
   Zobaczysz, że plik jest tworzony serwera. Po pomyślnym utworzeniu powitania serwera plików, otrzymasz powiadomienie.
   
   ![Konfigurowanie serwera plików](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs13m.png)
   
   Stan urządzenia Hello spowoduje również zmianę zbyt**Online**.
   
   ![Konfigurowanie serwera plików](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs14m.png)
   
   Można kontynuować tooadd udziału.

## <a name="step-3-add-a-share"></a>Krok 3: Dodaj udział
Wykonaj następujące kroki w hello hello [portalu Azure](https://portal.azure.com/) toocreate udziału.

#### <a name="toocreate-a-share"></a>toocreate udziału
1. Wybierz urządzenie serwera plików hello skonfigurowane w hello poprzedzających krok, a następnie kliknij przycisk **...**  (lub kliknij prawym przyciskiem myszy). W menu kontekstowym hello, wybierz **Dodaj udział**. Alternatywnie możesz kliknąć **+ Dodaj udział** na pasku poleceń hello urządzenia.
   
   ![Dodawanie udziału](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs15m.png)
2. Określ następujące ustawienia udziału hello:

    1. Unikatowa nazwa udziału użytkownika. Nazwa Hello musi być ciągiem o długości 3 znaków too127.
    
    2. Opcjonalny **opis** hello udziału. Opis Hello pomoże zidentyfikować hello właścicieli udziału.
    
    3. A **typu** hello udziału. Typ Hello można **warstwowego** lub **przypięty lokalnie**, z warstwową trwa hello domyślne. W przypadku obciążeń, które wymagają lokalnych gwarancji, małych opóźnień i większej wydajności, wybierz **przypięty lokalnie** udziału. Dla wszystkich innych danych wybierz **warstwowego** udziału.
    Udział przypięty lokalnie jest alokowany nieelastycznie i gwarantuje, że hello danych pierwotnych w udziale hello pozostaje toohello lokalne urządzenia i nie zostaną przeniesione toohello chmury. Udział warstwowego na powitania jest alokowany elastycznie drugiej strony. Podczas tworzenia udziału warstwowych 10% miejsca hello jest inicjowana na warstwie lokalne powitania i 90% miejsca hello jest obsługiwana w chmurze hello. Na przykład jeśli udostępniane wolumin 1 TB, 100 GB będzie znajdować się w lokalnej przestrzeni hello i 900 GB byłoby używanych w chmurze powitania po hello warstwy danych. Z kolei oznacza to, że po uruchomieniu poza wszystkie lokalne powitania miejsce na urządzeniu hello nie można dostarczać warstwowych udziału.
   
    4. W hello **ustawioną domyślną pełne uprawnienia** pola, należy przypisać hello uprawnienia toohello użytkownika lub grupy hello, który uzyskuje dostęp do tego udziału. Określ nazwę hello hello użytkownika lub grupy użytkowników hello w  *john@contoso.com*  format. Zalecane jest użycie tooaccess uprawnienia użytkownika grupy (zamiast jednego użytkownika) tooallow admin te udziały. Po przypisaniu hello uprawnienia w tym miejscu, następnie można toomodify Eksploratora plików te uprawnienia.
   
    5. Kliknij przycisk **Dodaj** toocreate hello udziału. 
    
        ![Dodawanie udziału](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs18m.png)
   
        Użytkownik jest powiadamiany, że trwa tworzenie udziału hello.
   
        ![Dodawanie udziału](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs19m.png)
   
    Po utworzeniu udziału hello z hello określonych ustawień, hello **udziałów** bloku zaktualizuje tooreflect hello nowego udziału. Domyślnie monitorowania i kopii zapasowej są włączone dla hello udziału.
   
    ![Dodawanie udziału](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs22m.png)

## <a name="step-4-connect-toohello-share"></a>Krok 4: Łączenie toohello udziału
Teraz należy tooconnect tooone lub więcej udziałów, które zostały utworzone w poprzednim kroku hello. Wykonaj następujące kroki na tooyour host połączony z systemu Windows Server tablicy wirtualne StorSimple.

#### <a name="tooconnect-toohello-share"></a>tooconnect toohello udziału
1. Naciśnij klawisz ![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png) + R. W oknie uruchamiania hello Określ hello *&#92; &#92;&lt; Nazwa serwera plików&gt;*  jako ścieżka hello, zastępując *nazwy serwera plików* z urządzeniem hello nazwa ten zostanie przypisany tooyour serwer plików. Kliknij przycisk **OK**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image23.png)
2. Spowoduje to otwarcie zapasowej Eksploratora plików. Teraz powinno być możliwe toosee hello udziałów, które tworzone jako foldery. Wybierz, a następnie kliknij dwukrotnie zawartość hello tooview udziału (folder).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image24.png)
3. Teraz możesz dodać pliki toothese udziałów i wykonaj kopię zapasową.

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak toouse hello lokalnego interfejsu użytkownika sieci web zbyt[administrowania tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).

