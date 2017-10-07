---
title: "urządzenia IoT aaaAzure zestawu SDK dla języka C - IoTHubClient | Dokumentacja firmy Microsoft"
description: "Jak toouse hello IoTHubClient biblioteki hello Azure IoT urządzenia zestawu SDK dla aplikacji dla urządzeń toocreate C komunikujących się z Centrum IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>Azure urządzenia IoT zestawu SDK dla języka C — więcej informacji na temat IoTHubClient
Witaj [najpierw artykuł](iot-hub-device-sdk-c-intro.md) w tej serii wprowadzone hello **urządzenia Azure IoT SDK dla języka C**. Tym artykule wyjaśniono, że istnieją dwie warstwy architektury w zestawie SDK. W podstawowej hello jest hello **IoTHubClient** biblioteki, który bezpośrednio prowadzi komunikację z Centrum IoT. Istnieje również hello **serializator** biblioteki, która tworzy znajdujący się na tooprovide szeregowanie usług. W tym artykule udostępnimy dodatkowych szczegółów na powitania **IoTHubClient** biblioteki.

Witaj poprzednim artykule opisano sposób toouse hello **IoTHubClient** biblioteki toosend zdarzenia tooIoT koncentratora i odbierania wiadomości. W tym artykule rozszerza tej dyskusji, wyjaśniający, jak zarządzać dokładnie toomore *podczas* wysyłać i odbierać dane, wprowadzenie toohello **interfejsów API niższego poziomu**. Prezentujemy również zasady jak tooevents właściwości tooattach (i pobrać wiadomości) przy użyciu właściwości hello obsługi funkcji w hello **IoTHubClient** biblioteki. Ponadto firma Microsoft udostępni dodatkowe objaśnienia dotyczące sposobów toohandle komunikatów odebranych z Centrum IoT.

Witaj artykuł zawiera przez obejmujące kilka różnych tematów, tym więcej informacji o poświadczeniach urządzenia i sposobu toochange hello zachowanie hello **IoTHubClient** za pomocą opcji konfiguracji.

Użyjemy hello **IoTHubClient** SDK przykłady tooexplain tych tematów. Toofollow wzdłuż, zobacz hello **Centrum iothub\_klienta\_próbki\_http** i **Centrum iothub\_klienta\_próbki\_amqp** aplikacji, które znajdują się w hello urządzenia Azure IoT SDK, aby przedstawionej C. wszystko, co opisano w hello następujące sekcje w tych przykładów.

