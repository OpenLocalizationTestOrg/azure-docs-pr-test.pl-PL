---
title: "aaaTroubleshoot problemów z magazynu plików Azure w systemie Linux | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4bdc3c6ed2e48f245060a03632fca9bd14d33545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Rozwiązywanie problemów magazyn plików Azure w systemie Linux

W tym artykule wymieniono typowe problemy, które są powiązane tooMicrosoft magazyn plików Azure po ustanowieniu połączenia od klientów systemu Linux. Zapewnia także możliwe przyczyny i rozwiązania tych problemów.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a>"Przekroczono przydział dysku [odmówiono uprawnienia]" podczas próby tooopen pliku

W systemie Linux pojawi się komunikat o błędzie podobny hello następujące czynności:

**<filename>[odmówiono uprawnienia] Przekroczono przydział dysku**

### <a name="cause"></a>Przyczyna

Osiągnięto hello górny limit współbieżnych otwartych dojść, które są dozwolone dla pliku.

### <a name="solution"></a>Rozwiązanie

Ograniczenia hello liczby równoczesnych otwartych dojść zamykając niektóre dojść, a następnie ponów operację hello. Aby uzyskać więcej informacji, zobacz [Lista kontrolna wydajności i skalowalności magazynu Microsoft Azure](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a>Powolne pliku kopiowanie tooand z usługi Magazyn plików Azure w systemie Linux

-   Jeśli użytkownik nie ma określonego minimalny wymagany rozmiar operacji We/Wy, zalecane jest użycie 1 MB, ponieważ hello rozmiaru we/wy, aby zapewnić optymalną wydajność.
-   Jeśli znasz hello rozmiaru końcowego, pliku, który powiększa się przy użyciu operacji zapisu, a oprogramowania nie występują problemy ze zgodnością, podczas niezapisanych tail hello pliku zawiera zera, ustaw rozmiar pliku hello wcześniej zamiast wprowadzania każdego zapisu rozszerzanie zapis.
-   Użyj metody copy prawo hello:
    -   Użyj [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) żadnych transferu między dwoma udziałami plików.
    -   Użyj [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) między udziałami plików na komputerze lokalnym.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>"Instalowanie error(112): Host nie działa" z powodu limitu ponowne nawiązanie połączenia

Błąd instalacji "112" występuje na powitania klienta systemu Linux, gdy długo powitania klienta. Po dłuższy czas bezczynności rozłączy powitania klienta i limit czasu połączenia hello.  

### <a name="cause"></a>Przyczyna

Witaj połączenia może być bezczynne dla hello z następujących powodów:

-   Błędy komunikacji sieci, które uniemożliwiają ponowne ustanowienie serwer toohello połączenia TCP, gdy jest używana opcja instalacji "ciąg soft" domyślne hello
-   Najnowsze poprawki ponowne nawiązanie połączenia, które nie są obecne w starszych jądra

### <a name="solution"></a>Rozwiązanie

To ponowne nawiązanie połączenia jądra systemu Linux hello teraz problemu jako część hello następujące zmiany:

- [Poprawka ponownie toonot odroczenie sesji protokołu smb3 ponownie gdy ponownego połączenia gniazda](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Wywołanie usługi echo natychmiast po ponownego połączenia gniazda](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS: Naprawić uszkodzenie pamięci możliwe podczas ponownego nawiązania połączenia](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: Usuń możliwe podwójne blokowanie obiektu mutex podczas ponownego nawiązania połączenia (dla jądra v4.9 i nowsze)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

Jednak te zmiany nie mogą być przenoszone, jeszcze tooall hello dystrybucje systemu Linux. Ta poprawka i inne poprawki ponowne nawiązanie połączenia są wprowadzane w powitania po popularnych jądra systemu Linux: 4.4.40, 4.8.16 i 4.9.1. Ta poprawka można uzyskać przez uaktualnienie tooone te wersje zalecane jądra.

### <a name="workaround"></a>Obejście problemu

Ten problem można obejść, określając instalacji twardej. Wymusza powitania klienta toowait, dopóki nie zostanie nawiązane połączenie lub do momentu jawnie zostało przerwane i może być używane tooprevent błędy z powodu limitów czasu sieci. To rozwiązanie może jednak spowodować nieograniczonego oczekiwania. Należy przygotować toostop połączeń w razie potrzeby.

Jeśli nie można uaktualnić toohello najnowsze wersje jądra, można obejść ten problem, przechowując pliku w udziale plików na platformę Azure hello zapisu tooevery 30 sekund lub mniej. Musi to być operacji zapisu, takie jak ponowne zapisywanie hello utworzone lub Data modyfikacji pliku hello. W przeciwnym razie może uzyskiwać wyniki z pamięci podręcznej, a operacja nie może wyzwolić hello ponowne nawiązanie połączenia.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>"Instalowanie error(115): operacja w toku" podczas instalowania usługi Magazyn plików Azure przy użyciu protokołu SMB 3.0

### <a name="cause"></a>Przyczyna

Niektóre dystrybucje systemu Linux nie jest jeszcze obsługiwany funkcji szyfrowania protokołu SMB 3.0 i użytkowników może zostać wyświetlony komunikat o błędzie "115", jeśli próbują toomount usługi Magazyn plików Azure przy użyciu protokołu SMB 3.0 ze względu na Brak funkcji.

### <a name="solution"></a>Rozwiązanie

Funkcja szyfrowania protokołu SMB 3.0 dla systemu Linux została wprowadzona w 4.11 jądra. Ta funkcja umożliwia instalowanie udziału plików platformy Azure z lokalnej lub w innym regionie Azure. W czasie hello publikowania ta funkcja została backported tooUbuntu 17.04 i Ubuntu 16.10. Jeśli klienta SMB systemu Linux nie obsługuje szyfrowania, należy zainstalować magazyn plików Azure przy użyciu protokołu SMB 2.1 z maszyny Wirtualnej systemu Linux platformy Azure, który znajduje się w hello tym samym centrum danych, ponieważ hello konta magazynu plików.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Niska wydajność w udziale plików na platformę Azure zainstalowane na maszynie Wirtualnej systemu Linux

### <a name="cause"></a>Przyczyna

Jedną z możliwych przyczyn niską wydajność jest wyłączone buforowanie.

### <a name="solution"></a>Rozwiązanie

toocheck czy buforowanie jest wyłączone, wyszukaj hello **pamięci podręcznej =** wpisu. 

**Pamięć podręczna = Brak** wskazuje, że buforowanie jest wyłączone.  Zainstalowanie hello udziału za pomocą polecenia instalacji domyślnej hello lub dodając jawnie hello **pamięci podręcznej = strict** tooensure polecenia instalacji toohello opcja, która domyślny tryb buforowania buforowania lub "strict" jest włączona.

W niektórych scenariuszach hello **serverino** opcji instalacji może spowodować hello **ls** stat toorun polecenie dla każdego wpisu w katalogu. Ten problem powoduje spadek wydajności podczas jest wyświetlania katalogu duży. Opcje instalacji hello można sprawdzić Twojej **/etc/fstab** wpis:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

Możesz również sprawdzić, czy prawidłowe opcje hello są używane przez uruchomienie hello **instalacji sudo | grep cifs** polecenia i sprawdzanie danych wyjściowych, takich jak hello następujące przykładowe dane wyjściowe:

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Jeśli hello **pamięci podręcznej = strict** lub **serverino** opcja jest nie istnieje, odinstaluj i ponownie zainstalować magazyn plików Azure, uruchamiając polecenie instalacji hello z hello [dokumentacji](../storage-how-to-use-files-linux.md). Następnie, sprawdź ponownie tego hello **/etc/fstab** wpis ma hello wybraniu odpowiednich opcji.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a>Sygnatury czasowe zostały utracone podczas kopiowania plików z tooLinux systemu Windows

Na platformach systemu Linux/Unix hello **cp -p** polecenie kończy się niepowodzeniem, jeśli plik 1 i 2 plików należą do firmy przez różnych użytkowników.

### <a name="cause"></a>Przyczyna

Witaj flagi force **f** w COPYFILE powoduje wykonywania **cp -p -f** w systemie Unix. To polecenie nie powiedzie się także sygnaturę czasową hello toopreserve hello pliku, który nie jesteś właścicielem.

### <a name="workaround"></a>Obejście problemu

Użyj hello magazynu konta użytkownika do kopiowania plików hello:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.

Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
