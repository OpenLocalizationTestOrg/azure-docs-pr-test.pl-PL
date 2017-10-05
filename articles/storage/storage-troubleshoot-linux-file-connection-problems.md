---
title: "Rozwiązywanie problemów magazyn plików Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów magazyn plików Azure w systemie Linux"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 62cd62ec3a2900f06acacc0852a48b5e3ff1c8cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Rozwiązywanie problemów magazyn plików Azure w systemie Linux

W tym artykule wymieniono typowe problemy, które są związane z magazyn plików Microsoft Azure, podczas łączenia z klientów systemu Linux. Zapewnia także możliwe przyczyny i rozwiązania tych problemów.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a>"Przekroczono przydział dysku [odmówiono uprawnienia]" podczas próby otwarcia pliku

W systemie Linux pojawi się komunikat o błędzie podobny do następującego:

**<filename>[odmówiono uprawnienia] Przekroczono przydział dysku**

### <a name="cause"></a>Przyczyna

Osiągnięto górny limit współbieżnych otwartych dojść, które są dozwolone dla pliku.

### <a name="solution"></a>Rozwiązanie

Zmniejszyć liczbę jednoczesnych otwartych dojść zamykając niektóre dojść, a następnie spróbuj ponownie wykonać operację. Aby uzyskać więcej informacji, zobacz [Lista kontrolna wydajności i skalowalności magazynu Microsoft Azure](storage-performance-checklist.md).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-linux"></a>Powolna kopiowanie plików do i z usługi Magazyn plików Azure w systemie Linux

