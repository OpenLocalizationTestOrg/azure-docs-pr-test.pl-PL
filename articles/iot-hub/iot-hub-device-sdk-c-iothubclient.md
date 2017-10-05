---
title: "Azure urządzenia IoT zestawu SDK dla języka C - IoTHubClient | Dokumentacja firmy Microsoft"
description: "Jak używać biblioteki IoTHubClient na urządzeniu Azure IoT SDK dla języka C do tworzenia aplikacji urządzenia, które komunikują się z Centrum IoT."
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
ms.openlocfilehash: 422d89014511f0d08ba57a893570ff7b253b7bc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="1e582-103">Azure urządzenia IoT zestawu SDK dla języka C — więcej informacji na temat IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="1e582-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="1e582-104">[Najpierw artykuł](iot-hub-device-sdk-c-intro.md) w tej serii wprowadzone **urządzenia Azure IoT SDK dla języka C**. Tym artykule wyjaśniono, że istnieją dwie warstwy architektury w zestawie SDK.</span><span class="sxs-lookup"><span data-stu-id="1e582-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="1e582-105">Na podstawowym jest **IoTHubClient** biblioteki, który bezpośrednio prowadzi komunikację z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1e582-105">At the base is the **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="1e582-106">Istnieje również **serializator** biblioteki, która tworzy znajdujący się na świadczenie usług serializacji.</span><span class="sxs-lookup"><span data-stu-id="1e582-106">There's also the **serializer** library that builds on top of that to provide serialization services.</span></span> <span data-ttu-id="1e582-107">W tym artykule udostępnimy dodatkowych szczegółów na **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="1e582-107">In this article we'll provide additional detail on the **IoTHubClient** library.</span></span>

<span data-ttu-id="1e582-108">Poprzednim artykule opisano sposób użycia **IoTHubClient** biblioteki do wysyłania zdarzeń do Centrum IoT i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1e582-108">The previous article described how to use the **IoTHubClient** library to send events to IoT Hub and receive messages.</span></span> <span data-ttu-id="1e582-109">W tym artykule rozszerza tej dyskusji, wyjaśniający, bardziej precyzyjne zarządzanie *podczas* wysyłania i odbierania danych, wprowadzenie do **interfejsów API niższego poziomu**.</span><span class="sxs-lookup"><span data-stu-id="1e582-109">This article extends that discussion by explaining how to more precisely manage *when* you send and receive data, introducing you to the **lower-level APIs**.</span></span> <span data-ttu-id="1e582-110">Prezentujemy również zasady do dołączania właściwości zdarzenia (i pobrać wiadomości) przy użyciu właściwości obsługi funkcji w **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="1e582-110">We'll also explain how to attach properties to events (and retrieve them from messages) using the property handling features in the **IoTHubClient** library.</span></span> <span data-ttu-id="1e582-111">Ponadto firma Microsoft udostępni dodatkowe objaśnienia dotyczące obsługi komunikatów odebranych z Centrum IoT na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="1e582-111">Finally, we'll provide additional explanation of different ways to handle messages received from IoT Hub.</span></span>

<span data-ttu-id="1e582-112">Artykuł zawiera przez kilka dodatkowych tematy, w tym więcej o poświadczenia urządzenia oraz sposobu zmiany zachowanie obejmujących **IoTHubClient** za pomocą opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1e582-112">The article concludes by covering a couple of miscellaneous topics, including more about device credentials and how to change the behavior of the **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="1e582-113">Użyjemy **IoTHubClient** te tematy wyjaśniają próbek zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="1e582-113">We'll use the **IoTHubClient** SDK samples to explain these topics.</span></span> <span data-ttu-id="1e582-114">Jeśli chcesz z niego skorzystać, zobacz **Centrum iothub\_klienta\_próbki\_http** i **Centrum iothub\_klienta\_próbki\_amqp**aplikacji, które znajdują się w urządzeniu Azure IoT SDK dla C. wszystkie elementy opisane w poniższych sekcjach przedstawiono w te przykłady.</span><span class="sxs-lookup"><span data-stu-id="1e582-114">If you want to follow along, see the **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in the Azure IoT device SDK for C. Everything described in the following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="1e582-115">Można znaleźć [ **urządzenia Azure IoT SDK dla języka C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repozytorium i wyświetlenia jej szczegółów interfejsu API w [dokumentacja interfejsu API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="1e582-115">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="1e582-116">Interfejsy API niższego poziomu</span><span class="sxs-lookup"><span data-stu-id="1e582-116">The lower-level APIs</span></span>
<span data-ttu-id="1e582-117">Poprzednim artykule opisano podstawowe operacje **IotHubClient** w kontekście **Centrum iothub\_klienta\_próbki\_amqp** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e582-117">The previous article described the basic operation of the **IotHubClient** within the context of the **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="1e582-118">Na przykład jego objaśniono, w jaki można zainicjować biblioteki przy użyciu tego kodu.</span><span class="sxs-lookup"><span data-stu-id="1e582-118">For example, it explained how to initialize the library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="1e582-119">On również opisany sposób wysyłania zdarzeń za pomocą tego wywołania funkcji.</span><span class="sxs-lookup"><span data-stu-id="1e582-119">It also described how to send events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="1e582-120">Tego artykułu opisano również jak odbierać komunikaty, rejestrując funkcję wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="1e582-120">The article also described how to receive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="1e582-121">Artykuł również pokazano, jak można zwolnić zasobów przy użyciu następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="1e582-121">The article also showed how to free resources using code such as the following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="1e582-122">Istnieją jednak funkcji pomocnika do każdego z poniższych interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="1e582-122">However there are companion functions to each of these APIs:</span></span>

