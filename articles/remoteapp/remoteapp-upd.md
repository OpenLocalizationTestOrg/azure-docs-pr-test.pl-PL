---
title: "aaaHow oznacza usługę Azure RemoteApp zapisywania danych i ustawień użytkownika? | Microsoft Docs"
description: "Dowiedz się, jak usługa Azure RemoteApp zapisuje dane użytkownika przy użyciu dysku profilu użytkownika hello."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Jak usługa Azure RemoteApp zapisać danych i ustawień użytkownika?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp zapisuje dostosowania i tożsamości użytkowników między urządzeniami i sesje. Dane tego użytkownika są przechowywane na dysku dla kolekcji użytkownika, znana jako funkcja dysku profilu użytkownika (UPD). dysk Hello następuje hello użytkownika i gwarantuje, że użytkownik hello ma spójne środowisko, niezależnie od tego, gdzie zalogują się w.

Dyski profilu użytkownika są całkowicie niewidoczne toohello użytkownika — użytkownicy zapisać folderu Dokumenty tootheir dokumentów (na wyświetlaną toobe dysk lokalny) i zmienianie ustawień aplikacji w zwykły sposób. At hello takie same ustawienia w czasie, wszystkie osobiste utrwalić podczas nawiązywania połączenia programów RemoteApp tooAzure z dowolnego urządzenia. Wszystkie użytkownika hello widzi swoje dane w hello jest tym samym miejscu.

Każdy UPD 50GB magazynu trwałego a zawiera zarówno ustawień danych użytkownika i aplikacji. 

Poniżej charakterystykę na dane profilu użytkownika.

> [!NOTE]
> Witaj toodisable potrzeby UPD? Możesz zrobić tego teraz - wyewidencjonowanie Pavithra w blogu [Wyłącz dyski profilu użytkownika (UPD) w usłudze Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), aby uzyskać szczegółowe informacje.
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a>Jak administrator może pobrać dane toohello?
Jeśli potrzebujesz tooaccess hello danych dla jednego użytkownika (w przypadku odzyskiwania po awarii lub jeśli hello użytkownik opuści firmę hello), skontaktuj się z pomocą techniczną platformy Azure i podanie informacji o subskrypcji hello hello kolekcji i tożsamości użytkownika hello. Zespół usługi Azure RemoteApp Hello Podaj adres URL toohello wirtualnego dysku twardego. Pobierz tego wirtualnego dysku twardego i pobrać wszystkie dokumenty lub pliki, które są potrzebne. Należy pamiętać, że hello wirtualnego dysku twardego jest 50GB, potrwa bit toodownload go.

## <a name="is-hello-data-backed-up"></a>Jest hello utworzyć kopię zapasową danych?
Tak, Zapisz kopię zapasową danych użytkownika hello według lokalizacji geograficznej. Hello danych jest tylko do odczytu i można uzyskać w hello sam sposób jak hello regularne dane byłyby (skontaktuj się z usługą Azure RemoteApp tooget go), jeśli Centrum danych podstawowych hello jest wyłączony. Hello dane są kopiowane w czasie rzeczywistym toohello lokalizacji kopii zapasowej i firma Microsoft nie zachowuj kopii różne wersje. Tak, na uszkodzenie danych, firma Microsoft nie będzie możliwe toorestore on tooa wcześniej znana dobra wersji, ale jeśli Centrum danych podstawowych hello jest wyłączony, będziesz w stanie tooget danych użytkownika z hello z innej lokalizacji.

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a>Jak użytkownicy widzą hello UPD na powitania po stronie serwera?
Każdy użytkownik będzie miał ich własnego katalogu na serwerze hello, która mapuje tootheir UPD: c:\Users\username.

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a>Co to jest hello najlepsze sposób toouse programu Outlook i UPD?
Usługa Azure RemoteApp zapisuje stan Outlook hello (skrzynek pocztowych, plików pst) między sesjami. tooenable, możemy muszą hello toobe PST przechowywane w dane profilu użytkownika hello (c:\users\<nazwa użytkownika >). Jest to domyślna lokalizacja hello hello danych, więc tak długo, jak lokalizacja hello nie należy zmieniać, pozostanie hello danych między sesjami.

Zalecamy również używać trybu "pamięci podręcznej" w programie Outlook, a następnie "serwera/online" w trybie do wyszukiwania.

Zapoznaj się z [w tym artykule](remoteapp-outlook.md) Aby uzyskać więcej informacji o korzystaniu z programu Outlook i usługi Azure RemoteApp.

