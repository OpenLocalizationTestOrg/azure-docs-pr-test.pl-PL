---
title: "aaaCreate pakietu obsługi StorSimple | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, odszyfrowywania i Edytuj pakiet obsługi dla urządzenia StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a>Tworzenie i zarządzanie nimi pakietu obsługi StorSimple
## <a name="overview"></a>Omówienie
Pakiet obsługi StorSimple jest mechanizm łatwy w użyciu, która gromadzi wszystkie dzienniki odpowiednich tooassist Microsoft Support dotyczącą rozwiązywania problemów urządzenia StorSimple. Witaj dzienniki zbierane są zaszyfrowane i skompresowane.

Ten samouczek zawiera instrukcje krok po kroku toocreate i zarządzaj nimi hello pakietu obsługi.

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a>Utworzyć i załadować pakiet obsługi w hello klasycznego portalu Azure
Możesz utworzyć i przekazać lokacji obsługi pakietu toohello Support firmy Microsoft za pośrednictwem hello **konserwacji** strony usługi hello w hello klasycznego portalu Azure.

> [!NOTE]
> przekazywanie Hello wymaga klucza dostępu pomocy technicznej. Specjalistą pomocy technicznej powinien zapewnić tym tooyou w wiadomości e-mail.
> 
> 

Pakiet obsługi zaszyfrowane i skompresowane (plik .cab) jest utworzony i przekazane toohello witrynę pomocy technicznej. Hello inżynier pomocy technicznej może następnie pobrać tego pakietu z hello witrynę pomocy technicznej, aby rozwiązać problem hello.

Wykonaj następujące kroki w hello klasycznego portalu toocreate pakietu obsługi hello.

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a>toocreate pakiet pomocy technicznej w hello klasycznego portalu Azure
1. Wybierz **urządzeń** > **konserwacji**.
2. W hello **pakietu obsługi** zaznacz **tworzenie i przekazywanie pakietu obsługi**.
3. W hello **tworzenie i przekazywanie pakietu obsługi** okna dialogowego pozycję hello następujące:
   
    ![Utwórz pakiet pomocy technicznej](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * W hello **klucz dostępu pomocy technicznej** tekst Wprowadź hello klucz dostępu. Specjalistą pomocy technicznej firmy Microsoft należy wysłać ten klucz dostępu tooyou w wiadomości e-mail.
   * Wybierz hello pole wyboru tooprovide zgody tooautomatically przekazywania hello pomocy technicznej pakietu toohello Microsoft Support lokację.
   * Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-create-manage-support-package/IC740895.png).

## <a name="manually-create-a-support-package"></a>Ręcznie Utwórz pakiet pomocy technicznej
W niektórych przypadkach należy toomanually tworzenia pakietu obsługi hello za pomocą programu Windows PowerShell dla urządzenia StorSimple. Na przykład:

* Jeśli potrzebujesz tooremove poufnych informacji z dziennika plików poprzedniego toosharing z Microsoft Support.
* Jeśli masz problemy przekazywanie pakietu hello powodu tooconnectivity problemów.

Możesz udostępniać pakietu ręcznie wygenerowane pomocy technicznej firmy Microsoft Support za pośrednictwem poczty e-mail. Wykonaj następujące kroki toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple hello.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple
1. toostart sesję programu Windows PowerShell jako administrator na komputerze zdalnym hello, który został użyty tooconnect tooyour urządzenia StorSimple, wprowadź hello następujące polecenie:
   
    `Start PowerShell`
2. W sesji środowiska Windows PowerShell hello Podłącz toohello konsoli SSAdmin urządzenia:
   
   * Witaj wiersza polecenia wpisz:
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * Okno dialogowe hello otwiera wprowadź hasło administratora urządzenia. Witaj domyślne hasło jest:
     
      `Password1`
     
      ![Okno dialogowe poświadczenie programu PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * Kliknij przycisk **OK**.
   * Witaj wiersza polecenia wpisz:
     
      `Enter-PSSession $MS`
3. W sesji hello, który zostanie otwarty wprowadź odpowiednie polecenie hello.
   
   * Udziały sieciowe, które są chronione hasłem wpisz:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       Zostanie wyświetlony monit o hasło, ścieżka folderu udostępnionego toohello sieci oraz hasło szyfrowania (ponieważ pakietu obsługi hello jest zaszyfrowany). W określonym folderze hello zostanie utworzona pakiet obsługi.
   * W przypadku udziałów, które nie są chronione hasłem, nie trzeba hello `-Credential` parametru. Wprowadź poniżej hello:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       Pakiet pomocy technicznej Hello został utworzony dla obu kontrolerów w folderze udostępnionym hello określonej sieci. Jest to plik zaszyfrowanych, skompresowanych, który można wysłać tooMicrosoft pomocy technicznej do rozwiązywania problemów. Aby uzyskać więcej informacji, zobacz [skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-contact-microsoft-support.md).

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
> Można edytować tylko pakietu obsługi, który został wygenerowany za pomocą programu Windows PowerShell dla StorSimple. Nie można edytować pakiet utworzony w hello klasycznego portalu Azure w usłudze Menedżer StorSimple.
> 
> 

tooedit pakiet obsługi przed przekazaniem go w witrynie Microsoft Support hello najpierw odszyfrować pakietu obsługi hello, Edytuj pliki hello i następnie ponownie go zaszyfrować. Wykonaj następujące kroki hello.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple
1. Generowanie pakietu obsługi, jak opisano wcześniej, w [toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).
2. [Pobierz skrypt hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokalnie na komputerze klienckim.
3. Zaimportuj moduł programu Windows PowerShell hello. Określ hello ścieżki toohello folder lokalny którego zostały pobrane hello skryptu. Moduł hello tooimport, wprowadź:
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. Wszystkie pliki hello są *.aes* pliki skompresowane i szyfrowane. toodecompress i odszyfrowywania plików, wpisz:
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Należy pamiętać, że rozszerzenia rzeczywisty plik hello są teraz wyświetlane dla wszystkich plików hello.
   
    ![Edytuj pakiet, pomocy technicznej](./media/storsimple-create-manage-support-package/IC750706.png)
5. Gdy zostanie wyświetlony monit o hasło szyfrowania hello, wprowadź hasło hello, który został użyty podczas tworzenia pakietu obsługi hello.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Przeglądaj toohello folderu, który zawiera pliki dziennika hello. Ponieważ teraz zdekompresować i odszyfrować hello plików dziennika, te będą mieć oryginalnego rozszerzenia pliku. Zmodyfikuj te pliki tooremove wszelkie informacje specyficzne dla klienta, takich jak nazwy woluminu i adresy IP urządzeń i Zapisz hello plików.
7. Zamknij hello pliki toocompress z gzip i szyfrowanie AES 256. Jest to szybkości i zabezpieczeń w przesyłania pakietu obsługi hello za pośrednictwem sieci. toocompress i szyfrowania plików, wprowadź następujące hello:
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Edytuj pakiet, pomocy technicznej](./media/storsimple-create-manage-support-package/IC750707.png)
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
* Dowiedz się, jak za[używana obsługa pakietów oraz urządzenia w dziennikach tootroubleshoot wdrożenia urządzenia](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

