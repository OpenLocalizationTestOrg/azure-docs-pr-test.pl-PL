---
title: "Jak usługa Azure RemoteApp zapisać danych i ustawień użytkownika? | Microsoft Docs"
description: "Dowiedz się, jak usługa Azure RemoteApp zapisuje dane użytkownika przy użyciu dysku profilu użytkownika."
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
ms.openlocfilehash: 4993bf507536659d7951e1552559cf0a6061d345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Jak usługa Azure RemoteApp zapisać danych i ustawień użytkownika?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Usługa Azure RemoteApp zapisuje dostosowania i tożsamości użytkowników między urządzeniami i sesje. Dane tego użytkownika są przechowywane na dysku dla kolekcji użytkownika, znana jako funkcja dysku profilu użytkownika (UPD). Dysk wykonuje użytkownika i gwarantuje, że użytkownik ma spójne środowisko, niezależnie od tego, gdzie zalogują się w.

Dyski profilu użytkownika są całkowicie niewidoczne dla użytkownika — użytkownicy zapisywać dokumenty do folderu Dokumenty (na co wydaje się być lokalny) i zmienianie ustawień aplikacji w zwykły sposób. W tym samym czasie wszystkie ustawienia osobiste utrwalić podczas nawiązywania połączenia z usługą Azure RemoteApp z dowolnego urządzenia. Użytkownik widzi będzie swoje dane w tym samym miejscu.

Każdy UPD 50GB magazynu trwałego a zawiera zarówno ustawień danych użytkownika i aplikacji. 

Poniżej charakterystykę na dane profilu użytkownika.

> [!NOTE]
> Należy wyłączyć UPD? Możesz zrobić tego teraz - wyewidencjonowanie Pavithra w blogu [Wyłącz dyski profilu użytkownika (UPD) w usłudze Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), aby uzyskać szczegółowe informacje.
> 
> 

## <a name="how-can-an-admin-get-to-the-data"></a>Jak administrator może uzyskać dostęp do danych?
Jeśli potrzebujesz dostępu do danych dla jednego użytkownika (w przypadku odzyskiwania po awarii lub jeśli użytkownik opuści firmę), skontaktuj się z pomocą techniczną platformy Azure i podanie informacji o subskrypcji kolekcji i tożsamości użytkownika. Zespół usługi Azure RemoteApp Podaj adres URL do dysku VHD. Pobierz tego wirtualnego dysku twardego i pobrać wszystkie dokumenty lub pliki, które są potrzebne. Należy pamiętać, że wirtualny dysk twardy 50GB, dlatego zajmie trochę jej pobranie.

## <a name="is-the-data-backed-up"></a>Jest wykonywana kopia zapasowa danych?
Tak, Zapisz kopię zapasową danych użytkownika według lokalizacji geograficznej. Danych jest tylko do odczytu i jest dostępny w taki sam sposób jak regularne dane byłyby (skontaktuj się z usługi Azure RemoteApp go), jeśli Centrum danych podstawowych jest wyłączony. Dane są kopiowane w czasie rzeczywistym do lokalizacji kopii zapasowej i firma Microsoft nie zachowuj kopii różne wersje. Tak na uszkodzenie danych, firma Microsoft nie będzie można przywrócić go do wcześniej znaną dobrą wersję, ale jeśli Centrum danych podstawowych jest wyłączony, można pobrać danych użytkownika z innej lokalizacji.

## <a name="how-do-users-see-the-upd-on-the-server-side"></a>Jak użytkownicy widzą UPD po stronie serwera?
Każdy użytkownik będzie miał ich własnego katalogu na serwerze, który jest mapowany na ich UPD: c:\Users\username.

## <a name="whats-the-best-way-to-use-outlook-and-upd"></a>Co to jest najlepszym sposobem użycia programu Outlook i UPD?
Usługa Azure RemoteApp zapisuje stan programu Outlook (skrzynek pocztowych, plików pst) między sesjami. Aby włączyć tę opcję, potrzebujemy PST mają być przechowywane w dane profilu użytkownika (c:\users\<nazwa użytkownika >). To jest domyślna lokalizacja dla danych, więc tak długo, jak lokalizacja nie należy zmieniać, dane pozostają między sesjami.

Zalecamy również używać trybu "pamięci podręcznej" w programie Outlook, a następnie "serwera/online" w trybie do wyszukiwania.

Zapoznaj się z [w tym artykule](remoteapp-outlook.md) Aby uzyskać więcej informacji o korzystaniu z programu Outlook i usługi Azure RemoteApp.