Można znaleźć hello [ **urządzenia Azure IoT SDK dla języka C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repozytorium i Wyświetl szczegóły hello interfejsu API w hello [dokumentacja interfejsu API C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-lower-level-apis"></a>Witaj interfejsów API niższego poziomu
Hello poprzednim artykule opisano podstawowe operacje hello hello **IotHubClient** w kontekście hello hello **Centrum iothub\_klienta\_próbki\_amqp** aplikacja. Na przykład wyjaśniono, jak tooinitialize hello bibliotekę przy użyciu tego kodu.

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Opisano również, jak za pomocą tego zdarzenia toosend wywołania funkcji.

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

Artykuł Hello są także opisane jak tooreceive wiadomości przez zarejestrowanie funkcję wywołania zwrotnego.

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

Artykuł Hello również pokazano, jak toofree zasobów przy użyciu kodu takie jak następujące hello.

```
IoTHubClient_Destroy(iotHubClientHandle);
```

Istnieją jednak tooeach funkcji Pomocnik tych interfejsów API:

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_zniszczyć

Wszystkie funkcje te obejmują "Wszystko" w hello Nazwa interfejsu API. Inną niż każda z tych funkcji hello parametry są identyczne tootheir z systemem innym niż LL odpowiedniki. Jednak hello tych funkcji jest różny w jednym ze sposobów ważne.

Podczas wywoływania **IoTHubClient\_CreateFromConnectionString**, biblioteki podstawowej hello utworzyć nowego wątku działającym w tle hello. Wysyła zdarzenia do tego wątku i odbiera komunikaty z Centrum IoT. Nie takiego wątku jest tworzony podczas pracy z hello "Wszystko" interfejsów API. Tworzenie Hello wątku w tle hello jest dewelopera toohello wygody. Nie masz tooworry o jawnie wysyłanie zdarzeń i odbieranie komunikatów z Centrum IoT — wykonywane automatycznie hello tła. Z kolei hello "Wszystko" interfejsów API zapewniają jawne kontroluje komunikację z Centrum IoT, jeśli zajdzie taka potrzeba.

toounderstand to lepiej Przyjrzyjmy się przykładem:

Podczas wywoływania **IoTHubClient\_SendEventAsync**, co faktycznie robimy obciążające hello zdarzeń w buforze. Witaj wątku w tle tworzone podczas wywoływania **IoTHubClient\_CreateFromConnectionString** stale monitoruje buforu i wysyła żadnych danych zawiera tooIoT koncentratora. Dzieje się to w tle hello na powitania sam czas hello tego wątku głównego jest wykonywanie innych zadań.

Podobnie po rejestracji funkcję wywołania zwrotnego dla wiadomości przy użyciu **IoTHubClient\_SetMessageCallback**, jest poinstruowanie hello SDK toohave hello tła wątku wywołania funkcji wywołania zwrotnego hello, gdy wiadomość Odebrano, niezależnie od wątku głównego hello.

Witaj "Wszystko" interfejsów API nie należy tworzyć wątku w tle. Zamiast tego nowy interfejs API musi zostać wywołana tooexplicitly wysyłania i odbierania danych z Centrum IoT. To jest przedstawiona w hello poniższy przykład.

Witaj **Centrum iothub\_klienta\_próbki\_http** aplikacji, która znajduje się w hello pokazuje SDK hello interfejsów API niższego poziomu. W tym przykładzie mamy wysłać zdarzenia tooIoT Centrum z kodem, takie jak następujące hello:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Witaj pierwsze trzy wiersze Utwórz wiadomość hello i hello ostatni wiersz wysyła zdarzenie hello. Jednak jak już wspomniano, "Wysyłanie" hello zdarzenie oznacza, że dane hello jest po prostu umieścić w buforze. Nic nie jest przesyłane w sieci hello podczas nazywamy **IoTHubClient\_LL\_SendEventAsync**. W kolejności tooactually wejściowych hello danych tooIoT koncentratora, należy wywołać **IoTHubClient\_LL\_DoWork**w tym przykładzie:

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Ten kod (z hello **Centrum iothub\_klienta\_próbki\_http** aplikacji) wielokrotnie wywołuje **IoTHubClient\_LL\_DoWork** . Zawsze **IoTHubClient\_LL\_DoWork** jest wywoływana, wysyła niektórych zdarzeń z tooIoT buforu hello Centrum i pobiera ona wiadomość w kolejce wysyłania toohello urządzenia. drugim przypadku Hello oznacza, że jeśli firma Microsoft zarejestrowana funkcja wywołania zwrotnego dla wiadomości, a następnie wywołania zwrotnego hello jest wywoływany (przy założeniu, że komunikaty są umieszczone w kolejce). Firma Microsoft będzie zarejestrowanych funkcję wywołania zwrotnego z kodem, takie jak następujące hello:

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

Hello przyczyny, że **IoTHubClient\_LL\_DoWork** jest często nazywana pętli jest to, że zawsze jest nazywana, wysyła *niektórych* buforowane tooIoT zdarzenia koncentratora i pobiera *hello obok* wiadomości w kolejce hello urządzenia. Każde wywołanie nie jest gwarantowana zdarzenia toosend buforowane lub tooretrieve wszystkich umieszczonych w kolejce wiadomości. Jeśli chcesz toosend wszystkie zdarzenia w hello buforu, a następnie kontynuuj na inne przetwarzania można zastąpić pętlę kodu, takie jak następujące hello:

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Ten kod wywołuje **IoTHubClient\_LL\_DoWork** dopóki wszystkie zdarzenia w buforze hello zostały wysłane tooIoT koncentratora. Należy pamiętać, że nie również oznacza otrzymanie wszystkie wiadomości w kolejce. Część hello przyczyną tego błędu jest, że sprawdzanie komunikatów "all" nie jest deterministyczna jako akcję. Co się stanie, jeśli pobierasz "wszystkie" wiadomości powitania, ale następnie wysyłane innego urządzenia toohello natychmiast po? Lepsze toodeal sposób, z którego jest zaprogramowanych limitu czasu. Na przykład funkcja wywołania zwrotnego wiadomość hello można zresetować czasomierz za każdym razem, gdy jest wywoływana. Możesz następnie zapisywać logiki toocontinue przetwarzania, jeśli na przykład żadnych komunikatów nie odebrano w hello ostatnio *X* sekund.

Po jest ingressing gotowego zdarzenia i odbieranie wiadomości, można się toocall hello odpowiedniej funkcji tooclean zasobów.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Zasadniczo istnieje tylko jeden zestaw interfejsów API toosend i odbierać dane z wątku w tle i inny zestaw interfejsów API, które hello samo bez hello wątku w tle. Wiele deweloperzy mogą preferować hello z systemem innym niż — wszystkie interfejsy API, ale hello interfejsów API niższego poziomu są przydatne, gdy hello Deweloper chce jawną kontrolę nad transmisji w sieci. Na przykład niektóre urządzenia zbieranie danych przez czasu i zdarzeń wejściowych tylko w określonych odstępach czasu (na przykład, jeden raz na godzinę lub raz dziennie). Witaj hello kontroli tooexplicitly możliwości wysyłania i odbierania danych z Centrum IoT zapewnia interfejsy API niższego poziomu. Inne po prostu preferowane hello uproszczenia tego hello zapewniają interfejsów API niższego poziomu. Wszystko, co się stanie w wątku głównego hello zamiast niektórych pracy w toku w tle hello.

Niezależnie od tego modelu, należy wybrać, należy się toobe spójne w których interfejsy API jest używany. Po uruchomieniu przez wywołanie metody **IoTHubClient\_LL\_CreateFromConnectionString**, należy używać tylko hello odpowiadającego interfejsy API niższego poziomu do monitowania pracę:

* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_zniszczyć
* IoTHubClient\_LL\_DoWork

Hello przeciwną jest również wartość true. Jeśli na początku zasubskrybujesz **IoTHubClient\_CreateFromConnectionString**, a następnie użyj hello z systemem innym niż — wszystkie interfejsy API dla dowolnego dodatkowego przetwarzania.

W hello urządzenia Azure IoT SDK dla języka C, zobacz hello **Centrum iothub\_klienta\_próbki\_http** aplikacji pełny przykład hello niższego poziomu interfejsów API. Witaj **Centrum iothub\_klienta\_próbki\_amqp** aplikacji można odwoływać się pełny przykład hello nie - LL interfejsów API.

## <a name="property-handling"></a>Obsługa właściwości
Do tej pory możemy zostały opisane wysyłanie danych, firma Microsoft już został odnosi toohello treści wiadomości powitania. Rozważmy na przykład ten kod:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

W tym przykładzie wysyła komunikat tooIoT Centrum hello tekst "Hello World". Centrum IoT umożliwia także właściwości toobe tooeach dołączonych wiadomości. Właściwości są pary nazwa/wartość, które mogą być dołączone toohello wiadomości. Możemy na przykład zmodyfikować hello poprzedniego kodu tooattach komunikat toohello właściwości:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Rozpoczniemy wywołując **IoTHubMessage\_właściwości** i przekazanie jej hello obsługi wiadomości. Co mamy wrócić jest **mapy\_obsługi** odwołania, który pozwala toostart Dodawanie właściwości. ostatnie Hello odbywa się przez wywołanie metody **mapy\_AddOrUpdate**, który przyjmuje odwołanie tooa mapy\_UCHWYTU, nazwa właściwości hello i wartość właściwości hello. W tym interfejsie API można dodać dowolną liczbę właściwości, jak firma Microsoft.

Zdarzenia hello jest odczytywana od **usługi Event Hubs**, odbiornika hello można wyliczyć właściwości hello i pobieranie ich wartości. Na przykład w środowisku .NET to może osiągnąć, uzyskując dostęp do hello [kolekcji właściwości w obiekcie EventData hello](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).

W poprzednim przykładzie hello możemy Cię dołączanie czy mamy wysłać tooIoT Centrum zdarzeń tooan właściwości. Właściwości można też dołączone toomessages odebranych z Centrum IoT. Aby tooretrieve właściwości z komunikatu, możemy użyć kodu, takie jak następujące hello w naszej funkcji wywołania zwrotnego komunikat:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

Witaj wywołanie za**IoTHubMessage\_właściwości** hello zwraca **mapy\_obsługi** odwołania. Następnie jest przekazywana odwołującymi się zbyt**mapy\_GetInternals** tooobtain tablicą tooan odwołanie wartości nazwy hello pary (a także liczbę właściwości hello). W tym momencie jest polegać wyliczania hello właściwości tooget toohello wartości, którą chcemy udostępnić.

Nie masz toouse właściwości w aplikacji. Jednak jeśli potrzebujesz tooset ich na zdarzenia lub pobrać je z wiadomości, hello **IoTHubClient** biblioteki ułatwia.

## <a name="message-handling"></a>Komunikat — Obsługa
Jak wspomniano wcześniej, gdy nadchodzą komunikaty z Centrum IoT hello **IoTHubClient** Biblioteka odpowiada za pomocą zarejestrowana funkcja wywołania zwrotnego. Brak parametru zwrotnego tej funkcji, która wymaga dodatkowych wyjaśnień. Oto fragment hello funkcja wywołania zwrotnego w hello **Centrum iothub\_klienta\_próbki\_http** aplikacji przykładowej:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Należy pamiętać, że typ zwracany hello **IOTHUBMESSAGE\_DYSPOZYCJI\_wynik** w tym przypadku zostanie zwrócona **IOTHUBMESSAGE\_ZAAKCEPTOWANE**. Istnieją inne wartości, firma Microsoft może zwracać z tej funkcji zmiany sposobu hello **IoTHubClient** biblioteki reaguje toohello wywołanie zwrotne komunikatu. Oto opcje hello.

* **IOTHUBMESSAGE\_ZAAKCEPTOWANE** — wiadomość hello został pomyślnie przetworzony. Witaj **IoTHubClient** biblioteki nie wywoła funkcję wywołania zwrotnego hello ponownie z hello tego samego komunikatu.
* **IOTHUBMESSAGE\_ODRZUCONE** — wiadomość hello nie została przetworzona i istnieje nie toodo desire hello dlatego w przyszłości. Witaj **IoTHubClient** biblioteki nie należy wywołać funkcję wywołania zwrotnego hello ponownie z hello tego samego komunikatu.
* **IOTHUBMESSAGE\_ABANDONED** — wiadomość hello nie została przetworzona pomyślnie, ale hello **IoTHubClient** biblioteki należy wywołać funkcję wywołania zwrotnego hello ponownie z hello tego samego komunikatu.

Dla hello pierwsze dwa kody powrotne, hello **IoTHubClient** biblioteki wysyła komunikat tooIoT wskazująca, że wiadomość hello koncentratora powinny być usuwane z kolejki urządzenia hello i nie można dostarczyć ponownie. Efekt netto Hello jest hello takie same (wiadomość hello jest usuwane z kolejki urządzenia hello), ale czy zaakceptowane lub odrzucone wiadomości powitania nadal jest rejestrowany.  Rejestrowanie tego rozróżnienie jest przydatne toosenders wiadomość hello, kto może nasłuchiwać opinii i sprawdzić, czy urządzenie ma zaakceptowane lub odrzucone danego komunikatu.

W przypadku ostatniego hello zostanie także wysłana wiadomość tooIoT koncentratora, ale oznacza ona tę wiadomość hello powinien być dostarczony ponownie. Zwykle będzie abandon komunikat, jeśli wystąpi błąd, ale chcę tootry tooprocess wiadomość hello ponownie. Z kolei odrzuca wiadomości jest odpowiednia, w przypadku wystąpienia nieodwracalnego błędu (lub po prostu zdecydować się, że nie chcesz, aby wiadomość hello tooprocess).

W każdym przypadku należy pamiętać różnych kodów powrotnych hello, dzięki czemu można wywołać z hello zachowanie hello **IoTHubClient** biblioteki.

## <a name="alternate-device-credentials"></a>Poświadczenia alternatywne urządzenia
Jak opisano wcześniej, hello po pierwsze toodo podczas pracy z hello **IoTHubClient** biblioteka jest tooobtain **Centrum IOTHUB\_klienta\_obsługi** przy użyciu wywołania, takich jak hello następujące:

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Witaj argumenty za**IoTHubClient\_CreateFromConnectionString** są parametry połączenia urządzenia hello i parametr, który wskazuje protokołu hello używamy toocommunicate z Centrum IoT. ciąg połączenia urządzenia Hello ma format, który wygląda następująco:

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

Istnieją cztery elementy informacji w tym ciągu: Nazwa centrum IoT, sufiks Centrum IoT identyfikator urządzenia i udostępniony klucz dostępu. Uzyskaj hello pełną nazwę domeny (FQDN) z Centrum IoT podczas tworzenia wystąpienia Centrum IoT w portalu Azure hello — umożliwia nazwę Centrum IoT hello (hello pierwsza część hello FQDN) i sufiks Centrum IoT hello (hello reszty hello FQDN). Pobierz identyfikator urządzenia hello i hello udostępniony klucz dostępu podczas rejestrowania urządzenia z Centrum IoT (zgodnie z opisem w hello [poprzednim artykule](iot-hub-device-sdk-c-intro.md)).

**IoTHubClient\_CreateFromConnectionString** umożliwia jednokierunkowej tooinitialize hello biblioteki. Jeśli wolisz, możesz utworzyć nową **Centrum IOTHUB\_klienta\_obsługi** przy użyciu tych parametrów zamiast ciągu połączenia hello urządzenia. Jest to osiągane z hello następującego kodu:

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

To umożliwia zrealizowanie hello odpowiednikiem **IoTHubClient\_CreateFromConnectionString**.

Może wydawać się oczywiste, warto toouse **IoTHubClient\_CreateFromConnectionString** zamiast tego pełniejsze metody inicjowania. Należy pamiętać, że podczas rejestrowania urządzenia w Centrum IoT można pobrać jest identyfikator urządzenia i klucz urządzenia (nie w ciągu połączenia). Hello *explorer urządzenia* narzędzia zestawu SDK wprowadzone w hello [poprzednim artykule](iot-hub-device-sdk-c-intro.md) korzysta z bibliotek w hello **zestawu SDK usług Azure IoT** ciąg połączenia urządzenia hello toocreate z Identyfikator urządzenia Hello klucza urządzenia i nazwy hosta Centrum IoT. Dlatego wywołanie **IoTHubClient\_LL\_Utwórz** może być preferowana, ponieważ wymaga kroku hello Generowanie ciągu połączenia. Należy użyć metody jest wygodne.

## <a name="configuration-options"></a>Opcje konfiguracji
Do tej pory wszystkie elementy opisane o hello sposób hello **IoTHubClient** works biblioteki odzwierciedla jego zachowanie domyślne. Istnieje jednak kilka opcji, które można ustawić toochange działania hello biblioteki. Jest to osiągane przez wykorzystanie hello **IoTHubClient\_LL\_SetOption** interfejsu API. Należy wziąć pod uwagę w tym przykładzie:

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

Istnieje kilka opcji, które są powszechnie stosowane:

* **SetBatching** (wartość logiczna) — Jeśli **true**, dane przesyłane tooIoT Centrum jest wysyłane w partiach. Jeśli **false**, komunikaty są wysyłane pojedynczo. Domyślnie Hello **false**. Należy pamiętać, że hello **SetBatching** dotyczy tylko protokołu toohello HTTP i nie toohello MQTT lub AMQP protokołów.
* **Limit czasu** (unsigned int) — ta wartość jest reprezentowana w milisekundach. Jeśli wysyła żądanie HTTP lub odebrania odpowiedzi trwa dłużej niż ten czas, a następnie połączenie hello upłynie limit czasu.

Przetwarzanie wsadowe opcja Hello jest ważna. Domyślnie hello zdarzeń ingresses biblioteki indywidualnie (pojedyncze zdarzenie jest niezależnie od przypadku przekazania za**IoTHubClient\_LL\_SendEventAsync**). Jeśli jest przetwarzanie wsadowe opcja hello **true**, biblioteka hello gromadzi zdarzenia tyle jak go z buforu hello (up toohello maksymalny rozmiar wiadomości akceptujące Centrum IoT).  Hello partii zdarzenia są wysyłane tooIoT Centrum w pojedynczym wywołaniu HTTP (hello pojedynczych zdarzeń są połączone w tablicy JSON). Włączanie przetwarzanie wsadowe zwykle powoduje duża wydajność, ponieważ jest zmniejszenie przechodzenia do sieci. Ponadto znacząco zmniejsza przepustowości od wysyłania jednego zestawu nagłówków HTTP z partii zdarzeń, a nie zestaw nagłówki dla każdego wybranego zdarzenia. Jeśli nie masz toodo powód inaczej, zazwyczaj należy tooenable przetwarzanie wsadowe.

## <a name="next-steps"></a>Następne kroki
W tym artykule opisano w zachowaniu hello szczegółów hello **IoTHubClient** Biblioteka odnaleziona w hello **urządzenia Azure IoT SDK dla języka C**. Dzięki tym informacjom powinien dysponować dobrą znajomością hello funkcji hello **IoTHubClient** biblioteki. Witaj [kolejnym artykule](iot-hub-device-sdk-c-serializer.md) zawiera szczegółowe informacje podobne na powitania **serializator** biblioteki.

toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz hello [Azure IoT SDK][lnk-sdks].

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
