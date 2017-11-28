---
title: Przewodnik dewelopera Centrum IoT Azure | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera usługi Azure IoT Hub omówiono punktów końcowych, zabezpieczeń, w rejestrze tożsamości, zarządzanie urządzeniami, bezpośrednie metod, twins urządzenia, przekazywania plików, zadań, Centrum IoT język zapytania, a wiadomości."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: adb9a12899e9040cd83d522c734448989636fe29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-developer-guide"></a><span data-ttu-id="b5c21-103">Przewodnik dewelopera Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="b5c21-103">Azure IoT Hub developer guide</span></span>

<span data-ttu-id="b5c21-104">Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia włączanie i niezawodności komunikację dwukierunkową między milionów urządzeń i zaplecze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b5c21-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="b5c21-105">Centrum IoT Azure oferuje:</span><span class="sxs-lookup"><span data-stu-id="b5c21-105">Azure IoT Hub provides you with:</span></span>

* <span data-ttu-id="b5c21-106">Bezpieczna komunikacja przy użyciu poświadczeń zabezpieczeń urządzenia i kontrola dostępu.</span><span class="sxs-lookup"><span data-stu-id="b5c21-106">Secure communications by using per-device security credentials and access control.</span></span>
* <span data-ttu-id="b5c21-107">Wiele opcji komunikacji hiperskali urządzenia do chmury i chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b5c21-107">Multiple device-to-cloud and cloud-to-device hyper-scale communication options.</span></span>
* <span data-ttu-id="b5c21-108">Kolejność przechowywania informacji o stanie na urządzenie i metadanych.</span><span class="sxs-lookup"><span data-stu-id="b5c21-108">Queryable storage of per-device state information and meta-data.</span></span>
* <span data-ttu-id="b5c21-109">Łatwe urządzenia łączność z bibliotekami urządzenia dla najbardziej popularnych języków i platform.</span><span class="sxs-lookup"><span data-stu-id="b5c21-109">Easy device connectivity with device libraries for the most popular languages and platforms.</span></span>

<span data-ttu-id="b5c21-110">Ten przewodnik dewelopera Centrum IoT zawiera następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="b5c21-110">This IoT Hub developer guide includes the following articles:</span></span>

