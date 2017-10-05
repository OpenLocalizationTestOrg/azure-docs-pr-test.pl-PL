---
title: "Podłącz urządzenie za pomocą C na mbed | Dokumentacja firmy Microsoft"
description: "Opisuje sposób podłącz urządzenie do wstępnie pakiet IoT Azure zdalnego monitorowania rozwiązania przy użyciu Aplikacja napisana w języku C działającej na urządzeniu mbed."
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
ms.openlocfilehash: ef7b78f85a787f8fbe22c0e26aa34f0cd1685d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a>Podłącz urządzenie do zdalnego wstępnie skonfigurowane rozwiązanie monitorowania (mbed)

## <a name="scenario-overview"></a>Omówienie scenariusza
W tym scenariuszu utworzysz urządzenie, które wysyła następujące dane telemetryczne do [wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][lnk-what-are-preconfig-solutions]:

* Temperatura zewnętrzna
* Temperatura wewnętrzna
* Wilgotność

Dla uproszczenia kod na urządzeniu generuje przykładowe wartości, ale zachęcamy do rozszerzenia przykładu przez podłączenie rzeczywistych czujników do urządzenia i wysyłanie rzeczywistych danych telemetrycznych.

Urządzenie potrafi także odpowiadać na metody wywołane z poziomu pulpitu nawigacyjnego rozwiązania i wartości żądanych właściwości ustawione na pulpicie nawigacyjnym rozwiązania.

Do wykonania kroków tego samouczka jest potrzebne aktywne konto platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].

## <a name="before-you-start"></a>Przed rozpoczęciem
Przed przystąpieniem do pisania jakiegokolwiek kodu dla urządzenia musisz przeprowadzić aprowizację wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego i nowego niestandardowego urządzenia w ramach tego rozwiązania.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Aprowizowanie wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego
Urządzenie, które utworzysz w ramach tego samouczka, będzie wysyłać dane do wystąpienia wstępnie skonfigurowanego rozwiązania do [monitorowania zdalnego][lnk-remote-monitoring]. Jeśli jeszcze nie przeprowadzono aprowizacji wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego na Twoim koncie platformy Azure, wykonaj poniższe kroki:

1. Na stronie <https://www.azureiotsuite.com/> kliknij pozycję **+**, aby utworzyć rozwiązanie.
2. Kliknij pozycję **Wybierz** w panelu **Monitorowanie zdalne**, aby utworzyć rozwiązanie.
3. Na stronie **Tworzenie rozwiązania do monitorowania zdalnego** w polu **Nazwa rozwiązania** wprowadź wybraną nazwę rozwiązania, w polu **Region** wybierz region, w którym chcesz przeprowadzić wdrożenie, a następnie wybierz subskrypcję platformy Azure, której chcesz użyć. Następnie kliknij pozycję **Utwórz rozwiązanie**.
4. Zaczekaj na ukończenie procesu aprowizowania.

> [!WARNING]
> Wstępnie skonfigurowane rozwiązania korzystają z płatnych usług platformy Azure. Pamiętaj o usunięciu wstępnie skonfigurowanego rozwiązania ze swojej subskrypcji po zakończeniu pracy z nim, aby uniknąć wszelkich zbędnych opłat. Możesz całkowicie usunąć wstępnie skonfigurowane rozwiązanie ze swojej subskrypcji, odwiedzając stronę <https://www.azureiotsuite.com/>.
> 
> 

Po zakończeniu procesu aprowizowania rozwiązania do monitorowania zdalnego kliknij pozycję **Uruchom**, aby otworzyć pulpit nawigacyjny rozwiązania w przeglądarce.

