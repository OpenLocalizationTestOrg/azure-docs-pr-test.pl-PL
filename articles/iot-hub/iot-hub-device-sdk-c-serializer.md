---
title: "urządzenia IoT aaaAzure zestawu SDK dla języka C - serializator | Dokumentacja firmy Microsoft"
description: "Jak toouse hello serializator biblioteki hello Azure IoT urządzenia zestawu SDK dla aplikacji dla urządzeń toocreate C komunikujących się z Centrum IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>Azure IoT urządzenia zestawu SDK dla języka C — więcej informacji na temat serializator
Witaj [najpierw artykuł](iot-hub-device-sdk-c-intro.md) w tej serii wprowadzone hello **urządzenia Azure IoT SDK dla języka C**. kolejnym artykule hello podane bardziej szczegółowy opis hello [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md). W tym artykule zakończeniu pokrycia hello zestawu SDK przez zapewnienie bardziej szczegółowy opis pozostałych składników hello: hello **serializator** biblioteki.

Artykuł wprowadzające Hello opisano sposób toouse hello **serializator** biblioteki toosend zdarzenia tooand odbierać komunikaty z Centrum IoT. W tym artykule rozbudowujemy tej dyskusji, zapewniając bardziej szczegółowy opis toomodel danych za pomocą hello **serializator** makra języka. Artykuł Hello zawiera także szczegółowe informacje o jak biblioteki hello serializuje wiadomości (i w niektórych przypadkach, jak można kontrolować zachowanie serializacji hello). Opiszemy także niektóre parametry, które można modyfikować określające rozmiar hello modeli hello, którą utworzysz.

Na koniec artykułu hello revisits niektóre tematy omówione w poprzednich artykułach, takie jak wiadomości i Obsługa właściwości. Jak możemy się dowiedzieć, te funkcje pracy w hello sam, jak za pomocą hello **serializator** biblioteki co z hello **IoTHubClient** biblioteki.

Wszystkie elementy opisane w tym artykule jest oparta na powitania **serializator** przykłady zestawu SDK. Jeśli chcesz toofollow wzdłuż, zobacz hello **simplesample\_protokołu amqp** i **simplesample\_http** aplikacje zawarte w hello urządzenia Azure IoT SDK dla C.