## <a name="what-about-redirection"></a>Co o przekierowywaniu?
Można skonfigurować usługę Azure RemoteApp, aby umożliwić użytkownikom dostęp do urządzeń lokalnych, konfigurując [przekierowania](remoteapp-redirection.md). Lokalne urządzenia będą w stanie uzyskać dostępu do danych w UPD.

## <a name="can-i-use-my-upd-as-a-network-share"></a>Jako udział sieciowy może używać mojego UPD?
Nie. Nie można użyć UPD jako udział sieciowy. UPD jest dostępne dla użytkownika tylko wtedy, gdy użytkownik jest aktywnie połączone z usługą Azure RemoteApp.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Jeśli użytkownik I usuwanie z kolekcji, jest usuwany ich UPD?
Nie, po usunięciu użytkownika firma Microsoft nie zostaną automatycznie usunięte UPD — zamiast tego są przechowywane dane do momentu usunięcia kolekcji. 90 dni, po usunięciu kolekcji, w razie usunięcia wszystkich UPD. 

Jeśli musisz usunąć UPD z kolekcji, skontaktuj się z usługą Azure RemoteApp — można usunąć UPD po naszej stronie.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>Można uzyskać dostęp UPD Moi użytkownicy (bieżący lub usuniętych użytkowników)?
Tak, jeśli zamierzasz zgłosić [usługi Azure RemoteApp](mailto:remoteappforum@microsoft.com), firma Microsoft można zdefiniować użytkownik z adresem URL dostępu do danych. Aby pobrać żadnych danych ani plików z UPD przed wygaśnięciem dostępu, będziesz mieć około 10 godzin.

## <a name="are-upds-available-offline"></a>UPD dostępne są w trybie offline?
W tej chwili nie udzielamy dostęp w trybie offline do UPD, poza oknie dostępu 10 godzin opisane powyżej. Oznacza to, że firma Microsoft aktualnie nie masz sposób zapewniają dostęp długo wystarczającej do ukończenia bardziej skomplikowane zadania, takie jak uruchamianie oprogramowania antywirusowego na UPD lub uzyskiwanie dostępu do danych na potrzeby inspekcji.

## <a name="do-registry-key-settings-persist"></a>Ustawienia kluczy rejestru są zachowywane?
Tak, niczego zapisywane do HKEY_Current_User jest częścią UPD.

## <a name="can-i-disable-upds-for-a-collection"></a>Dla kolekcji można wyłączyć UPD?
Tak, możesz poprosić usługi Azure RemoteApp, aby wyłączyć UPD subskrypcji, ale nie można tego użytkownika. Oznacza to, że UPD zostanie wyłączony dla wszystkich kolekcji w subskrypcji.

Możesz wyłączyć UPD w następujących sytuacjach: 

* Potrzebna jest pełna dostępu i kontroli danych użytkownika (dla inspekcji i przejrzyj celów, takich jak instytucji finansowych).
* Masz 3rd firm użytkownika profil zarządzania rozwiązań lokalnie i chcesz nadal z nich korzystać we wdrożeniu usługi Azure RemoteApp przyłączonych do domeny. Profil agenta do którego zostanie załadowana złoty obraz jest wymagany. 
* Nie ma potrzeby każdy magazyn danych lokalnych lub mają wszystkie dane w chmurze lub w udziale plików, a chcesz kontroli zapisywania danych lokalnie za pomocą usługi Azure RemoteApp.

Zobacz [Wyłącz dyski profilu użytkownika (UPD) w usłudze Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) Aby uzyskać więcej informacji.

## <a name="can-i-restrict-users-from-saving-data-to-the-system-drive"></a>Zapisywanie danych na dysk systemowy można ograniczyć użytkowników?
Tak, ale należy skonfigurować w obrazu szablonu przed utworzeniem kolekcji. Aby zablokować dostęp do dysku systemowego, wykonaj następujące kroki:

1. Uruchom **gpedit.msc** obrazu szablonu.
2. Przejdź do **Konfiguracja użytkownika > Szablony administracyjne > składniki systemu Windows > Explorer**.
3. Wybierz następujące opcje:
   * **Ukryj te określone dyski w tym komputerze**
   * **Zapobiegaj dostępowi do dysków z komputera**

## <a name="can-i-seed-upds-i-want-to-put-some-data-in-the-upd-thats-available-the-first-time-the-user-signs-in"></a>Czy może zapełnić UPD? Chcę wprowadzić niektóre dane w UPD, która jest dostępna podczas pierwszego logowania się użytkownika.
Podczas tworzenia obrazu szablonu można tak, Dodaj informacje do domyślnego profilu. Te informacje jest następnie dodawana do UPD.