-   Jeśli użytkownik nie ma określonego minimalny wymagany rozmiar operacji We/Wy, zalecane jest użycie 1 MB jako rozmiaru we/wy do uzyskania optymalnej wydajności.
-   Jeśli znasz końcowego rozmiar pliku, który powiększa się przy użyciu operacji zapisu, a oprogramowania nie występują problemy ze zgodnością, podczas niezapisanych tail na plik zawiera zera, następnie ustaw rozmiar pliku z wyprzedzeniem zamiast wprowadzania każdego zapisu rozszerzanie zapisu.
-   Użyj metody copy prawa:
    -   Użyj [AzCopy](storage-use-azcopy.md#file-copy) żadnych transferu między dwoma udziałami plików.
    -   Użyj [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) między udziałami plików na komputerze lokalnym.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>"Instalowanie error(112): Host nie działa" z powodu limitu ponowne nawiązanie połączenia

Błąd instalacji "112" występuje na komputerze klienckim systemu Linux, gdy klient był bezczynny przez długi czas. Po dłuższy czas bezczynności klient odłączy się i limit czasu połączenia.  

### <a name="cause"></a>Przyczyna

Połączenie może być bezczynne z następujących powodów:

-   Błędy komunikacji sieciowej uniemożliwiające ponowne ustanowienie połączenie TCP z serwerem, gdy jest używana opcja instalacji "ciąg soft" domyślne
-   Najnowsze poprawki ponowne nawiązanie połączenia, które nie są obecne w starszych jądra

### <a name="solution"></a>Rozwiązanie

To ponowne nawiązanie połączenia jądra systemu Linux teraz problemu w ramach następujących zmian:

- [Poprawka nawiązywać nie mają być odroczone sesji protokołu smb3 ponownie gdy ponownego połączenia gniazda](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Wywołanie usługi echo natychmiast po ponownego połączenia gniazda](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS: Naprawić uszkodzenie pamięci możliwe podczas ponownego nawiązania połączenia](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: Usuń możliwe podwójne blokowanie obiektu mutex podczas ponownego nawiązania połączenia (dla jądra v4.9 i nowsze)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

Jednak te zmiany mogą nie być przenoszone jeszcze do wszystkich dystrybucje systemu Linux. Ta poprawka i inne poprawki ponowne nawiązanie połączenia są wprowadzane w następujących popularnych jądra systemu Linux: 4.4.40, 4.8.16 i 4.9.1. Ta poprawka można uzyskać przez uaktualnienie do wersji zalecane jądra.

### <a name="workaround"></a>Obejście problemu

Ten problem można obejść, określając instalacji twardej. Dzięki temu klient czekać do momentu jest nawiązywane połączenie lub go jawnie zostanie przerwane i pozwala uniknąć błędów z powodu limitów czasu w sieci. To rozwiązanie może jednak spowodować nieograniczonego oczekiwania. Przygotuj się do zatrzymania połączenia w razie potrzeby.

Jeśli nie można uaktualnić do najnowszej wersji jądra, można obejść ten problem, przechowując pliku w udziale plików na platformę Azure, który można zapisać co 30 sekund lub mniej. Musi to być operacji zapisu, takie jak ponowne zapisywanie Data utworzone lub zmodyfikowane na plik. W przeciwnym razie może uzyskiwać wyniki z pamięci podręcznej, a operacja nie może wyzwolić ponowne połączenie.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>"Instalowanie error(115): operacja w toku" podczas instalowania usługi Magazyn plików Azure przy użyciu protokołu SMB 3.0

### <a name="cause"></a>Przyczyna

Niektóre dystrybucje systemu Linux nie jest jeszcze obsługiwany funkcji szyfrowania protokołu SMB 3.0 i użytkowników może zostać wyświetlony komunikat o błędzie "115", jeśli próby instalacji usługi Azure File storage przy użyciu protokołu SMB 3.0 ze względu na Brak funkcji.

### <a name="solution"></a>Rozwiązanie

Funkcja szyfrowania protokołu SMB 3.0 dla systemu Linux została wprowadzona w 4.11 jądra. Ta funkcja umożliwia instalowanie udziału plików platformy Azure z lokalnej lub w innym regionie Azure. Podczas publikowania ta funkcja została backported Ubuntu 17.04 i Ubuntu 16.10. Jeśli klienta SMB systemu Linux nie obsługuje szyfrowania, należy zainstalować magazyn plików Azure przy użyciu protokołu SMB 2.1 z maszyny Wirtualnej systemu Linux platformy Azure, który znajduje się w tym samym centrum danych, co konto magazynu plików.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Niska wydajność w udziale plików na platformę Azure zainstalowane na maszynie Wirtualnej systemu Linux

### <a name="cause"></a>Przyczyna

Jedną z możliwych przyczyn niską wydajność jest wyłączone buforowanie.

### <a name="solution"></a>Rozwiązanie

Aby sprawdzić, czy buforowanie jest wyłączone, należy wyszukać **pamięci podręcznej =** wpisu. 

**Pamięć podręczna = Brak** wskazuje, że buforowanie jest wyłączone.  Zainstaluj udziału za pomocą polecenia instalacji domyślnej lub jawnie dodając **pamięci podręcznej = strict** jest włączona opcja instalacji polecenie, aby zapewnić tym buforowanie domyślne lub "strict" tryb buforowania.

W niektórych scenariuszach **serverino** opcji instalacji może spowodować **ls** polecenie do uruchomienia stat dla każdego wpisu w katalogu. Ten problem powoduje spadek wydajności podczas jest wyświetlania katalogu duży. Opcje instalacji można sprawdzić Twojej **/etc/fstab** wpis:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

Możesz również sprawdzić, czy prawidłowe opcje są używane przez uruchomienie **instalacji sudo | grep cifs** polecenia i sprawdzanie danych wyjściowych, takie jak następujące przykładowe dane wyjściowe:

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Jeśli **pamięci podręcznej = strict** lub **serverino** opcja jest nie istnieje, odinstaluj i ponownie zainstalować magazyn plików Azure za pomocą polecenia instalacji z [dokumentacji](storage-how-to-use-files-linux.md). Następnie, która ponownie **/etc/fstab** wpis ma prawidłowe opcje.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a>Sygnatury czasowe zostały utracone podczas kopiowania plików z systemu Windows do systemu Linux

Na platformach systemu Linux/Unix **cp -p** polecenie kończy się niepowodzeniem, jeśli plik 1 i 2 plików należą do firmy przez różnych użytkowników.

### <a name="cause"></a>Przyczyna

Flagi force **f** w COPYFILE powoduje wykonywania **cp -p -f** w systemie Unix. To polecenie nie powiedzie się także zachować sygnatury czasowej pliku, który nie jesteś właścicielem.

### <a name="workaround"></a>Obejście problemu

Użyj użytkownika konta magazynu do kopiowania plików:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.

Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.