## <a name="what-about-redirection"></a>Co o przekierowywaniu?
Można skonfigurować usługę Azure RemoteApp toolet użytkownikom dostęp do urządzeń lokalnych, konfigurując [przekierowania](remoteapp-redirection.md). Lokalne urządzenia będą w stanie tooaccess hello danych na powitania UPD.

## <a name="can-i-use-my-upd-as-a-network-share"></a>Jako udział sieciowy może używać mojego UPD?
Nie. Nie można użyć UPD jako udział sieciowy. UPD jest tylko dostępne toohello użytkownika, gdy użytkownik hello jest aktywnie połączone tooAzure programów RemoteApp.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Jeśli użytkownik I usuwanie z kolekcji, jest usuwany ich UPD?
Nie, po usunięciu użytkownika firma Microsoft nie zostaną automatycznie usunięte hello UPD — zamiast tego są przechowywane dane hello do momentu usunięcia hello kolekcji. 90 dni, po usunięciu hello kolekcji, w razie usunięcia wszystkich UPD. 

Jeśli potrzebujesz toodelete UPD z kolekcji, skontaktuj się z usługą Azure RemoteApp — można usunąć UPD po naszej stronie.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>Można uzyskać dostęp UPD Moi użytkownicy (bieżący lub usuniętych użytkowników)?
Tak, jeśli zamierzasz zgłosić [usługi Azure RemoteApp](mailto:remoteappforum@microsoft.com), możemy skonfigurować możesz tooaccess adres URL hello danych. Będziesz mieć o 10 godzin toodownload wszelkie dane i pliki z hello UPD przed wygaśnięciem hello dostępu.

## <a name="are-upds-available-offline"></a>UPD dostępne są w trybie offline?
W tej chwili nie udzielamy tooUPDs dostęp w trybie offline, poza okno dostępu 10 godzin hello opisane powyżej. Oznacza to, że firma Microsoft nie dysponuje tooprovide sposób, z dostęp wystarczająco długie zadań toocomplete bardziej skomplikowane, takie jak uruchamianie oprogramowania antywirusowego na powitania UPD lub uzyskiwanie dostępu do danych na potrzeby inspekcji.

## <a name="do-registry-key-settings-persist"></a>Ustawienia kluczy rejestru są zachowywane?
Tak, niczego zapisywane tooHKEY_Current_User jest częścią hello UPD.

## <a name="can-i-disable-upds-for-a-collection"></a>Dla kolekcji można wyłączyć UPD?
Tak, poproś toodisable usługi Azure RemoteApp UPD subskrypcji, ale nie można tego użytkownika. Oznacza to, że dla wszystkich kolekcji w subskrypcji hello UPD zostanie wyłączone.

Może być UPD toodisable w żadnym hello następujące sytuacje: 

* Potrzebna jest pełna dostępu i kontroli danych użytkownika (dla inspekcji i przejrzyj celów, takich jak instytucji finansowych).
* Masz 3rd firm użytkownika profil zarządzania rozwiązań lokalnie i chcesz toocontinue ich użycie w danym wdrożeniu przyłączonych do domeny usługi Azure RemoteApp. Toobe agenta profilu hello ładowane do hello złoty obraz jest wymagany. 
* Nie ma potrzeby każdy magazyn danych lokalnych lub mają wszystkie dane w hello chmury lub w udziale plików i chcesz toocontrol zapisywania danych lokalnie za pomocą usługi Azure RemoteApp.

Zobacz [Wyłącz dyski profilu użytkownika (UPD) w usłudze Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) Aby uzyskać więcej informacji.

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a>Zapisywanie dysk systemowy toohello danych można ograniczyć użytkowników?
Tak, ale należy tooset, który się w szablonie hello obraz przed utworzeniem hello kolekcji. Użyj powitania po dysk systemowy toohello dostępu tooblock kroki:

1. Uruchom **gpedit.msc** na powitania obrazu szablonu.
2. Przejdź za**Konfiguracja użytkownika > Szablony administracyjne > składniki systemu Windows > Explorer**.
3. Wybierz hello następujące opcje:
   * **Ukryj te określone dyski w tym komputerze**
   * **Zapobiegaj toodrives dostęp z komputera**

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a>Czy może zapełnić UPD? Chcę tooput, który loguje się niektóre dane w hello UPD, który jest dostępny hello pierwszego czasu hello użytkownika.
Tak, podczas tworzenia obrazu szablonu hello można dodać profil domyślny toohello informacji. Te informacje są następnie dodawane toohello UPD.

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a>Można zmienić rozmiar hello hello UPD w zależności od ilości danych ma toostore?
Nie, wszystkie UPD ma 50 GB miejsca do magazynowania. Jeśli chcesz toostore różnych ilości danych, spróbuj następujących hello:

