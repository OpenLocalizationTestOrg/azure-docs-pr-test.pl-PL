---
title: "aaaStorSimple 8000 serii zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Opisuje hello funkcje zabezpieczeń i prywatności chroniących usługi StorSimple, urządzenia i danych lokalnie i w chmurze hello."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: a21d19c6-83b4-418c-9380-323bb9f76612
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/03/2016
ms.author: v-sharos
ms.openlocfilehash: b9e6c8b3371b4039549972cf507052312ed7cdaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-security-and-data-protection"></a>StorSimple zabezpieczeń i ochrony danych
## <a name="overview"></a>Omówienie
Zabezpieczeń jest głównym problemem dla każdego, kto wdraża to nowa technologia, szczególnie w przypadku technologii hello jest używany z danych poufnych lub zastrzeżonych. Jak można ocenić różnych technologii, należy wziąć pod uwagę zwiększone ryzyko i koszty związane z ochroną danych. Microsoft Azure StorSimple zawiera zabezpieczeń i prywatności rozwiązania ochrony danych, pomagając tooensure: 

* **Poufność** — tylko do autoryzowanych jednostek można wyświetlić danych. 
* **Integralność** — tylko autoryzowani jednostki można zmodyfikować lub usunąć dane.

Witaj rozwiązania Microsoft Azure StorSimple składa się z czterech głównych składników, które współdziałają ze sobą:

* **Usługę Menedżer StorSimple hostowana na platformie Microsoft Azure** — użycie tooconfigure i świadczenia usługi zarządzania hello hello urządzenia StorSimple.
* **Urządzenia StorSimple** — urządzenia fizycznego zainstalowany w centrum danych. Wszystkie hosty i klientów, które generują dane Podłącz urządzenie StorSimple toohello, a urządzenie hello zarządza danymi hello i przenosi ją toohello chmury Azure jako odpowiednie.
* **Klienci/hosty podłączone urządzenie toohello** — Witaj klientów w infrastrukturze łączących toohello urządzenia StorSimple i generować dane do potrzeb toobe chronione.
* **Magazyn w chmurze** — Witaj lokalizacji w hello chmury Azure, w którym są przechowywane dane.

Witaj poniższych sekcjach opisano funkcje zabezpieczeń StorSimple hello pomagających w ochronie każdego z tych składników oraz hello danych przechowywanych w nich. Zawiera także listę pytania, na które może być o zabezpieczeniach Microsoft Azure StorSimple i hello odpowiednich odpowiedzi.

## <a name="storsimple-manager-service-protection"></a>Ochrona usługi Menedżer StorSimple
Hello usługi Menedżer StorSimple jest usługą zarządzania hostowana na platformie Microsoft Azure i użyć toomanage wszystkie urządzenia StorSimple, które organizacja został uzyskany. Można uzyskać dostępu do hello usługi Menedżer StorSimple przy użyciu programu toolog poświadczeń w organizacji na toohello klasycznego portalu Azure za pośrednictwem przeglądarki sieci web. 

Toohello dostępu usługi Menedżer StorSimple wymaga, że Twoja organizacja ma subskrypcję platformy Azure, która obejmuje StorSimple. Subskrypcja podlega hello funkcje, które są dostępne w hello klasycznego portalu Azure. Jeśli Twoja organizacja nie ma subskrypcji platformy Azure i mają więcej informacji na temat ich toolearn, zobacz [tworzenia konta platformy Azure jako organizacja](../active-directory/sign-up-organization.md). 

Ponieważ hello usługi Menedżer StorSimple jest hostowana na platformie Azure, jest chroniona przez hello funkcje zabezpieczeń platformy Azure. Aby uzyskać więcej informacji na temat funkcji zabezpieczeń hello udostępniane przez Microsoft Azure, przejdź toohello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

## <a name="storsimple-device-protection"></a>Ochrona urządzenia StorSimple
urządzenia StorSimple Hello jest lokalnego urządzenia magazynu hybrydowego zawierający dysków półprzewodnikowych (SSD) i dysków twardych (HDD), wraz z nadmiarowe kontrolery i funkcji automatycznej pracy awaryjnej. Witaj kontrolerów zarządzania magazynem warstwy, umieszczania aktualnie używane (lub gorących) danych w magazynie lokalnym (w hello urządzenia StorSimple lub serwerów lokalnych), podczas przenoszenia toohello rzadziej używanych danych w chmurze.