![Pulpit nawigacyjny rozwiązania][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a>Aprowizowanie urządzenia w ramach rozwiązania do monitorowania zdalnego
> [!NOTE]
> Jeśli już przeprowadzono aprowizację urządzenia w ramach rozwiązania, możesz pominąć ten krok. Podczas tworzenia aplikacji klienckiej musisz znać poświadczenia urządzenia.
> 
> 

Aby urządzenie mogło nawiązać połączenie ze wstępnie skonfigurowanym rozwiązaniem, musi ono zidentyfikować się względem usługi IoT Hub za pomocą prawidłowych poświadczeń. Poświadczenia urządzenia możesz pobrać z pulpitu nawigacyjnego rozwiązania. W dalszej części tego samouczka podasz te poświadczenia urządzenia w Twojej aplikacji klienckiej.

Aby dodać urządzenie do swojego rozwiązania do monitorowania zdalnego, wykonaj poniższe kroki na pulpicie nawigacyjnym rozwiązania:

1. W lewym dolnym rogu pulpitu nawigacyjnego kliknij pozycję **Dodaj urządzenie**.
   
   ![Dodawanie urządzenia][1]
2. W panelu **Urządzenie niestandardowe** kliknij pozycję **Dodaj nowe**.
   
   ![Dodawanie urządzenia niestandardowego][2]
3. Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia**. Wprowadź identyfikator urządzenia, na przykład **moje_urządzenie**, kliknij pozycję **Sprawdź identyfikator**, aby sprawdzić, czy dana nazwa nie jest już używana, a następnie kliknij pozycję **Utwórz**, aby przeprowadzić aprowizację urządzenia.
   
   ![Dodawanie identyfikatora urządzenia][3]
4. Zanotuj poświadczenia urządzenia (identyfikator urządzenia, nazwę hosta usługi IoT Hub i klucz urządzenia). Twoja aplikacja kliencka potrzebuje tych wartości, aby mogła nawiązać połączenie z rozwiązaniem do monitorowania zdalnego. Następnie kliknij przycisk **Gotowe**.
   
    ![Wyświetlanie poświadczeń urządzenia][4]
5. Wybierz urządzenie na liście urządzeń na pulpicie nawigacyjnym rozwiązania. Następnie w panelu **Szczegóły urządzenia** kliknij pozycję **Włącz urządzenie**. Stan Twojego urządzenia to teraz **Uruchomione**. Rozwiązanie do monitorowania zdalnego może teraz odbierać dane telemetryczne z Twojego urządzenia i wywoływać metody na tym urządzeniu.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-the-c-sample-solution"></a>Skompilować i uruchomić przykładowe rozwiązanie C

Poniższe instrukcje przedstawiają kroki wymagane do połączenia [włączone mbed FRDM K64F Freescale] [ lnk-mbed-home] urządzenia zdalnego rozwiązanie monitorowania.

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a>Podłącz urządzenie mbed do komputera w sieci i pulpitu

1. Podłącz urządzenie mbed do sieci przy użyciu kabla Ethernet. Ten krok jest niezbędny, ponieważ przykładowej aplikacji wymaga dostępu do Internetu.

1. Zobacz [wprowadzenie mbed] [ lnk-mbed-getstarted] Podłącz urządzenie mbed do komputera.

1. Jeśli komputer pulpitu systemu Windows, zobacz [konfigurację komputera] [ lnk-mbed-pcconnect] do konfigurowania portu szeregowego dostęp do Twojego urządzenia mbed.

### <a name="create-an-mbed-project-and-import-the-sample-code"></a>Utwórz projekt mbed i zaimportować przykładowy kod

Wykonaj następujące kroki, aby dodać do projektu mbed niektórych przykładowy kod. Możesz zaimportować zdalnego monitorowania projektu starter, a następnie zmień projektu do korzystania z protokołu MQTT zamiast protokołu AMQP. Obecnie należy użyć protokołu MQTT do używania funkcji zarządzania urządzeniami Centrum IoT.

1. W przeglądarce sieci web, przejdź do mbed.org [deweloperskiej](https://developer.mbed.org/). Jeśli masz utworzonego konta, zobaczysz opcję, aby utworzyć konto (jest bezpłatna). W przeciwnym razie Zaloguj się przy użyciu poświadczeń konta. Następnie kliknij przycisk **kompilatora** w prawym górnym rogu strony. Ta akcja umożliwia do *obszaru roboczego* interfejsu.

1. Upewnij się, że platforma sprzętowa, którego używasz, zostanie wyświetlona w prawym górnym rogu okna, lub kliknij ikonę w prawym rogu, aby wybrać platforma sprzętowa.

1. Kliknij przycisk **importu** w menu głównym. Następnie kliknij przycisk **kliknij tutaj, aby zaimportować z adresu URL**.
   
    ![Uruchom importowanie do obszaru roboczego mbed][6]

1. W oknie podręcznym wprowadź link do https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ kod przykładowy, a następnie kliknij przycisk **importu**.
   
    ![Importuj przykładowy kod do obszaru roboczego mbed][7]

1. W oknie kompilatora mbed widać, że importowanie tego projektu również importuje bibliotek różnych. Niektóre są dostarczane i obsługiwane przez zespół Azure IoT ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), a inne są dostępne w katalogu bibliotek mbed bibliotek innych firm.
   
    ![Widok projektu mbed][8]

1. W **obszaru roboczego programu**, kliknij prawym przyciskiem myszy **Centrum iothub\_amqp\_transportu** biblioteki, kliknij przycisk **usunąć**, a następnie kliknij przycisk **OK** o potwierdzenie.

1. W **obszaru roboczego programu**, kliknij prawym przyciskiem myszy **azure\_amqp\_c** biblioteki, kliknij przycisk **usunąć**, a następnie kliknij przycisk **OK** o potwierdzenie.

1. Kliknij prawym przyciskiem myszy **remote_monitoring** projektu w **obszaru roboczego programu**, wybierz pozycję **biblioteki importu**, a następnie wybierz pozycję **z adresu URL**.
   
    ![Import biblioteki do obszaru roboczego mbed Start][6]

1. W oknie podręcznym wprowadź link do https://developer.mbed.org/users/AzureIoTClient/code/iothub biblioteki transportu MQTT\_mqtt\_transportu / kliknięcie **importu**.
   
    ![Importuj biblioteki do obszaru roboczego mbed][12]

1. Powtórz poprzedni krok, aby dodać biblioteki MQTT z https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.

1. Obszar roboczy teraz wygląda następująco:

    ![Wyświetl obszar roboczy mbed][13]

1. Otwórz zdalnego\_monitoring\remote_monitoring.c plików i Zastąp istniejące `#include` instrukcje następującym kodem:

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
1. Usuń wszystkie pozostałe kod w zdalnym\_monitoring\remote\_monitoring.c pliku.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a>Tworzenie i uruchamianie próbki

Dodaj kod, aby wywołać **zdalnego\_monitorowania\_Uruchom** funkcji, a następnie skompilować i uruchomić aplikację dla urządzeń.

1. Dodaj **głównego** funkcji z następujący kod na końcu zdalnego\_monitoring.c pliku do wywołania **zdalnego\_monitorowania\_Uruchom** funkcji:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Kliknij przycisk **skompilować** do tworzenia programu. Można bezpiecznie zignorować ostrzeżenia, ale jeśli kompilacja generuje błędy, usuń je przed kontynuowaniem.

1. Jeśli kompilacja zakończy się pomyślnie, witryna kompilatora mbed generuje plik bin z nazwą projektu i pliki do pobrania na komputerze lokalnym. Skopiuj plik bin na urządzeniu. Zapisywanie pliku bin do urządzenia powoduje, że urządzenie, aby ponownie uruchomić, a następnie uruchom program zawarte w pliku bin. Można ręcznie uruchomić ponownie program w dowolnym momencie naciśnięcia przycisku resetowania urządzenia mbed.

1. Nawiąż połączenie z urządzeniem przy użyciu aplikacji klienta SSH, takiego jak PuTTY. Można określić portu szeregowego, używanych przez urządzenia, sprawdzając Menedżera urządzeń z systemem Windows.
   
    ![][11]

1. W programu PuTTY, kliknij przycisk **Serial** typu połączenia. Urządzenie łączy się zwykle przy transmisji 9600, dlatego należy wprowadzić 9600 w **szybkości** pole. Następnie kliknij przycisk **Otwórz**.

1. Program rozpoczyna wykonywanie. Może zajść potrzeba zresetowania tablicy (naciśnij klawisze CTRL + Break lub naciśnij przycisk reset tablicy), jeśli program nie zostanie uruchomiony automatycznie po połączeniu.
   
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
