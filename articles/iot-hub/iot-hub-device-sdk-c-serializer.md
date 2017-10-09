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
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="e76d1-103">Azure IoT urządzenia zestawu SDK dla języka C — więcej informacji na temat serializator</span><span class="sxs-lookup"><span data-stu-id="e76d1-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="e76d1-104">Witaj [najpierw artykuł](iot-hub-device-sdk-c-intro.md) w tej serii wprowadzone hello **urządzenia Azure IoT SDK dla języka C**. kolejnym artykule hello podane bardziej szczegółowy opis hello [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="e76d1-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. hello next article provided a more detailed description of hello [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="e76d1-105">W tym artykule zakończeniu pokrycia hello zestawu SDK przez zapewnienie bardziej szczegółowy opis pozostałych składników hello: hello **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-105">This article completes coverage of hello SDK by providing a more detailed description of hello remaining component: hello **serializer** library.</span></span>

<span data-ttu-id="e76d1-106">Artykuł wprowadzające Hello opisano sposób toouse hello **serializator** biblioteki toosend zdarzenia tooand odbierać komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e76d1-106">hello introductory article described how toouse hello **serializer** library toosend events tooand receive messages from IoT Hub.</span></span> <span data-ttu-id="e76d1-107">W tym artykule rozbudowujemy tej dyskusji, zapewniając bardziej szczegółowy opis toomodel danych za pomocą hello **serializator** makra języka.</span><span class="sxs-lookup"><span data-stu-id="e76d1-107">In this article, we extend that discussion by providing a more complete explanation of how toomodel your data with hello **serializer** macro language.</span></span> <span data-ttu-id="e76d1-108">Artykuł Hello zawiera także szczegółowe informacje o jak biblioteki hello serializuje wiadomości (i w niektórych przypadkach, jak można kontrolować zachowanie serializacji hello).</span><span class="sxs-lookup"><span data-stu-id="e76d1-108">hello article also includes more detail about how hello library serializes messages (and in some cases how you can control hello serialization behavior).</span></span> <span data-ttu-id="e76d1-109">Opiszemy także niektóre parametry, które można modyfikować określające rozmiar hello modeli hello, którą utworzysz.</span><span class="sxs-lookup"><span data-stu-id="e76d1-109">We'll also describe some parameters you can modify that determine hello size of hello models you create.</span></span>

<span data-ttu-id="e76d1-110">Na koniec artykułu hello revisits niektóre tematy omówione w poprzednich artykułach, takie jak wiadomości i Obsługa właściwości.</span><span class="sxs-lookup"><span data-stu-id="e76d1-110">Finally, hello article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="e76d1-111">Jak możemy się dowiedzieć, te funkcje pracy w hello sam, jak za pomocą hello **serializator** biblioteki co z hello **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-111">As we'll find out, those features work in hello same way using hello **serializer** library as they do with hello **IoTHubClient** library.</span></span>

<span data-ttu-id="e76d1-112">Wszystkie elementy opisane w tym artykule jest oparta na powitania **serializator** przykłady zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="e76d1-112">Everything described in this article is based on hello **serializer** SDK samples.</span></span> <span data-ttu-id="e76d1-113">Jeśli chcesz toofollow wzdłuż, zobacz hello **simplesample\_protokołu amqp** i **simplesample\_http** aplikacje zawarte w hello urządzenia Azure IoT SDK dla C.</span><span class="sxs-lookup"><span data-stu-id="e76d1-113">If you want toofollow along, see hello **simplesample\_amqp** and **simplesample\_http** applications included in hello Azure IoT device SDK for C.</span></span>

<span data-ttu-id="e76d1-114">Można znaleźć hello [ **urządzenia Azure IoT SDK dla języka C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repozytorium i Wyświetl szczegóły hello interfejsu API w hello [dokumentacja interfejsu API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="e76d1-114">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-modeling-language"></a><span data-ttu-id="e76d1-115">Język modelowania Hello</span><span class="sxs-lookup"><span data-stu-id="e76d1-115">hello modeling language</span></span>
<span data-ttu-id="e76d1-116">Witaj [wprowadzające artykułu](iot-hub-device-sdk-c-intro.md) w tej serii wprowadzone hello **urządzenia Azure IoT SDK dla języka C** modeling language za pośrednictwem przykład Witaj w hello **simplesample\_protokołu amqp**  aplikacji:</span><span class="sxs-lookup"><span data-stu-id="e76d1-116">hello [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C** modeling language through hello example provided in hello **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="e76d1-117">Jak widać, hello język modelowania jest oparta na makr C.</span><span class="sxs-lookup"><span data-stu-id="e76d1-117">As you can see, hello modeling language is based on C macros.</span></span> <span data-ttu-id="e76d1-118">Zawsze należy zacząć definicja z **BEGIN\_przestrzeni nazw** i zawsze kończyć **zakończenia\_przestrzeni nazw**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="e76d1-119">Jest wspólnej tooname hello przestrzeni nazw w firmie lub, jak w poniższym przykładzie hello projektu, który pracuje.</span><span class="sxs-lookup"><span data-stu-id="e76d1-119">It's common tooname hello namespace for your company or, as in this example, hello project that you're working on.</span></span>

<span data-ttu-id="e76d1-120">Co jest umieszczane w obszarze nazw hello są definicje modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-120">What goes inside hello namespace are model definitions.</span></span> <span data-ttu-id="e76d1-121">W takim przypadku jest pojedynczego modelu dla anemometer.</span><span class="sxs-lookup"><span data-stu-id="e76d1-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="e76d1-122">Jeszcze raz hello modelu może mieć nazwę niczego, ale zazwyczaj jest to urządzenie hello lub typu danych ma zostać tooexchange z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e76d1-122">Once again, hello model can be named anything, but typically this is named for hello device or type of data you want tooexchange with IoT Hub.</span></span>  

<span data-ttu-id="e76d1-123">Modele zawiera definicji zdarzeń hello można tooIoT wejściowych koncentratora (hello *danych*) oraz wiadomości powitania może odbierać z Centrum IoT (hello *akcje*).</span><span class="sxs-lookup"><span data-stu-id="e76d1-123">Models contain a definition of hello events you can ingress tooIoT Hub (hello *data*) as well as hello messages you can receive from IoT Hub (hello *actions*).</span></span> <span data-ttu-id="e76d1-124">Jak widać na przykład Witaj, zdarzenia mają typem i nazwą; Akcje mieć nazwę i następujące parametry opcjonalne (każde z nich typu).</span><span class="sxs-lookup"><span data-stu-id="e76d1-124">As you can see from hello example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="e76d1-125">Co nie jest prezentowana w tym przykładzie są dodatkowe typy danych obsługiwane przez hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="e76d1-125">What’s not demonstrated in this sample are additional data types that are supported by hello SDK.</span></span> <span data-ttu-id="e76d1-126">Firma Microsoft będzie obejmować tego dalej.</span><span class="sxs-lookup"><span data-stu-id="e76d1-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="e76d1-127">Centrum IoT odwołuje się toohello dane urządzenie wysyła tooit jako *zdarzenia*, podczas gdy hello język modelowania odwołuje się tooit jako *danych* (zdefiniowany przy użyciu **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="e76d1-127">IoT Hub refers toohello data a device sends tooit as *events*, while hello modeling language refers tooit as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="e76d1-128">Podobnie, Centrum IoT odwołuje się wysłać toodevices jako dane toohello *wiadomości*, podczas gdy hello język modelowania odwołuje się tooit jako *akcje* (zdefiniowany przy użyciu **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="e76d1-128">Likewise, IoT Hub refers toohello data you send toodevices as *messages*, while hello modeling language refers tooit as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="e76d1-129">Należy pamiętać, że te terminy mogą używane zamiennie w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="e76d1-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="e76d1-130">Obsługiwane typy danych</span><span class="sxs-lookup"><span data-stu-id="e76d1-130">Supported data types</span></span>
<span data-ttu-id="e76d1-131">Witaj następujące typy danych są obsługiwane w modelach utworzone za pomocą hello **serializator** biblioteki:</span><span class="sxs-lookup"><span data-stu-id="e76d1-131">hello following data types are supported in models created with hello **serializer** library:</span></span>

| <span data-ttu-id="e76d1-132">Typ</span><span class="sxs-lookup"><span data-stu-id="e76d1-132">Type</span></span> | <span data-ttu-id="e76d1-133">Opis</span><span class="sxs-lookup"><span data-stu-id="e76d1-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e76d1-134">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="e76d1-134">double</span></span> |<span data-ttu-id="e76d1-135">Podwójna precyzja liczba zmiennoprzecinkowa</span><span class="sxs-lookup"><span data-stu-id="e76d1-135">double precision floating point number</span></span> |
| <span data-ttu-id="e76d1-136">int</span><span class="sxs-lookup"><span data-stu-id="e76d1-136">int</span></span> |<span data-ttu-id="e76d1-137">32-bitowa liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="e76d1-137">32 bit integer</span></span> |
| <span data-ttu-id="e76d1-138">Float</span><span class="sxs-lookup"><span data-stu-id="e76d1-138">float</span></span> |<span data-ttu-id="e76d1-139">Liczba zmiennoprzecinkowa pojedynczej precyzji</span><span class="sxs-lookup"><span data-stu-id="e76d1-139">single precision floating point number</span></span> |
| <span data-ttu-id="e76d1-140">długa</span><span class="sxs-lookup"><span data-stu-id="e76d1-140">long</span></span> |<span data-ttu-id="e76d1-141">długich liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="e76d1-141">long integer</span></span> |
| <span data-ttu-id="e76d1-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="e76d1-142">int8\_t</span></span> |<span data-ttu-id="e76d1-143">8-bitową liczbą całkowitą</span><span class="sxs-lookup"><span data-stu-id="e76d1-143">8 bit integer</span></span> |
| <span data-ttu-id="e76d1-144">Int16\_t</span><span class="sxs-lookup"><span data-stu-id="e76d1-144">int16\_t</span></span> |<span data-ttu-id="e76d1-145">16-bitową liczbę całkowitą</span><span class="sxs-lookup"><span data-stu-id="e76d1-145">16 bit integer</span></span> |
| <span data-ttu-id="e76d1-146">Int32\_t</span><span class="sxs-lookup"><span data-stu-id="e76d1-146">int32\_t</span></span> |<span data-ttu-id="e76d1-147">32-bitowa liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="e76d1-147">32 bit integer</span></span> |
| <span data-ttu-id="e76d1-148">Int64\_t</span><span class="sxs-lookup"><span data-stu-id="e76d1-148">int64\_t</span></span> |<span data-ttu-id="e76d1-149">64-bitowa liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="e76d1-149">64 bit integer</span></span> |
| <span data-ttu-id="e76d1-150">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="e76d1-150">bool</span></span> |<span data-ttu-id="e76d1-151">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="e76d1-151">boolean</span></span> |
| <span data-ttu-id="e76d1-152">ASCII\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="e76d1-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="e76d1-153">Ciąg ASCII</span><span class="sxs-lookup"><span data-stu-id="e76d1-153">ASCII string</span></span> |
| <span data-ttu-id="e76d1-154">EDM\_DATA\_CZASU\_PRZESUNIĘCIA</span><span class="sxs-lookup"><span data-stu-id="e76d1-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="e76d1-155">Przesunięcie czasu daty</span><span class="sxs-lookup"><span data-stu-id="e76d1-155">date time offset</span></span> |
| <span data-ttu-id="e76d1-156">EDM\_IDENTYFIKATOR GUID</span><span class="sxs-lookup"><span data-stu-id="e76d1-156">EDM\_GUID</span></span> |<span data-ttu-id="e76d1-157">IDENTYFIKATOR GUID</span><span class="sxs-lookup"><span data-stu-id="e76d1-157">GUID</span></span> |
| <span data-ttu-id="e76d1-158">EDM\_BINARNE</span><span class="sxs-lookup"><span data-stu-id="e76d1-158">EDM\_BINARY</span></span> |<span data-ttu-id="e76d1-159">Binarne</span><span class="sxs-lookup"><span data-stu-id="e76d1-159">binary</span></span> |
| <span data-ttu-id="e76d1-160">DEKLAROWANIE\_— STRUKTURA</span><span class="sxs-lookup"><span data-stu-id="e76d1-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="e76d1-161">Typ danych złożonych</span><span class="sxs-lookup"><span data-stu-id="e76d1-161">complex data type</span></span> |

<span data-ttu-id="e76d1-162">Zacznijmy od ostatniego hello — typ danych.</span><span class="sxs-lookup"><span data-stu-id="e76d1-162">Let’s start with hello last data type.</span></span> <span data-ttu-id="e76d1-163">Witaj **DECLARE\_struktury** pozwala toodefine złożone typy danych, które są grupami hello innych typów pierwotnych.</span><span class="sxs-lookup"><span data-stu-id="e76d1-163">hello **DECLARE\_STRUCT** allows you toodefine complex data types, which are groupings of hello other primitive types.</span></span> <span data-ttu-id="e76d1-164">Te grupy zezwolić nam toodefine modelu, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e76d1-164">These groupings allow us toodefine a model that looks like this:</span></span>

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

<span data-ttu-id="e76d1-165">Nasz model zawiera zdarzenie danych jednego typu **elementu TestType**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="e76d1-166">**Element TestType** jest typem złożonym, który zawiera kilka elementów członkowskich, zbiorczo potwierdzające, typy pierwotne hello obsługiwane przez hello **serializator** język modelowania.</span><span class="sxs-lookup"><span data-stu-id="e76d1-166">**TestType** is a complex type that includes several members, which collectively demonstrate hello primitive types supported by hello **serializer** modeling language.</span></span>

<span data-ttu-id="e76d1-167">Z modelem podobny do tego firma Microsoft można napisać kod toosend danych tooIoT koncentratora, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e76d1-167">With a model like this, we can write code toosend data tooIoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="e76d1-168">Zasadniczo jest przypisywanie wartości tooevery członkiem hello **testu** struktury i wywołując **SendAsync** toosend hello **testu** toohello zdarzeń danych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e76d1-168">Basically, we’re assigning a value tooevery member of hello **Test** structure and then calling **SendAsync** toosend hello **Test** data event toohello cloud.</span></span> <span data-ttu-id="e76d1-169">**SendAsync** funkcji pomocnika, która wysyła tooIoT zdarzeń danych jednego koncentratora jest:</span><span class="sxs-lookup"><span data-stu-id="e76d1-169">**SendAsync** is a helper function that sends a single data event tooIoT Hub:</span></span>

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

<span data-ttu-id="e76d1-170">Ta funkcja wykonuje serializację hello dane zdarzenie danych i wysyła je z tooIoT koncentratora za pomocą **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-170">This function serializes hello given data event and sends it tooIoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="e76d1-171">Jest to hello tego samego kodu omówione w poprzednich artykułach (**SendAsync** hermetyzuje hello logiki do funkcji wygodny).</span><span class="sxs-lookup"><span data-stu-id="e76d1-171">This is hello same code discussed in previous articles (**SendAsync** encapsulates hello logic into a convenient function).</span></span>

<span data-ttu-id="e76d1-172">Jeden innych funkcji pomocnika używany w poprzednim kodzie hello jest **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-172">One other helper function used in hello previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="e76d1-173">Ta funkcja przekształca hello podany czas na wartość typu **EDM\_data\_czasu\_PRZESUNIĘCIA**:</span><span class="sxs-lookup"><span data-stu-id="e76d1-173">This function transforms hello given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="e76d1-174">Po uruchomieniu tego kodu po wiadomość hello są wysyłane tooIoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="e76d1-174">If you run this code, hello following message is sent tooIoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="e76d1-175">Należy pamiętać, że hello serializacji JSON, który jest generowany przez hello format hello **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-175">Note that hello serialization is JSON, which is hello format generated by hello **serializer** library.</span></span> <span data-ttu-id="e76d1-176">Należy pamiętać, że każdy element członkowski hello serializowany obiekt JSON zgodny hello członkami hello **elementu TestType** zdefiniowanego w modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-176">Also note that each member of hello serialized JSON object matches hello members of hello **TestType** that we defined in our model.</span></span> <span data-ttu-id="e76d1-177">wartości Hello również dokładnie odpowiadać używanych w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-177">hello values also exactly match those used in hello code.</span></span> <span data-ttu-id="e76d1-178">Jednak należy pamiętać, że dane binarne hello algorytmem Base64: "AQID" jest hello kodowanie base64 {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="e76d1-178">However, note that hello binary data is base64-encoded: "AQID" is hello base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="e76d1-179">W tym przykładzie pokazano hello zaletą hello **serializator** biblioteki — umożliwia nam toosend JSON toohello chmury, bez konieczności tooexplicitly postępowania w przypadku serializacji w naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e76d1-179">This example demonstrates hello advantage of using hello **serializer** library -- it enables us toosend JSON toohello cloud, without having tooexplicitly deal with serialization in our application.</span></span> <span data-ttu-id="e76d1-180">Wszystko, co mamy tooworry o jest ustawienie wartości hello hello zdarzeń danych w modelu, a następnie wywołując prostych interfejsów API toosend chmury toohello tych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="e76d1-180">All we have tooworry about is setting hello values of hello data events in our model and then calling simple APIs toosend those events toohello cloud.</span></span>

<span data-ttu-id="e76d1-181">Dzięki tym informacjom można definiujemy modeli, które obejmują zakres hello obsługiwane typy danych, łącznie z typów złożonych (Firma Microsoft może nawet obejmują typy złożone w ramach innych typów złożonych).</span><span class="sxs-lookup"><span data-stu-id="e76d1-181">With this information, we can define models that include hello range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="e76d1-182">Jednak on serializacji JSON generowane przez hello w powyższym przykładzie wywołuje punkt ważne.</span><span class="sxs-lookup"><span data-stu-id="e76d1-182">However, he serialized JSON generated by hello example above brings up an important point.</span></span> <span data-ttu-id="e76d1-183">*Jak* wyślemy danych za pomocą hello **serializator** biblioteki określa dokładnie sposób powstaje hello JSON.</span><span class="sxs-lookup"><span data-stu-id="e76d1-183">*How* we send data with hello **serializer** library determines exactly how hello JSON is formed.</span></span> <span data-ttu-id="e76d1-184">Czy konkretnej jest co omówione zostaną następujące czynności dalej.</span><span class="sxs-lookup"><span data-stu-id="e76d1-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="e76d1-185">Więcej informacji na temat serializacji</span><span class="sxs-lookup"><span data-stu-id="e76d1-185">More about serialization</span></span>
<span data-ttu-id="e76d1-186">Hello poprzedniej sekcji przedstawiono przykład hello danych wyjściowych wygenerowanych przez hello **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-186">hello previous section highlights an example of hello output generated by hello **serializer** library.</span></span> <span data-ttu-id="e76d1-187">W tej sekcji wyjaśniamy sposób biblioteki hello serializuje dane i metody kontrolowania tego zachowania, za pomocą serializacji hello interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="e76d1-187">In this section, we'll explain how hello library serializes data and how you can control that behavior using hello serialization APIs.</span></span>

<span data-ttu-id="e76d1-188">W kolejności omówione hello tooadvance szeregowanie firma Microsoft będzie współpracować z nowy model oparty na termostacie.</span><span class="sxs-lookup"><span data-stu-id="e76d1-188">In order tooadvance hello discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="e76d1-189">Po pierwsze możemy podać niektóre tła na scenariusz hello próbujemy tooaddress.</span><span class="sxs-lookup"><span data-stu-id="e76d1-189">First, let's provide some background on hello scenario we're trying tooaddress.</span></span>

<span data-ttu-id="e76d1-190">Chcemy toomodel termostat, która temperatury i wilgotności.</span><span class="sxs-lookup"><span data-stu-id="e76d1-190">We want toomodel a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="e76d1-191">Każda część danych będzie toobe inaczej wysyłane tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="e76d1-191">Each piece of data is going toobe sent tooIoT Hub differently.</span></span> <span data-ttu-id="e76d1-192">Domyślnie program hello ingresses termostat zdarzeń temperatury raz na 2 minuty; Zdarzenie wilgotności jest ingressed co 15 minut.</span><span class="sxs-lookup"><span data-stu-id="e76d1-192">By default, hello thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="e76d1-193">Po ingressed obu zdarzeń, musi on zawierać sygnaturę przedstawia czas hello tego temperatury odpowiedniego hello lub zmierzono wilgotność.</span><span class="sxs-lookup"><span data-stu-id="e76d1-193">When either event is ingressed, it must include a timestamp that shows hello time that hello corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="e76d1-194">Podana w tym scenariuszu, zostanie przedstawiony dwa różne sposoby toomodel hello danych i wyjaśniamy efekt hello czy modelowania ma na powitania serializować danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="e76d1-194">Given this scenario, we'll demonstrate two different ways toomodel hello data, and we'll explain hello effect that modeling has on hello serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="e76d1-195">Model 1</span><span class="sxs-lookup"><span data-stu-id="e76d1-195">Model 1</span></span>
<span data-ttu-id="e76d1-196">Oto hello pierwszej wersji modelu czy obsługuje hello poprzednim scenariuszu:</span><span class="sxs-lookup"><span data-stu-id="e76d1-196">Here's hello first version of a model that supports hello previous scenario:</span></span>

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

<span data-ttu-id="e76d1-197">Uwaga modelu hello obejmuje dwa dane zdarzenia: **temperatury** i **wilgotności**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-197">Note that hello model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="e76d1-198">W przeciwieństwie do poprzednich przykładach, typ hello każdego zdarzenia jest strukturą zdefiniowane przy użyciu **DECLARE\_struktury**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-198">Unlike previous examples, hello type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="e76d1-199">**TemperatureEvent** zawiera miary temperatury i sygnaturę czasową; **HumidityEvent** zawiera miary wilgoć i sygnaturę czasową.</span><span class="sxs-lookup"><span data-stu-id="e76d1-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="e76d1-200">Ten model daje danych hello toomodel naturalny sposób scenariusz hello opisany powyżej.</span><span class="sxs-lookup"><span data-stu-id="e76d1-200">This model gives us a natural way toomodel hello data for hello scenario described above.</span></span> <span data-ttu-id="e76d1-201">Gdy mamy wysłać zdarzenie toohello chmury, albo wyślemy temperatury/sygnatura czasowa lub pary wilgotności/sygnatura czasowa.</span><span class="sxs-lookup"><span data-stu-id="e76d1-201">When we send an event toohello cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="e76d1-202">Możemy wysłać temperatury chmury toohello zdarzeń przy użyciu kodu, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="e76d1-202">We can send a temperature event toohello cloud using code such as hello following:</span></span>

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

<span data-ttu-id="e76d1-203">Firma Microsoft będzie używać zakodowanych wartości temperatury i wilgotności w hello przykładowy kod, ale Wyobraź sobie możemy poprzez próbkowanie czujników odpowiedniego hello na powitania termostat faktycznie jest pobierania tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e76d1-203">We'll use hard-coded values for temperature and humidity in hello sample code, but imagine that we’re actually retrieving these values by sampling hello corresponding sensors on hello thermostat.</span></span>

<span data-ttu-id="e76d1-204">Powyższy kod Hello używa hello **GetDateTimeOffset** pomocnika, który został wprowadzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="e76d1-204">hello code above uses hello **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="e76d1-205">Przyczyn, które będzie wyczyść nowsze ten kod jawnie oddziela zadania hello serializacji i wysyłania zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-205">For reasons that will become clear later, this code explicitly separates hello task of serializing and sending hello event.</span></span> <span data-ttu-id="e76d1-206">Poprzedni kod Hello serializuje hello temperatury zdarzeń do buforu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-206">hello previous code serializes hello temperature event into a buffer.</span></span> <span data-ttu-id="e76d1-207">Następnie **sendMessage** jest funkcją pomocnika (zawarte w **simplesample\_amqp**) czy wysyła hello tooIoT zdarzeń Centrum:</span><span class="sxs-lookup"><span data-stu-id="e76d1-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends hello event tooIoT Hub:</span></span>

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

<span data-ttu-id="e76d1-208">Ten kod jest podzbiorem hello **SendAsync** pomocnika opisanego w poprzedniej sekcji hello, dlatego firma Microsoft nie będą przekazywane go ponownie w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-208">This code is a subset of hello **SendAsync** helper described in hello previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="e76d1-209">Uruchomienie hello poprzedniego kodu toosend hello temperatury zdarzenia, ta forma serializacji hello zdarzenia są wysyłane tooIoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="e76d1-209">When we run hello previous code toosend hello Temperature event, this serialized form of hello event is sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="e76d1-210">Została wysłana temperatury, który jest typu **TemperatureEvent** i zawiera tej struktury **temperatury** i **czasu** elementu członkowskiego.</span><span class="sxs-lookup"><span data-stu-id="e76d1-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="e76d1-211">Znajduje to odzwierciedlenie bezpośrednio w danych serializacji hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-211">This is directly reflected in hello serialized data.</span></span>

<span data-ttu-id="e76d1-212">Podobnie możemy wysłać zdarzenie wilgotności o tym kodzie:</span><span class="sxs-lookup"><span data-stu-id="e76d1-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="e76d1-213">Formularz Hello serializacji, który wysłał tooIoT Centrum wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e76d1-213">hello serialized form that’s sent tooIoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="e76d1-214">Jest to ponownie, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="e76d1-214">Again, this is as expected.</span></span>

<span data-ttu-id="e76d1-215">Z tym modelem, w pewnym sensie jak dodatkowe zdarzenia można łatwo dodać.</span><span class="sxs-lookup"><span data-stu-id="e76d1-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="e76d1-216">Zdefiniuj więcej struktur za pomocą **DECLARE\_struktury**i dołączyć odpowiednie zdarzenie hello hello model przy użyciu **WITH\_danych**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-216">You define more structures using **DECLARE\_STRUCT**, and include hello corresponding event in hello model using **WITH\_DATA**.</span></span>

<span data-ttu-id="e76d1-217">Teraz zmodyfikujmy hello modelu co zawierają one hello tych samych danych, lecz z inną strukturę.</span><span class="sxs-lookup"><span data-stu-id="e76d1-217">Now, let’s modify hello model so that it includes hello same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="e76d1-218">Modelu 2</span><span class="sxs-lookup"><span data-stu-id="e76d1-218">Model 2</span></span>
<span data-ttu-id="e76d1-219">Należy wziąć pod uwagę toohello ten model alternatywny, jeden powyżej:</span><span class="sxs-lookup"><span data-stu-id="e76d1-219">Consider this alternative model toohello one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="e76d1-220">W takim przypadku został wyeliminowany hello **DECLARE\_struktury** makra i po prostu definiowania elementów danych hello w naszym scenariuszu przy użyciu proste typy z hello język modelowania.</span><span class="sxs-lookup"><span data-stu-id="e76d1-220">In this case we've eliminated hello **DECLARE\_STRUCT** macros and are simply defining hello data items from our scenario using simple types from hello modeling language.</span></span>

<span data-ttu-id="e76d1-221">Tylko dla obecnie hello umożliwia ignorowanie hello **czasu** zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="e76d1-221">Just for hello moment let’s ignore hello **Time** event.</span></span> <span data-ttu-id="e76d1-222">Z tym Zarezerwuj Oto hello kodu tooingress **temperatury**:</span><span class="sxs-lookup"><span data-stu-id="e76d1-222">With that aside, here’s hello code tooingress **Temperature**:</span></span>

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

<span data-ttu-id="e76d1-223">Ten kod wysyła następujące hello serializacji tooIoT zdarzeń Centrum:</span><span class="sxs-lookup"><span data-stu-id="e76d1-223">This code sends hello following serialized event tooIoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="e76d1-224">I hello kod umożliwiający wysyłanie zdarzeń wilgotności hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e76d1-224">And hello code for sending hello Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="e76d1-225">Ten kod wysyła ten tooIoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="e76d1-225">This code sends this tooIoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="e76d1-226">Do tej pory nie ma jeszcze nie niespodzianki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-226">So far there are still no surprises.</span></span> <span data-ttu-id="e76d1-227">Teraz Zmieńmy wykorzystanie hello SERIALIZACJA makra.</span><span class="sxs-lookup"><span data-stu-id="e76d1-227">Now let's change how we use hello SERIALIZE macro.</span></span>

<span data-ttu-id="e76d1-228">Witaj **SERIALIZACJA** makro może zająć wiele zdarzeń danych jako argumenty.</span><span class="sxs-lookup"><span data-stu-id="e76d1-228">hello **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="e76d1-229">Dzięki temu nam tooserialize hello **temperatury** i **wilgotności** zdarzeń razem i wysyłać je tooIoT Centrum w jednym wywołaniu:</span><span class="sxs-lookup"><span data-stu-id="e76d1-229">This enables us tooserialize hello **Temperature** and **Humidity** event together and send them tooIoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="e76d1-230">Może się odgadnąć, czy wynik hello ten kod jest czy dwóch danych zdarzenia są wysyłane tooIoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="e76d1-230">You might guess that hello result of this code is that two data events are sent tooIoT Hub:</span></span>

<span data-ttu-id="e76d1-231">[</span><span class="sxs-lookup"><span data-stu-id="e76d1-231">[</span></span>

<span data-ttu-id="e76d1-232">{"Temperatury": 75},</span><span class="sxs-lookup"><span data-stu-id="e76d1-232">{"Temperature":75},</span></span>

<span data-ttu-id="e76d1-233">{"Wilgotności": 45}</span><span class="sxs-lookup"><span data-stu-id="e76d1-233">{"Humidity":45}</span></span>

<span data-ttu-id="e76d1-234">]</span><span class="sxs-lookup"><span data-stu-id="e76d1-234">]</span></span>

<span data-ttu-id="e76d1-235">Innymi słowy, może spodziewać, że ten kod jest hello takie same jak wysyłanie **temperatury** i **wilgotności** oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="e76d1-235">In other words, you might expect that this code is hello same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="e76d1-236">Jest po prostu toopass wygody obu zdarzeń zbyt**SERIALIZACJA** hello sam wywołać.</span><span class="sxs-lookup"><span data-stu-id="e76d1-236">It’s just a convenience toopass both events too**SERIALIZE** in hello same call.</span></span> <span data-ttu-id="e76d1-237">Jednakże, który nie jest hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-237">However, that’s not hello case.</span></span> <span data-ttu-id="e76d1-238">Zamiast tego powyższym kodzie hello wysyła ten tooIoT zdarzeń danych jednego koncentratora:</span><span class="sxs-lookup"><span data-stu-id="e76d1-238">Instead, hello code above sends this single data event tooIoT Hub:</span></span>

<span data-ttu-id="e76d1-239">{"Temperatury": 75, "wilgotności": 45}</span><span class="sxs-lookup"><span data-stu-id="e76d1-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="e76d1-240">Może to wyglądać dziwne, ponieważ definiuje nasz model **temperatury** i **wilgotności** jako dwa *oddzielnych* zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="e76d1-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="e76d1-241">Jeden punkt toohello, firma Microsoft nie modelu te zdarzenia gdzie **temperatury** i **wilgotności** w hello tej samej struktury:</span><span class="sxs-lookup"><span data-stu-id="e76d1-241">More toohello point, we didn’t model these events where **Temperature** and **Humidity** are in hello same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="e76d1-242">Użycie tego modelu, będzie łatwiejszy toounderstand jak **temperatury** i **wilgotności** wysłania w hello sam serializacji komunikatów.</span><span class="sxs-lookup"><span data-stu-id="e76d1-242">If we used this model, it would be easier toounderstand how **Temperature** and **Humidity** would be sent in hello same serialized message.</span></span> <span data-ttu-id="e76d1-243">Jednak nie może być wyczyść Dlaczego działa w ten sposób zbyt przekazać obu zdarzeń danych**SERIALIZACJA** przy użyciu modelu 2.</span><span class="sxs-lookup"><span data-stu-id="e76d1-243">However it may not be clear why it works that way when you pass both data events too**SERIALIZE** using model 2.</span></span>

<span data-ttu-id="e76d1-244">To zachowanie jest łatwiejsze toounderstand, jeśli znasz założenia hello tego hello **serializator** biblioteki jest wprowadzenie.</span><span class="sxs-lookup"><span data-stu-id="e76d1-244">This behavior is easier toounderstand if you know hello assumptions that hello **serializer** library is making.</span></span> <span data-ttu-id="e76d1-245">toomake rozumieniu to przejdź wstecz tooour modelu:</span><span class="sxs-lookup"><span data-stu-id="e76d1-245">toomake sense of this let’s go back tooour model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="e76d1-246">W kategoriach zorientowane obiektowo należy traktować tego modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="e76d1-247">W takim przypadku jest modelowanie urządzenie fizyczne (termostacie) i urządzenia zawiera atrybutów, takich jak **temperatury** i **wilgotności**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="e76d1-248">Możemy wysłać hello cały stan modelu z kodem, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="e76d1-248">We can send hello entire state of our model with code such as hello following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="e76d1-249">Zakładając, że wartości hello temperatury i wilgotności czasu są ustawiane, czy widzimy zdarzenia, takiego jak to wysłane tooIoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="e76d1-249">Assuming hello values of Temperature, Humidity and Time are set, we would see an event like this sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="e76d1-250">Czasami może być tylko toosend *niektórych* właściwości chmury toohello modelu hello (jest to szczególnie istotne, jeśli model zawiera wiele zdarzeń danych).</span><span class="sxs-lookup"><span data-stu-id="e76d1-250">Sometimes you may only want toosend *some* properties of hello model toohello cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="e76d1-251">W naszym przykładzie wcześniejszych jest przydatne toosend tylko podzestaw danych dotyczących zdarzeń, takich jak:</span><span class="sxs-lookup"><span data-stu-id="e76d1-251">It’s useful toosend only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="e76d1-252">Spowoduje to wygenerowanie dokładnie hello sam serializacji zdarzeń tak, jakby była zdefiniowanego **TemperatureEvent** z **temperatury** i **czas** — członek, tak samo jak z możemy modelu 1.</span><span class="sxs-lookup"><span data-stu-id="e76d1-252">This generates exactly hello same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="e76d1-253">W takim przypadku możemy stanie toogenerate dokładnie hello sam serializacji zdarzeń za pomocą inny model (model 2), ponieważ dzwoniliśmy **SERIALIZACJA** w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="e76d1-253">In this case we were able toogenerate exactly hello same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="e76d1-254">Witaj ważnym jest to, że w przypadku przekazania zbyt wiele zdarzeń danych**SERIALIZACJA,** , a następnie przyjęto założenie, że każde wydarzenie jest właściwością w pojedynczy obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="e76d1-254">hello important point is that if you pass multiple data events too**SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="e76d1-255">najlepszym rozwiązaniem Hello zależy od tego, i jak myślisz na temat modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-255">hello best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="e76d1-256">Jeśli wysyłasz "zdarzenia" chmury toohello i każde zdarzenie zawiera określony zbiór właściwości, hello pierwszego podejścia umożliwia dużo znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-256">If you’re sending "events" toohello cloud and each event contains a defined set of properties, then hello first approach makes a lot of sense.</span></span> <span data-ttu-id="e76d1-257">W takim przypadku należy użyć **DECLARE\_struktury** toodefine hello strukturę każdego zdarzenia i dołącz je do modelu z hello **WITH\_danych** makra.</span><span class="sxs-lookup"><span data-stu-id="e76d1-257">In that case you would use **DECLARE\_STRUCT** toodefine hello structure of each event and then include them in your model with hello **WITH\_DATA** macro.</span></span> <span data-ttu-id="e76d1-258">Następnie możesz wysłać każde zdarzenie, jak robiliśmy w powyższym przykładzie pierwsze hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-258">Then you send each event as we did in hello first example above.</span></span> <span data-ttu-id="e76d1-259">W tej metody można tylko przejdzie zdarzeń danych jednego zbyt**SERIALIZATOR**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-259">In this approach you would only pass a single data event too**SERIALIZER**.</span></span>

<span data-ttu-id="e76d1-260">Jeśli myślisz o modelu w sposób zorientowane obiektowo, hello drugiej metody może własnych użytkownik.</span><span class="sxs-lookup"><span data-stu-id="e76d1-260">If you think about your model in an object-oriented fashion, then hello second approach may suit you.</span></span> <span data-ttu-id="e76d1-261">W takim przypadku hello elementy zdefiniowane przy użyciu **WITH\_danych** są hello "właściwości" obiektu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-261">In this case, hello elements defined using **WITH\_DATA** are hello "properties" of your object.</span></span> <span data-ttu-id="e76d1-262">Przekaż niezależnie od podzbioru zdarzeń za**SERIALIZACJA** czy chcesz, w zależności od ilości stanu użytkownika "obiektu" ma toosend toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="e76d1-262">You pass whatever subset of events too**SERIALIZE** that you like, depending on how much of your "object’s" state you want toosend toohello cloud.</span></span>

<span data-ttu-id="e76d1-263">Nether podejście jest nieprawidłowy lub w prawo.</span><span class="sxs-lookup"><span data-stu-id="e76d1-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="e76d1-264">Po prostu należy wiedzieć, jak hello **serializator** biblioteki działa prawidłowo, a metoda modelowania hello pobranie, która najlepiej odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="e76d1-264">Just be aware of how hello **serializer** library works, and pick hello modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="e76d1-265">Komunikat — Obsługa</span><span class="sxs-lookup"><span data-stu-id="e76d1-265">Message handling</span></span>
<span data-ttu-id="e76d1-266">Do tej pory w tym artykule tylko został omówiony wysyłania zdarzeń tooIoT Centrum i nie adresowane odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="e76d1-266">So far this article has only discussed sending events tooIoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="e76d1-267">Witaj Przyczyna dla to jest potrzebny tooknow o odbieranie komunikatów przede wszystkim zostały objęte [wcześniej artykuł](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="e76d1-267">hello reason for this is that what we need tooknow about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="e76d1-268">Z tego artykułu przypominają przetwarzania komunikatów przez zarejestrowanie funkcję wywołania zwrotnego komunikat:</span><span class="sxs-lookup"><span data-stu-id="e76d1-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="e76d1-269">Następnie napiszesz hello funkcja wywołania zwrotnego, które jest wywoływane, gdy wiadomość zostanie odebrana:</span><span class="sxs-lookup"><span data-stu-id="e76d1-269">You then write hello callback function that’s invoked when a message is received:</span></span>

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

<span data-ttu-id="e76d1-270">Ta implementacja **IoTHubMessage** wywołania hello określoną funkcję dla każdego działania w modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-270">This implementation of **IoTHubMessage** calls hello specific function for each action in your model.</span></span> <span data-ttu-id="e76d1-271">Na przykład, jeśli model definiuje tej akcji:</span><span class="sxs-lookup"><span data-stu-id="e76d1-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="e76d1-272">Zdefiniuj funkcję z tego podpisu:</span><span class="sxs-lookup"><span data-stu-id="e76d1-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="e76d1-273">**SetAirResistance** następnie jest wywoływana, gdy ten komunikat jest wysyłany tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e76d1-273">**SetAirResistance** is then called when that message is sent tooyour device.</span></span>

<span data-ttu-id="e76d1-274">Jeszcze co firma Microsoft nie zostały wyjaśnione jest jakiej wersji prawdopodobnie wiadomość hello serializacji.</span><span class="sxs-lookup"><span data-stu-id="e76d1-274">What we haven't explained yet is what hello serialized version of message looks like.</span></span> <span data-ttu-id="e76d1-275">Innymi słowy Jeśli chcesz, aby toosend **SetAirResistance** komunikat tooyour urządzenia, jak wygląda ten?</span><span class="sxs-lookup"><span data-stu-id="e76d1-275">In other words, if you want toosend a **SetAirResistance** message tooyour device, what does that look like?</span></span>

<span data-ttu-id="e76d1-276">Przy wysyłaniu wiadomości tooa urządzenia, czy tym za pośrednictwem usługi Azure IoT hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="e76d1-276">If you're sending a message tooa device, you would do so through hello Azure IoT service SDK.</span></span> <span data-ttu-id="e76d1-277">Nadal potrzebujesz tooknow co ciągu toosend tooinvoke określonej akcji.</span><span class="sxs-lookup"><span data-stu-id="e76d1-277">You still need tooknow what string toosend tooinvoke a particular action.</span></span> <span data-ttu-id="e76d1-278">ogólny format Hello wysyłanie wiadomości wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e76d1-278">hello general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="e76d1-279">Wysyłasz Zserializowany obiekt JSON z dwóch właściwości: **nazwa** jest nazwą hello hello akcji (komunikat) i **parametry** zawiera parametry hello działania.</span><span class="sxs-lookup"><span data-stu-id="e76d1-279">You're sending a serialized JSON object with two properties: **Name** is hello name of hello action (message) and **Parameters** contains hello parameters of that action.</span></span>

<span data-ttu-id="e76d1-280">Na przykład tooinvoke **SetAirResistance** można wysłać tego komunikatu tooa urządzenia:</span><span class="sxs-lookup"><span data-stu-id="e76d1-280">For example, tooinvoke **SetAirResistance** you can send this message tooa device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="e76d1-281">Nazwa akcji Hello musi dokładnie odpowiadać akcji zdefiniowanych w modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-281">hello action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="e76d1-282">nazwy parametrów Hello musi być również zgodna.</span><span class="sxs-lookup"><span data-stu-id="e76d1-282">hello parameter names must match as well.</span></span> <span data-ttu-id="e76d1-283">Należy również zauważyć uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="e76d1-283">Also note case sensitivity.</span></span> <span data-ttu-id="e76d1-284">**Nazwa** i **parametrów** są zawsze wielkimi literami.</span><span class="sxs-lookup"><span data-stu-id="e76d1-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="e76d1-285">Upewnij się, że przypadku hello toomatch nazwy akcji i parametrów w modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-285">Make sure toomatch hello case of your action name and parameters in your model.</span></span> <span data-ttu-id="e76d1-286">W tym przykładzie nazwa akcji hello jest "SetAirResistance", a nie "setairresistance".</span><span class="sxs-lookup"><span data-stu-id="e76d1-286">In this example, hello action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="e76d1-287">Witaj dwie inne akcje **TurnFanOn** i **TurnFanOff** może być wywoływany przez wysyłanie tych wiadomości tooa urządzenia:</span><span class="sxs-lookup"><span data-stu-id="e76d1-287">hello two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages tooa device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="e76d1-288">W tej sekcji opisano wszystkie elementy potrzebne tooknow podczas wysyłania zdarzeń i odbierania wiadomości z hello **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-288">This section described everything you need tooknow when sending events and receiving messages with hello **serializer** library.</span></span> <span data-ttu-id="e76d1-289">Przed kontynuowaniem, teraz obejmuje niektóre parametry, które można skonfigurować określające, jak duże jest modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="e76d1-290">Konfiguracja — makro</span><span class="sxs-lookup"><span data-stu-id="e76d1-290">Macro configuration</span></span>
<span data-ttu-id="e76d1-291">Jeśli używasz hello **serializator** biblioteki ważnym elementem toobe SDK hello świadomość znajduje się w hello azure-c udostępnione — Biblioteka narzędzi.</span><span class="sxs-lookup"><span data-stu-id="e76d1-291">If you’re using hello **Serializer** library an important part of hello SDK toobe aware of is found in hello azure-c-shared-utility library.</span></span>
<span data-ttu-id="e76d1-292">Jeśli zostały sklonowane repozytorium hello Azure-iot-sdk-c z serwisu GitHub, za pomocą opcji--cykliczne hello, będą dostępne w tej biblioteki jako narzędzia udostępnione:</span><span class="sxs-lookup"><span data-stu-id="e76d1-292">If you have cloned hello Azure-iot-sdk-c repository from GitHub using hello --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="e76d1-293">Jeśli nie zostały sklonowane hello biblioteki, możesz go znaleźć [tutaj](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="e76d1-293">If you have not cloned hello library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="e76d1-294">W bibliotece jako narzędzia udostępnione hello można znaleźć hello następującego folderu:</span><span class="sxs-lookup"><span data-stu-id="e76d1-294">Within hello shared utility library, you will find hello following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="e76d1-295">Ten folder zawiera rozwiązania Visual Studio o nazwie **makro\_witryny\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="e76d1-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="e76d1-296">program Hello w tym rozwiązaniu generuje hello **makro\_utils.h** pliku.</span><span class="sxs-lookup"><span data-stu-id="e76d1-296">hello program in this solution generates hello **macro\_utils.h** file.</span></span> <span data-ttu-id="e76d1-297">Brak domyślne makro\_pliku utils.h hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="e76d1-297">There’s a default macro\_utils.h file included with hello SDK.</span></span> <span data-ttu-id="e76d1-298">To rozwiązanie umożliwia toomodify niektórych parametrów i następnie ponownie utwórz hello pliku nagłówka, na podstawie tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="e76d1-298">This solution allows you toomodify some parameters and then recreate hello header file based on these parameters.</span></span>

<span data-ttu-id="e76d1-299">są Hello dwóch parametrów klucza toobe zajęto się **nArithmetic** i **nMacroParameters** które zostały określone w tych dwóch wierszach znaleziono w makrze\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="e76d1-299">hello two key parameters toobe concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="e76d1-300">Te wartości są parametry domyślne hello dołączonego hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="e76d1-300">These values are hello default parameters included with hello SDK.</span></span> <span data-ttu-id="e76d1-301">Każdy parametr ma hello następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="e76d1-301">Each parameter has hello following meaning:</span></span>

* <span data-ttu-id="e76d1-302">nMacroParameters — Określa, ile parametrów mogą mieć w jednej instrukcji DECLARE\_definicji makra w modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="e76d1-303">nArithmetic — formanty hello łączna liczba elementów członkowskich dozwolone w modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-303">nArithmetic – Controls hello total number of members allowed in a model.</span></span>

<span data-ttu-id="e76d1-304">przyczyny Hello te parametry są ważne jest, ponieważ decydować, jak duży może być modelu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-304">hello reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="e76d1-305">Rozważmy na przykład tej definicji modelu:</span><span class="sxs-lookup"><span data-stu-id="e76d1-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="e76d1-306">Jak wspomniano wcześniej, **DECLARE\_modelu** jest po prostu makr C.</span><span class="sxs-lookup"><span data-stu-id="e76d1-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="e76d1-307">Witaj nazwy modelu hello i hello **WITH\_danych** instrukcji (jeszcze innego makra) czy parametry **DECLARE\_modelu**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-307">hello names of hello model and hello **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="e76d1-308">**nMacroParameters** definiuje, ile parametry mogą być zawarte w **DECLARE\_modelu**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="e76d1-309">W rezultacie definiuje liczbę zdarzeń i akcji deklaracjach danych może mieć.</span><span class="sxs-lookup"><span data-stu-id="e76d1-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="e76d1-310">W związku z hello domyślny limit 124 oznacza to, zdefiniować modelu z kombinacją akcji około 60 i danych dotyczących zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="e76d1-310">As such, with hello default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="e76d1-311">Jeśli spróbujesz tooexceed ten limit, otrzymasz błędów, które wyglądają toothis podobne:</span><span class="sxs-lookup"><span data-stu-id="e76d1-311">If you try tooexceed this limit, you'll receive compiler errors that look similar toothis:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="e76d1-312">Witaj **nArithmetic** parametr jest więcej informacji na temat hello wewnętrzne działanie hello makra języka niż aplikacja.</span><span class="sxs-lookup"><span data-stu-id="e76d1-312">hello **nArithmetic** parameter is more about hello internal workings of hello macro language than your application.</span></span>  <span data-ttu-id="e76d1-313">Kontroluje hello łączna liczba elementów członkowskich w modelu, mogą znajdować się w tym **DECLARE_STRUCT** makra.</span><span class="sxs-lookup"><span data-stu-id="e76d1-313">It controls hello total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="e76d1-314">Jeśli możesz zacząć się wyświetlać błędy kompilatora, takich jak ta, a następnie spróbuj użyć zwiększenie **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="e76d1-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="e76d1-315">Toochange tych parametrów, zmodyfikuj wartości hello w makrze hello\_utils.tt plik, skompiluj ponownie hello makro\_witryny\_h\_generator.sln rozwiązania i skompilowany program hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e76d1-315">If you want toochange these parameters, modify hello values in hello macro\_utils.tt file, recompile hello macro\_utils\_h\_generator.sln solution, and run hello compiled program.</span></span> <span data-ttu-id="e76d1-316">Się nowe makro\_utils.h plik jest generowany i umieszczane w hello.\\ Typowe\\inc katalogu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-316">When you do so, a new macro\_utils.h file is generated and placed in hello .\\common\\inc directory.</span></span>

<span data-ttu-id="e76d1-317">W nowej wersji hello toouse kolejności makra\_utils.h, Usuń hello **serializator** pakietu NuGet z rozwiązania i w tym miejscu zawierają hello **serializator** projekt programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e76d1-317">In order toouse hello new version of macro\_utils.h, remove hello **serializer** NuGet package from your solution and in its place include hello **serializer** Visual Studio project.</span></span> <span data-ttu-id="e76d1-318">Dzięki temu toocompile Twojego kodu na kod źródłowy hello hello serializator biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-318">This enables your code toocompile against hello source code of hello serializer library.</span></span> <span data-ttu-id="e76d1-319">Obejmuje to makro hello zaktualizowane\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="e76d1-319">This includes hello updated macro\_utils.h.</span></span> <span data-ttu-id="e76d1-320">Jeśli chcesz toodo to dla **simplesample\_amqp**, uruchom przez usunięcie pakietu NuGet hello hello serializator biblioteki z rozwiązania hello:</span><span class="sxs-lookup"><span data-stu-id="e76d1-320">If you want toodo this for **simplesample\_amqp**, start by removing hello NuGet package for hello serializer library from hello solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="e76d1-321">Następnie dodaj ten tooyour projektu rozwiązania Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e76d1-321">Then add this project tooyour Visual Studio solution:</span></span>

> <span data-ttu-id="e76d1-322">. \\c\\serializator\\kompilacji\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="e76d1-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="e76d1-323">Gdy wszystko będzie gotowe rozwiązanie powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e76d1-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="e76d1-324">Teraz podczas kompilowania rozwiązania, hello zaktualizowane makro\_utils.h znajduje się w sieci danych binarnych.</span><span class="sxs-lookup"><span data-stu-id="e76d1-324">Now when you compile your solution, hello updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="e76d1-325">Należy pamiętać, że zwiększenie wartości wystarczająco wysoka, może być dłuższa niż limity kompilatora.</span><span class="sxs-lookup"><span data-stu-id="e76d1-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="e76d1-326">toothis punktu hello **nMacroParameters** hello parametr głównego o które toobe danych.</span><span class="sxs-lookup"><span data-stu-id="e76d1-326">toothis point, hello **nMacroParameters** is hello main parameter with which toobe concerned.</span></span> <span data-ttu-id="e76d1-327">Specyfikacja C99 Hello Określa, czy co najmniej 127 parametrów są dozwolone w definicji makra.</span><span class="sxs-lookup"><span data-stu-id="e76d1-327">hello C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="e76d1-328">Hello kompilatorem następuje hello specyfikację dokładnie (i ma limit 127), więc nie będzie możliwe tooincrease **nMacroParameters** ponad hello domyślną.</span><span class="sxs-lookup"><span data-stu-id="e76d1-328">hello Microsoft compiler follows hello spec exactly (and has a limit of 127), so you won't be able tooincrease **nMacroParameters** beyond hello default.</span></span> <span data-ttu-id="e76d1-329">Inne kompilatory może umożliwić toodo tak (na przykład kompilatora GNU hello obsługuje wyższy limit).</span><span class="sxs-lookup"><span data-stu-id="e76d1-329">Other compilers might allow you toodo so (for example, hello GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="e76d1-330">Do tej pory możemy zostały objęte prawie wszystkie elementy potrzebne tooknow o jak toowrite kodu z hello **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-330">So far we've covered just about everything you need tooknow about how toowrite code with hello **serializer** library.</span></span> <span data-ttu-id="e76d1-331">Przed zawierania, możemy ponownie niektóre tematy z poprzednich artykułów, które możesz się zastanawiać, informacje.</span><span class="sxs-lookup"><span data-stu-id="e76d1-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="e76d1-332">Witaj interfejsów API niższego poziomu</span><span class="sxs-lookup"><span data-stu-id="e76d1-332">hello lower-level APIs</span></span>
<span data-ttu-id="e76d1-333">Witaj przykładowej aplikacji, na którym fokus w tym artykule jest **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-333">hello sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="e76d1-334">W tym przykładzie używa hello wyższego poziomu (hello z systemem innym niż — "wszystko") interfejsów API toosend zdarzeń i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="e76d1-334">This sample uses hello higher-level (hello non-"LL") APIs toosend events and receive messages.</span></span> <span data-ttu-id="e76d1-335">Korzystając z poniższych interfejsów API, uruchamia wątku w tle, który zajmuje się zarówno zdarzenia wysyłania i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="e76d1-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="e76d1-336">Można jednak użyć hello niższego poziomu (wszystkie) interfejsów API tooeliminate wątku w tle i kontrolować jawne przez wysłanie zdarzenia lub odbieranie komunikatów z hello chmury.</span><span class="sxs-lookup"><span data-stu-id="e76d1-336">However, you can use hello lower-level (LL) APIs tooeliminate this background thread and take explicit control over when you send events or receive messages from hello cloud.</span></span>

<span data-ttu-id="e76d1-337">Zgodnie z opisem w [poprzednim artykule](iot-hub-device-sdk-c-iothubclient.md), istnieje zestaw funkcji, która składa się z hello wyższego poziomu interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="e76d1-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of hello higher-level APIs:</span></span>

* <span data-ttu-id="e76d1-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="e76d1-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="e76d1-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="e76d1-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="e76d1-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="e76d1-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="e76d1-341">IoTHubClient\_zniszczyć</span><span class="sxs-lookup"><span data-stu-id="e76d1-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="e76d1-342">Te interfejsy API przedstawiono w części **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="e76d1-343">Istnieje również analogiczne zestaw interfejsów API niższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="e76d1-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="e76d1-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="e76d1-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="e76d1-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="e76d1-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="e76d1-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="e76d1-347">IoTHubClient\_LL\_zniszczyć</span><span class="sxs-lookup"><span data-stu-id="e76d1-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="e76d1-348">Należy pamiętać, że pracy interfejsów API niższego poziomu hello dokładnie hello sam sposób, jak opisano w poprzednich artykułach hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-348">Note that hello lower-level APIs work exactly hello same way as described in hello previous articles.</span></span> <span data-ttu-id="e76d1-349">Jeśli chcesz, aby wątku tła w toohandle zdarzenia wysyłania i odbierania wiadomości, można użyć hello pierwszy zestaw interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="e76d1-349">You can use hello first set of APIs if you want a background thread toohandle sending events and receiving messages.</span></span> <span data-ttu-id="e76d1-350">Możesz użyć hello drugi zestaw interfejsów API jawną kontrolę nad podczas wysyłania i odbierania danych z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e76d1-350">You use hello second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="e76d1-351">Albo zestaw interfejsów API pracy oraz jednakowo z hello **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-351">Either set of APIs work equally well with hello **serializer** library.</span></span>

<span data-ttu-id="e76d1-352">Na przykład jak hello interfejsów API niższego poziomu są używane z hello **serializator** biblioteki, zobacz hello **simplesample\_http** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e76d1-352">For an example of how hello lower-level APIs are used with hello **serializer** library, see hello **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="e76d1-353">Tematy dodatkowe</span><span class="sxs-lookup"><span data-stu-id="e76d1-353">Additional topics</span></span>
<span data-ttu-id="e76d1-354">Kilka innych tematów, warto zauważyć, są ponownie właściwości obsługi, przy użyciu poświadczeń alternatywnych urządzenia i opcje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e76d1-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="e76d1-355">Są to wszystkie tematy objęte [poprzednim artykule](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="e76d1-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="e76d1-356">Hello główny punkt jest czy wszystkie te funkcje działają w hello sam sposób z hello **serializator** biblioteki co z hello **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-356">hello main point is that all of these features work in hello same way with hello **serializer** library as they do with hello **IoTHubClient** library.</span></span> <span data-ttu-id="e76d1-357">Na przykład, jeśli chcesz tooattach właściwości tooan zdarzeń z modelu, używasz **IoTHubMessage\_właściwości** i **mapy**\_**AddorUpdate**, hello sam sposób, jak opisano wcześniej:</span><span class="sxs-lookup"><span data-stu-id="e76d1-357">For example, if you want tooattach properties tooan event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, hello same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="e76d1-358">Określa, czy zdarzenie hello został wygenerowany na podstawie hello **serializator** biblioteki lub utworzone ręcznie za pomocą hello **IoTHubClient** biblioteki nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="e76d1-358">Whether hello event was generated from hello **serializer** library or created manually using hello **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="e76d1-359">Alternatywne poświadczenia urządzenia, za pomocą funkcji dla hello **IoTHubClient\_LL\_Utwórz** równie dobrze działa jako **IoTHubClient\_CreateFromConnectionString** dla przydzielanie **Centrum IOTHUB\_klienta\_obsługi**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-359">For hello alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="e76d1-360">Ponadto jeśli używasz hello **serializator** biblioteki, można ustawić opcji konfiguracji z **IoTHubClient\_LL\_SetOption** podobnie jak w przypadku przy użyciu hello **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-360">Finally, if you're using hello **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using hello **IoTHubClient** library.</span></span>

<span data-ttu-id="e76d1-361">Funkcja, która jest unikatowa toohello **serializator** biblioteki są hello inicjowania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="e76d1-361">A feature that is unique toohello **serializer** library are hello initialization APIs.</span></span> <span data-ttu-id="e76d1-362">Przed rozpoczęciem pracy z biblioteki hello należy wywołać **serializator\_init**:</span><span class="sxs-lookup"><span data-stu-id="e76d1-362">Before you can start working with hello library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="e76d1-363">Jest to realizowane tylko przed wywołaniem **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="e76d1-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="e76d1-364">Podobnie, po zakończeniu pracy z biblioteki hello, ostatnim wywołaniu hello należy podjąć jest zbyt**serializator\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="e76d1-364">Similarly, when you're done working with hello library, hello last call you’ll make is too**serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="e76d1-365">W przeciwnym razie hello wszystkie inne funkcje wymienione powyżej pracy hello sam hello **serializator** biblioteki tak jak w hello **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e76d1-365">Otherwise, all of hello other features listed above work hello same in hello **serializer** library as they do in hello **IoTHubClient** library.</span></span> <span data-ttu-id="e76d1-366">Aby uzyskać więcej informacji o tych tematów, zobacz hello [poprzednim artykule](iot-hub-device-sdk-c-iothubclient.md) w tej serii.</span><span class="sxs-lookup"><span data-stu-id="e76d1-366">For more information about any of these topics, see hello [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e76d1-367">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e76d1-367">Next steps</span></span>
<span data-ttu-id="e76d1-368">W tym artykule opisano szczegółowo hello unikatowe aspekty hello **serializator** biblioteki zawarte w hello **urządzenia Azure IoT SDK dla języka C**. Z informacjami hello należy dysponować dobrą znajomością o jak toouse modele toosend zdarzenia i odbierać komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e76d1-368">This article describes in detail hello unique aspects of hello **serializer** library contained in hello **Azure IoT device SDK for C**. With hello information provided you should have a good understanding of how toouse models toosend events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="e76d1-369">Teraz również hello trzyczęściowej serii na jak hello toodevelop aplikacji za pomocą **urządzenia Azure IoT SDK dla języka C**. To powinien być wystarczającej ilości informacji toonot tylko get, uruchamiany, ale także zapewniają dokładne zrozumienie działania hello interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="e76d1-369">This also concludes hello three-part series on how toodevelop applications with hello **Azure IoT device SDK for C**. This should be enough information toonot only get you started but give you a thorough understanding of how hello APIs work.</span></span> <span data-ttu-id="e76d1-370">Aby uzyskać dodatkowe informacje obejmuje kilka przykładów powitalne zestawu SDK nie pasuje do tutaj.</span><span class="sxs-lookup"><span data-stu-id="e76d1-370">For additional information, there are a few samples in hello SDK not covered here.</span></span> <span data-ttu-id="e76d1-371">W przeciwnym razie hello [dokumentacji zestawu SDK](https://github.com/Azure/azure-iot-sdk-c) jest dobrym zasobów, aby uzyskać dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="e76d1-371">Otherwise, hello [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="e76d1-372">toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz hello [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="e76d1-372">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="e76d1-373">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="e76d1-373">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="e76d1-374">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="e76d1-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