Tylko autoryzowane StorSimple, urządzenia będą mogły hello toojoin usługi Menedżer StorSimple, utworzony w ramach subskrypcji platformy Azure. tooauthorize urządzenie musi być zarejestrowany z hello usługi Menedżer StorSimple, zapewniając klucz rejestracji usługi hello. klucz rejestracji usługi Hello jest 128-bitowego losowy klucz wygenerowany w hello klasycznego portalu Azure. 

![klucz rejestracji usługi](./media/storsimple-security/ServiceRegistrationKey.png)

toolearn jak uzyskać Przejdź klucza, rejestracji usługi zbyt[krok 2: Pobierz klucz rejestracji usługi hello](storsimple-deployment-walkthrough.md#step-2-get-the-service-registration-key).

klucz rejestracji usługi Hello jest długa klucz, który zawiera znaki 100 +. Można skopiować klucza hello i zapisać go w pliku tekstowym w bezpiecznej lokalizacji, dzięki czemu można używać go tooauthorize dodatkowych urządzeń w razie potrzeby. Jeśli klucz rejestracji usługi hello zostaną utracone po zarejestrowaniu pierwszego urządzenia, możesz wygenerować nowy klucz na podstawie hello usługi Menedżer StorSimple. Nie wpłynie to na operację hello istniejących urządzeń. 

Po zarejestrowaniu urządzenia za pomocą tokenów toocommunicate i Microsoft Azure. klucz rejestracji usługi Hello nie jest używany po rejestracji urządzeń.

> [!NOTE]
> Zaleca się ponowne generowanie klucza rejestracji usługi powitania po każdym użyciu.
> 
> 

## <a name="protect-your-storsimple-solution-via-passwords"></a>Ochrona rozwiązania StorSimple przy użyciu hasła
Hasła są istotnym elementem zabezpieczenia komputera i są często używane w rozwiązaniu StorSimple hello toohelp upewnij się, że dane są tooauthorized dostępny tylko dla użytkowników. StorSimple umożliwia hello tooconfigure następującego hasła:

* Hasło administratora urządzenia StorSimple
* Żądanie hasła Inicjator i obiekt docelowy protokołu uwierzytelniania Handshake (CHAP)
* Hasło programu StorSimple Snapshot Manager

### <a name="windows-powershell-for-storsimple-and-hello-storsimple-device-administrator-password"></a>Program Windows PowerShell dla StorSimple i hello hasło administratora urządzenia StorSimple
Program Windows PowerShell dla urządzenia StorSimple jest interfejsu wiersza polecenia, których można używać urządzeń StorSimple hello toomanage. Program Windows PowerShell dla StorSimple zawiera funkcje, które pozwalają tooregister urządzenia, skonfiguruj interfejs sieciowy hello na urządzeniu zainstalować niektórych typów aktualizacji, rozwiązywania problemów z urządzeniem, uzyskując dostęp do sesji pomocy technicznej hello i zmienić stan urządzenia hello . Przy komunikacji zdalnej programu Windows PowerShell lub konsoli szeregowej toohello połączenia na urządzeniu hello miały dostęp do programu Windows PowerShell dla StorSimple.

Usługi zdalne środowiska PowerShell może odbywać się za pośrednictwem protokołu HTTP lub HTTPS. Po włączeniu zdalnego zarządzania za pośrednictwem protokołu HTTPS, konieczne będzie toodownload hello zdalne zarządzanie certyfikatu z urządzenia hello i zainstalować ją na powitania klienta zdalnego. Aby uzyskać więcej informacji na temat komunikacji zdalnej programu PowerShell Przejdź zbyt[połączyć się zdalnie urządzenia StorSimple tooyour](storsimple-remote-connect.md).

Po użyciu programu Windows PowerShell dla StorSimple tooconnect toohello urządzenia, konieczne będzie tooprovide toolog hasło administratora urządzenia hello na urządzeniu toohello.

![Hasło administratora urządzenia](./media/storsimple-security/DeviceAdminPW.png)

Zachowaj hello następujące najlepsze rozwiązania pod uwagę:

* Zdalne zarządzanie jest domyślnie wyłączona. Można użyć tooenable usługi Menedżer StorSimple hello go. Ze względów bezpieczeństwa dostępu zdalnego powinna być włączona tylko podczas hello okres czasu, który będzie to wymagane.
* Jeśli zmienisz hasło hello można toonotify się, że wszyscy użytkownicy dostępu zdalnego tak, aby nie będą występować utracie Nieoczekiwana łączności.
* Witaj usługi Menedżer StorSimple, nie można pobrać istniejące hasła: można tylko zresetować je. Firma Microsoft zaleca przechowywać wszystkie hasła w bezpiecznym miejscu, dzięki czemu nie trzeba tooreset hasła zapomnienia jest. Jeśli potrzebujesz tooreset hasła można toonotify się, że wszyscy użytkownicy przed je zresetować. 

Za pomocą połączenia szeregowego toohello urządzenia można uzyskać dostępu do hello interfejsu programu Windows PowerShell. Możesz również do niego dostęp zdalnie przy użyciu protokołu HTTP lub HTTPS, która zapewnia dodatkowe zabezpieczenia. HTTPS zapewnia wyższy poziom zabezpieczeń niż seryjny lub połączenia HTTP. Jednak toouse HTTPS, należy najpierw zainstalować certyfikat na komputerze klienckim hello dostępnym hello urządzenia. Certyfikat dostępu zdalnego hello można pobrać ze strony konfiguracji urządzenia hello w hello usługi Menedżer StorSimple. W przypadku utraty hello certyfikatu do dostępu zdalnego należy pobrać nowy certyfikat i Propaguj go tooall klientów, które są autoryzowane toouse zdalne zarządzanie.

### <a name="challenge-handshake-authentication-protocol-chap-initiator-and-target-passwords"></a>Żądanie hasła Inicjator i obiekt docelowy protokołu uwierzytelniania Handshake (CHAP)
Protokół CHAP jest schemat uwierzytelniania używany przez hello tożsamości hello toovalidate urządzenia StorSimple z klientów zdalnych. Weryfikacja Hello jest oparta na wspólne hasło. Protokół CHAP, może być jednokierunkowe (jednokierunkowe) lub wzajemne (dwukierunkowe). Za pomocą jednokierunkowego protokołu CHAP hello docelowego (hello urządzenia StorSimple) uwierzytelnia inicjatora (hosta). Wzajemnego lub wstecznego protokołu CHAP wymaga hello docelowy uwierzytelniania inicjatora hello i następnie inicjatora hello uwierzytelniania hello docelowej. Twoje StorSimple może być skonfigurowany toouse każdej z metod.

Konfigurowanie protokołu CHAP, należy pamiętać o następujących hello:

* Nazwa użytkownika protokołu CHAP Hello musi zawierać mniej niż 233 znaków.
* Hasło protokołu CHAP Hello musi należeć do zakresu od 12 do 16 znaków. Próba toouse dłużej nazwa użytkownika lub hasło spowoduje niepowodzenie uwierzytelniania na hoście Windows hello.
* Nie można użyć hello tego samego hasła dla hello inicjatora protokołu CHAP i hello obiektu docelowego protokołu CHAP.
* Po ustawieniu hasła hello, można zmienić, ale nie można pobrać. Zmiana hasła hello być toonotify się, że wszyscy użytkownicy dostępu zdalnego tak, aby pomyślnie umożliwić im połączenie toohello urządzenia StorSimple.

Aby uzyskać więcej informacji na temat protokołu CHAP i jak tooconfigure go do rozwiązania StorSimple Przejdź zbyt[Konfigurowanie protokołu CHAP dla urządzenia StorSimple](storsimple-configure-chap.md).

### <a name="storsimple-snapshot-manager-password"></a>Hasło programu StorSimple Snapshot Manager
StorSimple Snapshot Manager jest przystawki Microsoft Management Console (MMC), która używa grup woluminu i kopii zapasowych spójnych z aplikacją toogenerate usługi kopiowania woluminów w tle Windows hello. Ponadto można użyć programu StorSimple Snapshot Manager toocreate harmonogramy tworzenia kopii zapasowej i w klonowania lub Przywracanie woluminów.

Po skonfigurowaniu toouse urządzenia StorSimple Snapshot Manager będzie hasło programu StorSimple Snapshot Manager hello tooprovide wymagane. To hasło jest najpierw ustawić w programie Windows PowerShell dla StorSimple podczas rejestracji. można również ustawić hasło Hello i zmieniła się z hello usługi Menedżer StorSimple. To hasło służy do uwierzytelniania urządzenia hello z StorSimple Snapshot Manager.

![Hasło programu StorSimple Snapshot Manager](./media/storsimple-security/SnapshotMgrPassword.png)

hasło programu StorSimple Snapshot Manager Hello musi być 14 too15 znaków i może zawierać 3 lub więcej z kombinacji wielkie litery, małe litery, liczbowego i znaki specjalne. Po ustawieniu hello hasło programu StorSimple Snapshot Manager można zmienić, ale nie można pobrać. Jeśli zmienisz hasło hello można się toonotify wszystkich użytkowników zdalnych.

Aby uzyskać więcej informacji na temat programu StorSimple Snapshot Manager Przejdź zbyt[co to jest StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

### <a name="password-best-practices"></a>Najlepsze rozwiązania w zakresie hasła
Zalecane jest użycie hello następujące wytyczne toohelp zapewniać haseł usługi StorSimple silne i dobrze chroniony:

* Zmień hasła co trzy miesiące. Zmienianie haseł hello jest wymuszana co roku.
* Należy używać silnych haseł. Aby uzyskać więcej informacji, przejdź zbyt[tworzyć silniejsze hasła i chronić je](http://blogs.microsoft.com/cybertrust/2014/08/25/create-stronger-passwords-and-protect-them/).
* Zawsze używaj różnych haseł dla dostępu do różnych mechanizmów; Każdy hello haseł, które określisz powinna być unikatowa.
* Nie udostępniaj nikomu nie będącego urządzenia StorSimple hello tooaccess autoryzowanych hasła.
* Nie Czytaj o hasło przed innymi lub wskazówki na powitania format hasła.
* Jeśli podejrzewasz, że naruszono konto lub hasło, zgłoś dział bezpieczeństwa informacji tooyour zdarzenia hello.
* Traktuj wszystkie hasła jako poufne, poufne informacje. 

## <a name="storsimple-data-protection"></a>Ochrona danych StorSimple
W tej sekcji opisano funkcje zabezpieczeń StorSimple hello ochrony danych przesyłanych i przechowywanych danych.

Zgodnie z opisem w innych częściach, są używane tooauthorize i uwierzytelnia użytkowników przed uzyskaniem dostępu tooyour StorSimple rozwiązania hasła. Kolejnym zagadnieniem zabezpieczeń jest ochrona danych przed nieautoryzowanymi użytkownikami, gdy są przesyłane między systemami magazynowania, a podczas są przechowywane. Witaj poniższych sekcjach opisano funkcje ochrony danych hello wyposażone StorSimple.

> [!NOTE]
> Funkcja deduplikacji udostępnia dodatkową ochronę danych przechowywanych na urządzeniu StorSimple hello i magazynu Microsoft Azure. Gdy dane jest deduplikowany, obiekty danych hello są przechowywane oddzielnie od toomap metadane używane hello i uzyskiwać do nich dostęp: nie ma żadnych danych hello tooreconstruct dostępne kontekstu poziom przechowywania na podstawie struktury woluminu, system plików lub nazwę pliku.
> 
> 

## <a name="protect-data-flowing-through-hello-service"></a>Ochrona danych przepływających przez hello usługi
głównym celem hello usługi Menedżer StorSimple Hello jest toomanage i skonfiguruj hello urządzenia StorSimple. Hello usługi Menedżer StorSimple działa na platformie Microsoft Azure. Użyj hello Azure classic portal tooenter danych o konfiguracji urządzenia, a następnie używa usługi Menedżer StorSimple hello toosend urządzenie toohello danych hello w Microsoft Azure. Informacje są przechowywane w używa StorSimple system toohelp pary kluczy asymetrycznych upewnij się, że do naruszenia nie spowoduje naruszenie hello usługi Azure. 

![Szyfrowanie danych w locie](./media/storsimple-security/DataEncryption.png)

system klucza asymetrycznego Hello chroni hello danych za pośrednictwem usługi hello w następujący sposób:

1. Certyfikat szyfrowania danych, który używa publicznego i prywatnego para kluczy asymetrycznych jest generowany na urządzeniu hello i używanych tooprotect hello danych. klucze Hello są generowane, gdy hello pierwsze urządzenie jest zarejestrowane. 
2. Klucze certyfikatu szyfrowania danych Hello zostaną wyeksportowane do pliku wymiany informacji osobistych (pfx), który jest chroniony przez klucz szyfrowania danych usługi hello, czyli silnego klucza 128-bitowego, losowo generowany przez hello pierwszego urządzenia podczas rejestracji.
3. Hello klucz publiczny certyfikatu hello staje się bezpiecznie toohello dostępne usługi Menedżer StorSimple, a klucz prywatny hello pozostaje hello urządzenia.
4. Dane, które wprowadzanie usługi hello jest szyfrowana przy użyciu hello klucza publicznego ani odszyfrować przy użyciu klucza prywatnego hello przechowywane na urządzeniu hello, zapewnienie, że hello usługi Azure odszyfrowywać hello dane przepływające toohello urządzenia.

klucz szyfrowania danych usługi Hello jest generowany na powitania pierwszego urządzenia zarejestrowane w usłudze hello. Wszystkie kolejne urządzenia, które są zarejestrowane w usłudze hello należy użyć hello tego samego klucza szyfrowania danych usługi. 

> [!IMPORTANT]
> Jest bardzo ważne toomake kopię klucza szyfrowania danych usługi hello i zapisz go w bezpiecznej lokalizacji. Kopię klucza szyfrowania danych usługi hello powinny być przechowywane w taki sposób, mogą uzyskiwać przez osobę upoważnioną i mogą być łatwo przekazanych toohello administratora urządzenia.
> 
> W przypadku utraty klucza szyfrowania danych usługi hello działu pomocy technicznej firmy Microsoft pomoże Ci tooretrieve udostępniane, czy masz co najmniej jedno urządzenie w stanie online. Firma Microsoft zaleca zmianę klucza szyfrowania danych usługi powitania po jej pobraniu. Aby uzyskać instrukcje, przejdź zbyt[klucza szyfrowania danych usługi hello zmiany](storsimple-service-dashboard.md#change-the-service-data-encryption-key).
> 
> 

Można zmienić klucza szyfrowania danych usługi hello i hello odpowiedni certyfikat szyfrowania danych, wybierając hello **klucza szyfrowania danych usługi zmiany** opcji na powitania pulpit nawigacyjny usługi. tooensure, że bezpieczeństwo danych nie zostanie naruszony, należy użyć fizycznego StorSimple urządzenia toochange hello klucza szyfrowania danych usługi. Zmiana kluczy szyfrowania hello wymaga, aby wszystkie urządzenia zostać zaktualizowana przy użyciu nowego klucza hello. Dlatego zaleca się zmienić klucz hello, gdy wszystkie urządzenia są w trybie online. Jeśli urządzenia są w trybie offline, można zmienić ich kluczy w innym czasie. urządzenia Hello z kluczami nieaktualne będą nadal mogli toorun kopii zapasowych, ale nie będą mogli toorestore danych do czasu zaktualizowania hello klucza. Aby uzyskać więcej informacji, przejdź zbyt[nawigacyjnym usługi Menedżer StorSimple hello użyj](storsimple-service-dashboard.md).

klucz szyfrowania danych usługi Hello i certyfikat szyfrowania danych hello nie wygasa. Jednak zaleca się zmieniania szyfrowania danych usługi hello klucza rocznie toohelp zapobiec złamania klucza.

## <a name="protect-data-at-rest"></a>Ochrona danych w stanie spoczynku
urządzenia StorSimple Hello zarządza danymi przez zapisanie jej w warstwach lokalnie i w chmurze hello, w zależności od częstotliwości użytkowania. Wszystkie hosta maszyny, które są połączone toohello urządzenia wysyłania danych toohello urządzenia, które przenosi dane toohello chmury, zależnie od potrzeb. Dane są przesyłane z chmury toohello urządzenia hello bezpiecznie za pośrednictwem hello Internet. Każde urządzenie ma jeden obiekt docelowy iSCSI, która udostępnia wszystkie udostępnione woluminy na tym urządzeniu. Wszystkie dane są szyfrowane przed wysłaniem toocloud magazynu. 

![klucz szyfrowania magazynu w chmurze](./media/storsimple-security/CloudStorageEncryption.png)

toohelp zapewnić bezpieczeństwo hello i integralność danych przenieść toohello chmury, StorSimple umożliwia klucze szyfrowania magazynu chmury toodefine w następujący sposób:

* Klucz szyfrowania magazynu w chmurze hello można określić podczas tworzenia kontenera woluminów. Hello klucza nie może być zmodyfikowanie lub dodanie później. 
* Wszystkie woluminy w udziale kontenera woluminu hello tego samego klucza szyfrowania. Jeśli chcesz inny formularz szyfrowania dla określonego woluminu, zaleca się utworzenie nowego toohost kontenera woluminów tego woluminu.
* Po wprowadzeniu hello klucz szyfrowania magazynu w chmurze w hello usługi Menedżer StorSimple klucza hello są szyfrowane przy użyciu hello publicznej części klucza szyfrowania danych usługi hello, a następnie wyślij toohello urządzenia.
* klucz szyfrowania magazynu w chmurze Hello nie jest przechowywany w dowolnym miejscu w usłudze hello i jest znany tylko toohello urządzenia.
* Określenie klucz szyfrowania magazynu w chmurze jest opcjonalne. Możesz wysłać dane, które zostały zaszyfrowane na powitania hosta toohello urządzenia.

### <a name="additional-security-best-practices"></a>Dodatkowe najlepsze rozwiązania
* Podziel ruchu: wyizolować z sieci SAN iSCSI z ruchu danych w sieci lokalnej firmy wdrażania całkowicie rozdzielonych sieci i przy użyciu sieci VLAN, których fizycznych izolacji nie jest opcją. Sieć dedykowanych dla magazynu iSCSI zagwarantuje hello bezpieczeństwa i wydajności danych biznesowych o znaczeniu krytycznym. Mieszanie ruchu magazynu i użytkownika w firmowej sieci LAN nie jest zalecana i może zwiększyć czas oczekiwania i powodować awarie sieci.
* Na stronie zabezpieczenia sieci po stronie hosta należy użyć interfejsów sieciowych, które obsługują protokół TCP/IP Offload Engine (TOE). TOE zmniejsza obciążenie procesora CPU przez przetwarzanie TCP hello karty sieciowej.

## <a name="protect-data-via-storage-accounts"></a>Ochrona danych za pomocą kont magazynu
Każda subskrypcja Microsoft Azure można utworzyć co najmniej jedno konto magazynu. (Konto magazynu zapewnia unikatową przestrzeń nazw do pracy z danymi przechowywanymi w hello chmury Azure). Konto magazynu tooa dostęp jest kontrolowany przez klucze dostępu i subskrypcji hello skojarzonych z tym kontem magazynu. 

Podczas tworzenia konta magazynu Microsoft Azure generuje dwa klucze dostępu 512-bitowe magazynu, z których jeden jest używany do uwierzytelniania, gdy urządzenie StorSimple hello uzyskuje dostęp do konta magazynu hello. Należy pamiętać, że jest używany tylko jeden z tych kluczy. Witaj innego klucza jest przechowywana w rezerwy, dzięki czemu możesz toorotate hello klucze okresowo. klucze toorotate należy hello klucza pomocniczego aktywne, a następnie klucz podstawowy hello delete. Następnie można utworzyć nowego klucza do użycia podczas hello następny obrót. (Ze względów bezpieczeństwa wiele centrów danych wymagają rotacją kluczy). 

Firma Microsoft zaleca, należy wykonać następujące najlepsze rozwiązania dotyczące obrotu klucza:

* Należy obrócić klucze konta magazynu regularnie toohelp upewnij się, że Twoje konto magazynu nie jest używane przez nieautoryzowanych użytkowników.
* Okresowo administratora platformy Azure, należy zmienić lub ponownie wygenerować klucz podstawowy lub pomocniczy hello przy użyciu sekcji magazynu hello hello konta magazynu systemu Azure classic portal toodirectly dostępu hello.

## <a name="protect-data-via-encryption"></a>Ochrona danych za pomocą szyfrowania
StorSimple używa hello algorytmów szyfrowania, które tooprotect dane przechowywane w następujących lub podróży między składnikami hello rozwiązania StorSimple.

| Algorytm | Długość klucza | Komentarze protokołów/aplikacji |
| --- | --- | --- |
| RSA |2048 |1.5 RSA PKCS 1 jest używany przez hello Azure tooencrypt portalu klasycznego konfiguracji dane są przesyłane urządzenia toohello: na przykład poświadczenia, konfiguracji urządzenia StorSimple, konta magazynu i klucze szyfrowania magazynu w chmurze. |
| AES |256 |AES z CBC jest używane tooencrypt hello publicznej części klucza szyfrowania danych usługi hello przed ich wysłaniem z urządzenia StorSimple hello toohello klasycznego portalu Azure. Jest on również używany przez dane tooencrypt urządzenia StorSimple hello przed wysłaniem danych hello toohello konta magazynu w chmurze. |

## <a name="storsimple-virtual-device-security"></a>Zabezpieczenia urządzenia wirtualnego StorSimple
[!INCLUDE [storsimple virtual device security](../../includes/storsimple-virtual-device-security.md)]

## <a name="frequently-asked-questions-faq"></a>Często zadawane pytania
Witaj poniżej przedstawiono niektóre pytania i odpowiedzi dotyczące zabezpieczeń i Microsoft Azure StorSimple.

**Pytanie:** Moje usługi zostanie naruszony. Jakie powinny być następne kroki należy wykonać?

**Odpowiedź:** natychmiast należy zmienić klucza szyfrowania danych usługi hello i hello klucze konta magazynu dla konta magazynu hello, który jest używany dla danych warstw. Aby uzyskać instrukcje przejdź do: 

* [Klucz szyfrowania danych usługi hello zmiany](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Rotacją kluczy kont magazynu](storsimple-manage-storage-accounts.md#key-rotation-of-storage-accounts)

**Pytanie:** mam nowe urządzenie StorSimple, który żąda klucz rejestracji usługi hello. Jak pobrać go

**Odpowiedź:** ten klucz został utworzony przy pierwszym tworzeniu hello usługi Menedżer StorSimple. Gdy używasz hello — urządzenie toohello tooconnect usługi Menedżer StorSimple, można użyć tooview strony szybki start usługi hello lub klucz rejestracji usługi regenerate hello. Generowanie klucza rejestracji usługi nie wpłynie na hello istniejących zarejestrowanych urządzeń. Aby uzyskać instrukcje przejdź do:

* [Wyświetl lub ponownie wygenerować klucz rejestracji usługi hello](storsimple-service-dashboard.md#view-or-regenerate-the-service-registration-key)

**Pytanie:** utratą mój klucz szyfrowania danych usługi. Co mam zrobić?

**Odpowiedź:** skontaktuj się z pomocą techniczną firmy Microsoft. Możliwości zalogowania się tooa sesji pomocy technicznej na urządzeniu i pomocy pobrać klucz hello (zakładając, że co najmniej jedno urządzenie jest w trybie online). Natychmiast po uzyskaniu klucza szyfrowania danych usługi hello, należy ją zmienić tooensure tego nowego klucza hello jest znany tylko tooyou. Aby uzyskać instrukcje przejdź do:

* [Klucz szyfrowania danych usługi hello zmiany](storsimple-service-dashboard.md#change-the-service-data-encryption-key)

**Pytanie:** autoryzowany urządzenie na potrzeby usługi zmiany klucza szyfrowania danych, ale nie można uruchomić procesu zmiany klucza hello. Co mam zrobić?

**Odpowiedź:** Jeśli wygasł okres limitu czasu hello, należy tooreauthorize hello urządzenia do zmiany klucza szyfrowania danych usługi hello a ponowne uruchomienie procesu hello.

**Pytanie:** klucza szyfrowania danych usługi hello zostały zmienione, ale nie mógł I tooupdate hello innych urządzeniach w ciągu 4 godzin. Czy mam toostart ponownie?

**Odpowiedź:** hello jest 4-godzinnego okresu, tylko w przypadku inicjowania hello zmiany. Po rozpoczęciu procesu aktualizacji hello na powitania autoryzacji urządzenia StorSimple, autoryzacji hello jest prawidłowy, dopóki wszystkie urządzenia są aktualizowane.

**Pytanie:** administratora nasze StorSimple opuścił hello firmy. Co mam zrobić?

**Odpowiedź:** zmiany i resetowania hasła, które umożliwia urządzeniu StorSimple toohello dostępu i zmienić hello usługi danych szyfrowania klucza tooensure hello nowych informacji nie jest znany personelu toounauthorized hello. Aby uzyskać instrukcje przejdź do:

* [Użyj toochange usługi Menedżer StorSimple hello hasła storsimple](storsimple-change-passwords.md)
* [Klucz szyfrowania danych usługi hello zmiany](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Konfigurowanie protokołu CHAP dla urządzenia StorSimple](storsimple-configure-chap.md)

**Pytanie:** Chcę tooprovide hello StorSimple Snapshot Manager hasła tooa hosta, który nawiązuje połączenie toohello urządzenia StorSimple, ale hello hasło nie jest dostępne. Co można zrobić?

**Odpowiedź:** jeśli pamiętasz hasła hello, należy utworzyć nowy. Następnie upewnij się, że tooinform wszystkich istniejących użytkowników, którzy hello hasło zostało zmienione i powinien zaktualizowania ich toouse klientom Witaj nowe hasło. Aby uzyskać instrukcje przejdź do:

* [Zmień hasło programu StorSimple Snapshot Manager hello](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password)
* [Uwierzytelniania urządzenia](storsimple-snapshot-manager-manage-devices.md#authenticate-a-device)

**Pytanie:** hello certyfikat dla dostępu zdalnego toohello środowiska Windows PowerShell dla urządzenia StorSimple na urządzeniu hello został zmieniony. Jak zaktualizować moich klientów dostępu zdalnego?

**Odpowiedź:** pobrać hello nowego certyfikatu z hello usługi Menedżer StorSimple, a następnie podaj go toobe zainstalowany w magazynie certyfikatów hello klientów dostępu zdalnego. Aby uzyskać instrukcje przejdź do:

* [Polecenia cmdlet Import certyfikatu](https://technet.microsoft.com/library/hh848630.aspx)

**Pytanie:** dane chronione w przypadku złamania zabezpieczeń hello usługi Menedżer StorSimple?

**Odpowiedź:** danych konfiguracji usługi są zawsze szyfrowane kluczem publicznym, podczas wyświetlania w przeglądarce sieci web. Ponieważ usługa hello nie ma klucza prywatnego toohello dostępu, hello usługi nie będą się mogli toosee żadnych danych. W przypadku naruszenia zabezpieczeń hello usługi Menedżer StorSimple nie ma żadnego wpływu, ponieważ nie kluczy przechowywanych w hello usługi Menedżer StorSimple.

**Pytanie:** Jeśli ktoś uzyska certyfikat szyfrowania danych toohello dostępu, dane może stwarzać zagrożenie?

**Odpowiedź:** Microsoft Azure przechowuje klucz szyfrowania danych powitania klienta (pfx) w postaci zaszyfrowanej. Ponieważ plik .pfx hello jest zaszyfrowany i hello usługi StorSimple nie ma pliku PFX hello toodecrypt klucza szyfrowania hello usługi danych, po prostu pobieranie pliku PFX toohello dostępu będzie uwidacznia żadnych kluczy tajnych.

**Pytanie:** co się stanie w przypadku jednostki rządowe zapyta firmy Microsoft dla danych?

**Odpowiedź:** , dlatego wszystkie hello dane są szyfrowane na powitania usługi i hello klucz prywatny jest przechowywany z urządzeniem hello hello rządowych jednostki musi uzyskać powitania klienta hello danych. 

## <a name="next-steps"></a>Następne kroki
[Wdrażanie urządzenia StorSimple](storsimple-deployment-walkthrough.md).

