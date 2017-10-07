---
title: "Witaj aaaDeploy usługi Menedżer StorSimple urządzenia w usłudze Azure | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak toocreate i delete hello usługi Menedżer urządzenia StorSimple w hello portalu Azure, a w tym artykule opisano, jak toomanage hello klucz rejestracji usługi."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>Wdrażanie hello usługi Menedżer StorSimple urządzenia dla urządzeń z serii StorSimple 8000

## <a name="overview"></a>Omówienie

Hello usługi Menedżer StorSimple urządzenie działa w systemie Microsoft Azure i łączy toomultiple urządzenia StorSimple. Po utworzeniu usługi hello umożliwia toomanage usługi wszystkie urządzenia hello, które są połączone toohello Menedżera urządzeń StorSimple z jednej centralnej lokalizacji, minimalizując w ten sposób nakładu prac administracyjnych.

W tym samouczku opisano hello kroków wymaganych do hello tworzeniem, usuwaniem, migracji usługi hello i zarządzanie hello klucz rejestracji usługi hello. Hello informacje zawarte w tym artykule jest stosowane tylko tooStorSimple 8000 serii na urządzeniach. Aby uzyskać więcej informacji na tablice wirtualnego StorSimple, przejdź zbyt[wdrożyć usługę Menedżer StorSimple urządzenia dla macierzy wirtualnego StorSimple](storsimple-virtual-array-manage-service.md).

## <a name="create-a-service"></a>Tworzenie usługi
toocreate usługi Menedżera urządzeń StorSimple, należy toohave:

* Subskrypcja z umową Enterprise
* Aktywne konto magazynu Microsoft Azure
* Witaj informacji dotyczących rozliczeń, która służy do zarządzania dostępem

Dozwolone są tylko hello subskrypcji z umową Enterprise. Subskrypcje Sponsorship firmy Microsoft, które są dozwolone w hello klasycznego portalu Azure, nie są obsługiwane w hello portalu Azure. Zostanie wyświetlony hello następującą wiadomości, korzystając z nieobsługiwaną subskrypcji:

