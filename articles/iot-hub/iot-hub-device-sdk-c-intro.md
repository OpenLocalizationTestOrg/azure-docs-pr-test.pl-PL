---
title: "aaaThe urządzenia Azure IoT SDK dla języka C | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z hello urządzenia Azure IoT SDK dla języka C i Dowiedz się, jak toocreate aplikacji dla urządzeń, które do komunikacji z Centrum IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a>Azure urządzenia IoT zestawu SDK dla języka C

Witaj **urządzenia Azure IoT SDK** to zestaw bibliotek zaprojektowane toosimplify hello proces wysyłania wiadomości tooand odbieranie wiadomości z hello **Centrum IoT Azure** usługi. Istnieją możliwych kombinacji hello SDK każdego przeznaczonych dla określonej platformy, ale w tym artykule opisano hello **urządzenia Azure IoT SDK dla języka C**.

Hello urządzenia Azure IoT SDK dla języka C są zapisywane w przenośność toomaximize ANSI C (C99). Ta funkcja umożliwia hello bibliotek toooperate dobrze nadaje się na wielu platformach i urządzeniach, szczególnie w przypadku, gdy minimalizując dysku i zużycie pamięci jest priorytetem.

Istnieje szeroka gama platformy, na których hello został przetestowany zestaw SDK (zobacz hello [Azure certyfikowane dla katalogu urządzenia IoT](https://catalog.azureiotsuite.com/) szczegółowe informacje). Chociaż ten artykuł zawiera wskazówki przykładowy kod działających na platformie Windows hello, kod hello opisane w tym artykule jest identyczna w zakresie hello obsługiwanych platform.

W tym artykule przedstawiono toohello architektury urządzenia Azure IoT hello zestawu SDK dla C. Pokazano go, jak wysyłać dane tooIoT Centrum tooinitialize hello urządzenia biblioteki, i otrzymywać wiadomości. Hello informacje w tym artykule powinien być wystarczająco dużo tooget uruchomiony przy użyciu hello zestawu SDK, ale także wskaźniki tooadditional informacje o bibliotekach hello.

## <a name="sdk-architecture"></a>Architektura zestawu SDK

Można znaleźć hello [ **urządzenia Azure IoT SDK dla języka C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repozytorium i Wyświetl szczegóły hello interfejsu API w hello [dokumentacja interfejsu API C](https://azure.github.io/azure-iot-sdk-c/index.html).

najnowszą wersję Hello hello bibliotek można znaleźć w hello **wzorca** gałęzi repozytorium hello:

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* Witaj core implementacja hello zestawu SDK jest w hello **Centrum iothub\_klienta** folderu, który zawiera implementację hello hello najniższy poziom interfejsu API zestawu SDK hello: hello **IoTHubClient** biblioteki. Witaj **IoTHubClient** biblioteka zawiera interfejsy API Implementowanie raw wiadomości do wysyłania wiadomości tooIoT koncentratora i odbieranie komunikatów z Centrum IoT. Korzystając z tej biblioteki, jest odpowiedzialny za wdrażanie serializacji komunikatu, ale inne szczegóły komunikowania się z Centrum IoT są obsługiwane dla Ciebie.
* Witaj **serializator** folder zawiera funkcje pomocnicze i przykłady, które pokazują, jak tooserialize danych przed wysłaniem przy użyciu Centrum IoT tooAzure hello biblioteki klienta. Użycie Hello hello Serializator nie jest obowiązkowe i jest dostępne dla wygody. Witaj toouse **serializator** biblioteki, należy zdefiniować modelu, który określa danych toosend tooIoT koncentratora i hello wiadomości powitania oczekiwać tooreceive od niego. Po modelu hello jest zdefiniowany, hello zestaw SDK umożliwia powierzchni interfejsu API, która umożliwia tooeasily pracy z urządzenia do chmury i komunikaty chmury do urządzenia, nie martwiąc się o hello szczegóły serializacji. Biblioteka Hello jest zależny od innych bibliotek typu open source, które implementują transportu przy użyciu protokołów, takich jak MQTT i protokołu AMQP.
* Witaj **IoTHubClient** biblioteki jest zależny od innych bibliotek typu open source:
  * Witaj [Azure C udostępnione narzędzie](https://github.com/Azure/azure-c-shared-utility) biblioteki, która zawiera często używane funkcje podstawowe zadania (na przykład ciągi, manipulowanie listy i we/wy) wymagane przez zestawów SDK C związanych z platformy Azure.
  * Witaj [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) biblioteki, która jest implementacją protokołu AMQP zoptymalizowane pod kątem urządzeń zasobów ograniczone po stronie klienta.
  * Witaj [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) biblioteki, która jest biblioteką ogólnego przeznaczenia implementacji protokołu MQTT hello i zoptymalizowany pod kątem urządzeń zasobów ograniczone.

Te biblioteki jest łatwiejsze toounderstand analizując przykładowy kod. następujące sekcje Hello umożliwia przeprowadzenie kilka hello przykładowej aplikacji, które znajdują się w hello zestawu SDK. W tym przewodniku powinien zapewnić jest dobrą działanie hello różnych funkcjach warstwy architektury hello hello zestawu SDK i powitalne toohow wprowadzenie pracy interfejsów API.

## <a name="before-you-run-hello-samples"></a>Przed uruchomieniem hello próbek

Przed uruchomieniem hello próbek w hello urządzenia Azure IoT SDK dla języka C, należy najpierw [Utwórz wystąpienie hello usługi IoT Hub](iot-hub-create-through-portal.md) w Twojej subskrypcji platformy Azure. Następnie ukończyć powitalnych następujące zadania:

* Przygotowywanie środowiska projektowego
* Uzyskaj poświadczenia urządzenia.

### <a name="prepare-your-development-environment"></a>Przygotowywanie środowiska projektowego

Pakiety są dostępne dla wspólnego platformy (na przykład NuGet dla systemu Windows lub apt_get Debian i Ubuntu) i przykłady hello za pomocą tych pakietów, jeśli jest dostępna. W niektórych przypadkach należy hello toocompile zestawu SDK dla lub na urządzeniu. Jeśli potrzebujesz hello toocompile zestawu SDK, zobacz [przygotowywanie środowiska projektowego](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) w repozytorium GitHub hello.

tooobtain hello przykładowy kod aplikacji, Pobierz kopię hello SDK z usługi GitHub. Pobierz kopię hello źródła z hello **wzorca** gałęzi hello [repozytorium GitHub](https://github.com/Azure/azure-iot-sdk-c).


### <a name="obtain-hello-device-credentials"></a>Uzyskaj poświadczenia urządzenia hello

Teraz, gdy masz hello przykładowy kod źródłowy dalej toodo operacją hello jest tooget zestaw poświadczeń, urządzenie. Dla urządzenia toobe stanie tooaccess Centrum IoT najpierw należy dodać hello urządzenia toohello w rejestrze tożsamości Centrum IoT. Po dodaniu urządzenia otrzymasz zestaw poświadczeń urządzenia, wymagane dla Centrum IoT toohello toobe tooconnect stanie hello urządzenia. Hello przykładowe aplikacje omówiona w następnej sekcji hello mogą pojawić się te poświadczenia w postaci hello **ciąg połączenia urządzenia**.

Istnieje kilka toohelp narzędzi typu open source, zarządzanie Centrum IoT.

* Aplikacji systemu Windows o nazwie [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).
* Wywołuje narzędzie interfejsu wiersza polecenia i platform node.js [explorer Centrum iothub](https://github.com/azure/iothub-explorer).

W tym samouczku używana hello graficznego *explorer urządzenia* narzędzia. Można również użyć hello *explorer Centrum iothub* narzędzia, jeśli wolisz toouse narzędzia interfejsu wiersza polecenia.

Narzędzie explorer urządzenia Hello używa tooperform bibliotek usługi Azure IoT hello różnych funkcji w Centrum IoT, łącznie z dodawaniem urządzeń. Jeśli używasz hello urządzenia explorer narzędzia tooadd urządzenia, możesz uzyskać ciąg połączenia urządzenia. Należy to połączenie ciąg toorun hello przykładowe aplikacje.

Jeśli nie znasz za pomocą narzędzia Eksplorator hello urządzenia, hello procedury w tym artykule opisano sposób toouse on tooadd urządzenie i uzyskać ciąg połączenia urządzenia.

Narzędzie explorer tooinstall hello urządzenia, zobacz [jak toouse hello Explorer urządzenia dla urządzeń z Centrum IoT](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).

Po uruchomieniu hello program, zostanie wyświetlony ten interfejs:

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

Wprowadź użytkownika **parametry połączenia Centrum IoT** w hello pierwsze pole i kliknij przycisk **aktualizacji**. Ten krok obejmuje skonfigurowanie narzędzia hello tak, aby umożliwić komunikację z Centrum IoT.

Po skonfigurowaniu hello parametry połączenia Centrum IoT kliknij hello **zarządzania** karty:

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

Ta karta jest, którym zarządzasz hello urządzeń zarejestrowanych w Centrum IoT.

Urządzenie można tworzyć przez kliknięcie hello **Utwórz** przycisku. Wyświetla okno dialogowe z zestawu kluczy wstępnie wypełnione (podstawowych i pomocniczych). Wprowadź **identyfikator urządzenia** , a następnie kliknij przycisk **Utwórz**.

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

Po utworzeniu urządzenia hello urządzeń hello Wyświetl listę wszystkich hello zarejestrowanych urządzeń, takich jak hello utworzony co aktualizacji. Kliknięcie prawym przyciskiem myszy urządzenie nowej pojawić tego menu:

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

Jeśli wybierzesz **skopiuj parametry połączenia dla wybranego urządzenia**, ciąg połączenia urządzenia hello jest skopiowany toohello Schowka. Przechowywać kopię ciąg połączenia urządzenia hello. Należy go podczas uruchamiania aplikacji przykładowych hello opisanego w hello następujące sekcje.

Po ukończeniu powyższych kroków hello, wszystko jest gotowe toostart uruchamiania kodu. Oba przykłady ma stałą u góry hello hello główne źródło pliku, który umożliwia tooenter ciąg połączenia. Na przykład Witaj odpowiedni wiersz z hello **Centrum iothub\_klienta\_próbki\_mqtt** aplikacja pojawi się w następujący sposób.

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a>Użyj hello IoTHubClient biblioteki

W ramach hello **Centrum iothub\_klienta** folderu w hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repozytorium, Brak **przykłady** folder, który zawiera aplikację o nazwie **Centrum iothub\_klienta\_próbki\_mqtt**.

Wersja Windows Hello hello **Centrum iothub\_klienta\_próbki\_mqtt** aplikacja zawiera hello następujące rozwiązania Visual Studio:

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> Po otwarciu tego projektu w programie Visual Studio 2017 zaakceptować hello monity tooretarget hello projektu toohello najnowszej wersji.

To rozwiązanie zawiera jeden projekt. Istnieją cztery pakiety NuGet zainstalowany w tym rozwiązaniu:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.umqtt

Należy zawsze hello **Microsoft.Azure.C.SharedUtility** pakietu podczas pracy z hello zestawu SDK. Ten przykład wykorzystuje protokół MQTT hello, w związku z tym musi zawierać hello **Microsoft.Azure.umqtt** i **Microsoft.Azure.IoTHub.MqttTransport** pakietów (są równoważne pakietów dla protokołu AMQP i HTTP ). Ponieważ hello w przykładzie użyto hello **IoTHubClient** biblioteki, musi także obejmować hello **Microsoft.Azure.IoTHub.IoTHubClient** pakietu w rozwiązaniu.

Implementacja hello hello przykładowej aplikacji można znaleźć w hello **Centrum iothub\_klienta\_próbki\_mqtt.c** pliku źródłowego.

Witaj następujące kroki używać tej przykładowej aplikacji toowalk przez co wymagane toouse hello **IoTHubClient** biblioteki.

### <a name="initialize-hello-library"></a>Zainicjowanie biblioteki hello

> [!NOTE]
> Przed rozpoczęciem pracy z bibliotekami hello może być konieczne tooperform inicjowania niektóre specyficzne dla platformy. Na przykład jeśli planujesz toouse AMQP w systemie Linux należy zainicjować biblioteki OpenSSL hello. Witaj próbek w hello [repozytorium GitHub](https://github.com/Azure/azure-iot-sdk-c) wywołania funkcji narzędzia hello **platformy\_init** po hello uruchamia klienta i Wywołaj hello **platformy\_deinit**  funkcja przed zakończeniem. Te funkcje są zadeklarowane w pliku nagłówka platform.h hello. Sprawdź hello definicji funkcji dla danej platformy docelowej w hello [repozytorium](https://github.com/Azure/azure-iot-sdk-c) toodetermine tego, czy należy tooinclude dowolny kod inicjujący specyficzne dla platformy, na kliencie.

Praca z bibliotekami hello toostart najpierw przydzielić dojścia klienta Centrum IoT:

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

Należy przekazać kopię ciąg połączenia urządzenia hello uzyskane z hello urządzenia explorer narzędzia toothis funkcji. Możesz też określić hello komunikacji protokołu toouse. W tym przykładzie użyto MQTT, ale AMQP i HTTP są także opcje.

Jeśli użytkownik ma prawidłowy **Centrum IOTHUB\_klienta\_obsługi**, można uruchomić wywoływania hello toosend interfejsów API i odbieranie wiadomości tooand z Centrum IoT.

### <a name="send-messages"></a>Wysyłanie wiadomości

Centrum IoT pętli toosend wiadomości tooyour ustawia Hello przykładowej aplikacji. Witaj następujący fragment kodu:

- Tworzy komunikat.
- Dodaje komunikat toohello właściwości.
- Wysyła komunikat.

Najpierw utwórz komunikat:

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

Każdorazowym wysłaniu wiadomości, można określić funkcję wywołania zwrotnego tooa odwołanie, które jest wywoływane, gdy hello dane są wysyłane. W tym przykładzie jest wywoływana funkcja wywołania zwrotnego hello **SendConfirmationCallback**. powitania po fragment kodu przedstawia tej funkcji wywołania zwrotnego:

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

Należy zwrócić uwagę hello wywołania toohello **IoTHubMessage\_Destroy** działać po zakończeniu wiadomość hello. Ta funkcja zwalnia zasoby hello przydzielone podczas tworzenia wiadomości powitania.

### <a name="receive-messages"></a>Odbieranie komunikatów

Odbieranie wiadomości jest operacja asynchroniczna. Po pierwsze zarejestrujesz tooinvoke wywołania zwrotnego hello odebrania wiadomość hello urządzenia:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

Ostatni parametr Hello jest toowhatever void wskaźnika, który ma. W przykładowym hello jest liczba całkowita tooan wskaźnika, ale można jej tooa wskaźnika bardziej złożonych struktury danych. Ten parametr umożliwia toooperate funkcja wywołania zwrotnego hello na udostępniania stanu wywołującego hello tej funkcji.

Gdy hello urządzenie odbiera wiadomości, hello zarejestrowana funkcja wywołania zwrotnego jest wywoływany. Ta funkcja wywołania zwrotnego pobiera:

* Identyfikator wiadomości powitania i identyfikator korelacji z wiadomości powitania.
* zawartość wiadomości powitania.
* Wszystkie niestandardowe właściwości z wiadomości powitania.

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Użyj hello **IoTHubMessage\_GetByteArray** wiadomości powitania tooretrieve funkcja, której wartość jest ciągiem.

### <a name="uninitialize-hello-library"></a>Odinicjalizuj hello biblioteki

Po zakończeniu wysyłania zdarzeń i odbieranie wiadomości, można uninitialize hello IoT biblioteki. toodo wystawiania, powitania po wywołaniu funkcji:

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

To wywołanie zwolni zasoby hello przydzielona wcześniej przez hello **IoTHubClient\_CreateFromConnectionString** funkcji.

Jak widać, jest łatwe toosend i odbieranie komunikatów za pomocą hello **IoTHubClient** biblioteki. Witaj biblioteki obsługuje szczegóły hello komunikowania się z Centrum IoT, które toouse protokołu w tym (względem hello dewelopera hello jest opcja prostą konfigurację).

Witaj **IoTHubClient** Biblioteka również zapewnia precyzyjną kontrolę nad jak tooserialize hello dane urządzenie wysyła tooIoT koncentratora. W niektórych przypadkach ten poziom kontroli jest korzyści, ale w innych jest szczegółów implementacji, które nie mają toobe zajęto się. Jeśli to hello case, warto rozważyć przy użyciu hello **serializator** biblioteki, który jest opisany w następnej sekcji hello.

## <a name="use-hello-serializer-library"></a>Użyj hello serializator biblioteki

Koncepcyjnie hello **serializator** biblioteki znajduje się na szczycie hello **IoTHubClient** biblioteki w hello zestawu SDK. Używa hello **IoTHubClient** biblioteki hello bazowy komunikacji z Centrum IoT, ale dodaje modelowania możliwości, które usunąć obciążenia hello postępowania z serializacji komunikatu z hello developer. Jak działa ta biblioteka najlepsze dowodzą przykładem.

Witaj wewnątrz **serializator** folderu w hello [repozytorium azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c), jest **przykłady** folder, który zawiera aplikację o nazwie **simplesample \_mqtt**. wersja systemu Windows Hello tego przykładu obejmuje hello następujące rozwiązania Visual Studio:

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> Po otwarciu tego projektu w programie Visual Studio 2017 zaakceptować hello monity tooretarget hello projektu toohello najnowszej wersji.

Podobnie jak w przypadku hello poprzedni przykład, ta obejmuje kilka pakietów NuGet:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.IoTHub.Serializer
* Microsoft.Azure.umqtt

W tym samouczku większość tych pakietów hello powyższego przykładu, ale **Microsoft.Azure.IoTHub.Serializer** nowego. Ten pakiet jest wymagany, gdy używasz hello **serializator** biblioteki.

Implementacja hello hello przykładowej aplikacji można znaleźć w hello **simplesample\_mqtt.c** pliku.

Hello następnych sekcjach opisano części klucza hello tego przykładu.

### <a name="initialize-hello-library"></a>Zainicjowanie biblioteki hello

Praca z hello toostart **serializator** biblioteki, inicjowanie hello wywołania interfejsów API:

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

Witaj wywołania toohello **serializator\_init** funkcja jest wywołaniem jednorazowe i inicjuje hello podstawowej biblioteki. Następnie wywołaj metodę hello **IoTHubClient\_LL\_CreateFromConnectionString** funkcji, która jest hello tego samego interfejsu API tak jak hello **IoTHubClient** próbki. To wywołanie ustawia parametry połączenia urządzenia (to wywołanie jest również, gdzie należy wybrać protokół hello ma toouse). W tym przykładzie używa MQTT jako hello transportu, ale można użyć protokołu AMQP i HTTP.

Na koniec wywołania hello **Utwórz\_modelu\_wystąpienia** funkcji. **WeatherStation** jest przestrzenią nazw hello hello modelu i **ContosoAnemometer** jest nazwą hello hello modelu. Po utworzeniu hello wystąpienie modelu, można użyć toostart wysyłania i odbierania wiadomości. Jest jednak toounderstand ważne jest jakie modelu.

### <a name="define-hello-model"></a>Zdefiniuj hello modelu

Model w hello **serializator** Biblioteka definiuje wiadomości powitania, które urządzenie może wysyłać tooIoT koncentratora i hello, o nazwie *akcje* w hello język, który może odbierać modelowania. Zdefiniuj modelu przy użyciu zestawu makr C jak hello **simplesample\_mqtt** aplikacji przykładowej:

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Hello **rozpocząć\_przestrzeni nazw** i **zakończenia\_przestrzeni nazw** makra zarówno zająć hello przestrzeń nazw modelu hello jako argument. Oczekuje się, że wszystko między tymi makra jest hello definicji modelu lub modeli i struktury danych hello korzystających z modeli hello.

W tym przykładzie jest pojedynczego modelu o nazwie **ContosoAnemometer**. Ten model definiuje dwie części danych, czy urządzenie może wysyłać tooIoT Centrum: **DeviceId** i **prędkość wiatru**. Definiuje również trzy czynności (wiadomości), które urządzenia mogą odbierać: **TurnFanOn**, **TurnFanOff**, i **SetAirResistance**. Każdy element danych ma typ, a każda akcja ma nazwę (i opcjonalnie zestaw parametrów).

Hello danych i akcje zdefiniowane w modelu hello definiują powierzchni interfejsu API Użyj toosend wiadomości tooIoT koncentratora, a urządzenie toohello toomessages wysyłane odpowiedzi. Użycie tego modelu najlepiej jest rozpoznawany przez przykładowy.

### <a name="send-messages"></a>Wysyłanie wiadomości

Hello model definiuje hello danych, możesz wysłać tooIoT koncentratora. W tym przykładzie, oznacza to, co hello dwa elementy danych zdefiniowany przy użyciu hello **WITH_DATA** makra. Istnieje kilka czynności, wymagane toosend **DeviceId** i **prędkość wiatru** Centrum IoT tooan wartości. Hello jest najpierw tooset hello dane, które mają toosend:

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

Hello model został zdefiniowany wcześniej pozwala tooset hello wartości przez ustawienie członkami **struktury**. Następnie serializować wiadomość hello, które chcesz toosend:

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

Ten kod serializuje hello buforu tooa urządzenia do chmury (odwołuje **docelowego**). Kod Hello następnie wywołuje hello **sendMessage** funkcji tooIoT wiadomość hello toosend Centrum:

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


Witaj drugi parametr toolast **IoTHubClient\_LL\_SendEventAsync** jest odwołanie funkcji wywołania zwrotnego tooa jest wywoływane, gdy dane hello jest pomyślnie wysłane. W tym miejscu jest funkcja wywołania zwrotnego hello w przykładowym hello:

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

drugi parametr Hello jest kontekst toouser wskaźnika; Witaj tego samego wskaźnik przekazany za**IoTHubClient\_LL\_SendEventAsync**. W takim przypadku kontekst hello jest prostego licznika, ale może być dowolny.

To wszystko jest toosending wiadomości urządzenia do chmury. Witaj tylko po lewej toocover jest to, jak tooreceive wiadomości.

### <a name="receive-messages"></a>Odbieranie komunikatów

Odbieranie wiadomości działa podobnie sposób toohello komunikatów działa w hello **IoTHubClient** biblioteki. Najpierw należy zarejestrować funkcję wywołania zwrotnego komunikat:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

Następnie napiszesz hello funkcja wywołania zwrotnego, które jest wywoływane, gdy wiadomość zostanie odebrana:

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

Ten kod jest standardowy — ma hello takie same dla dowolnego rozwiązania. Ta funkcja odbiera wiadomości powitania i zajmuje się rozsyłania jej toohello odpowiednią funkcję za pomocą wywołania hello zbyt**EXECUTE\_polecenia**. wywołana funkcja Hello na tym etapie zależy od definicji hello hello działań w modelu.

Po zdefiniowaniu akcji w modelu jest wymagana tooimplement funkcję, która jest wywoływana, gdy urządzenie otrzyma odpowiednia wiadomość hello. Na przykład, jeśli model definiuje tej akcji:

```c
WITH_ACTION(SetAirResistance, int, Position)
```

Zdefiniuj funkcję z tego podpisu:

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

Należy zwrócić uwagę, jak nazwa hello funkcji hello odpowiada nazwie hello hello akcji w modelu hello a hello parametry funkcji hello są takie same parametry hello określone dla akcji hello. pierwszy parametr Hello jest zawsze wymagane i zawiera wskaźnik toohello wystąpienie modelu.

Witaj urządzenie otrzyma wiadomość pasującego do tego podpisu, jest nazywany hello odpowiednich funkcji. W związku z tym jako uzupełnienie o tooinclude hello schematyczny kod z **IoTHubMessage**, odbierania wiadomości jest wystarczy zdefiniować funkcję proste dla każdej akcji zdefiniowanych w modelu.

### <a name="uninitialize-hello-library"></a>Odinicjalizuj hello biblioteki

Po zakończeniu wysyłania danych i odbierania wiadomości, można uninitialize hello IoT biblioteki:

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

Każda z tych trzech funkcji wyrównana z hello trzech funkcji inicjowania opisanych powyżej. Te interfejsy API do wywoływania zapewnia zwolnienie wcześniej przydzielone zasoby.

## <a name="next-steps"></a>Następne kroki

W tym artykule omówione podstawy hello przy użyciu bibliotek hello hello **urządzenia Azure IoT SDK dla języka C**. On udostępniony za mało toounderstand informacji dostępnych w hello zestawu SDK, jego architektury i jak tooget pracę z hello przykładów Windows. kolejnym artykule Hello nadal hello opis hello zestawu SDK przez wyjaśniający [więcej informacji na temat biblioteki IoTHubClient hello](iot-hub-device-sdk-c-iothubclient.md).

toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz hello [Azure IoT SDK][lnk-sdks].

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
