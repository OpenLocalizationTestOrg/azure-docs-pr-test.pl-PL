---
title: "aaaTroubleshoot problemów z magazynu plików Azure w systemie Windows | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów magazyn plików Azure w systemie Windows"
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
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: 19529d8af5d98790e2e381cd21ad4d0284acb124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a>Rozwiązywanie problemów magazyn plików Azure w systemie Windows

W tym artykule wymieniono typowe problemy, które są powiązane tooMicrosoft magazyn plików Azure podczas nawiązywania połączenia przez klientów systemu Windows. Zapewnia także możliwe przyczyny i rozwiązania tych problemów. Ponadto toohello Rozwiązywanie problemów z kroków w tym artykule, można również użyć [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) aby upewnić się, że Windows hello środowiska klienta ma poprawne warunki wstępne. AzFileDiagnostics automatyzuje wykrywania większość objawy hello wymienionych w tym artykule i pomaga skonfigurować optymalną wydajność tooget środowiska. Informacje te można również znaleźć w hello [Rozwiązywanie problemów z udziałów plików Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) zapewnia tooassist czynności możesz problemów udziałów plików Azure łączenie/mapowanie/instalowanie.


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a>Błąd 53, 67 błąd lub 87 błąd podczas instalowania lub odinstalowania udziału plików na platformę Azure

Podczas próby toomount udostępniania plików z lokalnymi lub z różnych centrach danych, zostanie zgłoszony hello następujące błędy:

- Wystąpił błąd systemowy 53. Nie można odnaleźć ścieżki sieciowej Hello.
- Wystąpił błąd systemowy 67. Nie można odnaleźć nazwy sieci Hello.
- Wystąpił błąd systemowy 87. Parametr Hello jest nieprawidłowy.

### <a name="cause-1-unencrypted-communication-channel"></a>Przyczyny 1: Kanał komunikacyjny niezaszyfrowane

Ze względów bezpieczeństwa połączeń tooAzure udziały plików są zablokowane, jeśli nie jest szyfrowany kanał komunikacyjny hello i hello próba połączenia nie jest podejmowana z hello tym samym centrum danych, w którym znajdują się hello udziały plików platformy Azure. Szyfrowanie kanału komunikacji znajduje się tylko wtedy, gdy użytkownik hello kliencki system operacyjny obsługuje szyfrowanie protokołu SMB.

Windows 8, Windows Server 2012 i nowsze wersje każdego systemu negocjowania żądania zawierające SMB 3.0, który obsługuje szyfrowanie.

### <a name="solution-for-cause-1"></a>Rozwiązanie dla przyczyny 1

Połączenie z klienta, który wykonuje jedną z następujących hello:

- Spełnia wymagania hello systemu Windows 8 i Windows Server 2012 lub nowszy
- Nawiązuje połączenie z maszyną wirtualną w hello sam centrum danych, zgodnie z kontem magazynu platformy Azure, służący do udziału plików na platformę Azure hello hello

### <a name="cause-2-port-445-is-blocked"></a>Przyczyny 2: Port 445 jest zablokowany.

Błąd systemowy 53 lub błąd systemu 67 może wystąpić, jeśli port 445 komunikacji wychodzącej tooan plików Azure magazynu centrum danych jest zablokowana. Podsumowanie hello toosee usługodawców Zezwalaj lub nie zezwalaj na dostęp z portu 445, przejdź zbyt[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).

toounderstand czy jest to powód wiadomości powitania "Błąd systemu 53" hello, może użyć Portqry tooquery hello TCP:445 endpoint. Jeśli punkt końcowy TCP:445 hello jest wyświetlany jako filtrowane hello TCP port jest zablokowany. Poniżej przedstawiono przykładowe zapytanie:

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

Jeśli TCP port 445 jest zablokowany przez regułę wzdłuż ścieżki sieciowej hello, zostanie wyświetlony hello następujące dane wyjściowe:

  `TCP port 445 (microsoft-ds service): FILTERED`

