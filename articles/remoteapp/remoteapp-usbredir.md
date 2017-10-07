---
title: "aaaHow należy przekierowywać urządzenia USB w usłudze Azure RemoteApp? | Microsoft Docs"
description: "Dowiedz się, jak przekierowanie toouse dla urządzeń USB w usłudze Azure RemoteApp."
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
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Jak przekierować urządzenia USB w usłudze Azure RemoteApp?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Przekierowywanie urządzeń umożliwia użytkownikom komputera tootheir podłączonego urządzenia USB hello lub tablet za pomocą aplikacji hello w usłudze Azure RemoteApp. Na przykład jeśli udostępniony Skype za pośrednictwem usługi Azure RemoteApp, użytkownicy potrzebują toobe toouse stanie ich kamer urządzenia.

Zanim przejdziesz dalej, upewnij się, odczytać informacji o przekazywaniu USB hello w [w usłudze Azure RemoteApp przy użyciu przekierowania](remoteapp-redirection.md). Jednak hello zalecane nusbdevicestoredirect:s: * nie będzie działać dla kamer internetowych USB i nie mogą działać w przypadku niektórych drukarek USB lub wielofunkcyjnych urządzenia USB. Zgodnie z projektem i ze względów bezpieczeństwa hello Azure RemoteApp administrator ma przekierowania tooenable przez identyfikator GUID dla klasy urządzenie lub urządzenia, identyfikator wystąpienia przed użytkownicy mogą używać tych urządzeń.

Chociaż ten artykuł zawiera informacje o sieci web aparatu przekierowania, można użyć podobne drukarek USB tooredirect podejścia i innych urządzeń wielofunkcyjnych USB, które nie są przekierowywane przez hello **nusbdevicestoredirect:s:*** polecenia.

## <a name="redirection-options-for-usb-devices"></a>Opcje przekierowywania dla urządzeń USB
Usługa Azure RemoteApp używa mechanizmów bardzo podobne przekierowywania urządzenia USB, jak hello te, które są dostępne dla usług pulpitu zdalnego. Witaj podstawową technologią pozwala na wybór metody przekierowywania poprawne powitania dla danego urządzenia, hello tooget najlepsze obu wysokiego poziomu i Przekierowanie urządzenia RemoteFX USB przy użyciu hello **usbdevicestoredirect:s:** polecenia. Istnieją cztery elementy toothis polecenia:

| Kolejność przetwarzania | Parametr | Opis |
| --- | --- | --- |
| 1 |* |Wybiera wszystkie urządzenia, które nie są pobierane przez przekierowywanie wysokiego poziomu. Uwaga: zgodnie z projektem * nie działa dla kamer internetowych USB. |
| {Identyfikator GUID klasy urządzenia} |Wybiera wszystkie urządzenia, które odpowiada hello określona klasa konfiguracji urządzeń. | |
| USB\InstanceID |Wybiera urządzenia USB określony dla hello podany identyfikator wystąpienia. | |
| 2 |-Identyfikator USB\Instance |Usuwa hello ustawienia przekierowywania dla określonego urządzenia hello. |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>Przekierowywanie urządzenia USB przy użyciu klasy urządzeń hello identyfikator GUID
Istnieją dwa sposoby toofind hello urządzenia klasy identyfikatora GUID, który może służyć do przekierowania. 

Pierwsza opcja Hello jest toouse hello [tooVendors System-Defined urządzenia instalatora klasy dostępne](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx). Wybierz klasy hello, która najlepiej pasuje do komputera lokalnego toohello podłączonego urządzenia hello. Cyfrowe aparaty fotograficzne może to być klasy Imaging urządzenie lub urządzenia przechwytywania wideo. Będziesz potrzebować toodo niektórych eksperymenty z hello urządzenia klasy toofind hello poprawny identyfikator GUID, który współpracuje z lokalnie hello klasy dołączonego urządzenia USB (w naszym kamery internetowej hello przypadków).

Lepszy sposób lub hello drugą opcją jest toofollow te kroki toofind hello określonego urządzenia klasy identyfikatora GUID:

1. Otwórz hello Menedżera urządzeń, zlokalizuj hello urządzenie zostanie przekierowany i kliknij go prawym przyciskiem myszy, a następnie otwórz właściwości hello.
   ![Otwórz hello Menedżera urządzeń](./media/remoteapp-usbredir/ra-devicemanager.png)
2. Na powitania **szczegóły** , wybierz pozycję Właściwości hello **identyfikator Guid klasy**. wartość Hello, który jest wyświetlany jest hello identyfikator GUID klasy dla tego typu urządzenia.
   ![Właściwości kamery](./media/remoteapp-usbredir/ra-classguid.png)
3. Użyj hello identyfikator Guid klasy wartości tooredirect urządzenia, które jest zgodny.

Na przykład:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

Można połączyć wiele urządzeniu przekierowań w hello tego samego polecenia cmdlet. Na przykład: USB i Magazyn lokalny tooredirect sieci web aparatu, polecenia cmdlet wygląda następująco:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

W przypadku ustawienia przekierowywania przez identyfikator GUID klasy są przekierowywane wszystkie urządzenia, które odpowiada określenia klasy identyfikatora GUID w hello kolekcji. Na przykład, jeśli istnieje kilka komputerów w sieci lokalnej hello hello takie same kamery internetowe USB, możesz uruchomić tooredirect jednego polecenia cmdlet wszystkie hello kamer internetowych.

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>Przekierowywanie przy użyciu Identyfikatora wystąpienia urządzenia hello urządzenia USB
Jeśli mają bardziej precyzyjną kontrolę, a toocontrol przekierowanie na urządzenie, możesz użyć hello **USB\InstanceID** parametru przekierowania.

Witaj najtrudniejsze część tej metody jest znajdowanie hello USB urządzenia identyfikatora wystąpienia. Będzie konieczne dostęp do komputera toohello i hello określonym urządzeniem USB. Następnie wykonaj następujące kroki:

1. Włącz przekierowanie urządzenia hello w sesji pulpitu zdalnego, zgodnie z opisem w [I służy urządzeń i zasobów w sesji pulpitu zdalnego?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. Otwórz Podłączanie pulpitu zdalnego i kliknij przycisk **Pokaż opcje**.
3. Kliknij przycisk **Zapisz jako** toosave hello bieżącego połączenia ustawienia tooan pliku RDP.  
    ![Zapisz ustawienia hello w pliku RDP](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. Wybierz nazwę pliku i lokalizację, na przykład MyConnection.rdp i ten PC\Documents i Zapisz plik hello.
5. Otwórz hello MyConnection.rdp plików za pomocą edytora tekstu i Znajdź identyfikator wystąpienia hello hello urządzenia ma tooredirect.

Teraz można użyć Identyfikatora wystąpienia hello w hello następującego polecenia cmdlet:

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>Pomóż nam sobie pomóc
Czy wiesz, że w toorating dodanie ten artykuł i dodać komentarze poniżej, możesz wprowadzić samym artykule toohello zmiany? Brakuje informacji? Coś jest nie tak? Treść artykułu jest niejasna? Przewiń w górę i kliknij przycisk **Edytuj w serwisie GitHub** zmiany toomake - te modyfikacje zostaną toous do przeglądu, a następnie, zatwierdzeniu na nich, zostanie wyświetlone Twoje zmiany i udoskonalenia tutaj.

