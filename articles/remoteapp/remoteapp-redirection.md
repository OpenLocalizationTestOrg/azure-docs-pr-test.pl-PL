---
title: "Przy użyciu przekierowania w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konfigurowanie i używanie przekierowania w usłudze RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: b5a65d129225fde46e3b090bc3cd9427989005ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Przy użyciu przekierowania w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Przekierowywanie urządzeń pozwala użytkownikom interakcję z aplikacji zdalnych przy użyciu urządzenia podłączone do ich komputera lokalnego, telefon lub tablet. Na przykład jeśli podano Skype za pośrednictwem usługi Azure RemoteApp, użytkownika musi aparatu zainstalowana na danym komputerze do pracy za pomocą programu Skype. Dotyczy to również drukarki, głośniki monitorów i urządzenia peryferyjne podłączone zakresu USB.

Połączenia programów RemoteApp korzysta z protokołu RDP (Remote Desktop) i funkcja RemoteFX do przekierowywania.

## <a name="what-redirection-is-enabled-by-default"></a>Jakie przekierowania jest domyślnie włączone?
Gdy używasz usługi RemoteApp są domyślnie włączone następujące przekierowań. Informacje zawarte w nawiasach Pokaż ustawienia protokołu RDP.

* Odtwarzanie dźwięków na komputerze lokalnym (**Odtwarzaj na tym komputerze**). (audiomode:i:0)
* Przechwyć audio z komputera lokalnego i wysłać do komputera zdalnego (**Graj z tego komputera**). (audiocapturemode:i:1)
* Drukowanie do drukarek lokalnych (redirectprinters:i:1)
* Porty COM (redirectcomports:i:1)
* Karta inteligentna urządzenia (redirectsmartcards:i:1)
* Schowek (możliwość kopiowania i wklejania) (redirectclipboard:i:1)
* Wyczyść typ czcionki Wygładzanie (Zezwalaj na wygładzanie czcionek: i:1)
* Przekieruj urządzeń wszystkich obsługiwanych Plug and Play. (devicestoredirect:s: *)

## <a name="what-other-redirection-is-available"></a>Jakie inne przekierowania jest dostępny?
Dwie opcje przekierowania są domyślnie wyłączone:

* Przekierowywanie dysków (mapowanie dysku): zamapowanych dysków w sesji zdalnej stają się dyski twarde komputera lokalnego. Dzięki temu możesz zapisać lub otwarte pliki z dysków lokalnych podczas pracy w sesji zdalnej.
* Przekierowywaniem USB: można używać urządzeń USB podłączone do komputera lokalnego w sesji zdalnej.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Zmień ustawienia przekierowywania w programie RemoteApp
Ustawienia przekierowywania urządzeń dla kolekcji można zmienić za pomocą programu Microsoft Azure PowerShell przy użyciu zestawu SDK. Po zainstalowaniu nowego środowiska PowerShell i zestawu SDK, najpierw go skonfigurować do zarządzania subskrypcją, zgodnie z opisem w [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

Można ustawić właściwości niestandardowe RDP używać polecenie podobne do następującego:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Należy pamiętać, że  *`n*  jest używany jako separator poszczególnych właściwości.)

Aby uzyskać listę właściwości protokołu RDP, które niestandardowe są skonfigurowane, uruchom następujące polecenie cmdlet. Należy pamiętać, że tylko niestandardowe właściwości są wyświetlane jako wynik i nie domyślne właściwości:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

Po ustawieniu właściwości niestandardowe należy określić wszystkie niestandardowe właściwości zawsze; w przeciwnym razie ustawienie umożliwia przywrócenie na wyłączone.   

### <a name="common-examples"></a>Typowe przykłady
Aby włączyć przekierowywanie dysków, użyj następującego polecenia cmdlet:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

Użyj następującego polecenia cmdlet do włączenia USB i dysków przekierowania:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

To polecenie cmdlet umożliwia wyłączenie funkcji udostępniania Schowka:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Pamiętaj całkowicie Wyloguj wszystkich użytkowników w kolekcji (a nie tylko odłączać) przed przetestowaniem zmiany. Aby upewnić się, użytkownicy są całkowicie wylogowani, przejdź do **sesji** w kolekcji w portalu Azure i wylogowania wszyscy użytkownicy, którzy są odłączone lub zalogowany. Czasami może potrwać kilka sekund na dyskach lokalnych można wyświetlić w Eksploratorze w ramach sesji.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Zmień ustawienia przekierowywania USB na kliencie systemu Windows
Jeśli chcesz użyć przekierowywaniem USB na komputerze, który łączy się RemoteApp, istnieją 2 akcje, które muszą mieć miejsce. 1 - administrator musi włączyć przekierowywanie USB na poziomie kolekcji przy użyciu programu Azure PowerShell. 2 — na każdym urządzeniu, na którym ma być używany z przekierowywaniem USB musisz włączyć zasady grupy, która pozwala. Ten krok należy wykonać dla każdego użytkownika, który chce korzystać z przekierowywaniem USB.

> [!NOTE]
> Przekierowywaniem USB z usługą Azure RemoteApp jest obsługiwana tylko dla komputerów z systemem Windows.
> 
> 

### <a name="enable-usb-redirection-for-the-remoteapp-collection"></a>Włącz przekierowywaniem USB kolekcji usługi RemoteApp
Aby włączyć przekierowywaniem USB na poziomie kolekcji, użyj następującego polecenia cmdlet:

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-the-client-computer"></a>Włącz przekierowywaniem USB do komputera klienckiego
Aby skonfigurować ustawienia przekierowywania USB na komputerze:

1. Otwórz Edytor lokalnych zasad grupy (GPEDIT. MSC). (Uruchom gpedit.msc z wiersza polecenia).
2. Otwórz **komputera Konfiguracja komputera\Zasady\Szablony administracyjne\Składniki systemu Windows\Usługi usług pulpitu Podłączanie pulpitu Client\RemoteFX urządzenia przekierowywaniem USB**.
3. Kliknij dwukrotnie **Zezwalaj na RDP przekierowywanie inne obsługiwane urządzenia USB funkcji RemoteFX z tego komputera**.
4. Wybierz **włączone**, a następnie wybierz **administratorów i użytkowników w prawa dostępu przekierowania USB RemoteFX**.
5. Otwórz wiersz polecenia z uprawnieniami administracyjnymi i uruchom następujące polecenie:
   
        gpupdate /force
6. Uruchom ponownie komputer.

Można także użyć narzędzia do zarządzania zasadami grupy do tworzenia i stosowania zasad przekierowania USB dla wszystkich komputerów w domenie:

1. Zaloguj się do kontrolera domeny jako administrator domeny.
2. Otwórz konsolę zarządzania zasadami grupy. (Kliknij **Start > Narzędzia administracyjne > Zarządzanie zasadami grupy**.)
3. Przejdź do domeny lub jednostki organizacyjnej, dla której chcesz utworzyć zasady.
4. Kliknij prawym przyciskiem myszy **domyślne zasady domeny**, a następnie kliknij przycisk **Edytuj**.
5. Otwórz **komputera Konfiguracja komputera\Zasady\Szablony administracyjne\Składniki systemu Windows\Usługi usług pulpitu Podłączanie pulpitu Client\RemoteFX urządzenia przekierowywaniem USB**.
6. Kliknij dwukrotnie **Zezwalaj na RDP przekierowywanie inne obsługiwane urządzenia USB funkcji RemoteFX z tego komputera**.
7. Wybierz **włączone**, a następnie wybierz **administratorów i użytkowników w prawa dostępu przekierowania USB RemoteFX**.
8. Kliknij przycisk **OK**.  