* <span data-ttu-id="b5c21-111">[Wskazówki dotyczące komunikacji urządzenia do chmury] [ lnk-d2c-guidance] ułatwia wybór między wiadomości urządzenia do chmury, dwie urządzenia zgłoszonego właściwości i przekazywania pliku.</span><span class="sxs-lookup"><span data-stu-id="b5c21-111">[Device-to-cloud communication guidance][lnk-d2c-guidance] helps you choose between device-to-cloud messages, device twin's reported properties, and file upload.</span></span>
* <span data-ttu-id="b5c21-112">[Wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] ułatwia wybór między metody bezpośredniego, odpowiednie właściwości dwie urządzenia i komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b5c21-112">[Cloud-to-device communication guidance][lnk-c2d-guidance] helps you choose between direct methods, device twin's desired properties, and cloud-to-device messages.</span></span>
* <span data-ttu-id="b5c21-113">[Urządzenia do chmury i wiadomości z Centrum IoT chmury do urządzenia] [ devguide-messaging] opisano funkcje obsługi wiadomości (urządzenia do chmury i chmury do urządzenia), które udostępnia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b5c21-113">[Device-to-cloud and cloud-to-device messaging with IoT Hub][devguide-messaging] describes the messaging features (device-to-cloud and cloud-to-device) that IoT Hub exposes.</span></span>
  * <span data-ttu-id="b5c21-114">[Wysyłanie komunikatów urządzenia do chmury do Centrum IoT][devguide-messages-d2c].</span><span class="sxs-lookup"><span data-stu-id="b5c21-114">[Send device-to-cloud messages to IoT Hub][devguide-messages-d2c].</span></span>
  * <span data-ttu-id="b5c21-115">[Przeczytaj komunikaty urządzenia do chmury z wbudowanym punktem końcowym][devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="b5c21-115">[Read device-to-cloud messages from the built-in endpoint][devguide-builtin].</span></span>
  * <span data-ttu-id="b5c21-116">[Użyj niestandardowe punkty końcowe i reguły routingu dla komunikatów urządzenia do chmury][devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="b5c21-116">[Use custom endpoints and routing rules for device-to-cloud messages][devguide-custom].</span></span>
  * <span data-ttu-id="b5c21-117">[Wysyłanie wiadomości chmury do urządzenia z Centrum IoT][devguide-messages-c2d].</span><span class="sxs-lookup"><span data-stu-id="b5c21-117">[Send cloud-to-device messages from IoT Hub][devguide-messages-c2d].</span></span>
  * <span data-ttu-id="b5c21-118">[Tworzenie i odczytywanie wiadomości Centrum IoT][devguide-format].</span><span class="sxs-lookup"><span data-stu-id="b5c21-118">[Create and read IoT Hub messages][devguide-format].</span></span>
* <span data-ttu-id="b5c21-119">[Przekazywanie plików z urządzenia] [ devguide-upload] w tym artykule opisano, jak można przekazać pliki z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b5c21-119">[Upload files from a device][devguide-upload] describes how you can upload files from a device.</span></span> <span data-ttu-id="b5c21-120">Artykuł zawiera także informacje o tematów, takich jak powiadomienia, czy można wysyłać procesu przekazywania.</span><span class="sxs-lookup"><span data-stu-id="b5c21-120">The article also includes information about topics such as the notifications the upload process can send.</span></span>
* <span data-ttu-id="b5c21-121">[Zarządzanie tożsamościami urządzenie w Centrum IoT] [ devguide-identities] opisuje jakie informacje o każdej Centrum IoT magazyny rejestru tożsamości i jak można uzyskać dostęp i zmodyfikować go.</span><span class="sxs-lookup"><span data-stu-id="b5c21-121">[Manage device identities in IoT Hub][devguide-identities] describes what information each IoT hub's identity registry stores, and how you can access and modify it.</span></span>
* <span data-ttu-id="b5c21-122">[Kontrola dostępu do Centrum IoT] [ devguide-security] opisano model zabezpieczeń używany do udostępnienia funkcji Centrum IoT dla obu urządzeń i składniki w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b5c21-122">[Control access to IoT Hub][devguide-security] describes the security model used to grant access to IoT Hub functionality for both devices and cloud components.</span></span> <span data-ttu-id="b5c21-123">Artykuł zawiera informacje dotyczące używania tokenów i certyfikaty X.509 i szczegóły uprawnień, które mogą udzielać dostępu.</span><span class="sxs-lookup"><span data-stu-id="b5c21-123">The article includes information about using tokens and X.509 certificates, and details of the permissions you can grant.</span></span>
* <span data-ttu-id="b5c21-124">[Umożliwia synchronizowanie stanu i konfiguracji urządzenia twins] [ devguide-device-twins] opisuje *dwie urządzenia* koncepcji i funkcji eksponuje takich jak synchronizowanie urządzenia z jego dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b5c21-124">[Use device twins to synchronize state and configurations][devguide-device-twins] describes the *device twin* concept and the functionality it exposes such as synchronizing a device with its device twin.</span></span> <span data-ttu-id="b5c21-125">Artykuł zawiera informacje na temat danych przechowywanych w dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b5c21-125">The article includes information about the data stored in a device twin.</span></span>
* <span data-ttu-id="b5c21-126">[Wywoływanie metody bezpośrednio na urządzeniu] [ devguide-directmethods] informacje o cyklu życia metoda bezpośrednia informacji dotyczących sposobu wywoływania metod na urządzeniu z aplikacji zaplecza i obsługiwać metodę bezpośrednio na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="b5c21-126">[Invoke a direct method on a device][devguide-directmethods] describes the lifecycle of a direct method, information about how to invoke methods on a device from your back-end app and handle the direct method on your device.</span></span>
* <span data-ttu-id="b5c21-127">[Planowanie zadań na wielu urządzeniach] [ devguide-jobs] zawiera opis sposobu tworzenia harmonogramu zadań na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="b5c21-127">[Schedule jobs on multiple devices][devguide-jobs] describes how you can schedule jobs on multiple devices.</span></span> <span data-ttu-id="b5c21-128">Artykuł opisuje sposób przesyłania zadań, wykonujących zadania jako wykonywania metoda bezpośrednia aktualizacja urządzenia przy użyciu podwójnego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b5c21-128">The article describes how to submit jobs that perform tasks as executing a direct method, updating a device using a device twin.</span></span> <span data-ttu-id="b5c21-129">On również opis zbadać stanu zadania.</span><span class="sxs-lookup"><span data-stu-id="b5c21-129">It also describes how to query the status of a job.</span></span>
* <span data-ttu-id="b5c21-130">[Odwołanie — wybierz protokół komunikacyjny] [ devguide-protocol] opisuje protokołów komunikacyjnych, że Centrum IoT do komunikacji urządzeń i obsługuje listę portów, które powinno być otwarte.</span><span class="sxs-lookup"><span data-stu-id="b5c21-130">[Reference - choose a communication protocol][devguide-protocol] describes the communication protocols that IoT Hub supports for device communication and lists the ports that should be open.</span></span>
* <span data-ttu-id="b5c21-131">[Odwołanie — punkty końcowe Centrum IoT] [ devguide-endpoints] opisano różne punkty końcowe, które udostępnia każdego centrum IoT dla operacji obsługi i zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b5c21-131">[Reference - IoT Hub endpoints][devguide-endpoints] describes the various endpoints that each IoT hub exposes for runtime and management operations.</span></span> <span data-ttu-id="b5c21-132">Artykuł opisuje również sposób możesz utworzyć dodatkowe punkty końcowe w Centrum IoT i jak użyć bramy pola, aby umożliwić łączność urządzeń z punktami końcowymi Centrum IoT w scenariuszach niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="b5c21-132">The article also describes how you can create additional endpoints in your IoT hub, and how to use a field gateway to enable devices connectivity to your IoT Hub endpoints in non-standard scenarios.</span></span>
* <span data-ttu-id="b5c21-133">[Odwołanie - Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości] [ devguide-query] opisuje tego języka zapytania Centrum IoT, która umożliwia pobieranie informacji z Centrum temat zadań i twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b5c21-133">[Reference - IoT Hub query language for device twins, jobs, and message routing][devguide-query] describes that IoT Hub query language that enables you to retrieve information from your hub about your device twins and jobs.</span></span>
* <span data-ttu-id="b5c21-134">[Odwołanie - przydziały i ograniczenia przepustowości] [ devguide-quotas] podsumowuje przydziały w usłudze IoT Hub i zachowanie ograniczania przepustowości, można oczekiwać, aby zobaczyć, gdy przekracza limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="b5c21-134">[Reference - quotas and throttling][devguide-quotas] summarizes the quotas set in the IoT Hub service and the throttling behavior you can expect to see when you exceed a quota.</span></span>
* <span data-ttu-id="b5c21-135">[Odwołanie — cennik] [ devguide-pricing] zawiera ogólne informacje dotyczące różnych jednostki SKU i cenach dla Centrum IoT i szczegółowe informacje o sposobie różne funkcje Centrum IoT są mierzone jako wiadomości przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b5c21-135">[Reference - pricing][devguide-pricing] provides general information on different SKUs and pricing for IoT Hub and details on how the various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>
* <span data-ttu-id="b5c21-136">[Odwołanie - urządzeń i usług zestawów SDK] [ devguide-sdks] zawiera zestawy SDK usługi Azure IoT służy do opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b5c21-136">[Reference - Device and service SDKs][devguide-sdks] lists the Azure IoT SDKs you can use to develop both device and service apps that interact with your IoT hub.</span></span> <span data-ttu-id="b5c21-137">Artykuł zawiera linki do dokumentacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b5c21-137">The article includes links to online API documentation.</span></span>
* <span data-ttu-id="b5c21-138">[Odwołanie — Obsługa MQTT Centrum IoT] [ devguide-mqtt] zawiera szczegółowe informacje o sposobie obsługi protokołu MQTT w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b5c21-138">[Reference - IoT Hub MQTT support][devguide-mqtt] provides detailed information about how IoT Hub supports the MQTT protocol.</span></span> <span data-ttu-id="b5c21-139">Tym artykule opisano obsługę protokołu MQTT wbudowanych do zestawów SDK IoT Azure i zawiera informacje dotyczące korzystania z protokołu MQTT bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="b5c21-139">The article describes the support for the MQTT protocol built-in to the Azure IoT SDKs and provides information about using the MQTT protocol directly.</span></span>
* <span data-ttu-id="b5c21-140">[Słownik] [ devguide-glossary] listę typowe terminy związane z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b5c21-140">[Glossary][devguide-glossary] a list of common IoT Hub-related terms.</span></span>

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
