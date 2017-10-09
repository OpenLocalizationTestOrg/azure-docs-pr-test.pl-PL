---
title: "aaaConnect urządzenia za pomocą C na mbed | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconnect toohello urządzenia pakiet IoT Azure wstępnie zdalnego rozwiązanie monitorowania przy użyciu Aplikacja napisana w języku C działającej na urządzeniu mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a>Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie (mbed)

## <a name="scenario-overview"></a>Omówienie scenariusza
W tym scenariuszu, Utwórz urządzenie, które wysyła powitania po monitorowania zdalnego toohello telemetrii [wstępnie skonfigurowane rozwiązanie][lnk-what-are-preconfig-solutions]:

* Temperatura zewnętrzna
* Temperatura wewnętrzna
* Wilgotność

Dla uproszczenia kodu hello na urządzeniu hello generuje przykładowe wartości, ale firma Microsoft zachęca możesz tooextend hello próbki podłączania urządzenia tooyour rzeczywistych czujników i wysyła rzeczywistych danych telemetrycznych.

urządzenie Hello jest również toomethods toorespond można wywołać z poziomu pulpitu nawigacyjnego rozwiązania hello i potrzebne wartości właściwości ustawione na pulpicie nawigacyjnym rozwiązania hello.

toocomplete tego samouczka potrzebne aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].

## <a name="before-you-start"></a>Przed rozpoczęciem
Przed przystąpieniem do pisania jakiegokolwiek kodu dla urządzenia musisz przeprowadzić aprowizację wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego i nowego niestandardowego urządzenia w ramach tego rozwiązania.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Aprowizowanie wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego
urządzenie Hello Utwórz w tym samouczku wysyła dane wystąpienia tooan hello [monitorowania zdalnego] [ lnk-remote-monitoring] wstępnie skonfigurowane rozwiązanie. Jeśli nie zostało już przydzielona hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie w konta platformy Azure, użyj hello następujące kroki:

1. Na powitania <https://www.azureiotsuite.com/> kliknij przycisk  **+**  toocreate rozwiązania.
2. Kliknij przycisk **wybierz** na powitania **monitorowania zdalnego** panelu toocreate rozwiązania.
3. Na powitania **utworzyć zdalnego rozwiązanie monitorujące** wprowadź **Nazwa rozwiązania** wybranych przez użytkownika, wybierz hello **Region** toodeploy do, a następnie wybierz hello Azure toouse toowant subskrypcji. Następnie kliknij pozycję **Utwórz rozwiązanie**.
4. Poczekaj na zakończenie procesu udostępniania hello.

> [!WARNING]
> rozwiązania Hello wstępnie skonfigurowane za pomocą usług Azure rozliczeniowy. Pamiętaj, że tooremove hello wstępnie skonfigurowane rozwiązanie z subskrypcji, gdy wszystko będzie gotowe z nim tooavoid opłaty niepotrzebne. Wstępnie skonfigurowane rozwiązanie można całkowicie usunąć z subskrypcji, odwiedzając hello <https://www.azureiotsuite.com/> strony.
> 
> 

Po zakończeniu hello inicjowania obsługi administracyjnej proces hello zdalnego rozwiązanie monitorujące, kliknij przycisk **uruchamianie** pulpit nawigacyjny rozwiązania hello tooopen w przeglądarce.