## <a name="can-i-change-the-size-of-the-upd-depending-on-how-much-data-i-want-to-store"></a>Czy można zmienić rozmiar UPD w zależności od ilości danych, warto przechowywać?
Nie, wszystkie UPD ma 50 GB miejsca do magazynowania. Jeśli chcesz przechowywać różnych ilości danych, spróbuj wykonać następujące czynności:

1. Wyłącz UPD dla kolekcji.
2. Konfigurowanie użytkownikom dostępu do udziału plików.
3. Ładowanie udziału plików za pomocą skryptu uruchomieniowego. Wymienione poniżej, aby uzyskać więcej informacji na temat uruchamiania skryptów w usłudze Azure RemoteApp.
4. Bezpośrednie użytkownikom na zapisywanie wszystkich danych do udziału plików.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>Jak uruchomić skrypt uruchamiania w usłudze Azure RemoteApp?
Jeśli chcesz uruchomić skrypt uruchamiania, Rozpocznij od utworzenia zaplanowane zadanie w obrazie szablonu, którego chcesz użyć dla kolekcji. (W tym *przed* Uruchom program sysprep.) 

![Utwórz zadanie systemowe](./media/remoteapp-upd/upd1.png)

![Utwórz zadania systemowego, który jest uruchamiany, gdy użytkownik loguje się](./media/remoteapp-upd/upd2.png)

Na **ogólne** karcie, należy zmienić **konta użytkownika** zabezpieczenia do "BUILTIN\Użytkownicy."

![Zmień konto użytkownika do grupy](./media/remoteapp-upd/upd4.png)

Zaplanowane zadanie uruchamia skrypt uruchamiania przy użyciu poświadczeń użytkownika. Zaplanuj uruchomienie zadania każdym razem, kiedy użytkownik loguje się.

![Ustaw wyzwalacz dla zadania "na logowanie"](./media/remoteapp-upd/upd3.png)

Można również użyć [skrypty uruchamiania oparte na zasadach grupy](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-the-start-menu-would-that-work"></a>Co zrobić w Start menu wprowadzania do skryptu uruchamiania? Czy to pomoże?
Innymi słowy można I Utwórz plik .bat, który uruchamia skrypt okno konfiguracji i zapisać go w folderze Start\Programy\Autostart c:\ProgramData\Microsoft\Windows\Start oraz zmuszony tego skryptu, uruchom przy każdym uruchomieniu sesji usługi RemoteApp?

Nie, który nie jest obsługiwany z usługą Azure RemoteApp, która używa RDSH, który nie obsługuje również skrypty uruchamiania w Start menu.

## <a name="can-i-use-mstscexe-the-remote-desktop-program-to-configure-logon-scripts"></a>Aby skonfigurować skrypty logowania można używać mstsc.exe (program pulpitu zdalnego)?
Nie, dziękuję nie obsługiwane przez usługę Azure RemoteApp.

## <a name="can-i-store-data-on-the-vm-locally"></a>Czy mogę przechowywać dane lokalnie w maszynie wirtualnej
Nie, zostaną utracone dane przechowywane w dowolnym miejscu na maszynie Wirtualnej innej niż w UPD. Istnieje wysokie prawdopodobieństwo użytkownik nie otrzyma tej samej maszyny Wirtualnej następnej razem zalogują się do usługi Azure RemoteApp. Firma Microsoft nie obsługują trwałości maszyny Wirtualnej użytkownika, dzięki czemu użytkownik nie będzie zalogować się do tej samej maszyny Wirtualnej i dane zostaną utracone. Ponadto podczas aktualizowania kolekcji, istniejące maszyny wirtualne są zastępowane nowy zestaw maszyn wirtualnych — oznacza, że dane przechowywane na samej maszyny Wirtualnej zostaną utracone. To zalecanie służy do przechowywania danych w UPD magazynu udostępnionego, takich jak pliki Azure, serwer plików w sieci Wirtualnej lub w chmurze przy użyciu systemu magazynu chmurze, takiego jak DropBox.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>Jak zainstalować udział plików Azure na maszynie Wirtualnej, przy użyciu programu PowerShell?
Polecenia cmdlet elementu PSDrive Net służy do instalacji na dysku, w następujący sposób:

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


Można także zapisać swoje poświadczenia, uruchamiając następujące czynności:

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Umożliwia Pomiń parametr Credential w poleceniu cmdlet New-elementu PSDrive.