1. Wyłącz UPD hello kolekcji.
2. Konfigurowanie udziału plików dla tooaccess użytkowników.
3. Udział plików hello obciążenia za pomocą skryptu uruchomieniowego. Wymienione poniżej, aby uzyskać więcej informacji na temat uruchamiania skryptów w usłudze Azure RemoteApp.
4. Kierowanie wszystkich udziału plików toohello danych toosave użytkowników.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>Jak uruchomić skrypt uruchamiania w usłudze Azure RemoteApp?
Jeśli chcesz toorun skryptu uruchamiania, należy uruchomić przy tworzeniu zaplanowanego zadania w obrazie szablonu hello ma toouse hello kolekcji. (W tym *przed* Uruchom program sysprep.) 

![Utwórz zadanie systemowe](./media/remoteapp-upd/upd1.png)

![Utwórz zadania systemowego, który jest uruchamiany, gdy użytkownik loguje się](./media/remoteapp-upd/upd2.png)

Na powitania **ogólne** karcie, można się hello toochange **konta użytkownika** zabezpieczenia zbyt "BUILTIN\Użytkownicy."

![Zmień grupę tooa konta użytkownika hello](./media/remoteapp-upd/upd4.png)

zaplanowane zadanie Hello spowoduje uruchomienie skryptu uruchamiania, przy użyciu poświadczeń użytkownika hello. Zaplanuj hello zadań toorun każdym razem, kiedy użytkownik loguje się.

![Zestaw hello wyzwalacz zadania hello "W logowania"](./media/remoteapp-upd/upd3.png)

Można również użyć [skrypty uruchamiania oparte na zasadach grupy](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a>Menu Start co umieszczenie skryptu uruchamiania w hello? Czy to pomoże?
Innymi słowy można I Utwórz plik .bat, który uruchamia skrypt okno konfiguracji i zapisz go w folderze Start\Programy\Autostart c:\ProgramData\Microsoft\Windows\Start toohello oraz zmuszony tego skryptu, uruchom przy każdym uruchomieniu sesji usługi RemoteApp?

Nie, który nie jest obsługiwany z usługą Azure RemoteApp, która używa RDSH, który nie obsługuje również skrypty uruchamiania w hello Start menu.

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a>Można użyć skryptów logowania tooconfigure (program hello pulpitu zdalnego) mstsc.exe?
Nie, dziękuję nie obsługiwane przez usługę Azure RemoteApp.

## <a name="can-i-store-data-on-hello-vm-locally"></a>Czy mogę przechowywać dane lokalnie hello maszyny Wirtualnej?
Nie, przechowywany w dowolnym miejscu na powitania maszyn wirtualnych innych niż w hello UPD dane zostaną utracone. Brak użytkownika hello dużym prawdopodobieństwem nie zapewni hello tej samej maszyny Wirtualnej hello następnym razem zalogują się do usługi Azure RemoteApp. Firma Microsoft nie obsługują trwałości maszyny Wirtualnej użytkownika, więc użytkownik hello nie będzie zalogować się do tej samej maszyny Wirtualnej hello i hello dane zostaną utracone. Ponadto podczas aktualizowania kolekcji hello, powitalne istniejące maszyny wirtualne są zamieniane na nowy zestaw maszyn wirtualnych — oznacza, że dane przechowywane na powitania samej maszyny Wirtualnej zostaną utracone. zalecenie Hello są danymi toostore hello UPD, udostępnionego magazynu, takich jak pliki Azure, serwer plików w sieci Wirtualnej lub w chmurze hello przy użyciu systemu magazynu chmurze, takiego jak DropBox.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>Jak zainstalować udział plików Azure na maszynie Wirtualnej, przy użyciu programu PowerShell?
Program hello elementu PSDrive Net polecenia cmdlet toomount hello stacji w następujący sposób:

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


Można także zapisać swoje poświadczenia, uruchamiając następujące hello:

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Umożliwia pominąć hello — parametr Credential w poleceniu cmdlet hello elementu PSDrive nowy.

