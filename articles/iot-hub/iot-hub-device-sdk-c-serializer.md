---
title: "Azure urządzenia IoT zestawu SDK dla języka C - serializator | Dokumentacja firmy Microsoft"
description: "Jak używać biblioteki serializator na urządzeniu Azure IoT SDK dla języka C do tworzenia aplikacji urządzenia, które komunikują się z Centrum IoT."
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
ms.openlocfilehash: aa03c29c54d75538b1fdf987cac5f09d5d344f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="44181-103">Azure IoT urządzenia zestawu SDK dla języka C — więcej informacji na temat serializator</span><span class="sxs-lookup"><span data-stu-id="44181-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="44181-104">[Najpierw artykuł](iot-hub-device-sdk-c-intro.md) w tej serii wprowadzone **urządzenia Azure IoT SDK dla języka C**. Kolejnym artykule podano bardziej szczegółowy opis [ **IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="44181-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. The next article provided a more detailed description of the [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="44181-105">W tym artykule zakończeniu pokrycia zestawu SDK, zapewniając bardziej szczegółowy opis pozostałych składników: **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="44181-105">This article completes coverage of the SDK by providing a more detailed description of the remaining component: the **serializer** library.</span></span>

<span data-ttu-id="44181-106">Wprowadzające artykule opisano sposób użycia **serializator** biblioteki do zdarzeń w celu wysyłania i odbierania wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="44181-106">The introductory article described how to use the **serializer** library to send events to and receive messages from IoT Hub.</span></span> <span data-ttu-id="44181-107">W tym artykule rozbudowujemy zapewniając bardziej szczegółowy opis modelu danych za pomocą tej dyskusji **serializator** makra języka.</span><span class="sxs-lookup"><span data-stu-id="44181-107">In this article, we extend that discussion by providing a more complete explanation of how to model your data with the **serializer** macro language.</span></span> <span data-ttu-id="44181-108">Artykuł obejmuje również więcej szczegółów na temat sposobu biblioteki serializuje wiadomości (i w niektórych przypadkach, jak można kontrolować zachowanie serializacji).</span><span class="sxs-lookup"><span data-stu-id="44181-108">The article also includes more detail about how the library serializes messages (and in some cases how you can control the serialization behavior).</span></span> <span data-ttu-id="44181-109">Opiszemy także niektóre parametry, które można modyfikować określające rozmiar tworzenia modeli.</span><span class="sxs-lookup"><span data-stu-id="44181-109">We'll also describe some parameters you can modify that determine the size of the models you create.</span></span>

<span data-ttu-id="44181-110">Na koniec tego artykułu revisits niektóre tematy omówione w poprzednich artykułach, takie jak wiadomości i Obsługa właściwości.</span><span class="sxs-lookup"><span data-stu-id="44181-110">Finally, the article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="44181-111">Jako firma Microsoft będzie Znajdź prace, te funkcje w taki sam sposób przy użyciu **serializator** biblioteki co z **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="44181-111">As we'll find out, those features work in the same way using the **serializer** library as they do with the **IoTHubClient** library.</span></span>

<span data-ttu-id="44181-112">Wszystkie elementy opisane w tym artykule jest oparta na **serializator** przykłady zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="44181-112">Everything described in this article is based on the **serializer** SDK samples.</span></span> <span data-ttu-id="44181-113">Jeśli chcesz z niego skorzystać, zobacz **simplesample\_amqp** i **simplesample\_http** aplikacje zawarte w urządzenia Azure IoT SDK dla C.</span><span class="sxs-lookup"><span data-stu-id="44181-113">If you want to follow along, see the **simplesample\_amqp** and **simplesample\_http** applications included in the Azure IoT device SDK for C.</span></span>

<span data-ttu-id="44181-114">Można znaleźć [ **urządzenia Azure IoT SDK dla języka C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repozytorium i wyświetlenia jej szczegółów interfejsu API w [dokumentacja interfejsu API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="44181-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-modeling-language"></a><span data-ttu-id="44181-115">Język modelowania</span><span class="sxs-lookup"><span data-stu-id="44181-115">The modeling language</span></span>
<span data-ttu-id="44181-116">[Wprowadzające artykułu](iot-hub-device-sdk-c-intro.md) w tej serii wprowadzone **urządzenia Azure IoT SDK dla języka C** modeling language za pośrednictwem przykładzie przedstawionym w **simplesample\_amqp** aplikacji:</span><span class="sxs-lookup"><span data-stu-id="44181-116">The [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C** modeling language through the example provided in the **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="44181-117">Jak widać, język modelowania jest oparta na makr C.</span><span class="sxs-lookup"><span data-stu-id="44181-117">As you can see, the modeling language is based on C macros.</span></span> <span data-ttu-id="44181-118">Zawsze należy zacząć definicja z **BEGIN\_przestrzeni nazw** i zawsze kończyć **zakończenia\_przestrzeni nazw**.</span><span class="sxs-lookup"><span data-stu-id="44181-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="44181-119">Są często nazwę przestrzeni nazw w firmie lub, jak w poniższym przykładzie w projekcie, który pracuje.</span><span class="sxs-lookup"><span data-stu-id="44181-119">It's common to name the namespace for your company or, as in this example, the project that you're working on.</span></span>

<span data-ttu-id="44181-120">Co jest umieszczane w obszarze nazw są definicje modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-120">What goes inside the namespace are model definitions.</span></span> <span data-ttu-id="44181-121">W takim przypadku jest pojedynczego modelu dla anemometer.</span><span class="sxs-lookup"><span data-stu-id="44181-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="44181-122">Ponownie model może mieć nazwę niczego, ale zazwyczaj jest to urządzenie lub typu danych, który chcesz wymiany z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="44181-122">Once again, the model can be named anything, but typically this is named for the device or type of data you want to exchange with IoT Hub.</span></span>  

<span data-ttu-id="44181-123">Modele zawiera definicji zdarzeń umożliwia transfer danych przychodzących z Centrum IoT ( *danych*) oraz komunikaty mogą odbierać z Centrum IoT ( *akcje*).</span><span class="sxs-lookup"><span data-stu-id="44181-123">Models contain a definition of the events you can ingress to IoT Hub (the *data*) as well as the messages you can receive from IoT Hub (the *actions*).</span></span> <span data-ttu-id="44181-124">Jak widać w przykładzie zdarzenia mają typem i nazwą; Akcje mieć nazwę i następujące parametry opcjonalne (każde z nich typu).</span><span class="sxs-lookup"><span data-stu-id="44181-124">As you can see from the example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="44181-125">Co nie jest prezentowana w tym przykładzie są typy dodatkowe dane, które są obsługiwane przez zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="44181-125">What’s not demonstrated in this sample are additional data types that are supported by the SDK.</span></span> <span data-ttu-id="44181-126">Firma Microsoft będzie obejmować tego dalej.</span><span class="sxs-lookup"><span data-stu-id="44181-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="44181-127">Centrum IoT odwołuje się do danych urządzenie wysyła do niego jako *zdarzenia*, podczas gdy język modelowania odwołuje się do niego jako *danych* (zdefiniowany przy użyciu **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="44181-127">IoT Hub refers to the data a device sends to it as *events*, while the modeling language refers to it as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="44181-128">Podobnie, Centrum IoT odwołuje się do danych, możesz wysłać do urządzenia jako *wiadomości*, podczas gdy język modelowania odwołuje się do niego jako *akcje* (zdefiniowany przy użyciu **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="44181-128">Likewise, IoT Hub refers to the data you send to devices as *messages*, while the modeling language refers to it as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="44181-129">Należy pamiętać, że te terminy mogą używane zamiennie w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="44181-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="44181-130">Obsługiwane typy danych</span><span class="sxs-lookup"><span data-stu-id="44181-130">Supported data types</span></span>
<span data-ttu-id="44181-131">Następujące typy danych są obsługiwane w modelach utworzone za pomocą **serializator** biblioteki:</span><span class="sxs-lookup"><span data-stu-id="44181-131">The following data types are supported in models created with the **serializer** library:</span></span>

| <span data-ttu-id="44181-132">Typ</span><span class="sxs-lookup"><span data-stu-id="44181-132">Type</span></span> | <span data-ttu-id="44181-133">Opis</span><span class="sxs-lookup"><span data-stu-id="44181-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44181-134">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="44181-134">double</span></span> |<span data-ttu-id="44181-135">Podwójna precyzja liczba zmiennoprzecinkowa</span><span class="sxs-lookup"><span data-stu-id="44181-135">double precision floating point number</span></span> |
| <span data-ttu-id="44181-136">int</span><span class="sxs-lookup"><span data-stu-id="44181-136">int</span></span> |<span data-ttu-id="44181-137">32-bitowa liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="44181-137">32 bit integer</span></span> |
| <span data-ttu-id="44181-138">Float</span><span class="sxs-lookup"><span data-stu-id="44181-138">float</span></span> |<span data-ttu-id="44181-139">Liczba zmiennoprzecinkowa pojedynczej precyzji</span><span class="sxs-lookup"><span data-stu-id="44181-139">single precision floating point number</span></span> |
| <span data-ttu-id="44181-140">długa</span><span class="sxs-lookup"><span data-stu-id="44181-140">long</span></span> |<span data-ttu-id="44181-141">długich liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="44181-141">long integer</span></span> |
| <span data-ttu-id="44181-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="44181-142">int8\_t</span></span> |<span data-ttu-id="44181-143">8-bitową liczbą całkowitą</span><span class="sxs-lookup"><span data-stu-id="44181-143">8 bit integer</span></span> |
| <span data-ttu-id="44181-144">Int16\_t</span><span class="sxs-lookup"><span data-stu-id="44181-144">int16\_t</span></span> |<span data-ttu-id="44181-145">16-bitową liczbę całkowitą</span><span class="sxs-lookup"><span data-stu-id="44181-145">16 bit integer</span></span> |
| <span data-ttu-id="44181-146">Int32\_t</span><span class="sxs-lookup"><span data-stu-id="44181-146">int32\_t</span></span> |<span data-ttu-id="44181-147">32-bitowa liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="44181-147">32 bit integer</span></span> |
| <span data-ttu-id="44181-148">Int64\_t</span><span class="sxs-lookup"><span data-stu-id="44181-148">int64\_t</span></span> |<span data-ttu-id="44181-149">64-bitowa liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="44181-149">64 bit integer</span></span> |
| <span data-ttu-id="44181-150">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="44181-150">bool</span></span> |<span data-ttu-id="44181-151">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="44181-151">boolean</span></span> |
| <span data-ttu-id="44181-152">ASCII\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="44181-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="44181-153">Ciąg ASCII</span><span class="sxs-lookup"><span data-stu-id="44181-153">ASCII string</span></span> |
| <span data-ttu-id="44181-154">EDM\_DATA\_CZASU\_PRZESUNIĘCIA</span><span class="sxs-lookup"><span data-stu-id="44181-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="44181-155">Przesunięcie czasu daty</span><span class="sxs-lookup"><span data-stu-id="44181-155">date time offset</span></span> |
| <span data-ttu-id="44181-156">EDM\_IDENTYFIKATOR GUID</span><span class="sxs-lookup"><span data-stu-id="44181-156">EDM\_GUID</span></span> |<span data-ttu-id="44181-157">IDENTYFIKATOR GUID</span><span class="sxs-lookup"><span data-stu-id="44181-157">GUID</span></span> |
| <span data-ttu-id="44181-158">EDM\_BINARNE</span><span class="sxs-lookup"><span data-stu-id="44181-158">EDM\_BINARY</span></span> |<span data-ttu-id="44181-159">Binarne</span><span class="sxs-lookup"><span data-stu-id="44181-159">binary</span></span> |
| <span data-ttu-id="44181-160">DEKLAROWANIE\_— STRUKTURA</span><span class="sxs-lookup"><span data-stu-id="44181-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="44181-161">Typ danych złożonych</span><span class="sxs-lookup"><span data-stu-id="44181-161">complex data type</span></span> |

<span data-ttu-id="44181-162">Zacznijmy od ostatniego typu danych.</span><span class="sxs-lookup"><span data-stu-id="44181-162">Let’s start with the last data type.</span></span> <span data-ttu-id="44181-163">**DECLARE\_struktury** można zdefiniować złożone typy danych, które są grupami innych typów pierwotnych.</span><span class="sxs-lookup"><span data-stu-id="44181-163">The **DECLARE\_STRUCT** allows you to define complex data types, which are groupings of the other primitive types.</span></span> <span data-ttu-id="44181-164">Te grupy umożliwiają definiowanie modelu, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="44181-164">These groupings allow us to define a model that looks like this:</span></span>

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

<span data-ttu-id="44181-165">Nasz model zawiera zdarzenie danych jednego typu **elementu TestType**.</span><span class="sxs-lookup"><span data-stu-id="44181-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="44181-166">**Element TestType** jest typem złożonym, który zawiera kilka elementów członkowskich, które wykazują zbiorczo, typy pierwotne, obsługiwane przez **serializator** język modelowania.</span><span class="sxs-lookup"><span data-stu-id="44181-166">**TestType** is a complex type that includes several members, which collectively demonstrate the primitive types supported by the **serializer** modeling language.</span></span>

<span data-ttu-id="44181-167">Z modelem takie firma Microsoft można napisać kod do wysyłania danych do Centrum IoT, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="44181-167">With a model like this, we can write code to send data to IoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="44181-168">Zasadniczo, firma Microsoft jest przypisywanie wartości do wszystkich członków **testu** struktury i wywołując **SendAsync** do wysyłania **testu** zdarzenie danych do chmury.</span><span class="sxs-lookup"><span data-stu-id="44181-168">Basically, we’re assigning a value to every member of the **Test** structure and then calling **SendAsync** to send the **Test** data event to the cloud.</span></span> <span data-ttu-id="44181-169">**SendAsync** jest funkcji pomocnika, która wysyła zdarzenia pojedynczego danych do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="44181-169">**SendAsync** is a helper function that sends a single data event to IoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate the string
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

<span data-ttu-id="44181-170">Ta funkcja wykonuje serializację danego zdarzenie i wysyła go do Centrum IoT przy użyciu **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="44181-170">This function serializes the given data event and sends it to IoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="44181-171">Jest to ten sam kod omówione w poprzednich artykułach (**SendAsync** hermetyzuje logiki do funkcji wygodny).</span><span class="sxs-lookup"><span data-stu-id="44181-171">This is the same code discussed in previous articles (**SendAsync** encapsulates the logic into a convenient function).</span></span>

<span data-ttu-id="44181-172">Jest jednym innych funkcji pomocnika używany w poprzednim kodzie **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="44181-172">One other helper function used in the previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="44181-173">Ta funkcja przekształca danej chwili w wartości typu **EDM\_data\_czasu\_PRZESUNIĘCIA**:</span><span class="sxs-lookup"><span data-stu-id="44181-173">This function transforms the given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="44181-174">Po uruchomieniu tego kodu następujący komunikat jest wysyłany do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="44181-174">If you run this code, the following message is sent to IoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="44181-175">Należy pamiętać, że serializacji JSON, czyli format generowane przez **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="44181-175">Note that the serialization is JSON, which is the format generated by the **serializer** library.</span></span> <span data-ttu-id="44181-176">Należy również zauważyć, że każdy element członkowski Zserializowany obiekt JSON odpowiada członków **elementu TestType** zdefiniowanego w modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-176">Also note that each member of the serialized JSON object matches the members of the **TestType** that we defined in our model.</span></span> <span data-ttu-id="44181-177">Wartości również dokładnie odpowiadać używanych w kodzie.</span><span class="sxs-lookup"><span data-stu-id="44181-177">The values also exactly match those used in the code.</span></span> <span data-ttu-id="44181-178">Jednak należy pamiętać, że dane binarne algorytmem Base64: "AQID" jest base64 kodowanie {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="44181-178">However, note that the binary data is base64-encoded: "AQID" is the base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="44181-179">W tym przykładzie pokazano, zaletą korzystania z **serializator** biblioteki — umożliwia firmie Microsoft w celu wysyłania JSON w chmurze, bez konieczności jawnego postępowania w przypadku serializacji w naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44181-179">This example demonstrates the advantage of using the **serializer** library -- it enables us to send JSON to the cloud, without having to explicitly deal with serialization in our application.</span></span> <span data-ttu-id="44181-180">Wszystko, co mamy martwić się o jest ustawienie wartości danych zdarzeń w modelu, a następnie wywołując prostych interfejsów API do wysyłania zdarzeń do chmury.</span><span class="sxs-lookup"><span data-stu-id="44181-180">All we have to worry about is setting the values of the data events in our model and then calling simple APIs to send those events to the cloud.</span></span>

<span data-ttu-id="44181-181">Dzięki tym informacjom możemy zdefiniować modele, które obejmują zakres obsługiwane typy danych, łącznie z typów złożonych (Firma Microsoft może nawet obejmują typy złożone w ramach innych typów złożonych).</span><span class="sxs-lookup"><span data-stu-id="44181-181">With this information, we can define models that include the range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="44181-182">Jednak on serializacji JSON generowanych przez w powyższym przykładzie wywołuje punkt ważne.</span><span class="sxs-lookup"><span data-stu-id="44181-182">However, he serialized JSON generated by the example above brings up an important point.</span></span> <span data-ttu-id="44181-183">*Jak* wyślemy danych za pomocą **serializator** biblioteki określa dokładnie, jak kod JSON jest sformatowany.</span><span class="sxs-lookup"><span data-stu-id="44181-183">*How* we send data with the **serializer** library determines exactly how the JSON is formed.</span></span> <span data-ttu-id="44181-184">Czy konkretnej jest co omówione zostaną następujące czynności dalej.</span><span class="sxs-lookup"><span data-stu-id="44181-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="44181-185">Więcej informacji na temat serializacji</span><span class="sxs-lookup"><span data-stu-id="44181-185">More about serialization</span></span>
<span data-ttu-id="44181-186">Poprzedniej sekcji przedstawiono przykładowe dane wyjściowe, generowane przez **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="44181-186">The previous section highlights an example of the output generated by the **serializer** library.</span></span> <span data-ttu-id="44181-187">W tej sekcji wyjaśniamy sposób biblioteki serializuje dane i metody kontrolowania tego zachowania, za pomocą serializacji interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="44181-187">In this section, we'll explain how the library serializes data and how you can control that behavior using the serialization APIs.</span></span>

<span data-ttu-id="44181-188">Aby poprawić dyskusji w serializacji, firma Microsoft będzie współpracować z nowy model oparty na termostacie.</span><span class="sxs-lookup"><span data-stu-id="44181-188">In order to advance the discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="44181-189">Po pierwsze umożliwia zawierają niektóre tła na scenariuszu próbujemy adres.</span><span class="sxs-lookup"><span data-stu-id="44181-189">First, let's provide some background on the scenario we're trying to address.</span></span>

<span data-ttu-id="44181-190">Chcemy termostat, która temperatury i wilgotności modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-190">We want to model a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="44181-191">Każda część danych będzie wysyłane do Centrum IoT inaczej.</span><span class="sxs-lookup"><span data-stu-id="44181-191">Each piece of data is going to be sent to IoT Hub differently.</span></span> <span data-ttu-id="44181-192">Domyślnie ingresses termostat zdarzeniem temperatury raz na 2 minuty; Zdarzenie wilgotności jest ingressed co 15 minut.</span><span class="sxs-lookup"><span data-stu-id="44181-192">By default, the thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="44181-193">W przypadku ingressed obu zdarzeń, musi on zawierać sygnatury czasowej, która przedstawia czas odpowiedniego temperatury i wilgotności zmierzono.</span><span class="sxs-lookup"><span data-stu-id="44181-193">When either event is ingressed, it must include a timestamp that shows the time that the corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="44181-194">Zostanie przedstawiony dwa różne sposoby modelu danych podane w tym scenariuszu, i wyjaśniamy efekt czy modelowania ma na serializowane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="44181-194">Given this scenario, we'll demonstrate two different ways to model the data, and we'll explain the effect that modeling has on the serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="44181-195">Model 1</span><span class="sxs-lookup"><span data-stu-id="44181-195">Model 1</span></span>
<span data-ttu-id="44181-196">Oto pierwszej wersji modelu, który obsługuje poprzedniego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="44181-196">Here's the first version of a model that supports the previous scenario:</span></span>

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

<span data-ttu-id="44181-197">Należy pamiętać, że model zawiera dwa zdarzenia danych: **temperatury** i **wilgotności**.</span><span class="sxs-lookup"><span data-stu-id="44181-197">Note that the model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="44181-198">W przeciwieństwie do poprzednich przykładach, typ każdego zdarzenia jest strukturą zdefiniowane przy użyciu **DECLARE\_struktury**.</span><span class="sxs-lookup"><span data-stu-id="44181-198">Unlike previous examples, the type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="44181-199">**TemperatureEvent** zawiera miary temperatury i sygnaturę czasową; **HumidityEvent** zawiera miary wilgoć i sygnaturę czasową.</span><span class="sxs-lookup"><span data-stu-id="44181-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="44181-200">Ten model umożliwia nam fizycznych modelu danych scenariusz opisany powyżej.</span><span class="sxs-lookup"><span data-stu-id="44181-200">This model gives us a natural way to model the data for the scenario described above.</span></span> <span data-ttu-id="44181-201">Gdy firma Microsoft wysyła zdarzenie do chmury, albo wyślemy temperatury/sygnatura czasowa lub pary wilgotności/sygnatura czasowa.</span><span class="sxs-lookup"><span data-stu-id="44181-201">When we send an event to the cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="44181-202">Możemy wysłać zdarzenie temperatury w chmurze przy użyciu kodu, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="44181-202">We can send a temperature event to the cloud using code such as the following:</span></span>

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

<span data-ttu-id="44181-203">Firma Microsoft będzie używać zakodowanych wartości temperatury i wilgotności w przykładowym kodzie, ale Wyobraź sobie możemy poprzez próbkowanie odpowiednich czujników na termostat faktycznie jest pobierania tych wartości.</span><span class="sxs-lookup"><span data-stu-id="44181-203">We'll use hard-coded values for temperature and humidity in the sample code, but imagine that we’re actually retrieving these values by sampling the corresponding sensors on the thermostat.</span></span>

<span data-ttu-id="44181-204">Kod nad używa **GetDateTimeOffset** pomocnika, który został wprowadzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="44181-204">The code above uses the **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="44181-205">Przyczyn, które będzie wyczyść nowsze ten kod jawnie oddziela zadania serializacji i wysyła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="44181-205">For reasons that will become clear later, this code explicitly separates the task of serializing and sending the event.</span></span> <span data-ttu-id="44181-206">Poprzedni kod serializuje zdarzeń temperatury do buforu.</span><span class="sxs-lookup"><span data-stu-id="44181-206">The previous code serializes the temperature event into a buffer.</span></span> <span data-ttu-id="44181-207">Następnie **sendMessage** jest funkcją pomocnika (objęte **simplesample\_amqp**) która wysyła zdarzenia do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="44181-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends the event to IoT Hub:</span></span>

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

<span data-ttu-id="44181-208">Ten kod jest podzbiorem **SendAsync** pomocnika opisanych w poprzedniej sekcji, dlatego firma Microsoft nie będą przekazywane go ponownie w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="44181-208">This code is a subset of the **SendAsync** helper described in the previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="44181-209">Uruchomienie poprzedni kod do wysyłania zdarzeń temperatury, ta forma serializacji zdarzenia są wysyłane do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="44181-209">When we run the previous code to send the Temperature event, this serialized form of the event is sent to IoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="44181-210">Została wysłana temperatury, który jest typu **TemperatureEvent** i zawiera tej struktury **temperatury** i **czasu** elementu członkowskiego.</span><span class="sxs-lookup"><span data-stu-id="44181-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="44181-211">Znajduje to odzwierciedlenie bezpośrednio w danych serializacji.</span><span class="sxs-lookup"><span data-stu-id="44181-211">This is directly reflected in the serialized data.</span></span>

<span data-ttu-id="44181-212">Podobnie możemy wysłać zdarzenie wilgotności o tym kodzie:</span><span class="sxs-lookup"><span data-stu-id="44181-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="44181-213">Zserializowany formularz, który jest wysyłany do Centrum IoT wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="44181-213">The serialized form that’s sent to IoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="44181-214">Jest to ponownie, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="44181-214">Again, this is as expected.</span></span>

<span data-ttu-id="44181-215">Z tym modelem, w pewnym sensie jak dodatkowe zdarzenia można łatwo dodać.</span><span class="sxs-lookup"><span data-stu-id="44181-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="44181-216">Zdefiniuj więcej struktur za pomocą **DECLARE\_struktury**i dołączyć odpowiednie zdarzenie w modelu, używając **WITH\_danych**.</span><span class="sxs-lookup"><span data-stu-id="44181-216">You define more structures using **DECLARE\_STRUCT**, and include the corresponding event in the model using **WITH\_DATA**.</span></span>

<span data-ttu-id="44181-217">Teraz zmodyfikujmy modelu co zawierają one te same dane, ale z inną strukturę.</span><span class="sxs-lookup"><span data-stu-id="44181-217">Now, let’s modify the model so that it includes the same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="44181-218">Modelu 2</span><span class="sxs-lookup"><span data-stu-id="44181-218">Model 2</span></span>
<span data-ttu-id="44181-219">Należy wziąć pod uwagę alternatywnych modelu poprzednim:</span><span class="sxs-lookup"><span data-stu-id="44181-219">Consider this alternative model to the one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="44181-220">W takim przypadku możemy Wyeliminowano **DECLARE\_struktury** makra i po prostu są definiowane w naszym scenariuszu przy użyciu proste typy z język modelowania elementów danych.</span><span class="sxs-lookup"><span data-stu-id="44181-220">In this case we've eliminated the **DECLARE\_STRUCT** macros and are simply defining the data items from our scenario using simple types from the modeling language.</span></span>

<span data-ttu-id="44181-221">Tylko dla obecnie umożliwia ignorowanie **czasu** zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="44181-221">Just for the moment let’s ignore the **Time** event.</span></span> <span data-ttu-id="44181-222">Z tym Zarezerwuj Oto kod, aby ruch przychodzący **temperatury**:</span><span class="sxs-lookup"><span data-stu-id="44181-222">With that aside, here’s the code to ingress **Temperature**:</span></span>

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

<span data-ttu-id="44181-223">Ten kod wysyła następujące zdarzenie Zserializowany do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="44181-223">This code sends the following serialized event to IoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="44181-224">I kod umożliwiający wysyłanie zdarzeń wilgotności wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="44181-224">And the code for sending the Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="44181-225">Ten kod wysyła to Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="44181-225">This code sends this to IoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="44181-226">Do tej pory nie ma jeszcze nie niespodzianki.</span><span class="sxs-lookup"><span data-stu-id="44181-226">So far there are still no surprises.</span></span> <span data-ttu-id="44181-227">Teraz Zmieńmy wykorzystanie makro SERIALIZACJA.</span><span class="sxs-lookup"><span data-stu-id="44181-227">Now let's change how we use the SERIALIZE macro.</span></span>

<span data-ttu-id="44181-228">**SERIALIZACJA** makro może zająć wiele zdarzeń danych jako argumenty.</span><span class="sxs-lookup"><span data-stu-id="44181-228">The **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="44181-229">Pozwala na serializować **temperatury** i **wilgotności** razem zdarzeń i wyślij je do Centrum IoT w jednym wywołaniu:</span><span class="sxs-lookup"><span data-stu-id="44181-229">This enables us to serialize the **Temperature** and **Humidity** event together and send them to IoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="44181-230">Może się odgadnąć, czy wynik ten kod jest czy dwóch danych zdarzenia są wysyłane do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="44181-230">You might guess that the result of this code is that two data events are sent to IoT Hub:</span></span>

<span data-ttu-id="44181-231">[</span><span class="sxs-lookup"><span data-stu-id="44181-231">[</span></span>

<span data-ttu-id="44181-232">{"Temperatury": 75},</span><span class="sxs-lookup"><span data-stu-id="44181-232">{"Temperature":75},</span></span>

<span data-ttu-id="44181-233">{"Wilgotności": 45}</span><span class="sxs-lookup"><span data-stu-id="44181-233">{"Humidity":45}</span></span>

<span data-ttu-id="44181-234">]</span><span class="sxs-lookup"><span data-stu-id="44181-234">]</span></span>

<span data-ttu-id="44181-235">Innymi słowy, może spodziewać, ten kod jest taka sama, jak wysyłanie **temperatury** i **wilgotności** oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="44181-235">In other words, you might expect that this code is the same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="44181-236">Jest po prostu wygody do przekazywania zarówno zdarzeń do **SERIALIZACJA** w tym samym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="44181-236">It’s just a convenience to pass both events to **SERIALIZE** in the same call.</span></span> <span data-ttu-id="44181-237">Jednak to nie jest wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="44181-237">However, that’s not the case.</span></span> <span data-ttu-id="44181-238">Zamiast tego kodu powyżej wysyła to zdarzenie danych jednego z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="44181-238">Instead, the code above sends this single data event to IoT Hub:</span></span>

<span data-ttu-id="44181-239">{"Temperatury": 75, "wilgotności": 45}</span><span class="sxs-lookup"><span data-stu-id="44181-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="44181-240">Może to wyglądać dziwne, ponieważ definiuje nasz model **temperatury** i **wilgotności** jako dwa *oddzielnych* zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="44181-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="44181-241">Więcej do punktu, firma Microsoft nie tych zdarzeń modelu gdzie **temperatury** i **wilgotności** znajdują się w tej samej struktury:</span><span class="sxs-lookup"><span data-stu-id="44181-241">More to the point, we didn’t model these events where **Temperature** and **Humidity** are in the same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="44181-242">Użycie tego modelu, będzie można łatwiej zrozumieć, jak **temperatury** i **wilgotności** wysłania w tym samym szeregowanego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="44181-242">If we used this model, it would be easier to understand how **Temperature** and **Humidity** would be sent in the same serialized message.</span></span> <span data-ttu-id="44181-243">Jednak nie może być wyczyść Dlaczego podczas przekazywania obu zdarzeń danych działa w ten sposób **SERIALIZACJA** przy użyciu modelu 2.</span><span class="sxs-lookup"><span data-stu-id="44181-243">However it may not be clear why it works that way when you pass both data events to **SERIALIZE** using model 2.</span></span>

<span data-ttu-id="44181-244">To zachowanie jest łatwiejsze do zrozumienia, jeśli znasz założeń który **serializator** biblioteki jest wprowadzenie.</span><span class="sxs-lookup"><span data-stu-id="44181-244">This behavior is easier to understand if you know the assumptions that the **serializer** library is making.</span></span> <span data-ttu-id="44181-245">Aby zorientować się, to wróć do naszego modelu:</span><span class="sxs-lookup"><span data-stu-id="44181-245">To make sense of this let’s go back to our model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="44181-246">W kategoriach zorientowane obiektowo należy traktować tego modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="44181-247">W takim przypadku jest modelowanie urządzenie fizyczne (termostacie) i urządzenia zawiera atrybutów, takich jak **temperatury** i **wilgotności**.</span><span class="sxs-lookup"><span data-stu-id="44181-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="44181-248">Możemy wysłać cały stan modelu z kodem, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="44181-248">We can send the entire state of our model with code such as the following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="44181-249">Zakładając, że wartości temperatury, wilgotności i godzina są ustawione, firma Microsoft będzie Zobacz zdarzenia, takiego jak to wysyłane do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="44181-249">Assuming the values of Temperature, Humidity and Time are set, we would see an event like this sent to IoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="44181-250">Czasami może tylko chcesz wysłać *niektórych* właściwości modelu do chmury (jest to szczególnie istotne, jeśli model zawiera wiele zdarzeń danych).</span><span class="sxs-lookup"><span data-stu-id="44181-250">Sometimes you may only want to send *some* properties of the model to the cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="44181-251">Warto wysłać tylko podzestaw danych dotyczących zdarzeń, takich jak w naszym przykładzie wcześniej:</span><span class="sxs-lookup"><span data-stu-id="44181-251">It’s useful to send only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="44181-252">Spowoduje to wygenerowanie dokładnie tego samego zdarzenia serializacji tak, jakby była zdefiniowanego **TemperatureEvent** z **temperatury** i **czas** — członek, tak samo jak z możemy modelu 1.</span><span class="sxs-lookup"><span data-stu-id="44181-252">This generates exactly the same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="44181-253">W takim przypadku udało się wygenerować dokładnie tego samego zdarzenia serializacji przy użyciu inny model (model 2), ponieważ dzwoniliśmy **SERIALIZACJA** w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="44181-253">In this case we were able to generate exactly the same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="44181-254">Istotne jest to, że w przypadku przekazania wiele zdarzeń danych do **SERIALIZACJA,** , a następnie przyjęto założenie, że każde wydarzenie jest właściwością w pojedynczy obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="44181-254">The important point is that if you pass multiple data events to **SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="44181-255">Najlepszym rozwiązaniem jest zależna od i jak myślisz na temat modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-255">The best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="44181-256">Jeśli wysyłasz "zdarzenia" w chmurze, a każde zdarzenie zawiera określony zbiór właściwości, pierwszego podejścia udostępnia wiele znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="44181-256">If you’re sending "events" to the cloud and each event contains a defined set of properties, then the first approach makes a lot of sense.</span></span> <span data-ttu-id="44181-257">W takim przypadku należy użyć **DECLARE\_struktury** definiować strukturę każdego zdarzenia i dołącz je do modelu z **WITH\_danych** makra.</span><span class="sxs-lookup"><span data-stu-id="44181-257">In that case you would use **DECLARE\_STRUCT** to define the structure of each event and then include them in your model with the **WITH\_DATA** macro.</span></span> <span data-ttu-id="44181-258">Następnie możesz wysłać każde zdarzenie, jak robiliśmy w pierwszym przykładzie powyżej.</span><span class="sxs-lookup"><span data-stu-id="44181-258">Then you send each event as we did in the first example above.</span></span> <span data-ttu-id="44181-259">W tym podejście przejdzie tylko danych jednego zdarzenia **SERIALIZATOR**.</span><span class="sxs-lookup"><span data-stu-id="44181-259">In this approach you would only pass a single data event to **SERIALIZER**.</span></span>

<span data-ttu-id="44181-260">Jeśli myślisz o modelu w sposób zorientowane obiektowo, drugiej metody może własnych użytkownik.</span><span class="sxs-lookup"><span data-stu-id="44181-260">If you think about your model in an object-oriented fashion, then the second approach may suit you.</span></span> <span data-ttu-id="44181-261">W takim przypadku elementy zdefiniowane przy użyciu **WITH\_danych** są "właściwości" obiektu.</span><span class="sxs-lookup"><span data-stu-id="44181-261">In this case, the elements defined using **WITH\_DATA** are the "properties" of your object.</span></span> <span data-ttu-id="44181-262">Przekaż niezależnie od podzbioru zdarzeń do **SERIALIZACJA** które lubisz, w zależności od ilości stanu użytkownika "obiektu" chcesz wysyłać do chmury.</span><span class="sxs-lookup"><span data-stu-id="44181-262">You pass whatever subset of events to **SERIALIZE** that you like, depending on how much of your "object’s" state you want to send to the cloud.</span></span>

<span data-ttu-id="44181-263">Nether podejście jest nieprawidłowy lub w prawo.</span><span class="sxs-lookup"><span data-stu-id="44181-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="44181-264">Po prostu znać sposób **serializator** works biblioteki i pobrania metoda modelowania, która najlepiej odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="44181-264">Just be aware of how the **serializer** library works, and pick the modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="44181-265">Komunikat — Obsługa</span><span class="sxs-lookup"><span data-stu-id="44181-265">Message handling</span></span>
<span data-ttu-id="44181-266">Do tej pory w tym artykule tylko został omówiony wysyłania zdarzeń do Centrum IoT i nie adresowane odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="44181-266">So far this article has only discussed sending events to IoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="44181-267">Powód dla tego jest to, że co należy wiedzieć o odbieranie wiadomości ma przede wszystkim zostały omówione w [wcześniej artykuł](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="44181-267">The reason for this is that what we need to know about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="44181-268">Z tego artykułu przypominają przetwarzania komunikatów przez zarejestrowanie funkcję wywołania zwrotnego komunikat:</span><span class="sxs-lookup"><span data-stu-id="44181-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="44181-269">Następnie napiszesz funkcja wywołania zwrotnego, które jest wywoływane, gdy wiadomość zostanie odebrana:</span><span class="sxs-lookup"><span data-stu-id="44181-269">You then write the callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="44181-270">Ta implementacja **IoTHubMessage** wywołuje funkcję określonych dla każdej akcji w modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-270">This implementation of **IoTHubMessage** calls the specific function for each action in your model.</span></span> <span data-ttu-id="44181-271">Na przykład, jeśli model definiuje tej akcji:</span><span class="sxs-lookup"><span data-stu-id="44181-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="44181-272">Zdefiniuj funkcję z tego podpisu:</span><span class="sxs-lookup"><span data-stu-id="44181-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="44181-273">**SetAirResistance** następnie jest wywoływane, gdy ten komunikat jest wysyłane do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="44181-273">**SetAirResistance** is then called when that message is sent to your device.</span></span>

<span data-ttu-id="44181-274">Jeszcze co firma Microsoft nie zostały wyjaśnione jest wygląda wersja serializowanego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="44181-274">What we haven't explained yet is what the serialized version of message looks like.</span></span> <span data-ttu-id="44181-275">Innymi słowy Jeśli chcesz wysłać **SetAirResistance** komunikat na urządzeniu, jak wygląda ten?</span><span class="sxs-lookup"><span data-stu-id="44181-275">In other words, if you want to send a **SetAirResistance** message to your device, what does that look like?</span></span>

<span data-ttu-id="44181-276">Jeśli wiadomość jest wysyłana do urządzenia, czy Zrób to za pomocą zestawu SDK usług Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="44181-276">If you're sending a message to a device, you would do so through the Azure IoT service SDK.</span></span> <span data-ttu-id="44181-277">Nadal trzeba wiedzieć, jak ciąg znaków, aby wysłać do wywołania określonej akcji.</span><span class="sxs-lookup"><span data-stu-id="44181-277">You still need to know what string to send to invoke a particular action.</span></span> <span data-ttu-id="44181-278">Ogólny format wysyłania komunikatu wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="44181-278">The general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="44181-279">Wysyłasz Zserializowany obiekt JSON z dwóch właściwości: **nazwa** jest nazwa akcji (komunikat) i **parametry** zawiera parametry tej akcji.</span><span class="sxs-lookup"><span data-stu-id="44181-279">You're sending a serialized JSON object with two properties: **Name** is the name of the action (message) and **Parameters** contains the parameters of that action.</span></span>

<span data-ttu-id="44181-280">Na przykład, aby wywołać **SetAirResistance** możesz wysłać tę wiadomość na urządzeniu:</span><span class="sxs-lookup"><span data-stu-id="44181-280">For example, to invoke **SetAirResistance** you can send this message to a device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="44181-281">Nazwa akcji musi dokładnie odpowiadać akcji zdefiniowanych w modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-281">The action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="44181-282">Nazwy parametrów muszą być zgodne, jak również.</span><span class="sxs-lookup"><span data-stu-id="44181-282">The parameter names must match as well.</span></span> <span data-ttu-id="44181-283">Należy również zauważyć uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="44181-283">Also note case sensitivity.</span></span> <span data-ttu-id="44181-284">**Nazwa** i **parametrów** są zawsze wielkimi literami.</span><span class="sxs-lookup"><span data-stu-id="44181-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="44181-285">Upewnij się, że wielkość liter nazwy akcji i parametrów w modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-285">Make sure to match the case of your action name and parameters in your model.</span></span> <span data-ttu-id="44181-286">W tym przykładzie nazwa akcji jest "SetAirResistance", a nie "setairresistance".</span><span class="sxs-lookup"><span data-stu-id="44181-286">In this example, the action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="44181-287">Dwie inne akcje **TurnFanOn** i **TurnFanOff** może być wywoływany przez wysyłanie tych wiadomości na urządzeniu:</span><span class="sxs-lookup"><span data-stu-id="44181-287">The two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages to a device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="44181-288">W tej sekcji opisano wszystko, co należy wiedzieć, kiedy zdarzenia wysyłanie i odbieranie komunikatów z **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="44181-288">This section described everything you need to know when sending events and receiving messages with the **serializer** library.</span></span> <span data-ttu-id="44181-289">Przed kontynuowaniem, teraz obejmuje niektóre parametry, które można skonfigurować określające, jak duże jest modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="44181-290">Konfiguracja — makro</span><span class="sxs-lookup"><span data-stu-id="44181-290">Macro configuration</span></span>
<span data-ttu-id="44181-291">Jeśli używasz **serializator** biblioteki ważnym elementem zestaw SDK, aby mieć świadomość znajduje się w bibliotece azure-c udostępnione — narzędzie.</span><span class="sxs-lookup"><span data-stu-id="44181-291">If you’re using the **Serializer** library an important part of the SDK to be aware of is found in the azure-c-shared-utility library.</span></span>
<span data-ttu-id="44181-292">Jeśli zostały sklonowane repozytorium Azure-iot-sdk-c z serwisu GitHub, za pomocą opcji--cykliczne, będą dostępne w tej biblioteki jako narzędzia udostępnione:</span><span class="sxs-lookup"><span data-stu-id="44181-292">If you have cloned the Azure-iot-sdk-c repository from GitHub using the --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="44181-293">Jeśli nie zostały sklonowane biblioteki, możesz go znaleźć [tutaj](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="44181-293">If you have not cloned the library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="44181-294">W bibliotece jako narzędzia udostępnione można znaleźć następujący folder:</span><span class="sxs-lookup"><span data-stu-id="44181-294">Within the shared utility library, you will find the following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="44181-295">Ten folder zawiera rozwiązania Visual Studio o nazwie **makro\_witryny\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="44181-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="44181-296">W tym rozwiązaniu program generuje **makro\_utils.h** pliku.</span><span class="sxs-lookup"><span data-stu-id="44181-296">The program in this solution generates the **macro\_utils.h** file.</span></span> <span data-ttu-id="44181-297">Brak domyślne makro\_plik utils.h dołączony do zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="44181-297">There’s a default macro\_utils.h file included with the SDK.</span></span> <span data-ttu-id="44181-298">To rozwiązanie umożliwia modyfikowanie niektórych parametrów, a następnie utwórz ponownie plik nagłówka, na podstawie tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="44181-298">This solution allows you to modify some parameters and then recreate the header file based on these parameters.</span></span>

<span data-ttu-id="44181-299">Są dwa parametry klucza zainteresowanych z **nArithmetic** i **nMacroParameters** które zostały określone w tych dwóch wierszach znaleziono w makrze\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="44181-299">The two key parameters to be concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="44181-300">Te wartości są domyślne parametry dołączone do zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="44181-300">These values are the default parameters included with the SDK.</span></span> <span data-ttu-id="44181-301">Każdy parametr ma następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="44181-301">Each parameter has the following meaning:</span></span>

* <span data-ttu-id="44181-302">nMacroParameters — Określa, ile parametrów mogą mieć w jednej instrukcji DECLARE\_definicji makra w modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="44181-303">Określa, nArithmetic — łączna liczba elementów członkowskich dozwolone w modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-303">nArithmetic – Controls the total number of members allowed in a model.</span></span>

<span data-ttu-id="44181-304">Przyczyny, dla której te parametry są ważne jest, ponieważ decydować, jak duży może być modelu.</span><span class="sxs-lookup"><span data-stu-id="44181-304">The reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="44181-305">Rozważmy na przykład tej definicji modelu:</span><span class="sxs-lookup"><span data-stu-id="44181-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="44181-306">Jak wspomniano wcześniej, **DECLARE\_modelu** jest po prostu makr C.</span><span class="sxs-lookup"><span data-stu-id="44181-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="44181-307">Nazwy modelu i **WITH\_danych** instrukcji (jeszcze innego makra) czy parametry **DECLARE\_modelu**.</span><span class="sxs-lookup"><span data-stu-id="44181-307">The names of the model and the **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="44181-308">**nMacroParameters** definiuje, ile parametry mogą być zawarte w **DECLARE\_modelu**.</span><span class="sxs-lookup"><span data-stu-id="44181-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="44181-309">W rezultacie definiuje liczbę zdarzeń i akcji deklaracjach danych może mieć.</span><span class="sxs-lookup"><span data-stu-id="44181-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="44181-310">W związku z domyślnym limitem 124 oznacza to, zdefiniować modelu z kombinacją akcji około 60 i zdarzenia danych.</span><span class="sxs-lookup"><span data-stu-id="44181-310">As such, with the default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="44181-311">Jeśli spróbujesz przekracza ten limit, otrzymasz błędów, które wyglądać podobnie do poniższego:</span><span class="sxs-lookup"><span data-stu-id="44181-311">If you try to exceed this limit, you'll receive compiler errors that look similar to this:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="44181-312">**NArithmetic** parametr jest więcej informacji na temat wewnętrzne działanie języka makro niż aplikacja.</span><span class="sxs-lookup"><span data-stu-id="44181-312">The **nArithmetic** parameter is more about the internal workings of the macro language than your application.</span></span>  <span data-ttu-id="44181-313">Kontroluje łączna liczba elementów członkowskich w modelu, mogą znajdować się w tym **DECLARE_STRUCT** makra.</span><span class="sxs-lookup"><span data-stu-id="44181-313">It controls the total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="44181-314">Jeśli możesz zacząć się wyświetlać błędy kompilatora, takich jak ta, a następnie spróbuj użyć zwiększenie **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="44181-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="44181-315">Jeśli chcesz zmienić te parametry, zmodyfikuj wartości w makrze\_utils.tt plików, skompiluj ponownie makra\_witryny\_h\_generator.sln rozwiązania, a następnie uruchom program skompilowany.</span><span class="sxs-lookup"><span data-stu-id="44181-315">If you want to change these parameters, modify the values in the macro\_utils.tt file, recompile the macro\_utils\_h\_generator.sln solution, and run the compiled program.</span></span> <span data-ttu-id="44181-316">Się nowe makro\_utils.h plik jest generowany i umieszczane w.\\ Typowe\\inc katalogu.</span><span class="sxs-lookup"><span data-stu-id="44181-316">When you do so, a new macro\_utils.h file is generated and placed in the .\\common\\inc directory.</span></span>

<span data-ttu-id="44181-317">Aby można było używać nowej wersji makro\_utils.h, Usuń **serializator** obejmują pakietu NuGet z rozwiązania i w jego miejsce **serializator** projekt programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44181-317">In order to use the new version of macro\_utils.h, remove the **serializer** NuGet package from your solution and in its place include the **serializer** Visual Studio project.</span></span> <span data-ttu-id="44181-318">Dzięki temu kodu do kompilacji z kodem źródłowym biblioteki serializatora.</span><span class="sxs-lookup"><span data-stu-id="44181-318">This enables your code to compile against the source code of the serializer library.</span></span> <span data-ttu-id="44181-319">Obejmuje to makro zaktualizowane\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="44181-319">This includes the updated macro\_utils.h.</span></span> <span data-ttu-id="44181-320">Jeśli chcesz to zrobić **simplesample\_amqp**, uruchom przez usunięcie pakietu NuGet dla biblioteki serializator z rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="44181-320">If you want to do this for **simplesample\_amqp**, start by removing the NuGet package for the serializer library from the solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="44181-321">Następnie dodaj ten projekt do rozwiązania Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="44181-321">Then add this project to your Visual Studio solution:</span></span>

> <span data-ttu-id="44181-322">. \\c\\serializator\\kompilacji\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="44181-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="44181-323">Gdy wszystko będzie gotowe rozwiązanie powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="44181-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="44181-324">Teraz podczas kompilowania rozwiązania zaktualizowane makro\_utils.h znajduje się w sieci danych binarnych.</span><span class="sxs-lookup"><span data-stu-id="44181-324">Now when you compile your solution, the updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="44181-325">Należy pamiętać, że zwiększenie wartości wystarczająco wysoka, może być dłuższa niż limity kompilatora.</span><span class="sxs-lookup"><span data-stu-id="44181-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="44181-326">W tym punkcie **nMacroParameters** parametru głównego, z którą zainteresowanym.</span><span class="sxs-lookup"><span data-stu-id="44181-326">To this point, the **nMacroParameters** is the main parameter with which to be concerned.</span></span> <span data-ttu-id="44181-327">Specyfikacja C99 Określa, czy co najmniej 127 parametrów są dozwolone w definicji makra.</span><span class="sxs-lookup"><span data-stu-id="44181-327">The C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="44181-328">Kompilator Microsoft następuje specyfikację dokładnie (i ma limit 127), więc nie można zwiększyć **nMacroParameters** ponad wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="44181-328">The Microsoft compiler follows the spec exactly (and has a limit of 127), so you won't be able to increase **nMacroParameters** beyond the default.</span></span> <span data-ttu-id="44181-329">Inne kompilatory może zezwalać na zrobić (na przykład kompilatora GNU obsługuje wyższy limit).</span><span class="sxs-lookup"><span data-stu-id="44181-329">Other compilers might allow you to do so (for example, the GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="44181-330">Do tej pory możemy zostały omówione prawie wszystko, co należy wiedzieć o tym, jak napisać kod z **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="44181-330">So far we've covered just about everything you need to know about how to write code with the **serializer** library.</span></span> <span data-ttu-id="44181-331">Przed zawierania, możemy ponownie niektóre tematy z poprzednich artykułów, które możesz się zastanawiać, informacje.</span><span class="sxs-lookup"><span data-stu-id="44181-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="44181-332">Interfejsy API niższego poziomu</span><span class="sxs-lookup"><span data-stu-id="44181-332">The lower-level APIs</span></span>
<span data-ttu-id="44181-333">Przykładowa aplikacja, na którym ten artykuł skupia się **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="44181-333">The sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="44181-334">W przykładzie użyto wyższego poziomu (z systemem innym niż — "wszystko") interfejsy API służące do wysyłania zdarzeń i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="44181-334">This sample uses the higher-level (the non-"LL") APIs to send events and receive messages.</span></span> <span data-ttu-id="44181-335">Korzystając z poniższych interfejsów API, uruchamia wątku w tle, który zajmuje się zarówno zdarzenia wysyłania i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="44181-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="44181-336">Jednak można użyć interfejsów API niższego poziomu (wszystkie), aby wyeliminować ten wątek w tle, a następnie jawną kontrolę nad wysłanie zdarzenia lub odbieranie komunikatów z chmury.</span><span class="sxs-lookup"><span data-stu-id="44181-336">However, you can use the lower-level (LL) APIs to eliminate this background thread and take explicit control over when you send events or receive messages from the cloud.</span></span>

<span data-ttu-id="44181-337">Zgodnie z opisem w [poprzednim artykule](iot-hub-device-sdk-c-iothubclient.md), istnieje zestaw funkcji, która składa się z wyższego poziomu interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="44181-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of the higher-level APIs:</span></span>

* <span data-ttu-id="44181-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="44181-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="44181-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="44181-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="44181-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="44181-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="44181-341">IoTHubClient\_zniszczyć</span><span class="sxs-lookup"><span data-stu-id="44181-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="44181-342">Te interfejsy API przedstawiono w części **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="44181-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="44181-343">Istnieje również analogiczne zestaw interfejsów API niższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="44181-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="44181-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="44181-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="44181-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="44181-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="44181-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="44181-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="44181-347">IoTHubClient\_LL\_zniszczyć</span><span class="sxs-lookup"><span data-stu-id="44181-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="44181-348">Należy pamiętać, interfejsy API niższego poziomu pracować dokładnie tak samo, zgodnie z opisem w poprzedniej artykułów.</span><span class="sxs-lookup"><span data-stu-id="44181-348">Note that the lower-level APIs work exactly the same way as described in the previous articles.</span></span> <span data-ttu-id="44181-349">Jeśli chcesz, aby wątku w tle do obsługi zdarzeń wysyłanie i odbieranie wiadomości, można użyć pierwszy zestaw interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="44181-349">You can use the first set of APIs if you want a background thread to handle sending events and receiving messages.</span></span> <span data-ttu-id="44181-350">Drugi zestaw interfejsów API można użyć, jeśli możesz jawną kontrolę nad podczas wysyłania i odbierania danych z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="44181-350">You use the second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="44181-351">Albo zestaw interfejsów API pracy jednakowo oraz z **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="44181-351">Either set of APIs work equally well with the **serializer** library.</span></span>

<span data-ttu-id="44181-352">Przykład użycia interfejsów API niższego poziomu z **serializator** biblioteki, zobacz **simplesample\_http** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44181-352">For an example of how the lower-level APIs are used with the **serializer** library, see the **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="44181-353">Tematy dodatkowe</span><span class="sxs-lookup"><span data-stu-id="44181-353">Additional topics</span></span>
<span data-ttu-id="44181-354">Kilka innych tematów, warto zauważyć, są ponownie właściwości obsługi, przy użyciu poświadczeń alternatywnych urządzenia i opcje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="44181-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="44181-355">Są to wszystkie tematy objęte [poprzednim artykule](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="44181-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="44181-356">Jest głównym punktem, czy wszystkie te funkcje działają tak samo jak z **serializator** biblioteki co z **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="44181-356">The main point is that all of these features work in the same way with the **serializer** library as they do with the **IoTHubClient** library.</span></span> <span data-ttu-id="44181-357">Na przykład, jeśli chcesz dołączyć właściwości na zdarzenie z modelu, należy użyć **IoTHubMessage\_właściwości** i **mapy**\_**AddorUpdate**, tak samo, jak opisano wcześniej:</span><span class="sxs-lookup"><span data-stu-id="44181-357">For example, if you want to attach properties to an event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, the same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="44181-358">Czy to zdarzenie zostało wygenerowane z **serializator** biblioteki lub utworzone ręcznie za pomocą **IoTHubClient** biblioteki nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="44181-358">Whether the event was generated from the **serializer** library or created manually using the **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="44181-359">W przypadku poświadczeń alternatywnych urządzenia przy użyciu **IoTHubClient\_LL\_Utwórz** działa równie dobrze jako **IoTHubClient\_CreateFromConnectionString** dla przydzielanie **Centrum IOTHUB\_klienta\_obsługi**.</span><span class="sxs-lookup"><span data-stu-id="44181-359">For the alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="44181-360">Ponadto jeśli używasz **serializator** biblioteki, można ustawić opcji konfiguracji z **IoTHubClient\_LL\_SetOption** podobnie jak w przypadku korzystania z **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="44181-360">Finally, if you're using the **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using the **IoTHubClient** library.</span></span>

<span data-ttu-id="44181-361">Funkcja, która jest unikatowa dla **serializator** biblioteki są inicjowania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="44181-361">A feature that is unique to the **serializer** library are the initialization APIs.</span></span> <span data-ttu-id="44181-362">Przed rozpoczęciem pracy z biblioteki, należy wywołać **serializator\_init**:</span><span class="sxs-lookup"><span data-stu-id="44181-362">Before you can start working with the library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="44181-363">Jest to realizowane tylko przed wywołaniem **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="44181-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="44181-364">Podobnie, po zakończeniu pracy z biblioteki, jest ostatnim wywołaniu, które należy podjąć do **serializator\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="44181-364">Similarly, when you're done working with the library, the last call you’ll make is to **serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="44181-365">W przeciwnym razie wszystkie inne funkcje wymienione powyżej działać w identyczny **serializator** biblioteki tak jak w **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="44181-365">Otherwise, all of the other features listed above work the same in the **serializer** library as they do in the **IoTHubClient** library.</span></span> <span data-ttu-id="44181-366">Aby uzyskać więcej informacji o tych tematów, zobacz [poprzednim artykule](iot-hub-device-sdk-c-iothubclient.md) w tej serii.</span><span class="sxs-lookup"><span data-stu-id="44181-366">For more information about any of these topics, see the [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44181-367">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="44181-367">Next steps</span></span>
<span data-ttu-id="44181-368">W tym artykule opisano szczegółowo unikatowe aspekty **serializator** zawartych w bibliotece **urządzenia Azure IoT SDK dla języka C**. Z informacjami pod warunkiem, że powinien dysponować dobrą znajomością używania modeli do wysyłania zdarzeń i odbieranie komunikatów z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="44181-368">This article describes in detail the unique aspects of the **serializer** library contained in the **Azure IoT device SDK for C**. With the information provided you should have a good understanding of how to use models to send events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="44181-369">Teraz również serii trzech części o tworzeniu aplikacji za pomocą **urządzenia Azure IoT SDK dla języka C**. Powinno to być wystarczających informacji do nie tylko ułatwiające rozpoczęcie pracy, ale umożliwiają dokładne zrozumienie działania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="44181-369">This also concludes the three-part series on how to develop applications with the **Azure IoT device SDK for C**. This should be enough information to not only get you started but give you a thorough understanding of how the APIs work.</span></span> <span data-ttu-id="44181-370">Aby uzyskać dodatkowe informacje istnieje kilka przykładów w zestawie SDK nie pasuje do tutaj.</span><span class="sxs-lookup"><span data-stu-id="44181-370">For additional information, there are a few samples in the SDK not covered here.</span></span> <span data-ttu-id="44181-371">W przeciwnym razie [dokumentacji zestawu SDK](https://github.com/Azure/azure-iot-sdk-c) jest dobrym zasobów, aby uzyskać dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="44181-371">Otherwise, the [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="44181-372">Aby dowiedzieć się więcej o tworzeniu aplikacji Centrum IoT, zobacz [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="44181-372">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="44181-373">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="44181-373">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="44181-374">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="44181-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