![Subskrypcja nie jest prawidłowy](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

Możesz również toogenerate domyślne konto magazynu podczas tworzenia usługi hello.

Jednej usługi można zarządzać wieloma urządzeniami. Jednak urządzenia nie może obejmować wiele usług. Duże przedsiębiorstwa mogą być wielu toowork wystąpienia usługi z różnych subskrypcji, organizacji lub nawet miejsc wdrożenia. 

> [!NOTE]
> Należy oddzielnego wystąpienia Menedżera urządzeń StorSimple usługi toomanage StorSimple 8000 serii urządzeń i tablice wirtualne StorSimple.

Wykonaj następujące kroki toocreate usługi hello.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


Dla każdej usługi Menedżer StorSimple urządzenia istnieje hello następujące atrybuty:

* **Nazwa** — hello nazwę, która została przypisana tooyour usługi Menedżer urządzeń StorSimple, podczas tworzenia. **Nie można zmienić nazwy usługi Hello, po utworzeniu hello usługi. Dotyczy to również dla innych jednostek, takich jak urządzenia, woluminy, kontenery woluminów i zasad tworzenia kopii zapasowych, które nie można zmienić nazwy hello portalu Azure.**
* **Stan** — Witaj stanu usługi hello, który może być **Active**, **tworzenie**, lub **Online**.
* **Lokalizacja** — Witaj lokalizacji geograficznej, w których hello StorSimple urządzenie zostanie wdrożona.
* **Subskrypcja** — Witaj subskrypcji, która jest skojarzona z usługą rozliczeń.

## <a name="move-a-service-tooazure-portal"></a>Przenieś portalu tooAzure usługi
Z serii StorSimple 8000 można teraz zarządzać hello portalu Azure. Jeśli masz istniejące urządzenia StorSimple hello toomanage usługi, zalecamy przeniesienie toohello Twojego usługi portalu Azure. Witaj klasycznego portalu Azure do usługi Menedżer StorSimple hello nie jest dostępna po 30 września 2017 r.

Hello opcja toomigrate toohello portalu Azure jest dostępna w fazach. Jeśli nie widzisz opcji toomigrate tooAzure portalu, ale mają toomove i przejrzał hello wpływ migracji, zgodnie z opisem w hello [zagadnienia dotyczące przejścia](#considerations-for-transition), możesz [Prześlij żądanie](https://aka.ms/ss8000-cx-signup).

### <a name="considerations-for-transition"></a>Zagadnienia dotyczące przejścia

Przejrzyj hello wpływ Migrowanie toohello nowego portalu Azure, przed przeniesieniem hello usługi.

#### <a name="before-you-transition"></a>Przed przejście

* Urządzeniu jest uruchomiona aktualizacji w wersji 3.0 lub nowszej. Jeśli urządzenie działa starsza wersja, należy zainstalować najnowsze aktualizacje hello. Aby uzyskać więcej informacji, przejdź zbyt[zainstalować aktualizacji 4](storsimple-8000-install-update-4.md). Jeśli przy użyciu urządzenia StorSimple w chmurze (8010/8020), należy utworzyć nowe urządzenia chmury 4.0 aktualizacji. 

* Po przejściu wykonano przejście toohello nowego portalu Azure, nie można użyć hello Azure classic portal toomanage urządzenia StorSimple.

* Przejście Hello jest brak i nie ma żadnych przestojów w przypadku urządzeń hello.

* Wszyscy menedżerowie urządzenia StorSimple hello w obszarze hello określonej subskrypcji są optymalizowane.

#### <a name="during-hello-transition"></a>Podczas przejścia hello

* Nie można zarządzać urządzenia z portalu hello.
* Operacje takie jak warstw i zaplanowanych kopii zapasowych nadal toooccur.
* Nie usuwaj hello starego menedżerów urządzenia StorSimple, gdy trwa przejście hello.

#### <a name="after-hello-transition"></a>Po przejściu hello

* Urządzenia nie będzie można zarządzać z hello klasycznego portalu.

* Witaj istniejących poleceń cmdlet programu PowerShell usługi Azure Service Management (ASM) nie są obsługiwane. Zaktualizuj toomanage skrypty hello urządzenia za pośrednictwem hello Azure Resource Manager.

* Konfiguracji usługi i urządzenia są zachowywane. Wszystkie woluminy i kopie zapasowe są również wykonano przejście toohello portalu Azure.

### <a name="begin-transition"></a>Rozpocznij przejścia

Wykonaj następujące kroki tootransition hello toohello Twojego usługi portalu Azure.

1. Przejdź tooyour już usługę Menedżer StorSimple w portalu klasycznym hello.

2. Zostanie wyświetlone powiadomienie informujące o tym, że usługa Menedżera urządzeń StorSimple hello jest teraz dostępna w hello portalu Azure. Należy pamiętać, że w hello portalu Azure, usługa hello tooas określonego usługi Menedżer StorSimple urządzenia.

    ![Migracja powiadomień](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. Upewnij się, że użytkownik przejrzał hello wpływ pełnej migracji.
    2. Przejrzyj listę hello menedżerów urządzenia StorSimple, który ma zostać przeniesiona z klasycznego portalu hello.

3. Kliknij przycisk **migracji**. Przejście Hello rozpoczyna się i zajmuje kilka minut toocomplete.

Po zakończeniu przejścia hello można zarządzać urządzeniami za pośrednictwem hello usługi Menedżer urządzenia StorSimple w hello portalu Azure.

W hello portalu Azure tylko hello urządzeń StorSimple z aktualizacji 3.0 i wyższe są obsługiwane. obsługują ograniczoną liczbę Hello urządzeń, które są uruchomione wcześniejsze wersje. powitania po summrizes tabeli, jakie operacje są obsługiwane na urządzeniu hello uruchomione wcześniejsze tooUpdate versios 3.0, po przeprowadzeniu migracji z hello toohello klasycznego portalu Azure.

| Operacja                                                                                                                       | Obsługiwane      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| Zarejestruj urządzenie                                                                                                               | Tak            |
| Konfigurowanie ustawień urządzenia, takie jak ogólne, sieci i zabezpieczeń                                                                | Tak            |
| Skanowanie, Pobierz i zainstaluj aktualizacje                                                                                             | Tak            |
| Dezaktywować urządzenie                                                                                                               | Tak            |
| Usuwanie urządzenia                                                                                                                   | Tak            |
| Tworzenie, modyfikowanie i usuwanie kontenera woluminów                                                                                   | Nie             |
| Tworzenie, modyfikowanie i usuwanie woluminu                                                                                             | Nie             |
| Tworzenie, modyfikowanie i usuwanie zasad tworzenia kopii zapasowej                                                                                      | Nie             |
| Wykonaj kopię zapasową ręczne                                                                                                            | Nie             |
| Wykonać zaplanowaną kopię zapasową                                                                                                         | Nie dotyczy |
| Przywrócenie z zestawu kopii zapasowych                                                                                                        | Nie             |
| Klonowanie tooa urządzenie, na którym uruchomiono aktualizacji 3.0 i nowszych <br> urządzenia źródłowego Hello działa tooUpdate wcześniejszych wersji 3.0.                                | Tak            |
| Klonowanie tooa urządzenie z systemem tooUpdate wcześniejszych wersji 3.0                                                                          | Nie             |
| Trybu failover jako urządzenia źródłowego <br> (z urządzenia z uruchomioną wersji wcześniejszych tooUpdate 3.0 tooa urządzenie, na którym uruchomiono aktualizacji 3.0 i nowszych)                                                               | Tak            |
| Trybu failover jako urządzenia docelowego <br> (tooa urządzenie z systemem tooUpdate poprzednie oprogramowanie w wersji 3.0)                                                                                   | Nie             |
| Wyczyść alert                                                                                                                  | Tak            |
| Wyświetl zasady tworzenia kopii zapasowej, katalogu kopii zapasowej woluminów, kontenery woluminów, wykresy monitorowania, zadania i alerty tworzone w klasycznym portalu | Tak            |
| Włączanie i wyłączanie kontrolery urządzeń                                                                                              | Tak            |


## <a name="delete-a-service"></a>Usuwanie usługi

Przed usunięciem usługi, upewnij się, że żadnych podłączonych urządzeń używają go. Jeśli usługa hello jest używany, Dezaktywuj hello podłączone urządzenia. Witaj dezaktywować operacji sever hello połączenie między hello urządzeń i usług hello, ale zachować dane urządzenie hello w chmurze hello.

> [!IMPORTANT]
> Po usunięciu usługi hello operacji nie można cofnąć. Dowolne urządzenie, które zostało przy użyciu usługi hello musi toobe resetowania toofactory domyślne, zanim będzie można go używać z innej usługi. W tym scenariuszu dane lokalne powitania na powitania urządzenia, a także konfiguracji hello zostaną utracone.

Wykonaj następujące kroki toodelete usługi hello.

### <a name="toodelete-a-service"></a>toodelete usługi

1. Wyszukiwania usługi hello ma toodelete. Kliknij przycisk **zasobów** ikony, jak i następnie dane wejściowe hello toosearch odpowiednich warunków. W wynikach wyszukiwania hello kliknij usługę hello ma toodelete.

    ![Toodelete usługi wyszukiwania](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. Trwa bloku usługi Menedżer StorSimple urządzenia toohello. Kliknij polecenie **Usuń**.

    ![Usuwanie usługi](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. Kliknij przycisk **tak** hello powiadomienia o potwierdzenie. Może upłynąć kilka minut, aż toobe usługi hello usunięte.

    ![Potwierdzenie usunięcia](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a>Pobierz klucz rejestracji usługi hello

Po pomyślnym utworzeniu usługi należy tooregister urządzenie StorSimple przy użyciu usługi hello. tooregister pierwszego urządzenia StorSimple, będzie konieczne hello klucz rejestracji usługi. tooregister dodatkowych urządzeń z istniejącej usługi StorSimple wymagane zarówno klucz rejestracji hello, jak i klucz szyfrowania danych usługi hello, (który jest generowany na powitania pierwszego urządzenia podczas rejestracji). Aby uzyskać więcej informacji na temat klucza szyfrowania danych usługi hello, zobacz [zabezpieczenia usługi StorSimple](storsimple-8000-security.md). Klucz rejestracji hello można uzyskać, uzyskując dostęp do **kluczy** w bloku Menedżera urządzeń StorSimple.

Wykonaj powitania po klucz rejestracji usługi hello tooget czynności.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Klucz rejestracji usługi hello należy przechowywać w bezpiecznym miejscu. Należy tego klucza, a także klucz szyfrowania danych usługi hello tooregister dodatkowych urządzeń z tą usługą. Po uzyskaniu klucza rejestracji usługi hello, musisz skonfigurować urządzenia za pośrednictwem hello środowiska Windows PowerShell dla StorSimple interfejsu.

Aby uzyskać więcej informacji na temat toouse tego klucza, zobacz rejestracji [krok 3: Konfigurowanie i rejestrowanie urządzenia hello przy użyciu programu Windows PowerShell dla StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Wygeneruj ponownie klucz rejestracji usługi hello
Należy tooregenerate klucz rejestracji usługi, jeśli są wymagane tooperform obrotu klucza lub jeśli zmieniono hello listy administratorów usługi. Podczas ponownego generowania klucza hello, nowy klucz hello jest używany tylko do celów rejestracji kolejnych urządzeń. przez ten proces nie dotyczy to urządzeń Hello, które zostały już zarejestrowane.

Wykonaj hello następujące kroki tooregenerate klucz rejestracji usługi.

### <a name="tooregenerate-hello-service-registration-key"></a>klucz rejestracji usługi hello tooregenerate
1. W hello **Menedżera urządzeń StorSimple** bloku Przejdź zbyt**zarządzania &gt;**  **klucze**.
    
    ![Blok Klucze](./media/storsimple-8000-manage-service/regenregkey2.png)

2. W hello **klucze** bloku, kliknij przycisk **ponownie wygenerować**.

    ![Kliknij przycisk regenerate](./media/storsimple-8000-manage-service/regenregkey3.png)
3. W hello **klucz rejestracji usługi Regenerate** bloku, przejrzyj hello Akcja wymagana, gdy hello klucze są generowane. Wszystkie urządzenia kolejnych hello, które są zarejestrowane w usłudze tej usługi użyj hello nowy klucz rejestracji. Kliknij przycisk **ponownie wygenerować** tooconfirm. Użytkownik jest powiadamiany po zakończeniu ponownego wygenerowania hello.

    ![Potwierdź regenerate](./media/storsimple-8000-manage-service/regenregkey4.png)

4. Pojawi się nowy klucz rejestracji usługi.

5. Skopiuj ten klucz i zapisać go do rejestracji żadnych nowych urządzeń z tą usługą.



## <a name="change-hello-service-data-encryption-key"></a>Klucz szyfrowania danych usługi hello zmiany
Klucze szyfrowania danych usługi są używane tooencrypt klienta poufnych danych, takich jak poświadczeń konta magazynu, które są wysyłane z urządzenia StorSimple toohello usługi Menedżer StorSimple. Konieczne będzie toochange te klucze okresowo Jeśli Twoja organizacja IT zasady rotacją kluczy w urządzeniach magazynujących hello. Witaj proces zmiany klucza może być nieznacznie różnić w zależności od tego, czy istnieje jednego lub wielu urządzeniach zarządzanych przez hello usługi Menedżer StorSimple. Aby uzyskać więcej informacji, przejdź zbyt[StorSimple zabezpieczeń i ochrony danych](storsimple-8000-security.md).

Zmiana klucza szyfrowania danych usługi hello jest procesem krok 3:

1. Za pomocą skryptów środowiska Windows PowerShell dla usługi Azure Resource Manager, zezwolić urządzeniu toochange hello klucza szyfrowania danych usługi.
2. Przy użyciu programu Windows PowerShell dla urządzenia StorSimple, inicjują zmiany klucza szyfrowania danych usługi hello.
3. Jeśli masz więcej niż jedno urządzenie StorSimple, należy zaktualizować klucz szyfrowania danych usługi hello na powitania innych urządzeń.

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a>Krok 1: Użyj środowiska Windows PowerShell skryptu tooAuthorize urządzenia toochange hello klucza szyfrowania danych usługi
Zazwyczaj administratora urządzenia hello żądania, czy administrator usługi hello autoryzować klucze szyfrowania danych usługi urządzenia toochange. administrator usługi Hello następnie autoryzacji hello urządzenia toochange hello klucza.

Ten krok jest wykonywane przy użyciu hello Azure Resource Manager na podstawie skryptu. Witaj usługi administrator może wybrać urządzenie jest toobe kwalifikują autoryzację. urządzenia Hello jest to klucz szyfrowania danych usługi hello toostart autoryzowanych zmienić procesu. 

Aby uzyskać więcej informacji o używaniu skryptu hello Przejdź zbyt[ServiceEncryptionRollover.ps1 autoryzacji](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Urządzenia, które mogą być autoryzowane klucze szyfrowania danych usługi toochange?
Urządzenie musi spełniać następujące kryteria, aby można było zmiany klucza szyfrowania danych usługi autoryzowanych tooinitiate hello:

* Witaj, urządzenie musi być online toobe kwalifikuje się do autoryzacji zmiany klucza szyfrowania danych usługi.
* Można autoryzować powitalne tym samym urządzeniu ponownie po 30 minutach zmiany hello klucz nie został zainicjowany.
* Inne urządzenie, można zezwolić pod warunkiem, że zmiany klucza hello nie została zainicjowana przez urządzenie wcześniej upoważnionego hello. Po autoryzacji hello nowe urządzenie hello starym urządzeniem nie można zainicjować hello zmiany.
* Nie można autoryzować urządzenia, gdy hello przerzucania klucza szyfrowania danych usługi hello jest w toku.
* W przypadku niektórych urządzeń hello zarejestrowany w usludze hello ma przerzuceniem hello szyfrowania, podczas gdy inne nie zawierają można autoryzować urządzenia. 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Krok 2: Użyj środowiska Windows PowerShell dla StorSimple tooinitiate hello danych szyfrowania klucza zmiany usługi
Wykonanie tego kroku w hello środowiska Windows PowerShell dla StorSimple interfejsu na powitania autoryzacji urządzenia StorSimple.

> [!NOTE]
> Żadne operacje nie można wykonać w portalu Azure usługi Menedżer StorSimple hello ukończenie hello przerzucania klucza.
> 
> 

Jeśli używasz interfejsu programu Windows PowerShell toohello tooconnect w konsoli szeregowej urządzenia hello wykonać hello następujące kroki.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>zmiana klucza szyfrowania danych usługi hello tooinitiate
1. Wybierz opcję 1 toolog na z pełnym dostępem.
2. Witaj wiersza polecenia wpisz:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Po pomyślnym ukończeniu hello polecenia cmdlet otrzymasz nowy klucz szyfrowania danych usługi. Skopiuj i Zapisz ten klucz do użycia w kroku 3 tego procesu. Ten klucz będzie używany tooupdate hello wszystkich pozostałych urządzeń zarejestrowanych w usłudze Menedżer StorSimple hello.
   
   > [!NOTE]
   > Ten proces musi zostać zainicjowany w ciągu czterech godzin autoryzowania urządzenia StorSimple.
   > 
   > 
   
   Ten nowy klucz jest następnie wysyłana toohello usługi toobe wypychana tooall hello urządzeń, które są zarejestrowane w usłudze hello. Na pulpicie nawigacyjnym usługi hello pojawi się alert. Usługa Hello spowoduje wyłączenie wszystkich operacji hello na urządzeniach zarejestrowanych hello i hello administratora urządzenia będą musieli tooupdate klucza szyfrowania danych usługi hello na powitania innych urządzeń. Jednak hello operacji We/Wy (wysyłanie danych w chmurze toohello hostów) zostanie nie jest zakłócona.
   
   Jeśli masz jednego urządzenia zarejestrowane usługi tooyour, hello przerzucania proces został już ukończony i można przejść hello następnego kroku. Jeśli masz wiele usługi tooyour zarejestrowanych urządzeń, przejdź toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Krok 3: Zaktualizuj klucz szyfrowania danych usługi hello na innych urządzeń StorSimple
Te czynności należy wykonać w interfejsie programu Windows PowerShell hello urządzenia StorSimple, jeśli masz wiele usługi Menedżer StorSimple tooyour zarejestrowanych urządzeń. Witaj klucza, który został uzyskany w kroku 2 musi być używane tooupdate, który hello wszystkie pozostałe urządzenia StorSimple w zarejestrowany hello usługi Menedżer StorSimple.

Wykonaj powitania po szyfrowania danych usługi hello tooupdate kroki na urządzeniu.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>klucz szyfrowania danych usługi hello tooupdate
1. Użyj środowiska Windows PowerShell dla StorSimple tooconnect toohello konsoli. Wybierz opcję 1 toolog na z pełnym dostępem.
2. Witaj wiersza polecenia wpisz:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Podaj klucz szyfrowania danych usługi hello, które zostały uzyskane w [krok 2: Użyj środowiska Windows PowerShell dla StorSimple tooinitiate hello danych szyfrowania klucza zmiany usługi](#to-initiate-the-service-data-encryption-key-change).


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o hello [procesu wdrażania StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
* Dowiedz się więcej o [Zarządzanie kontem magazynu StorSimple](storsimple-8000-manage-storage-accounts.md).
* Dowiedz się więcej o tym, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).