* <span data-ttu-id="1e582-123">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="1e582-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="1e582-124">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="1e582-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="1e582-125">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="1e582-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="1e582-126">IoTHubClient\_LL\_zniszczyć</span><span class="sxs-lookup"><span data-stu-id="1e582-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="1e582-127">Wszystkie funkcje te obejmują "Wszystko" w nazwie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1e582-127">These functions all include “LL” in the API name.</span></span> <span data-ttu-id="1e582-128">Inną niż parametry każda z tych funkcji są takie same jak ich odpowiedniki nie wszystko.</span><span class="sxs-lookup"><span data-stu-id="1e582-128">Other than that, the parameters of each of these functions are identical to their non-LL counterparts.</span></span> <span data-ttu-id="1e582-129">Jednak działanie tych funkcji różni się w jednym ze sposobów ważne.</span><span class="sxs-lookup"><span data-stu-id="1e582-129">However, the behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="1e582-130">Podczas wywoływania **IoTHubClient\_CreateFromConnectionString**, podstawowe biblioteki utworzyć nowego wątku, który działa w tle.</span><span class="sxs-lookup"><span data-stu-id="1e582-130">When you call **IoTHubClient\_CreateFromConnectionString**, the underlying libraries create a new thread that runs in the background.</span></span> <span data-ttu-id="1e582-131">Wysyła zdarzenia do tego wątku i odbiera komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1e582-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="1e582-132">Nie takiego wątku jest tworzony podczas pracy z interfejsów API "wszystko".</span><span class="sxs-lookup"><span data-stu-id="1e582-132">No such thread is created when working with the "LL" APIs.</span></span> <span data-ttu-id="1e582-133">Tworzenie wątku w tle jest wygodne do deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1e582-133">The creation of the background thread is a convenience to the developer.</span></span> <span data-ttu-id="1e582-134">Nie trzeba martwić jawnie wysyłanie zdarzeń i odbieranie komunikatów z Centrum IoT — wykonywane automatycznie w tle.</span><span class="sxs-lookup"><span data-stu-id="1e582-134">You don’t have to worry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in the background.</span></span> <span data-ttu-id="1e582-135">Z kolei "Wszystko" interfejsów API zapewniają jawne kontroluje komunikację z Centrum IoT, jeśli zajdzie taka potrzeba.</span><span class="sxs-lookup"><span data-stu-id="1e582-135">In contrast, the "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="1e582-136">Aby lepiej zrozumieć to, Przyjrzyjmy się przykładem:</span><span class="sxs-lookup"><span data-stu-id="1e582-136">To understand this better, let’s look at an example:</span></span>

<span data-ttu-id="1e582-137">Podczas wywoływania **IoTHubClient\_SendEventAsync**, co faktycznie robimy obciążające zdarzenia w buforze.</span><span class="sxs-lookup"><span data-stu-id="1e582-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting the event in a buffer.</span></span> <span data-ttu-id="1e582-138">Wątek w tle tworzone podczas wywoływania **IoTHubClient\_CreateFromConnectionString** stale monitoruje buforu i wysyła on żadnych danych do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1e582-138">The background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains to IoT Hub.</span></span> <span data-ttu-id="1e582-139">Dzieje się w tle w tym samym czasie, że wątku głównego jest wykonywać inne zadania.</span><span class="sxs-lookup"><span data-stu-id="1e582-139">This happens in the background at the same time that the main thread is performing other work.</span></span>

<span data-ttu-id="1e582-140">Podobnie po rejestracji funkcję wywołania zwrotnego dla wiadomości przy użyciu **IoTHubClient\_SetMessageCallback**, jest poinstruowanie zestaw SDK, aby mieć wywołania funkcji wywołania zwrotnego, gdy komunikat jest wątku w tle Odebrano, niezależnie od wątku głównego.</span><span class="sxs-lookup"><span data-stu-id="1e582-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing the SDK to have the background thread invoke the callback function when a message is received, independent of the main thread.</span></span>

<span data-ttu-id="1e582-141">"Wszystkie" interfejsów API nie należy tworzyć wątku w tle.</span><span class="sxs-lookup"><span data-stu-id="1e582-141">The "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="1e582-142">Zamiast tego nowy interfejs API musi zostać wywołany jawnie wysyłanie i odbieranie danych z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1e582-142">Instead, a new API must be called to explicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="1e582-143">Jest to pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1e582-143">This is demonstrated in the following example.</span></span>