Aby uzyskać więcej informacji o tym, jak toouse Portqry, zobacz [opis narzędzia wiersza polecenia Portqry.exe hello](https://support.microsoft.com/help/310099).

### <a name="solution-for-cause-2"></a>Rozwiązanie dla przyczyny 2

Praca z port 445 wychodzących tooopen dział IT za[zakresów adresów IP Azure](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="cause-3-ntlmv1-is-enabled"></a>Przyczyny 3: NTLMv1 jest włączona.

Błąd systemowy 53 lub błąd systemu: 87 może wystąpić, jeśli włączono komunikację NTLMv1 na powitania klienta. Magazyn plików Azure obsługuje tylko z uwierzytelniania NTLMv2. Mających włączone NTLMv1 tworzy mniej bezpiecznych klienta. W związku z tym komunikacja jest zablokowana dla usługi Magazyn plików Azure. 

toodetermine czy jest to hello Przyczyna błędu hello, sprawdź, czy ten powitania po podklucz rejestru jest ustawiona wartość tooa 3:

**Kluczu HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**

Aby uzyskać więcej informacji, zobacz hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) temacie w witrynie TechNet.

### <a name="solution-for-cause-3"></a>Rozwiązanie dla przyczyny 3

Przywróć hello **LmCompatibilityLevel** wartość toohello domyślna wartość 3 w powitania po podklucz rejestru:

  **Kluczu HKLM\SYSTEM\CurrentControlSet\Control\Lsa**

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a>Błąd 1816 "za mało zasobów jest dostępne tooprocess to polecenie" przy kopiowaniu tooan udziału plików na platformę Azure

### <a name="cause"></a>Przyczyna

Błąd 1816 odbywa się po osiągnięciu hello górny limit współbieżnych otwartych dojść, które są dozwolone dla pliku na komputerze hello, którym jest zainstalowany hello udziału plików.

### <a name="solution"></a>Rozwiązanie

Ograniczenia hello liczby równoczesnych otwartych dojść zamykając niektóre dojść, a następnie spróbuj ponownie. Aby uzyskać więcej informacji, zobacz [Lista kontrolna wydajności i skalowalności magazynu Microsoft Azure](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a>Powolne pliku kopiowanie tooand z usługi Magazyn plików Azure w systemie Windows

Niska wydajność napotkać podczas próby tootransfer pliki toohello usługa plików Azure.

- Jeśli użytkownik nie ma określonego minimalny wymagany rozmiar operacji We/Wy, zalecane jest użycie 1 MB, ponieważ hello rozmiaru we/wy, aby zapewnić optymalną wydajność.
-   Jeśli znasz zapisuje hello rozmiaru końcowego, pliku, który powiększa się z, a oprogramowanie nie ma problemów ze zgodnością, gdy hello niezapisanych tail hello pliku zawiera zera, a następnie ustaw hello rozmiar pliku z wyprzedzeniem zamiast wprowadzania każdego zapisu rozszerzanie zapisu.
-   Użyj metody copy prawo hello:
    -   Użyj [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) żadnych transferu między dwoma udziałami plików.
    -   Użyj [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) między udziałami plików na komputerze lokalnym.

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a>Zagadnienia dotyczące Windows 8.1 lub Windows Server 2012 R2

Dla klientów z systemem Windows 8.1 lub Windows Server 2012 R2, upewnij się, że hello [KB3114025](https://support.microsoft.com/help/3114025) poprawka jest zainstalowana. Ta poprawka poprawia wydajność hello Utwórz i zamknąć dojścia.

Można uruchomić następującego skryptu toocheck, czy zainstalowano poprawkę hello hello:

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

Jeśli zainstalowano poprawkę hello następujące dane wyjściowe są wyświetlane:

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> Obrazy systemu Windows Server 2012 R2 w portalu Azure Marketplace mają poprawki KB3114025 instalowane domyślnie począwszy od grudnia 2015 r.

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a>Nie folderu z literą dysku w **Mój komputer**

Jeśli mapujesz udziału plików na platformę Azure jako administrator przy użyciu polecenie net use udziału hello pojawia się toobe Brak.

### <a name="cause"></a>Przyczyna

Domyślnie Eksploratorze plików systemu Windows nie działa jako administrator. Jeśli uruchomisz polecenie net use z wiersza polecenia z uprawnieniami administracyjnymi, mapowania dysku sieciowego hello jako administrator. Ponieważ zamapowanych dysków są skoncentrowane na użytkowniku, hello konta użytkownika, który jest zalogowany nie są wyświetlane hello dysków, jeśli są one zainstalowane przy użyciu konta innego użytkownika.

### <a name="solution"></a>Rozwiązanie
Instalowanie udziału hello z wiersza polecenia bez uprawnień administratora. Alternatywnie, można wykonać [w tym temacie w witrynie TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** wartości rejestru.

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a>Polecenie net use zakończy się niepowodzeniem, jeśli konto magazynu hello zawiera ukośnik

### <a name="cause"></a>Przyczyna

polecenie net use Hello ukośnika (/) są interpretowane jako opcji wiersza polecenia. Nazwa konta użytkownika rozpoczyna się od ukośnika, mapowanie dysku hello kończy się niepowodzeniem.

### <a name="solution"></a>Rozwiązanie

Możesz użyć dowolnej z hello następujące kroki toowork wokół hello problemu:

- Uruchom następujące polecenia programu PowerShell hello:

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  Z pliku wsadowego możesz uruchomić polecenie hello w ten sposób:

  `Echo new-smbMapping ... | powershell -command –`

- Wprowadzone znaki cudzysłowu wokół hello toowork klucza tego problemu —, chyba że hello pierwszego znaku ukośnika hello. Jeśli tak jest, użyj trybie interakcyjnym hello i wprowadź swoje hasło oddzielnie lub ponownie wygenerować tooget Twoje klucze klucz, który nie zaczyna się od ukośnika.

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a>Aplikacja lub usługa nie może uzyskać dostępu zainstalowany dysk magazynu plików Azure

### <a name="cause"></a>Przyczyna

Dyski są zainstalowane dla poszczególnych użytkowników. Jeśli aplikacji lub usługi jest uruchomiony w ramach innego konta użytkownika niż hello, który zainstalowany dysk hello, aplikacja hello nie będą widzieć hello dysku.

### <a name="solution"></a>Rozwiązanie

Użyj jednej z następujących rozwiązań hello:

-   Dysk hello zainstalować z hello tego samego konta użytkownika, który zawiera aplikacji hello. Można użyć narzędzia, takiego jak narzędzia PsExec.
- Przekazywanie hello parametry nazwę i hasło użytkownika z polecenia net use hello nazwy konta magazynu hello i klucz.

Po wykonaniu tych instrukcji, może zostać wyświetlony następujący komunikat o błędzie, uruchamiając polecenie net use dla konta usługi systemu i sieci hello hello: "Wystąpił błąd systemowy 1312. Określona sesja logowania nie istnieje. Go może została już zakończona." W takim przypadku należy sprawdzić tej nazwie użytkownika hello przekazywany toonet Użyj zawiera informacje o domenie (na przykład: "[nazwa konta magazynu]. file.core.windows .net").

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a>Błąd "Kopiujesz plik docelowy tooa, który nie obsługuje szyfrowania"

Po skopiowaniu pliku za pośrednictwem sieci hello plik hello jest odszyfrowany na komputerze źródłowym hello, przekazywane w postaci zwykłego tekstu, a następnie ponownie szyfrowane w miejscu docelowym hello. Jednak zostanie wyświetlony następujący błąd, jeśli próbujesz toocopy zaszyfrowanego pliku hello: "Kopiujesz hello plik tooa docelowy nie obsługuje szyfrowania."

### <a name="cause"></a>Przyczyna
Ten problem może wystąpić, jeśli używasz systemu szyfrowania plików (EFS). Pliki zaszyfrowane przez funkcję BitLocker można tooAzure skopiowanego pliku magazynu. Magazyn plików Azure nie obsługuje jednak systemu szyfrowania plików NTFS.

### <a name="workaround"></a>Obejście problemu
toocopy pliku za pośrednictwem sieci hello, musisz najpierw musisz go odszyfrować. Użyj jednej z następujących metod hello:

- Użyj hello **skopiuj /d** polecenia. Umożliwia hello zaszyfrowane pliki toobe zapisane jako odszyfrowane pliki w miejscu docelowym hello.
- Ustaw powitania po klucz rejestru:
  - Ścieżka = HKLM\Software\Policies\Microsoft\Windows\System
  - Typ wartości = DWORD
  - Nazwa = CopyFileAllowDecryptedRemoteDestination
  - Wartość = 1

Należy pamiętać, że tego klucza rejestru hello ustawienie ma wpływ na wszystkie operacje kopii wykonywanych toonetwork udziałów.

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