![Pulpit nawigacyjny rozwiązania][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Zapewnij urządzenia w hello zdalne monitorowanie rozwiązania
> [!NOTE]
> Jeśli już przeprowadzono aprowizację urządzenia w ramach rozwiązania, możesz pominąć ten krok. Należy tooknow hello urządzenia poświadczeń podczas tworzenia powitania klienta aplikacji.
> 
> 

Jako rozwiązanie toohello wstępnie tooconnect urządzenia, jego musi identyfikacji tooIoT Centrum używając poprawnych poświadczeń. Pulpit nawigacyjny rozwiązania hello może pobrać poświadczenia urządzeń hello. Wprowadzono poświadczenia urządzeń hello w dalszej części tego samouczka aplikacji klienta.

tooadd urządzenia tooyour zdalnego rozwiązanie monitorowania pełną hello następujące kroki na pulpicie nawigacyjnym rozwiązania hello:

1. W hello lewym dolnym rogu hello pulpitu nawigacyjnego, kliknij przycisk **dodać urządzenie**.
   
   ![Dodawanie urządzenia][1]
2. W hello **urządzenia niestandardowe** panelu, kliknij przycisk **Dodaj nowe**.
   
   ![Dodawanie urządzenia niestandardowego][2]
3. Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia**. Wprowadź identyfikator urządzenia, takie jak **mydevice**, kliknij przycisk **Sprawdź identyfikator** tooverify tej nazwie nie jest już w użyciu, a następnie kliknij **Utwórz** tooprovision hello urządzenia.
   
   ![Dodawanie identyfikatora urządzenia][3]
4. Należy skonfigurować urządzenie hello Uwaga poświadczeń (identyfikator urządzenia, nazwy hosta Centrum IoT i klucz urządzenia). Aplikacja kliencka musi zdalne monitorowanie rozwiązania toohello tooconnect tych wartości. Następnie kliknij przycisk **Gotowe**.
   
    ![Wyświetlanie poświadczeń urządzenia][4]
5. Wybierz urządzenie na liście urządzeń hello na pulpicie nawigacyjnym rozwiązania hello. Następnie w hello **szczegóły urządzenia** panelu, kliknij przycisk **Włącz urządzenie**. Witaj stan urządzenia jest teraz **systemem**. rozwiązanie monitorowania zdalnego Hello teraz może odbierać dane telemetryczne z urządzenia i wywołania metod na urządzeniu hello.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a>Tworzenie i uruchamianie hello C przykładowe rozwiązanie

Witaj poniższe instrukcje przedstawiają kroki hello podłączania [włączone mbed FRDM K64F Freescale] [ lnk-mbed-home] toohello urządzenie zdalne monitorowanie rozwiązania.

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a>Połącz hello mbed urządzenia tooyour sieci i komputerów

1. Połącz hello mbed urządzenia tooyour sieci przy użyciu kabla Ethernet. Ten krok jest niezbędny, ponieważ hello przykładowej aplikacji wymaga dostępu do Internetu.

1. Zobacz [wprowadzenie mbed] [ lnk-mbed-getstarted] tooconnect mbed urządzenia tooyour pulpitu komputera.

1. Jeśli komputer pulpitu systemu Windows, zobacz [konfigurację komputera] [ lnk-mbed-pcconnect] tooconfigure portu szeregowego dostępu tooyour mbed urządzenia.

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a>Utwórz projekt mbed i zaimportować hello przykładowy kod

Wykonaj te kroki tooadd niektórych przykładowy kod tooan mbed projekt. Możesz zaimportować hello zdalnego monitorowania starter projektu, a następnie zmień hello projektu toouse hello protokołu MQTT zamiast hello protokołu AMQP. Obecnie należy toouse hello MQTT protokołu toouse hello funkcji zarządzania urządzeniami Centrum IoT.

1. W przeglądarce sieci web przejdź toohello mbed.org [deweloperskiej](https://developer.mbed.org/). Jeśli masz utworzonego konta, zobaczysz opcję toocreate konta (jest bezpłatna). W przeciwnym razie Zaloguj się przy użyciu poświadczeń konta. Następnie kliknij przycisk **kompilatora** w hello prawym górnym rogu strony hello. Ta akcja powoduje toohello *obszaru roboczego* interfejsu.

1. Upewnij się, platforma sprzętowa hello używanego pojawia się w hello prawym górnym rogu okna hello, lub kliknij ikonę hello w tooselect prawym rogu hello platformy sprzętu.

1. Kliknij przycisk **importu** na powitania w menu głównym. Następnie kliknij przycisk **kliknij tutaj tooimport z adresu URL**.
   
    ![Uruchom workspace toombed importu][6]

1. W oknie podręcznym hello, wprowadź łącze hello hello przykładowy kod https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, a następnie kliknij przycisk **importu**.
   
    ![Importuj roboczym toombed kod przykładowy][7]

1. W oknie kompilatora mbed hello widać, że importowanie tego projektu również importuje bibliotek różnych. Niektóre są dostarczane i obsługiwane przez zespół Azure IoT hello ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), a inne są dostępne w katalogu bibliotek mbed hello bibliotek innych firm.
   
    ![Widok projektu mbed][8]

1. W hello **obszaru roboczego programu**, powitania kliknij prawym przyciskiem myszy **Centrum iothub\_amqp\_transportu** biblioteki, kliknij przycisk **usunąć**, a następnie kliknij przycisk **OK** tooconfirm.

1. W hello **obszaru roboczego programu**, powitania kliknij prawym przyciskiem myszy **azure\_amqp\_c** biblioteki, kliknij przycisk **usunąć**, a następnie kliknij przycisk **OK**  tooconfirm.

1. Powitania kliknij prawym przyciskiem myszy **remote_monitoring** projektu w hello **obszaru roboczego programu**, wybierz pozycję **biblioteki importu**, a następnie wybierz pozycję **z adresu URL**.
   
    ![Uruchom obszaru roboczego Biblioteka importu toombed][6]

1. W oknie podręcznym hello, wprowadź łącze hello hello MQTT transportu biblioteki https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transportu / kliknięcie **importu**.
   
    ![Importuj obszaru roboczego Biblioteka toombed][12]

1. Powtórz hello poprzedniego kroku tooadd hello MQTT biblioteki z https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.

1. Obszar roboczy teraz wygląda hello:

    ![Wyświetl obszar roboczy mbed][13]

1. Otwórz hello zdalnego\_monitoring\remote_monitoring.c plików i Zastąp hello istniejących `#include` instrukcji z hello następującego kodu:

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. Usuń wszystkie hello pozostałych kodu w hello zdalnego\_monitoring\remote\_monitoring.c pliku.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Tworzenie i uruchamianie przykładowych hello

Dodaj kod tooinvoke hello **zdalnego\_monitorowania\_Uruchom** funkcji, a następnie skompilować i uruchomić aplikację dla urządzeń hello.

1. Dodaj **głównego** funkcji z następujący kod na końcu hello hello zdalnego\_monitoring.c pliku tooinvoke hello **zdalnego\_monitorowania\_Uruchom** funkcji:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Kliknij przycisk **skompilować** toobuild hello program. Można bezpiecznie zignorować ostrzeżenia, ale jeśli kompilacji hello generuje błędy, usuń je przed kontynuowaniem.

1. Jeśli hello kompilacja zakończy się pomyślnie, witryny sieci Web hello mbed kompilatora generuje plik bin o nazwie hello projektu i pobiera go tooyour komputera lokalnego. Kopiuj hello bin pliku toohello urządzenia. Zapisywanie hello bin pliku toohello urządzenia powoduje hello toorestart urządzenia i uruchom program hello zawarte w pliku bin hello. Można ręcznie uruchomić ponownie hello program w dowolnym momencie naciśnięcie przycisku resetowania hello na powitania mbed urządzenia.

1. Podłącz urządzenie toohello za pomocą aplikacji klienckiej SSH, takiego jak PuTTY. Można określić hello portu szeregowego, używanych przez urządzenia, sprawdzając Menedżera urządzeń z systemem Windows.
   
    ![][11]

1. W programu PuTTY, kliknij przycisk hello **Serial** typu połączenia. zwykle łączy urządzenie Hello na 9600 transmisji, dlatego należy wprowadzić 9600 w hello **szybkości** pole. Następnie kliknij przycisk **Otwórz**.

1. Hello program rozpoczyna wykonywanie. Jeśli hello program nie zostanie uruchomiony automatycznie po połączeniu, może być tooreset hello tablicy (naciśnij klawisze CTRL + Break lub tablicy hello naciśnij przycisk reset).
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
