---
title: "pakiet obsługi serii StorSimple 8000 aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, odszyfrowywania i Edytuj pakiet obsługi dla danego urządzenia z serii StorSimple 8000."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a>Tworzenie i zarządzanie nimi pakiet obsługi serii StorSimple 8000

## <a name="overview"></a>Omówienie

Pakiet obsługi StorSimple jest mechanizm łatwy w użyciu, która gromadzi wszystkie dzienniki odpowiednich tooassist Microsoft Support dotyczącą rozwiązywania problemów urządzenia StorSimple. Witaj dzienniki zbierane są zaszyfrowane i skompresowane.

Ten samouczek zawiera instrukcje krok po kroku toocreate i zarządzaj nimi hello pakietu obsługi dla danego urządzenia z serii StorSimple 8000. Jeśli pracujesz z tablicą wirtualnego StorSimple, przejdź zbyt[generowanie pakietu dziennika](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="create-a-support-package"></a>Utwórz pakiet pomocy technicznej

W niektórych przypadkach należy toomanually tworzenia pakietu obsługi hello za pomocą programu Windows PowerShell dla urządzenia StorSimple. Na przykład:

* Jeśli potrzebujesz tooremove poufnych informacji z dziennika plików poprzedniego toosharing z Microsoft Support.
* Jeśli masz problemy przekazywanie pakietu hello powodu tooconnectivity problemów.

Możesz udostępniać pakietu ręcznie wygenerowane pomocy technicznej firmy Microsoft Support za pośrednictwem poczty e-mail. Wykonaj następujące kroki toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple hello.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple

1. toostart sesję programu Windows PowerShell jako administrator na komputerze zdalnym hello, który został użyty tooconnect tooyour urządzenia StorSimple, wprowadź hello następujące polecenie:
   
    `Start PowerShell`
2. W sesji środowiska Windows PowerShell hello Podłącz toohello konsoli SSAdmin urządzenia:
   
   1. Witaj wiersza polecenia wpisz:
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. Okno dialogowe hello otwiera wprowadź hasło administratora urządzenia. Witaj domyślne hasło jest _Password1_.
     
      ![Okno dialogowe poświadczenie programu PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. Kliknij przycisk **OK**.
   4. Witaj wiersza polecenia wpisz:
     
      `Enter-PSSession $MS`
3. W sesji hello, który zostanie otwarty wprowadź odpowiednie polecenie hello.
   
   * Udziały sieciowe, które są chronione hasłem wpisz:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       Zostanie wyświetlony monit o hasło, ścieżka folderu udostępnionego toohello sieci oraz hasło szyfrowania (ponieważ pakietu obsługi hello jest zaszyfrowany). W określonym folderze hello zostanie utworzona pakiet obsługi.
   * W przypadku udziałów, które nie są chronione hasłem, nie trzeba hello `-Credential` parametru. Wprowadź poniżej hello:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       Pakiet pomocy technicznej Hello został utworzony dla obu kontrolerów w folderze udostępnionym hello określonej sieci. Jest to plik zaszyfrowanych, skompresowanych, który można wysłać tooMicrosoft pomocy technicznej do rozwiązywania problemów. Aby uzyskać więcej informacji, zobacz [skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-8000-contact-microsoft-support.md).

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a>Parametry polecenia cmdlet Hello HcsSupportPackage eksportu

Można użyć następujących parametrów polecenia cmdlet hello HcsSupportPackage eksportu hello.

| Parametr | Wymagane opcjonalne | Opis |
| --- | --- | --- |
| `-Path` |Wymagane |Użyj lokalizacji hello tooprovide sieciowy folder udostępniony hello, w których hello znajduje się pakiet pomocy technicznej. |
| `-EncryptionPassphrase` |Wymagane |Użyj tooprovide toohelp hasło szyfrowania hello pakietu obsługi. |
| `-Credential` |Optional (Opcjonalność) |Użyj poświadczeń dostępu toosupply dla hello udostępnionego folderu sieciowego. |
| `-Force` |Optional (Opcjonalność) |Użyj tooskip hello szyfrowania hasła potwierdzenie kroku. |
| `-PackageTag` |Optional (Opcjonalność) |Użyj toospecify w katalogu *ścieżki* w obsłudze hello, który znajduje się pakiet. Domyślna Hello to [nazwa]-[bieżącą datę i time:yyyy-MM-dd-HH-mm-ss]. |
| `-Scope` |Optional (Opcjonalność) |Określ jako **klastra** toocreate (ustawienie domyślne) pakiet obsługi dla obu kontrolerów. Jeśli tylko dla bieżącego kontrolera hello toocreate pakietu, określić **kontrolera**. |

## <a name="edit-a-support-package"></a>Edytuj pakiet pomocy technicznej

Po wygenerowaniu pakietu obsługi może być konieczne tooedit hello pakietu tooremove poufne informacje. Mogą to być nazwy woluminów, urządzenia adresów IP i nazwy kopii zapasowej z plików dziennika hello.

> [!IMPORTANT]
> Można edytować tylko pakietu obsługi, który został wygenerowany za pomocą programu Windows PowerShell dla StorSimple. Nie można edytować pakiet utworzony w hello portalu Azure w usłudze Menedżer StorSimple urządzenia.

tooedit pakiet obsługi przed przekazaniem go w witrynie Microsoft Support hello najpierw odszyfrować pakietu obsługi hello, Edytuj pliki hello i następnie ponownie go zaszyfrować. Wykonaj następujące kroki hello.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple

1. Generowanie pakietu obsługi, jak opisano wcześniej, w [toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).
2. [Pobierz skrypt hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokalnie na komputerze klienckim.
3. Zaimportuj moduł programu Windows PowerShell hello. Określ hello ścieżki toohello folder lokalny którego zostały pobrane hello skryptu. Moduł hello tooimport, wprowadź:
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. Wszystkie pliki hello są *.aes* pliki skompresowane i szyfrowane. toodecompress i odszyfrowywania plików, wpisz:
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Należy pamiętać, że rozszerzenia rzeczywisty plik hello są teraz wyświetlane dla wszystkich plików hello.
   
    ![Edytuj pakiet, pomocy technicznej](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. Gdy zostanie wyświetlony monit o hasło szyfrowania hello, wprowadź hasło hello, który został użyty podczas tworzenia pakietu obsługi hello.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Przeglądaj toohello folderu, który zawiera pliki dziennika hello. Ponieważ teraz zdekompresować i odszyfrować hello plików dziennika, te będą mieć oryginalnego rozszerzenia pliku. Zmodyfikuj te pliki tooremove wszelkie informacje specyficzne dla klienta, takich jak nazwy woluminu i adresy IP urządzeń i Zapisz hello plików.
7. Zamknij hello pliki toocompress z gzip i szyfrowanie AES 256. Jest to szybkości i zabezpieczeń w przesyłania pakietu obsługi hello za pośrednictwem sieci. toocompress i szyfrowania plików, wprowadź następujące hello:
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Edytuj pakiet, pomocy technicznej](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. Po wyświetleniu monitu podaj hasło szyfrowania dla pakietu obsługi zmodyfikowane hello.
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. Zapisz hello nowe hasło, dzięki czemu można udostępniać Microsoft Support na żądanie.

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a>Przykład: Edytowanie plików w pakiecie pomocy technicznej w udziale chronione hasłem

Witaj poniższy przykład pokazuje, jak toodecrypt, edytować i ponownie zaszyfrować pakiet obsługi.

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o hello [informacje zebrane w hello pakietu obsługi](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)
* Dowiedz się, jak za[używana obsługa pakietów oraz urządzenia w dziennikach tootroubleshoot wdrożenia urządzenia](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

