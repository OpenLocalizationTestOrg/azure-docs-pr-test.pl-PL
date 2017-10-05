---
title: "Jak przekierować urządzenia USB w usłudze Azure RemoteApp? | Microsoft Docs"
description: "Dowiedz się, jak używać przekierowywania dla urządzeń USB w usłudze Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3d7165d2c3dafe87b829e588b9e7f2c377552a35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Jak przekierować urządzenia USB w usłudze Azure RemoteApp?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Przekierowywanie urządzeń umożliwia użytkownikom na korzystanie z urządzenia USB podłączone do jego komputera lub tabletu z aplikacjami w usłudze Azure RemoteApp. Na przykład jeśli udostępniony Skype za pośrednictwem usługi Azure RemoteApp, użytkownicy potrzebują można używać ich kamer urządzenia.

Zanim przejdziesz dalej, upewnij się, odczytać informacji o przekazywaniu USB w [w usłudze Azure RemoteApp przy użyciu przekierowania](remoteapp-redirection.md). Jednak zalecane nusbdevicestoredirect:s: * nie będzie działać dla kamer internetowych USB i nie mogą działać w przypadku niektórych drukarek USB lub wielofunkcyjnych urządzenia USB. Zgodnie z projektem i ze względów bezpieczeństwa administrator usługi Azure RemoteApp musi włączyć przekierowywanie przez identyfikator GUID dla klasy urządzenie lub urządzenia, identyfikator wystąpienia przed użytkownicy mogą używać tych urządzeń.

Chociaż ten artykuł zawiera informacje o sieci web aparatu przekierowania, można użyć podejście podobne do przekierowywania drukarki USB i inne urządzenia wielofunkcyjne USB, które nie są przekierowywane przez **nusbdevicestoredirect:s:*** polecenia.

## <a name="redirection-options-for-usb-devices"></a>Opcje przekierowywania dla urządzeń USB
Usługa Azure RemoteApp używa mechanizmów bardzo podobne przekierowywania urządzenia USB jako z dostępnymi dla usług pulpitu zdalnego. Podstawową technologią umożliwia wybranie metody poprawne przekierowywania dla danego urządzenia, aby uzyskać najlepsze cechy obu wysokiego poziomu i urządzenia RemoteFX USB przy użyciu przekierowania **usbdevicestoredirect:s:** polecenia. Istnieją cztery elementy tego polecenia:

| Kolejność przetwarzania | Parametr | Opis |
| --- | --- | --- |
| 1 |* |Wybiera wszystkie urządzenia, które nie są pobierane przez przekierowywanie wysokiego poziomu. Uwaga: zgodnie z projektem * nie działa dla kamer internetowych USB. |
| {Identyfikator GUID klasy urządzenia} |Wybiera wszystkie urządzenia, które odpowiada klasę konfiguracji określonego urządzenia. | |
| USB\InstanceID |Wybiera określony dla identyfikatora wystąpienia danego urządzenia USB | |
| 2 |-Identyfikator USB\Instance |Usuwa ustawienia przekierowywania dla określonego urządzenia. |

## <a name="redirecting-a-usb-device-by-using-the-device-class-guid"></a>Przekierowywanie urządzenia USB przy użyciu identyfikatora GUID klasy urządzenia
Istnieją dwa sposoby znajdowania klasę urządzeń identyfikator GUID, który może służyć do przekierowania. 

Pierwsza opcja jest użycie [System-Defined urządzenia instalatora klasy dostępny dla dostawców](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx). Wybierz klasę, która najlepiej pasuje do urządzenia podłączone do komputera lokalnego. Cyfrowe aparaty fotograficzne może to być klasy Imaging urządzenie lub urządzenia przechwytywania wideo. Należy wykonać niektóre eksperymenty z klas urządzeń można znaleźć klasy poprawny identyfikator GUID, który działa z lokalnie podłączonego urządzenia USB (w tym przypadku kamery internetowej).

Lepiej lub drugą opcją jest wykonaj następujące kroki, aby znaleźć identyfikator GUID klasy określonego urządzenia:

1. Otwórz Menedżera urządzeń, zlokalizuj urządzenia, które będą przekierowywane i kliknij go prawym przyciskiem myszy, a następnie otwórz właściwości.
   ![Otwórz Menedżera urządzeń](./media/remoteapp-usbredir/ra-devicemanager.png)
2. Na **szczegóły** , wybierz pozycję właściwości **identyfikator Guid klasy**. Wartość, która jest wyświetlana jest identyfikator GUID klasy dla tego typu urządzenia.
   ![Właściwości kamery](./media/remoteapp-usbredir/ra-classguid.png)
3. Wartość identyfikatora Guid klasy umożliwia przekierowanie urządzenia, które jest zgodny.

Na przykład:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

Można połączyć wiele urządzeniu przekierowań w tych samych poleceń cmdlet. Na przykład: Aby przekierować Magazyn lokalny i kamery internetowej USB, polecenia cmdlet wygląda następująco:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

W przypadku ustawienia przekierowywania przez identyfikator GUID klasy są przekierowywane wszystkie urządzenia zgodne z tym identyfikator GUID klasy w określonej kolekcji. Na przykład jeśli istnieje kilka komputerów w sieci lokalnej samej kamery internetowe USB, można uruchomić jednego polecenia cmdlet, aby przekierować wszystkie kamer internetowych.

## <a name="redirecting-a-usb-device-by-using-the-device-instance-id"></a>Przekierowywanie urządzenia USB przy użyciu Identyfikatora wystąpienia urządzenia
Jeśli chcesz więcej precyzyjną kontrolę, aby kontrolować przekierowanie na urządzenie, możesz użyć **USB\InstanceID** parametru przekierowania.

Najtrudniejsze część tej metody jest znajdowanie identyfikatora wystąpienia urządzenia USB. Musisz mieć dostęp do komputera i określonym urządzeniem USB. Następnie wykonaj następujące kroki:

1. Włącz przekierowanie urządzenia w sesji pulpitu zdalnego, zgodnie z opisem w [I służy urządzeń i zasobów w sesji pulpitu zdalnego?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. Otwórz Podłączanie pulpitu zdalnego i kliknij przycisk **Pokaż opcje**.
3. Kliknij przycisk **Zapisz jako** można zapisać bieżące ustawienia połączenia w pliku RDP.  
    ![Zapisz ustawienia w pliku RDP](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. Wybierz nazwę pliku i lokalizację, na przykład MyConnection.rdp i ten PC\Documents i Zapisz plik.
5. Otwórz plik MyConnection.rdp za pomocą edytora tekstów i Znajdź identyfikator wystąpienia urządzenia, które ma być przekierowywana.

Teraz Użyj Identyfikatora wystąpienia poniższe polecenie cmdlet:

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>Pomóż nam sobie pomóc
Czy wiesz, że możesz nie tylko ocenić ten artykuł i dodać komentarze poniżej, ale także wprowadzać zmiany w samym artykule? Brakuje informacji? Coś jest nie tak? Treść artykułu jest niejasna? Przewiń w górę i kliknij pozycję **Edit on GitHub** (Edytuj w serwisie GitHub) w celu wprowadzenia zmian. Te modyfikacje zostaną przez nas sprawdzone, a po zatwierdzeniu Twoje zmiany i poprawki będą widoczne w tym miejscu.