Można znaleźć hello [ **urządzenia Azure IoT SDK dla języka C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repozytorium i Wyświetl szczegóły hello interfejsu API w hello [dokumentacja interfejsu API C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-modeling-language"></a>Język modelowania Hello
Witaj [wprowadzające artykułu](iot-hub-device-sdk-c-intro.md) w tej serii wprowadzone hello **urządzenia Azure IoT SDK dla języka C** modeling language za pośrednictwem przykład Witaj w hello **simplesample\_protokołu amqp**  aplikacji:

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Jak widać, hello język modelowania jest oparta na makr C. Zawsze należy zacząć definicja z **BEGIN\_przestrzeni nazw** i zawsze kończyć **zakończenia\_przestrzeni nazw**. Jest wspólnej tooname hello przestrzeni nazw w firmie lub, jak w poniższym przykładzie hello projektu, który pracuje.

Co jest umieszczane w obszarze nazw hello są definicje modelu. W takim przypadku jest pojedynczego modelu dla anemometer. Jeszcze raz hello modelu może mieć nazwę niczego, ale zazwyczaj jest to urządzenie hello lub typu danych ma zostać tooexchange z Centrum IoT.  

Modele zawiera definicji zdarzeń hello można tooIoT wejściowych koncentratora (hello *danych*) oraz wiadomości powitania może odbierać z Centrum IoT (hello *akcje*). Jak widać na przykład Witaj, zdarzenia mają typem i nazwą; Akcje mieć nazwę i następujące parametry opcjonalne (każde z nich typu).

Co nie jest prezentowana w tym przykładzie są dodatkowe typy danych obsługiwane przez hello zestawu SDK. Firma Microsoft będzie obejmować tego dalej.

> [!NOTE]
> Centrum IoT odwołuje się toohello dane urządzenie wysyła tooit jako *zdarzenia*, podczas gdy hello język modelowania odwołuje się tooit jako *danych* (zdefiniowany przy użyciu **WITH_DATA**). Podobnie, Centrum IoT odwołuje się wysłać toodevices jako dane toohello *wiadomości*, podczas gdy hello język modelowania odwołuje się tooit jako *akcje* (zdefiniowany przy użyciu **WITH_ACTION**). Należy pamiętać, że te terminy mogą używane zamiennie w tym artykule.
> 
> 

### <a name="supported-data-types"></a>Obsługiwane typy danych
Witaj następujące typy danych są obsługiwane w modelach utworzone za pomocą hello **serializator** biblioteki:

| Typ | Opis |
| --- | --- |
| O podwójnej precyzji |Podwójna precyzja liczba zmiennoprzecinkowa |
| int |32-bitowa liczba całkowita |
| Float |Liczba zmiennoprzecinkowa pojedynczej precyzji |
| długa |długich liczb całkowitych |
| int8\_t |8-bitową liczbą całkowitą |
| Int16\_t |16-bitową liczbę całkowitą |
| Int32\_t |32-bitowa liczba całkowita |
| Int64\_t |64-bitowa liczba całkowita |
| wartość logiczna |Wartość logiczna |
| ASCII\_char\_ptr |Ciąg ASCII |
| EDM\_DATA\_CZASU\_PRZESUNIĘCIA |Przesunięcie czasu daty |
| EDM\_IDENTYFIKATOR GUID |IDENTYFIKATOR GUID |
| EDM\_BINARNE |Binarne |
| DEKLAROWANIE\_— STRUKTURA |Typ danych złożonych |

Zacznijmy od ostatniego hello — typ danych. Witaj **DECLARE\_struktury** pozwala toodefine złożone typy danych, które są grupami hello innych typów pierwotnych. Te grupy zezwolić nam toodefine modelu, który wygląda następująco:

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

Nasz model zawiera zdarzenie danych jednego typu **elementu TestType**. **Element TestType** jest typem złożonym, który zawiera kilka elementów członkowskich, zbiorczo potwierdzające, typy pierwotne hello obsługiwane przez hello **serializator** język modelowania.

Z modelem podobny do tego firma Microsoft można napisać kod toosend danych tooIoT koncentratora, który wygląda następująco:

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

Zasadniczo jest przypisywanie wartości tooevery członkiem hello **testu** struktury i wywołując **SendAsync** toosend hello **testu** toohello zdarzeń danych w chmurze. **SendAsync** funkcji pomocnika, która wysyła tooIoT zdarzeń danych jednego koncentratora jest:

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

Ta funkcja wykonuje serializację hello dane zdarzenie danych i wysyła je z tooIoT koncentratora za pomocą **IoTHubClient\_SendEventAsync**. Jest to hello tego samego kodu omówione w poprzednich artykułach (**SendAsync** hermetyzuje hello logiki do funkcji wygodny).

Jeden innych funkcji pomocnika używany w poprzednim kodzie hello jest **GetDateTimeOffset**. Ta funkcja przekształca hello podany czas na wartość typu **EDM\_data\_czasu\_PRZESUNIĘCIA**:

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

Po uruchomieniu tego kodu po wiadomość hello są wysyłane tooIoT Centrum:

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

Należy pamiętać, że hello serializacji JSON, który jest generowany przez hello format hello **serializator** biblioteki. Należy pamiętać, że każdy element członkowski hello serializowany obiekt JSON zgodny hello członkami hello **elementu TestType** zdefiniowanego w modelu. wartości Hello również dokładnie odpowiadać używanych w kodzie hello. Jednak należy pamiętać, że dane binarne hello algorytmem Base64: "AQID" jest hello kodowanie base64 {0x01, 0x02, 0x03}.

W tym przykładzie pokazano hello zaletą hello **serializator** biblioteki — umożliwia nam toosend JSON toohello chmury, bez konieczności tooexplicitly postępowania w przypadku serializacji w naszej aplikacji. Wszystko, co mamy tooworry o jest ustawienie wartości hello hello zdarzeń danych w modelu, a następnie wywołując prostych interfejsów API toosend chmury toohello tych zdarzeń.

Dzięki tym informacjom można definiujemy modeli, które obejmują zakres hello obsługiwane typy danych, łącznie z typów złożonych (Firma Microsoft może nawet obejmują typy złożone w ramach innych typów złożonych). Jednak on serializacji JSON generowane przez hello w powyższym przykładzie wywołuje punkt ważne. *Jak* wyślemy danych za pomocą hello **serializator** biblioteki określa dokładnie sposób powstaje hello JSON. Czy konkretnej jest co omówione zostaną następujące czynności dalej.

## <a name="more-about-serialization"></a>Więcej informacji na temat serializacji
Hello poprzedniej sekcji przedstawiono przykład hello danych wyjściowych wygenerowanych przez hello **serializator** biblioteki. W tej sekcji wyjaśniamy sposób biblioteki hello serializuje dane i metody kontrolowania tego zachowania, za pomocą serializacji hello interfejsów API.

W kolejności omówione hello tooadvance szeregowanie firma Microsoft będzie współpracować z nowy model oparty na termostacie. Po pierwsze możemy podać niektóre tła na scenariusz hello próbujemy tooaddress.

Chcemy toomodel termostat, która temperatury i wilgotności. Każda część danych będzie toobe inaczej wysyłane tooIoT koncentratora. Domyślnie program hello ingresses termostat zdarzeń temperatury raz na 2 minuty; Zdarzenie wilgotności jest ingressed co 15 minut. Po ingressed obu zdarzeń, musi on zawierać sygnaturę przedstawia czas hello tego temperatury odpowiedniego hello lub zmierzono wilgotność.

Podana w tym scenariuszu, zostanie przedstawiony dwa różne sposoby toomodel hello danych i wyjaśniamy efekt hello czy modelowania ma na powitania serializować danych wyjściowych.

### <a name="model-1"></a>Model 1
Oto hello pierwszej wersji modelu czy obsługuje hello poprzednim scenariuszu:

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

Uwaga modelu hello obejmuje dwa dane zdarzenia: **temperatury** i **wilgotności**. W przeciwieństwie do poprzednich przykładach, typ hello każdego zdarzenia jest strukturą zdefiniowane przy użyciu **DECLARE\_struktury**. **TemperatureEvent** zawiera miary temperatury i sygnaturę czasową; **HumidityEvent** zawiera miary wilgoć i sygnaturę czasową. Ten model daje danych hello toomodel naturalny sposób scenariusz hello opisany powyżej. Gdy mamy wysłać zdarzenie toohello chmury, albo wyślemy temperatury/sygnatura czasowa lub pary wilgotności/sygnatura czasowa.

Możemy wysłać temperatury chmury toohello zdarzeń przy użyciu kodu, takie jak następujące hello:

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Firma Microsoft będzie używać zakodowanych wartości temperatury i wilgotności w hello przykładowy kod, ale Wyobraź sobie możemy poprzez próbkowanie czujników odpowiedniego hello na powitania termostat faktycznie jest pobierania tych wartości.

Powyższy kod Hello używa hello **GetDateTimeOffset** pomocnika, który został wprowadzony wcześniej. Przyczyn, które będzie wyczyść nowsze ten kod jawnie oddziela zadania hello serializacji i wysyłania zdarzeń hello. Poprzedni kod Hello serializuje hello temperatury zdarzeń do buforu. Następnie **sendMessage** jest funkcją pomocnika (zawarte w **simplesample\_amqp**) czy wysyła hello tooIoT zdarzeń Centrum:

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

Ten kod jest podzbiorem hello **SendAsync** pomocnika opisanego w poprzedniej sekcji hello, dlatego firma Microsoft nie będą przekazywane go ponownie w tym miejscu.

Uruchomienie hello poprzedniego kodu toosend hello temperatury zdarzenia, ta forma serializacji hello zdarzenia są wysyłane tooIoT Centrum:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Została wysłana temperatury, który jest typu **TemperatureEvent** i zawiera tej struktury **temperatury** i **czasu** elementu członkowskiego. Znajduje to odzwierciedlenie bezpośrednio w danych serializacji hello.

Podobnie możemy wysłać zdarzenie wilgotności o tym kodzie:

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Formularz Hello serializacji, który wysłał tooIoT Centrum wygląda następująco:

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Jest to ponownie, zgodnie z oczekiwaniami.

Z tym modelem, w pewnym sensie jak dodatkowe zdarzenia można łatwo dodać. Zdefiniuj więcej struktur za pomocą **DECLARE\_struktury**i dołączyć odpowiednie zdarzenie hello hello model przy użyciu **WITH\_danych**.

Teraz zmodyfikujmy hello modelu co zawierają one hello tych samych danych, lecz z inną strukturę.

### <a name="model-2"></a>Modelu 2
Należy wziąć pod uwagę toohello ten model alternatywny, jeden powyżej:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

W takim przypadku został wyeliminowany hello **DECLARE\_struktury** makra i po prostu definiowania elementów danych hello w naszym scenariuszu przy użyciu proste typy z hello język modelowania.

Tylko dla obecnie hello umożliwia ignorowanie hello **czasu** zdarzeń. Z tym Zarezerwuj Oto hello kodu tooingress **temperatury**:

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Ten kod wysyła następujące hello serializacji tooIoT zdarzeń Centrum:

```
{"Temperature":75}
```

I hello kod umożliwiający wysyłanie zdarzeń wilgotności hello wygląda następująco:

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Ten kod wysyła ten tooIoT Centrum:

```
{"Humidity":45}
```

Do tej pory nie ma jeszcze nie niespodzianki. Teraz Zmieńmy wykorzystanie hello SERIALIZACJA makra.

Witaj **SERIALIZACJA** makro może zająć wiele zdarzeń danych jako argumenty. Dzięki temu nam tooserialize hello **temperatury** i **wilgotności** zdarzeń razem i wysyłać je tooIoT Centrum w jednym wywołaniu:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Może się odgadnąć, czy wynik hello ten kod jest czy dwóch danych zdarzenia są wysyłane tooIoT Centrum:

[

{"Temperatury": 75},

{"Wilgotności": 45}

]

Innymi słowy, może spodziewać, że ten kod jest hello takie same jak wysyłanie **temperatury** i **wilgotności** oddzielnie. Jest po prostu toopass wygody obu zdarzeń zbyt**SERIALIZACJA** hello sam wywołać. Jednakże, który nie jest hello. Zamiast tego powyższym kodzie hello wysyła ten tooIoT zdarzeń danych jednego koncentratora:

{"Temperatury": 75, "wilgotności": 45}

Może to wyglądać dziwne, ponieważ definiuje nasz model **temperatury** i **wilgotności** jako dwa *oddzielnych* zdarzenia:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Jeden punkt toohello, firma Microsoft nie modelu te zdarzenia gdzie **temperatury** i **wilgotności** w hello tej samej struktury:

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

Użycie tego modelu, będzie łatwiejszy toounderstand jak **temperatury** i **wilgotności** wysłania w hello sam serializacji komunikatów. Jednak nie może być wyczyść Dlaczego działa w ten sposób zbyt przekazać obu zdarzeń danych**SERIALIZACJA** przy użyciu modelu 2.

To zachowanie jest łatwiejsze toounderstand, jeśli znasz założenia hello tego hello **serializator** biblioteki jest wprowadzenie. toomake rozumieniu to przejdź wstecz tooour modelu:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

W kategoriach zorientowane obiektowo należy traktować tego modelu. W takim przypadku jest modelowanie urządzenie fizyczne (termostacie) i urządzenia zawiera atrybutów, takich jak **temperatury** i **wilgotności**.

Możemy wysłać hello cały stan modelu z kodem, takie jak następujące hello:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Zakładając, że wartości hello temperatury i wilgotności czasu są ustawiane, czy widzimy zdarzenia, takiego jak to wysłane tooIoT Centrum:

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Czasami może być tylko toosend *niektórych* właściwości chmury toohello modelu hello (jest to szczególnie istotne, jeśli model zawiera wiele zdarzeń danych). W naszym przykładzie wcześniejszych jest przydatne toosend tylko podzestaw danych dotyczących zdarzeń, takich jak:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Spowoduje to wygenerowanie dokładnie hello sam serializacji zdarzeń tak, jakby była zdefiniowanego **TemperatureEvent** z **temperatury** i **czas** — członek, tak samo jak z możemy modelu 1. W takim przypadku możemy stanie toogenerate dokładnie hello sam serializacji zdarzeń za pomocą inny model (model 2), ponieważ dzwoniliśmy **SERIALIZACJA** w inny sposób.

Witaj ważnym jest to, że w przypadku przekazania zbyt wiele zdarzeń danych**SERIALIZACJA,** , a następnie przyjęto założenie, że każde wydarzenie jest właściwością w pojedynczy obiekt JSON.

najlepszym rozwiązaniem Hello zależy od tego, i jak myślisz na temat modelu. Jeśli wysyłasz "zdarzenia" chmury toohello i każde zdarzenie zawiera określony zbiór właściwości, hello pierwszego podejścia umożliwia dużo znaczeniu. W takim przypadku należy użyć **DECLARE\_struktury** toodefine hello strukturę każdego zdarzenia i dołącz je do modelu z hello **WITH\_danych** makra. Następnie możesz wysłać każde zdarzenie, jak robiliśmy w powyższym przykładzie pierwsze hello. W tej metody można tylko przejdzie zdarzeń danych jednego zbyt**SERIALIZATOR**.

Jeśli myślisz o modelu w sposób zorientowane obiektowo, hello drugiej metody może własnych użytkownik. W takim przypadku hello elementy zdefiniowane przy użyciu **WITH\_danych** są hello "właściwości" obiektu. Przekaż niezależnie od podzbioru zdarzeń za**SERIALIZACJA** czy chcesz, w zależności od ilości stanu użytkownika "obiektu" ma toosend toohello chmury.

Nether podejście jest nieprawidłowy lub w prawo. Po prostu należy wiedzieć, jak hello **serializator** biblioteki działa prawidłowo, a metoda modelowania hello pobranie, która najlepiej odpowiada Twoim potrzebom.

## <a name="message-handling"></a>Komunikat — Obsługa
Do tej pory w tym artykule tylko został omówiony wysyłania zdarzeń tooIoT Centrum i nie adresowane odbierania wiadomości. Witaj Przyczyna dla to jest potrzebny tooknow o odbieranie komunikatów przede wszystkim zostały objęte [wcześniej artykuł](iot-hub-device-sdk-c-intro.md). Z tego artykułu przypominają przetwarzania komunikatów przez zarejestrowanie funkcję wywołania zwrotnego komunikat:

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

Następnie napiszesz hello funkcja wywołania zwrotnego, które jest wywoływane, gdy wiadomość zostanie odebrana:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
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

Ta implementacja **IoTHubMessage** wywołania hello określoną funkcję dla każdego działania w modelu. Na przykład, jeśli model definiuje tej akcji:

```
WITH_ACTION(SetAirResistance, int, Position)
```

Zdefiniuj funkcję z tego podpisu:

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** następnie jest wywoływana, gdy ten komunikat jest wysyłany tooyour urządzenia.

Jeszcze co firma Microsoft nie zostały wyjaśnione jest jakiej wersji prawdopodobnie wiadomość hello serializacji. Innymi słowy Jeśli chcesz, aby toosend **SetAirResistance** komunikat tooyour urządzenia, jak wygląda ten?

Przy wysyłaniu wiadomości tooa urządzenia, czy tym za pośrednictwem usługi Azure IoT hello zestawu SDK. Nadal potrzebujesz tooknow co ciągu toosend tooinvoke określonej akcji. ogólny format Hello wysyłanie wiadomości wygląda następująco:

```
{"Name" : "", "Parameters" : "" }
```

Wysyłasz Zserializowany obiekt JSON z dwóch właściwości: **nazwa** jest nazwą hello hello akcji (komunikat) i **parametry** zawiera parametry hello działania.

Na przykład tooinvoke **SetAirResistance** można wysłać tego komunikatu tooa urządzenia:

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

Nazwa akcji Hello musi dokładnie odpowiadać akcji zdefiniowanych w modelu. nazwy parametrów Hello musi być również zgodna. Należy również zauważyć uwzględniana wielkość liter. **Nazwa** i **parametrów** są zawsze wielkimi literami. Upewnij się, że przypadku hello toomatch nazwy akcji i parametrów w modelu. W tym przykładzie nazwa akcji hello jest "SetAirResistance", a nie "setairresistance".

Witaj dwie inne akcje **TurnFanOn** i **TurnFanOff** może być wywoływany przez wysyłanie tych wiadomości tooa urządzenia:

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

W tej sekcji opisano wszystkie elementy potrzebne tooknow podczas wysyłania zdarzeń i odbierania wiadomości z hello **serializator** biblioteki. Przed kontynuowaniem, teraz obejmuje niektóre parametry, które można skonfigurować określające, jak duże jest modelu.

## <a name="macro-configuration"></a>Konfiguracja — makro
Jeśli używasz hello **serializator** biblioteki ważnym elementem toobe SDK hello świadomość znajduje się w hello azure-c udostępnione — Biblioteka narzędzi.
Jeśli zostały sklonowane repozytorium hello Azure-iot-sdk-c z serwisu GitHub, za pomocą opcji--cykliczne hello, będą dostępne w tej biblioteki jako narzędzia udostępnione:

```
.\\c-utility
```

Jeśli nie zostały sklonowane hello biblioteki, możesz go znaleźć [tutaj](https://github.com/Azure/azure-c-shared-utility).

W bibliotece jako narzędzia udostępnione hello można znaleźć hello następującego folderu:

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

Ten folder zawiera rozwiązania Visual Studio o nazwie **makro\_witryny\_h\_generator.sln**:

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

program Hello w tym rozwiązaniu generuje hello **makro\_utils.h** pliku. Brak domyślne makro\_pliku utils.h hello zestawu SDK. To rozwiązanie umożliwia toomodify niektórych parametrów i następnie ponownie utwórz hello pliku nagłówka, na podstawie tych parametrów.

są Hello dwóch parametrów klucza toobe zajęto się **nArithmetic** i **nMacroParameters** które zostały określone w tych dwóch wierszach znaleziono w makrze\_utils.tt:

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

Te wartości są parametry domyślne hello dołączonego hello zestawu SDK. Każdy parametr ma hello następujące znaczenie:

* nMacroParameters — Określa, ile parametrów mogą mieć w jednej instrukcji DECLARE\_definicji makra w modelu.
* nArithmetic — formanty hello łączna liczba elementów członkowskich dozwolone w modelu.

przyczyny Hello te parametry są ważne jest, ponieważ decydować, jak duży może być modelu. Rozważmy na przykład tej definicji modelu:

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

Jak wspomniano wcześniej, **DECLARE\_modelu** jest po prostu makr C. Witaj nazwy modelu hello i hello **WITH\_danych** instrukcji (jeszcze innego makra) czy parametry **DECLARE\_modelu**. **nMacroParameters** definiuje, ile parametry mogą być zawarte w **DECLARE\_modelu**. W rezultacie definiuje liczbę zdarzeń i akcji deklaracjach danych może mieć. W związku z hello domyślny limit 124 oznacza to, zdefiniować modelu z kombinacją akcji około 60 i danych dotyczących zdarzeń. Jeśli spróbujesz tooexceed ten limit, otrzymasz błędów, które wyglądają toothis podobne:

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

Witaj **nArithmetic** parametr jest więcej informacji na temat hello wewnętrzne działanie hello makra języka niż aplikacja.  Kontroluje hello łączna liczba elementów członkowskich w modelu, mogą znajdować się w tym **DECLARE_STRUCT** makra. Jeśli możesz zacząć się wyświetlać błędy kompilatora, takich jak ta, a następnie spróbuj użyć zwiększenie **nArithmetic**:

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

Toochange tych parametrów, zmodyfikuj wartości hello w makrze hello\_utils.tt plik, skompiluj ponownie hello makro\_witryny\_h\_generator.sln rozwiązania i skompilowany program hello wykonywania. Się nowe makro\_utils.h plik jest generowany i umieszczane w hello.\\ Typowe\\inc katalogu.

W nowej wersji hello toouse kolejności makra\_utils.h, Usuń hello **serializator** pakietu NuGet z rozwiązania i w tym miejscu zawierają hello **serializator** projekt programu Visual Studio. Dzięki temu toocompile Twojego kodu na kod źródłowy hello hello serializator biblioteki. Obejmuje to makro hello zaktualizowane\_utils.h. Jeśli chcesz toodo to dla **simplesample\_amqp**, uruchom przez usunięcie pakietu NuGet hello hello serializator biblioteki z rozwiązania hello:

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

Następnie dodaj ten tooyour projektu rozwiązania Visual Studio:

> . \\c\\serializator\\kompilacji\\windows\\serializer.vcxproj
> 
> 

Gdy wszystko będzie gotowe rozwiązanie powinien wyglądać następująco:

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

Teraz podczas kompilowania rozwiązania, hello zaktualizowane makro\_utils.h znajduje się w sieci danych binarnych.

Należy pamiętać, że zwiększenie wartości wystarczająco wysoka, może być dłuższa niż limity kompilatora. toothis punktu hello **nMacroParameters** hello parametr głównego o które toobe danych. Specyfikacja C99 Hello Określa, czy co najmniej 127 parametrów są dozwolone w definicji makra. Hello kompilatorem następuje hello specyfikację dokładnie (i ma limit 127), więc nie będzie możliwe tooincrease **nMacroParameters** ponad hello domyślną. Inne kompilatory może umożliwić toodo tak (na przykład kompilatora GNU hello obsługuje wyższy limit).

Do tej pory możemy zostały objęte prawie wszystkie elementy potrzebne tooknow o jak toowrite kodu z hello **serializator** biblioteki. Przed zawierania, możemy ponownie niektóre tematy z poprzednich artykułów, które możesz się zastanawiać, informacje.

## <a name="hello-lower-level-apis"></a>Witaj interfejsów API niższego poziomu
Witaj przykładowej aplikacji, na którym fokus w tym artykule jest **simplesample\_amqp**. W tym przykładzie używa hello wyższego poziomu (hello z systemem innym niż — "wszystko") interfejsów API toosend zdarzeń i odbierania wiadomości. Korzystając z poniższych interfejsów API, uruchamia wątku w tle, który zajmuje się zarówno zdarzenia wysyłania i odbierania wiadomości. Można jednak użyć hello niższego poziomu (wszystkie) interfejsów API tooeliminate wątku w tle i kontrolować jawne przez wysłanie zdarzenia lub odbieranie komunikatów z hello chmury.

Zgodnie z opisem w [poprzednim artykule](iot-hub-device-sdk-c-iothubclient.md), istnieje zestaw funkcji, która składa się z hello wyższego poziomu interfejsów API:

* IoTHubClient\_CreateFromConnectionString
* IoTHubClient\_SendEventAsync
* IoTHubClient\_SetMessageCallback
* IoTHubClient\_zniszczyć

Te interfejsy API przedstawiono w części **simplesample\_amqp**.

Istnieje również analogiczne zestaw interfejsów API niższego poziomu.

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_zniszczyć

Należy pamiętać, że pracy interfejsów API niższego poziomu hello dokładnie hello sam sposób, jak opisano w poprzednich artykułach hello. Jeśli chcesz, aby wątku tła w toohandle zdarzenia wysyłania i odbierania wiadomości, można użyć hello pierwszy zestaw interfejsów API. Możesz użyć hello drugi zestaw interfejsów API jawną kontrolę nad podczas wysyłania i odbierania danych z Centrum IoT. Albo zestaw interfejsów API pracy oraz jednakowo z hello **serializator** biblioteki.

Na przykład jak hello interfejsów API niższego poziomu są używane z hello **serializator** biblioteki, zobacz hello **simplesample\_http** aplikacji.

## <a name="additional-topics"></a>Tematy dodatkowe
Kilka innych tematów, warto zauważyć, są ponownie właściwości obsługi, przy użyciu poświadczeń alternatywnych urządzenia i opcje konfiguracji. Są to wszystkie tematy objęte [poprzednim artykule](iot-hub-device-sdk-c-iothubclient.md). Hello główny punkt jest czy wszystkie te funkcje działają w hello sam sposób z hello **serializator** biblioteki co z hello **IoTHubClient** biblioteki. Na przykład, jeśli chcesz tooattach właściwości tooan zdarzeń z modelu, używasz **IoTHubMessage\_właściwości** i **mapy**\_**AddorUpdate**, hello sam sposób, jak opisano wcześniej:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Określa, czy zdarzenie hello został wygenerowany na podstawie hello **serializator** biblioteki lub utworzone ręcznie za pomocą hello **IoTHubClient** biblioteki nie ma znaczenia.

Alternatywne poświadczenia urządzenia, za pomocą funkcji dla hello **IoTHubClient\_LL\_Utwórz** równie dobrze działa jako **IoTHubClient\_CreateFromConnectionString** dla przydzielanie **Centrum IOTHUB\_klienta\_obsługi**.

Ponadto jeśli używasz hello **serializator** biblioteki, można ustawić opcji konfiguracji z **IoTHubClient\_LL\_SetOption** podobnie jak w przypadku przy użyciu hello **IoTHubClient** biblioteki.

Funkcja, która jest unikatowa toohello **serializator** biblioteki są hello inicjowania interfejsów API. Przed rozpoczęciem pracy z biblioteki hello należy wywołać **serializator\_init**:

```
serializer_init(NULL);
```

Jest to realizowane tylko przed wywołaniem **IoTHubClient\_CreateFromConnectionString**.

Podobnie, po zakończeniu pracy z biblioteki hello, ostatnim wywołaniu hello należy podjąć jest zbyt**serializator\_deinit**:

```
serializer_deinit();
```

W przeciwnym razie hello wszystkie inne funkcje wymienione powyżej pracy hello sam hello **serializator** biblioteki tak jak w hello **IoTHubClient** biblioteki. Aby uzyskać więcej informacji o tych tematów, zobacz hello [poprzednim artykule](iot-hub-device-sdk-c-iothubclient.md) w tej serii.

## <a name="next-steps"></a>Następne kroki
W tym artykule opisano szczegółowo hello unikatowe aspekty hello **serializator** biblioteki zawarte w hello **urządzenia Azure IoT SDK dla języka C**. Z informacjami hello należy dysponować dobrą znajomością o jak toouse modele toosend zdarzenia i odbierać komunikaty z Centrum IoT.

Teraz również hello trzyczęściowej serii na jak hello toodevelop aplikacji za pomocą **urządzenia Azure IoT SDK dla języka C**. To powinien być wystarczającej ilości informacji toonot tylko get, uruchamiany, ale także zapewniają dokładne zrozumienie działania hello interfejsów API. Aby uzyskać dodatkowe informacje obejmuje kilka przykładów powitalne zestawu SDK nie pasuje do tutaj. W przeciwnym razie hello [dokumentacji zestawu SDK](https://github.com/Azure/azure-iot-sdk-c) jest dobrym zasobów, aby uzyskać dodatkowe informacje.

toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz hello [Azure IoT SDK][lnk-sdks].

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