<span data-ttu-id="1e582-144">**Centrum iothub\_klienta\_próbki\_http** aplikacji, który znajduje się w zestawie SDK pokazuje interfejsów API niższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="1e582-144">The **iothub\_client\_sample\_http** application that’s included in the SDK demonstrates the lower-level APIs.</span></span> <span data-ttu-id="1e582-145">W tym przykładzie mamy wysyłania zdarzeń do Centrum IoT z kodem, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="1e582-145">In that sample, we send events to IoT Hub with code such as the following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="1e582-146">Pierwsze trzy wiersze utworzyć komunikat, a ostatni wiersz wysyła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="1e582-146">The first three lines create the message, and the last line sends the event.</span></span> <span data-ttu-id="1e582-147">Jednak jak już wspomniano, "Wysyłanie" zdarzenie oznacza, że dane są po prostu umieszczane w buforze.</span><span class="sxs-lookup"><span data-stu-id="1e582-147">However, as mentioned previously, "sending" the event means that the data is simply placed in a buffer.</span></span> <span data-ttu-id="1e582-148">Nic nie jest przesyłane w sieci, gdy taki stan nazywa się **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="1e582-148">Nothing is transmitted on the network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="1e582-149">Aby rzeczywiście transferu danych do Centrum IoT, należy wywołać **IoTHubClient\_LL\_DoWork**w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="1e582-149">In order to actually ingress the data to IoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="1e582-150">Ten kod (z **Centrum iothub\_klienta\_próbki\_http** aplikacji) wielokrotnie wywołuje **IoTHubClient\_LL\_DoWork**.</span><span class="sxs-lookup"><span data-stu-id="1e582-150">This code (from the **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="1e582-151">Zawsze **IoTHubClient\_LL\_DoWork** jest wywoływana, wysyła niektórych zdarzeń z buforu do Centrum IoT i pobiera ona wiadomość w kolejce są wysyłane do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1e582-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from the buffer to IoT Hub and it retrieves a queued message being sent to the device.</span></span> <span data-ttu-id="1e582-152">Drugim przypadku oznacza to, że jeśli firma Microsoft zarejestrowana funkcja wywołania zwrotnego dla wiadomości, następnie wywołania zwrotnego została wywołana (przy założeniu, że komunikaty są umieszczone w kolejce).</span><span class="sxs-lookup"><span data-stu-id="1e582-152">The latter case means that if we registered a callback function for messages, then the callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="1e582-153">Firma Microsoft będzie zarejestrowanych funkcję wywołania zwrotnego z kodem, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="1e582-153">We would have registered such a callback function with code such as the following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="1e582-154">Powód który **IoTHubClient\_LL\_DoWork** jest często nazywana pętli jest to, że zawsze jest nazywana, wysyła *niektórych* buforowane zdarzenia do Centrum IoT i pobiera *następne* wiadomości w kolejce dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1e582-154">The reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events to IoT Hub and retrieves *the next* message queued up for the device.</span></span> <span data-ttu-id="1e582-155">Każde wywołanie nie jest gwarantowana do wysłania wszystkich buforowanych zdarzeń lub pobranie wszystkich wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="1e582-155">Each call isn’t guaranteed to send all buffered events or to retrieve all queued messages.</span></span> <span data-ttu-id="1e582-156">Jeśli chcesz wysłać wszystkie zdarzenia w buforze, a następnie kontynuuj na inne przetwarzania można zastąpić tę pętlę kodu, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="1e582-156">If you want to send all events in the buffer and then continue on with other processing you can replace this loop with code such as the following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="1e582-157">Ten kod wywołuje **IoTHubClient\_LL\_DoWork** dopóki wszystkie zdarzenia w buforze zostały wysłane do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1e582-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in the buffer have been sent to IoT Hub.</span></span> <span data-ttu-id="1e582-158">Należy pamiętać, że nie również oznacza otrzymanie wszystkie wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="1e582-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="1e582-159">Część przyczynę jest, że sprawdzanie komunikatów "all" nie jest deterministyczna jako akcję.</span><span class="sxs-lookup"><span data-stu-id="1e582-159">Part of the reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="1e582-160">Co się stanie, jeśli pobrać "wszystkie" wiadomości, ale następnie inny jest wysyłane do urządzenia bezpośrednio po?</span><span class="sxs-lookup"><span data-stu-id="1e582-160">What happens if you retrieve "all" of the messages, but then another one is sent to the device immediately after?</span></span> <span data-ttu-id="1e582-161">Lepszy sposób postępowania w przypadku z zaprogramowanych limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="1e582-161">A better way to deal with that is with a programmed timeout.</span></span> <span data-ttu-id="1e582-162">Na przykład funkcja wywołania zwrotnego komunikat można zresetować czasomierz za każdym razem, gdy jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="1e582-162">For example, the message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="1e582-163">Następnie można napisać logiki, aby kontynuować przetwarzanie, jeśli na przykład żadnych komunikatów nie odebrano w ciągu ostatnich *X* sekund.</span><span class="sxs-lookup"><span data-stu-id="1e582-163">You can then write logic to continue processing if, for example, no messages have been received in the last *X* seconds.</span></span>

<span data-ttu-id="1e582-164">Gdy jest ingressing gotowego zdarzenia i odbieranie komunikatów, należy wywołać funkcję odpowiednie, aby wyczyścić zasoby.</span><span class="sxs-lookup"><span data-stu-id="1e582-164">When you’re finished ingressing events and receiving messages, be sure to call the corresponding function to clean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="1e582-165">Zasadniczo jest tylko jeden zestaw interfejsów API, aby wysyłać i odbierać dane z wątku w tle i inny zestaw interfejsów API, które jest równoznaczne bez wątku w tle.</span><span class="sxs-lookup"><span data-stu-id="1e582-165">Basically there’s only one set of APIs to send and receive data with a background thread and another set of APIs that does the same thing without the background thread.</span></span> <span data-ttu-id="1e582-166">Wiele deweloperzy mogą preferować z systemem innym niż — wszystkie interfejsy API, ale interfejsów API niższego poziomu są przydatne, jeśli deweloper chce jawną kontrolę nad transmisji w sieci.</span><span class="sxs-lookup"><span data-stu-id="1e582-166">A lot of developers may prefer the non-LL APIs, but the lower-level APIs are useful when the developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="1e582-167">Na przykład niektóre urządzenia zbieranie danych przez czasu i zdarzeń wejściowych tylko w określonych odstępach czasu (na przykład, jeden raz na godzinę lub raz dziennie).</span><span class="sxs-lookup"><span data-stu-id="1e582-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="1e582-168">Interfejsy API niższego poziomu dać możliwość kontroli jawnie, wysyłania i odbierania danych z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1e582-168">The lower-level APIs give you the ability to explicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="1e582-169">Inne po prostu preferowane prostotę, które zapewniają interfejsów API niższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="1e582-169">Others will simply prefer the simplicity that the lower-level APIs provide.</span></span> <span data-ttu-id="1e582-170">Wszystko, co się stanie w wątku głównego zamiast niektórych pracy w toku w tle.</span><span class="sxs-lookup"><span data-stu-id="1e582-170">Everything happens on the main thread rather than some work happening in the background.</span></span>

<span data-ttu-id="1e582-171">Niezależnie od tego modelu, należy wybrać, pamiętaj zachować spójność interfejsów API, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="1e582-171">Whichever model you choose, be sure to be consistent in which APIs you use.</span></span> <span data-ttu-id="1e582-172">Po uruchomieniu przez wywołanie metody **IoTHubClient\_LL\_CreateFromConnectionString**, należy korzystać jedynie odpowiednich interfejsów API niższego poziomu kolejnych pracę:</span><span class="sxs-lookup"><span data-stu-id="1e582-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use the corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="1e582-173">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="1e582-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="1e582-174">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="1e582-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="1e582-175">IoTHubClient\_LL\_zniszczyć</span><span class="sxs-lookup"><span data-stu-id="1e582-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="1e582-176">IoTHubClient\_LL\_DoWork</span><span class="sxs-lookup"><span data-stu-id="1e582-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="1e582-177">Wartość true, jest również odwrotny.</span><span class="sxs-lookup"><span data-stu-id="1e582-177">The opposite is true as well.</span></span> <span data-ttu-id="1e582-178">Jeśli na początku zasubskrybujesz **IoTHubClient\_CreateFromConnectionString**, następnie użyć z systemem innym niż — wszystkie interfejsy API dla dowolnego dodatkowego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="1e582-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use the non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="1e582-179">Na urządzeniu Azure IoT SDK dla języka C, zobacz **Centrum iothub\_klienta\_próbki\_http** aplikacji pełny przykład interfejsów API niższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="1e582-179">In the Azure IoT device SDK for C, see the **iothub\_client\_sample\_http** application for a complete example of the lower-level APIs.</span></span> <span data-ttu-id="1e582-180">**Centrum iothub\_klienta\_próbki\_amqp** aplikacji można odwoływać się na przykład Pełna z innych niż — wszystkie interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="1e582-180">The **iothub\_client\_sample\_amqp** application can be referenced for a full example of the non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="1e582-181">Obsługa właściwości</span><span class="sxs-lookup"><span data-stu-id="1e582-181">Property handling</span></span>
<span data-ttu-id="1e582-182">Do tej pory gdy mamy już opisane wysyłanie danych, firma Microsoft już został odwołujących się do treści wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1e582-182">So far when we've described sending data, we've been referring to the body of the message.</span></span> <span data-ttu-id="1e582-183">Rozważmy na przykład ten kod:</span><span class="sxs-lookup"><span data-stu-id="1e582-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="1e582-184">W tym przykładzie wysyła komunikat do Centrum IoT na tekst "Hello World".</span><span class="sxs-lookup"><span data-stu-id="1e582-184">This example sends a message to IoT Hub with the text "Hello World."</span></span> <span data-ttu-id="1e582-185">Centrum IoT umożliwia także właściwości, które mają być dołączone do każdej wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1e582-185">However, IoT Hub also allows properties to be attached to each message.</span></span> <span data-ttu-id="1e582-186">Właściwości są pary nazwa/wartość, które można dołączyć do wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1e582-186">Properties are name/value pairs that can be attached to the message.</span></span> <span data-ttu-id="1e582-187">Możemy na przykład zmodyfikować poprzedni kod można dołączyć właściwości komunikat:</span><span class="sxs-lookup"><span data-stu-id="1e582-187">For example, we can modify the previous code to attach a property to the message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="1e582-188">Rozpoczniemy wywołując **IoTHubMessage\_właściwości** i przekazanie jej przez dojście wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1e582-188">We start by calling **IoTHubMessage\_Properties** and passing it the handle of our message.</span></span> <span data-ttu-id="1e582-189">Co mamy wrócić jest **mapy\_obsługi** odwołania, który pozwala rozpocząć dodawanie właściwości.</span><span class="sxs-lookup"><span data-stu-id="1e582-189">What we get back is a **MAP\_HANDLE** reference that enables us to start adding properties.</span></span> <span data-ttu-id="1e582-190">Drugie odbywa się przez wywołanie metody **mapy\_AddOrUpdate**, który przyjmuje odwołanie do mapy\_UCHWYTU, nazwa właściwości i wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="1e582-190">The latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference to a MAP\_HANDLE, the property name, and the property value.</span></span> <span data-ttu-id="1e582-191">W tym interfejsie API można dodać dowolną liczbę właściwości, jak firma Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e582-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="1e582-192">Gdy zdarzenie zostanie odczytany z **usługi Event Hubs**, odbiorca może wyliczenia właściwości i pobieranie ich wartości.</span><span class="sxs-lookup"><span data-stu-id="1e582-192">When the event is read from **Event Hubs**, the receiver can enumerate the properties and retrieve their corresponding values.</span></span> <span data-ttu-id="1e582-193">Na przykład w środowisku .NET to może osiągnąć, uzyskując dostęp do [kolekcji właściwości w obiekcie EventData](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e582-193">For example, in .NET this would be accomplished by accessing the [Properties collection on the EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="1e582-194">W poprzednim przykładzie możemy Cię dołączanie właściwości do zdarzenia, możemy wysyłać do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1e582-194">In the previous example, we’re attaching properties to an event that we send to IoT Hub.</span></span> <span data-ttu-id="1e582-195">Ponadto można dołączyć właściwości do komunikatów odebranych z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1e582-195">Properties can also be attached to messages received from IoT Hub.</span></span> <span data-ttu-id="1e582-196">Jeśli chcemy, aby pobrać właściwości z komunikatu, możemy użyć następującego kodu w naszej funkcji wywołania zwrotnego komunikat:</span><span class="sxs-lookup"><span data-stu-id="1e582-196">If we want to retrieve properties from a message, we can use code such as the following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from the message
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

<span data-ttu-id="1e582-197">Wywołanie **IoTHubMessage\_właściwości** zwraca **mapy\_obsługi** odwołania.</span><span class="sxs-lookup"><span data-stu-id="1e582-197">The call to **IoTHubMessage\_Properties** returns the **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="1e582-198">Następnie jest przekazywana odwołujące się do **mapy\_GetInternals** uzyskać odwołanie do tablicy pary nazwa/wartość (a także liczbę właściwości).</span><span class="sxs-lookup"><span data-stu-id="1e582-198">We then pass that reference to **Map\_GetInternals** to obtain a reference to an array of the name/value pairs (as well as a count of the properties).</span></span> <span data-ttu-id="1e582-199">W tym momencie jest polegać wyliczania właściwości, aby uzyskać dostęp do wartości, którą chcemy udostępnić.</span><span class="sxs-lookup"><span data-stu-id="1e582-199">At that point it's a simple matter of enumerating the properties to get to the values we want.</span></span>

<span data-ttu-id="1e582-200">Nie trzeba używać właściwości w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e582-200">You don't have to use properties in your application.</span></span> <span data-ttu-id="1e582-201">Jednak, aby ustawić je na zdarzenia lub pobrać je z wiadomości, **IoTHubClient** biblioteki ułatwia.</span><span class="sxs-lookup"><span data-stu-id="1e582-201">However, if you need to set them on events or retrieve them from messages, the **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="1e582-202">Komunikat — Obsługa</span><span class="sxs-lookup"><span data-stu-id="1e582-202">Message handling</span></span>
<span data-ttu-id="1e582-203">Jak wspomniano wcześniej, gdy nadchodzą komunikaty z Centrum IoT **IoTHubClient** Biblioteka odpowiada za pomocą zarejestrowana funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="1e582-203">As stated previously, when messages arrive from IoT Hub the **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="1e582-204">Brak parametru zwrotnego tej funkcji, która wymaga dodatkowych wyjaśnień.</span><span class="sxs-lookup"><span data-stu-id="1e582-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="1e582-205">Oto fragment funkcja wywołania zwrotnego w **Centrum iothub\_klienta\_próbki\_http** aplikacji przykładowej:</span><span class="sxs-lookup"><span data-stu-id="1e582-205">Here’s an excerpt of the callback function in the **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="1e582-206">Należy pamiętać, że typ zwracany jest **IOTHUBMESSAGE\_DYSPOZYCJI\_wynik** w tym przypadku zostanie zwrócona **IOTHUBMESSAGE\_ZAAKCEPTOWANE**.</span><span class="sxs-lookup"><span data-stu-id="1e582-206">Note that the return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="1e582-207">Istnieją inne wartości firma Microsoft może zwracać z tej funkcji, które zmieniają sposób **IoTHubClient** biblioteki reaguje na wywołanie zwrotne komunikatu.</span><span class="sxs-lookup"><span data-stu-id="1e582-207">There are other values we can return from this function that change how the **IoTHubClient** library reacts to the message callback.</span></span> <span data-ttu-id="1e582-208">Poniżej przedstawiono opcje.</span><span class="sxs-lookup"><span data-stu-id="1e582-208">Here are the options.</span></span>

* <span data-ttu-id="1e582-209">**IOTHUBMESSAGE\_ZAAKCEPTOWANE** — komunikat został pomyślnie przetworzony.</span><span class="sxs-lookup"><span data-stu-id="1e582-209">**IOTHUBMESSAGE\_ACCEPTED** – The message has been processed successfully.</span></span> <span data-ttu-id="1e582-210">**IoTHubClient** biblioteki nie wywoła funkcję wywołania zwrotnego ponownie, podając tę samą wiadomość.</span><span class="sxs-lookup"><span data-stu-id="1e582-210">The **IoTHubClient** library will not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="1e582-211">**IOTHUBMESSAGE\_ODRZUCONE** — wiadomość nie została przetworzona, i chcesz to zrobić w przyszłości nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="1e582-211">**IOTHUBMESSAGE\_REJECTED** – The message was not processed and there is no desire to do so in the future.</span></span> <span data-ttu-id="1e582-212">**IoTHubClient** biblioteki nie powinna wywołać funkcję wywołania zwrotnego ponownie, podając tę samą wiadomość.</span><span class="sxs-lookup"><span data-stu-id="1e582-212">The **IoTHubClient** library should not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="1e582-213">**IOTHUBMESSAGE\_ABANDONED** — wiadomość nie została przetworzona pomyślnie, ale **IoTHubClient** biblioteki należy wywołać funkcję wywołania zwrotnego ponownie, podając tę samą wiadomość.</span><span class="sxs-lookup"><span data-stu-id="1e582-213">**IOTHUBMESSAGE\_ABANDONED** – The message was not processed successfully, but the **IoTHubClient** library should invoke the callback function again with the same message.</span></span>

<span data-ttu-id="1e582-214">Dla dwóch pierwszych zwraca kody, **IoTHubClient** biblioteki wysyła komunikat do Centrum IoT informujący, że usuwane z kolejki urządzenia i nie można dostarczyć ponownie wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1e582-214">For the first two return codes, the **IoTHubClient** library sends a message to IoT Hub indicating that the message should be deleted from the device queue and not delivered again.</span></span> <span data-ttu-id="1e582-215">Net efekt jest taki sam (komunikat jest usuwany z kolejki urządzenia), ale nadal jest rejestrowany czy zaakceptowane lub odrzucone wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1e582-215">The net effect is the same (the message is deleted from the device queue), but whether the message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="1e582-216">Rejestrowanie tego rozróżnienie przydaje się do nadawców wiadomości, którzy mogą nasłuchiwać opinii i sprawdzić, czy urządzenie ma zaakceptowane lub odrzucone danego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="1e582-216">Recording this distinction is useful to senders of the message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="1e582-217">W przypadku ostatniego komunikatu jest również przesyłany do Centrum IoT, ale wskazuje, czy komunikat powinien być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="1e582-217">In the last case a message is also sent to IoT Hub, but it indicates that the message should be redelivered.</span></span> <span data-ttu-id="1e582-218">Zwykle będzie abandon komunikat, jeśli wystąpi błąd, ale chcesz spróbować ponownie przetworzyć komunikatu.</span><span class="sxs-lookup"><span data-stu-id="1e582-218">Typically you’ll abandon a message if you encounter some error but want to try to process the message again.</span></span> <span data-ttu-id="1e582-219">Z kolei odrzuca wiadomości jest odpowiednia, w przypadku wystąpienia nieodwracalnego błędu (lub po prostu zdecydować się, że nie chcesz przetworzyć komunikatu).</span><span class="sxs-lookup"><span data-stu-id="1e582-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want to process the message).</span></span>

<span data-ttu-id="1e582-220">W każdym przypadku należy pamiętać różnych kodów powrotnych, dzięki czemu można wywołać z zachowaniem **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="1e582-220">In any case, be aware of the different return codes so that you can elicit the behavior you want from the **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="1e582-221">Poświadczenia alternatywne urządzenia</span><span class="sxs-lookup"><span data-stu-id="1e582-221">Alternate device credentials</span></span>
<span data-ttu-id="1e582-222">Jak opisano wcześniej, najpierw musisz podczas pracy z **IoTHubClient** biblioteki jest uzyskanie **Centrum IOTHUB\_klienta\_obsługi** przy użyciu wywołania, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="1e582-222">As explained previously, the first thing to do when working with the **IoTHubClient** library is to obtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as the following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="1e582-223">Argumenty **IoTHubClient\_CreateFromConnectionString** są parametry połączenia urządzenia i parametrem, który wskazuje protokołu używamy w celu komunikowania się z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1e582-223">The arguments to **IoTHubClient\_CreateFromConnectionString** are the device connection string and a parameter that indicates the protocol we use to communicate with IoT Hub.</span></span> <span data-ttu-id="1e582-224">Ciąg połączenia urządzenia ma format, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="1e582-224">The device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="1e582-225">Istnieją cztery elementy informacji w tym ciągu: Nazwa centrum IoT, sufiks Centrum IoT identyfikator urządzenia i udostępniony klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="1e582-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="1e582-226">W pełni kwalifikowaną nazwę (FQDN) można uzyskać z Centrum IoT podczas tworzenia wystąpienia Centrum IoT w portalu Azure — dzięki temu można nazwę Centrum IoT (pierwsza część nazwy FQDN) i sufiksu Centrum IoT (reszty nazwy FQDN).</span><span class="sxs-lookup"><span data-stu-id="1e582-226">You obtain the fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in the Azure portal — this gives you the IoT hub name (the first part of the FQDN) and the IoT hub suffix (the rest of the FQDN).</span></span> <span data-ttu-id="1e582-227">Pobierz identyfikator urządzenia i klucza dostępu współdzielonego podczas rejestrowania urządzenia z Centrum IoT (zgodnie z opisem w [poprzednim artykule](iot-hub-device-sdk-c-intro.md)).</span><span class="sxs-lookup"><span data-stu-id="1e582-227">You get the device ID and the shared access key when you register your device with IoT Hub (as described in the [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="1e582-228">**IoTHubClient\_CreateFromConnectionString** udostępnia jeden sposób zainicjować biblioteki.</span><span class="sxs-lookup"><span data-stu-id="1e582-228">**IoTHubClient\_CreateFromConnectionString** gives you one way to initialize the library.</span></span> <span data-ttu-id="1e582-229">Jeśli wolisz, możesz utworzyć nową **Centrum IOTHUB\_klienta\_obsługi** przy użyciu tych parametrów, a nie parametry połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1e582-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than the device connection string.</span></span> <span data-ttu-id="1e582-230">Jest to osiągane następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="1e582-230">This is achieved with the following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="1e582-231">Wykonuje to samo jako **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="1e582-231">This accomplishes the same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="1e582-232">Może wydawać się oczywiste, czy chcesz użyć **IoTHubClient\_CreateFromConnectionString** zamiast tego pełniejsze metody inicjowania.</span><span class="sxs-lookup"><span data-stu-id="1e582-232">It may seem obvious that you would want to use **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="1e582-233">Należy pamiętać, że podczas rejestrowania urządzenia w Centrum IoT można pobrać jest identyfikator urządzenia i klucz urządzenia (nie w ciągu połączenia).</span><span class="sxs-lookup"><span data-stu-id="1e582-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="1e582-234">*Explorer urządzenia* narzędzia zestawu SDK wprowadzone w systemie [poprzednim artykule](iot-hub-device-sdk-c-intro.md) korzysta z bibliotek w **zestawu SDK usług Azure IoT** Aby utworzyć parametry połączenia urządzenia z identyfikator urządzenia , klucz urządzenia i nazwy hosta Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1e582-234">The *device explorer* SDK tool introduced in the [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in the **Azure IoT service SDK** to create the device connection string from the device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="1e582-235">Dlatego wywołanie **IoTHubClient\_LL\_Utwórz** może być preferowana, ponieważ zapisuje kroku Generowanie ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="1e582-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you the step of generating a connection string.</span></span> <span data-ttu-id="1e582-236">Należy użyć metody jest wygodne.</span><span class="sxs-lookup"><span data-stu-id="1e582-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="1e582-237">Opcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="1e582-237">Configuration options</span></span>
<span data-ttu-id="1e582-238">Do tej pory wszystkie elementy opisane o sposobie **IoTHubClient** works biblioteki odzwierciedla jego zachowanie domyślne.</span><span class="sxs-lookup"><span data-stu-id="1e582-238">So far everything described about the way the **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="1e582-239">Istnieje jednak kilka opcji, które można ustawić, aby zmienić sposób działania biblioteki.</span><span class="sxs-lookup"><span data-stu-id="1e582-239">However, there are a few options that you can set to change how the library works.</span></span> <span data-ttu-id="1e582-240">Jest to osiągane przez wykorzystanie **IoTHubClient\_LL\_SetOption** interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1e582-240">This is accomplished by leveraging the **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="1e582-241">Należy wziąć pod uwagę w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="1e582-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="1e582-242">Istnieje kilka opcji, które są powszechnie stosowane:</span><span class="sxs-lookup"><span data-stu-id="1e582-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="1e582-243">**SetBatching** (wartość logiczna) — Jeśli **true**, dane wysyłane do Centrum IoT jest wysyłane w partiach.</span><span class="sxs-lookup"><span data-stu-id="1e582-243">**SetBatching** (bool) – If **true**, then data sent to IoT Hub is sent in batches.</span></span> <span data-ttu-id="1e582-244">Jeśli **false**, komunikaty są wysyłane pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="1e582-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="1e582-245">Wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="1e582-245">The default is **false**.</span></span> <span data-ttu-id="1e582-246">Należy pamiętać, że **SetBatching** dotyczy tylko protokołu HTTP, a nie MQTT lub AMQP protokołów.</span><span class="sxs-lookup"><span data-stu-id="1e582-246">Note that the **SetBatching** option only applies to the HTTP protocol and not to the MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="1e582-247">**Limit czasu** (unsigned int) — ta wartość jest reprezentowana w milisekundach.</span><span class="sxs-lookup"><span data-stu-id="1e582-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="1e582-248">Jeśli wysyła żądanie HTTP lub odebrania odpowiedzi trwa dłużej niż ten czas, a następnie upłynie limit czasu połączenia.</span><span class="sxs-lookup"><span data-stu-id="1e582-248">If sending an HTTP request or receiving a response takes longer than this time, then the connection times out.</span></span>

<span data-ttu-id="1e582-249">Opcja łączenia we wsady jest ważna.</span><span class="sxs-lookup"><span data-stu-id="1e582-249">The batching option is important.</span></span> <span data-ttu-id="1e582-250">Domyślnie zdarzenia ingresses biblioteki indywidualnie (pojedyncze zdarzenie jest niezależnie od przekazania do **IoTHubClient\_LL\_SendEventAsync**).</span><span class="sxs-lookup"><span data-stu-id="1e582-250">By default, the library ingresses events individually (a single event is whatever you pass to **IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="1e582-251">Jeśli opcja łączenia we wsady jest **true**, biblioteki gromadzi zdarzenia tyle jak go z buforu (maksymalnie maksymalny rozmiar wiadomości akceptujące Centrum IoT).</span><span class="sxs-lookup"><span data-stu-id="1e582-251">If the batching option is **true**, the library collects as many events as it can from the buffer (up to the maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="1e582-252">Wsadowe zdarzenia są wysyłane do Centrum IoT w pojedynczym wywołaniu HTTP (zdarzenia są połączone w tablicy JSON).</span><span class="sxs-lookup"><span data-stu-id="1e582-252">The event batch is sent to IoT Hub in a single HTTP call (the individual events are bundled into a JSON array).</span></span> <span data-ttu-id="1e582-253">Włączanie przetwarzanie wsadowe zwykle powoduje duża wydajność, ponieważ jest zmniejszenie przechodzenia do sieci.</span><span class="sxs-lookup"><span data-stu-id="1e582-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="1e582-254">Ponadto znacząco zmniejsza przepustowości od wysyłania jednego zestawu nagłówków HTTP z partii zdarzeń, a nie zestaw nagłówki dla każdego wybranego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="1e582-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="1e582-255">Chyba że masz powód, aby nie zwykle należy włączyć przetwarzanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="1e582-255">Unless you have a specific reason to do otherwise, typically you’ll want to enable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e582-256">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e582-256">Next steps</span></span>
<span data-ttu-id="1e582-257">W tym artykule opisano szczegółowo zachowanie **IoTHubClient** Biblioteka odnaleziona w **urządzenia Azure IoT SDK dla języka C**. Dzięki tym informacjom powinien dysponować dobrą znajomością możliwości **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="1e582-257">This article describes in detail the behavior of the **IoTHubClient** library found in the **Azure IoT device SDK for C**. With this information, you should have a good understanding of the capabilities of the **IoTHubClient** library.</span></span> <span data-ttu-id="1e582-258">[Kolejnym artykule](iot-hub-device-sdk-c-serializer.md) zawiera szczegółowe informacje podobne na **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="1e582-258">The [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on the **serializer** library.</span></span>

<span data-ttu-id="1e582-259">Aby dowiedzieć się więcej o tworzeniu aplikacji Centrum IoT, zobacz [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="1e582-259">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="1e582-260">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="1e582-260">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1e582-261">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="1e582-261">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
