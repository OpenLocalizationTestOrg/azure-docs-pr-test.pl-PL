---
title: "aaaUnderstand Obsługa MQTT Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Deweloper przewodnik — Obsługa urządzeń łączących się przy użyciu punktu końcowego urządzeń połączonych z Centrum IoT tooan hello MQTT protokołu. Zawiera informacje na temat wbudowana obsługa MQTT w hello zestawy SDK urządzenia Azure IoT."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="9445f-104">Komunikować się z Centrum IoT przy użyciu protokołu MQTT hello</span><span class="sxs-lookup"><span data-stu-id="9445f-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="9445f-105">Centrum IoT umożliwia toocommunicate urządzeń z hello urządzenia punkty końcowe Centrum IoT przy użyciu hello [MQTT v3.1.1] [ lnk-mqtt-org] protokołu na porcie 8883 lub v3.1.1 MQTT za pośrednictwem protokołu WebSocket na porcie 443.</span><span class="sxs-lookup"><span data-stu-id="9445f-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="9445f-106">Centrum IoT wymaga wszystkie urządzenia komunikacji toobe zabezpieczone przy użyciu protokołu TLS/SSL (w związku z tym Centrum IoT nie obsługuje niezabezpieczonego połączenia za pośrednictwem portu 1883).</span><span class="sxs-lookup"><span data-stu-id="9445f-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="9445f-107">Łączenie tooIoT Centrum</span><span class="sxs-lookup"><span data-stu-id="9445f-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="9445f-108">Urządzenie można użyć Centrum IoT hello MQTT protokołu tooconnect tooan przy użyciu bibliotek hello hello [Azure IoT SDK] [ lnk-device-sdks] lub przy użyciu protokołu MQTT hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="9445f-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="9445f-109">Za pomocą urządzenia hello zestawów SDK</span><span class="sxs-lookup"><span data-stu-id="9445f-109">Using hello device SDKs</span></span>

<span data-ttu-id="9445f-110">[Zestawy SDK urządzenia] [ lnk-device-sdks] hello tej obsługi protokołu MQTT są dostępne dla języka Java, Node.js, C, C# i Python.</span><span class="sxs-lookup"><span data-stu-id="9445f-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="9445f-111">urządzenie Hello zestawów SDK używać hello standardowe Centrum IoT połączenia ciąg tooestablish Centrum IoT tooan połączenia.</span><span class="sxs-lookup"><span data-stu-id="9445f-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="9445f-112">Protokół MQTT hello toouse, powitania klienta protokołu parametr musi być ustawiony zbyt**MQTT**.</span><span class="sxs-lookup"><span data-stu-id="9445f-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="9445f-113">Domyślnie urządzenia hello zestawów SDK łączą tooan Centrum IoT hello **CleanSession** zbyt ustawiona flaga**0** i użyj **QoS 1** w wymianie wiadomości powitania Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9445f-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="9445f-114">Gdy urządzenie jest połączone tooan Centrum IoT, urządzenia hello zestawy SDK zapewniają metod, które umożliwiają wiadomości toosend urządzenia powitania tooand odbierać komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9445f-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="9445f-115">Witaj Poniższa tabela zawiera linki toocode przykłady dla każdego obsługiwanego języka i określa hello parametru toouse tooestablish tooIoT połączenia koncentratora przy użyciu protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="9445f-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="9445f-116">Język</span><span class="sxs-lookup"><span data-stu-id="9445f-116">Language</span></span> | <span data-ttu-id="9445f-117">Parametr protokołu</span><span class="sxs-lookup"><span data-stu-id="9445f-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="9445f-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="9445f-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="9445f-119">Azure — iot urządzenie mqtt</span><span class="sxs-lookup"><span data-stu-id="9445f-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="9445f-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="9445f-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="9445f-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="9445f-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="9445f-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="9445f-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="9445f-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="9445f-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="9445f-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="9445f-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="9445f-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="9445f-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="9445f-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="9445f-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="9445f-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="9445f-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="9445f-128">Migrowanie aplikacji urządzenia z protokołu AMQP tooMQTT</span><span class="sxs-lookup"><span data-stu-id="9445f-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="9445f-129">Jeśli używasz hello [urządzenia zestawów SDK][lnk-device-sdks], przełączania przy użyciu protokołu AMQP tooMQTT konieczna jest zmiana parametru protokołu hello w powitania klienta inicjowania, jak wspomniano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9445f-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="9445f-130">Po tej czynności upewnij się, że hello toocheck następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9445f-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="9445f-131">Protokół AMQP zwraca błędy wiele warunków, gdy MQTT zakończy połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="9445f-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="9445f-132">W związku z tym wyjątku obsługi logiki ewentualnej konieczności wprowadzenia zmian.</span><span class="sxs-lookup"><span data-stu-id="9445f-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="9445f-133">MQTT nie obsługuje hello *Odrzuć* operacji podczas odbierania [wiadomości chmury do urządzenia][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="9445f-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="9445f-134">Jeśli aplikacja zaplecza musi tooreceive odpowiedzi z aplikacji urządzenia hello, rozważ użycie [bezpośrednie metody][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="9445f-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="9445f-135">Przy użyciu protokołu MQTT hello bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="9445f-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="9445f-136">Jeśli urządzenie nie można używać urządzeń hello zestawów SDK, nadal można połączyć z punktów końcowych urządzenie toohello przy użyciu protokołu MQTT hello na porcie 8883.</span><span class="sxs-lookup"><span data-stu-id="9445f-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="9445f-137">W hello **CONNECT** pakietów hello urządzeń należy używać hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="9445f-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="9445f-138">Dla hello **ClientId** Użyj hello **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="9445f-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="9445f-139">Dla hello **Username** użyj `{iothubhostname}/{device_id}/api-version=2016-11-14`, gdzie {iothubhostname} jest hello pełne CName hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9445f-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="9445f-140">Na przykład, jeśli hello nazwa Centrum IoT to **contoso.azure devices.net** i jeśli hello nazwa urządzenia jest **MyDevice01**, hello pełne **Username** pole powinno zawierać `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="9445f-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="9445f-141">Dla hello **hasło** Użyj tokenu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="9445f-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="9445f-142">format Hello powitalne SAS token jest hello takie same jak w przypadku zarówno hello HTTP, jak i protokołów AMQP:</span><span class="sxs-lookup"><span data-stu-id="9445f-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="9445f-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="9445f-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="9445f-144">Aby uzyskać więcej informacji o tym, jak toogenerate tokeny sygnatury dostępu Współdzielonego, zobacz sekcję urządzenia hello [tokeny zabezpieczające przy użyciu Centrum IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="9445f-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="9445f-145">Podczas testowania, możesz również użyć hello [explorer urządzenia] [ lnk-device-explorer] tooquickly narzędzie do generowania tokenu sygnatury dostępu Współdzielonego, który możesz skopiować i wkleić w swoim własnym kodem:</span><span class="sxs-lookup"><span data-stu-id="9445f-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="9445f-146">Przejdź toohello **zarządzania** karcie **Explorer urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="9445f-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="9445f-147">Kliknij przycisk **tokenu sygnatury dostępu Współdzielonego** (z góry po prawej).</span><span class="sxs-lookup"><span data-stu-id="9445f-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="9445f-148">Na **SASTokenForm**, wybierz swoje urządzenie w hello **DeviceID** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="9445f-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="9445f-149">Ustaw użytkownika **TTL**.</span><span class="sxs-lookup"><span data-stu-id="9445f-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="9445f-150">Kliknij przycisk **Generuj** toocreate Twojego tokenu.</span><span class="sxs-lookup"><span data-stu-id="9445f-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="9445f-151">Witaj tokenu sygnatury dostępu Współdzielonego, który jest generowany ma ta struktura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="9445f-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="9445f-152">Witaj częścią tego tokenu toouse jako hello **hasło** jest tooconnect pola przy użyciu MQTT: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="9445f-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="9445f-153">MQTT łączyć i Odłącz pakietów, Centrum IoT wystawia zdarzenie na powitania **operacje monitorowania** kanału o dodatkowe informacje, które mogą ułatwić tootroubleshoot problemy z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="9445f-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="9445f-154">Wysyłanie wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="9445f-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="9445f-155">Po wprowadzeniu udane połączenie, urządzenie może wysyłać wiadomości tooIoT koncentratora za pomocą `devices/{device_id}/messages/events/` lub `devices/{device_id}/messages/events/{property_bag}` jako **nazwa tematu**.</span><span class="sxs-lookup"><span data-stu-id="9445f-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="9445f-156">Witaj `{property_bag}` element włącza hello urządzenia toosend wiadomości z dodatkowych właściwości w formacie zakodowane w adresie url.</span><span class="sxs-lookup"><span data-stu-id="9445f-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="9445f-157">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9445f-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="9445f-158">To `{property_bag}` element hello używa tego samego kodowania, podobnie jak w przypadku ciągi zapytań w protokole hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="9445f-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="9445f-159">Hello aplikacji urządzenia można także użyć `devices/{device_id}/messages/events/{property_bag}` jako hello **nazwa tematu zostanie** toodefine *będzie wiadomości* toobe przekazywane jako wiadomość telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9445f-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="9445f-160">Centrum IoT nie obsługuje komunikaty QoS 2.</span><span class="sxs-lookup"><span data-stu-id="9445f-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="9445f-161">Jeśli aplikacja urządzenia publikuje komunikat z **QoS 2**, Centrum IoT zamyka hello połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="9445f-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="9445f-162">Centrum IoT nie jest trwały Zachowaj wiadomości.</span><span class="sxs-lookup"><span data-stu-id="9445f-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="9445f-163">Jeśli urządzenie wysyła wiadomość hello **Zachowaj** too1 ustawiona flaga, Centrum IoT dodaje hello **x-opt — Zachowaj** komunikat toohello właściwości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9445f-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="9445f-164">W takim przypadku zamiast utrwalanie hello zachować wiadomości, Centrum IoT przekazuje toohello wewnętrznej bazy danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9445f-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="9445f-165">Centrum IoT obsługuje tylko jedno aktywne połączenie MQTT na urządzenie.</span><span class="sxs-lookup"><span data-stu-id="9445f-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="9445f-166">Wszystkie nowe połączenie MQTT imieniu hello tego samego Identyfikatora urządzenia powoduje, że Centrum IoT toodrop hello istniejącego połączenia.</span><span class="sxs-lookup"><span data-stu-id="9445f-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="9445f-167">Aby uzyskać więcej informacji, zobacz [wiadomości przewodnik dewelopera][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="9445f-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="9445f-168">Odbieranie komunikatów chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="9445f-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="9445f-169">tooreceive wiadomości z Centrum IoT, urządzenie powinno Subskrybuj przy użyciu `devices/{device_id}/messages/devicebound/#` jako **filtru tematu**.</span><span class="sxs-lookup"><span data-stu-id="9445f-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="9445f-170">Witaj wielopoziomowe symbolu wieloznacznego  **#**  w hello filtr tematu jest używany tylko tooallow hello urządzenia tooreceive dodatkowe właściwości w nazwie tematu hello.</span><span class="sxs-lookup"><span data-stu-id="9445f-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="9445f-171">Centrum IoT nie zezwala na użycie hello hello  **#**  lub **?**</span><span class="sxs-lookup"><span data-stu-id="9445f-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="9445f-172">symbole wieloznaczne w celu filtrowania tematy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="9445f-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="9445f-173">Ponieważ Centrum IoT nie jest brokera obsługi komunikatów pub-sub ogólnego przeznaczenia, obsługuje on tylko nazwy tematów hello udokumentowany i filtry tematu.</span><span class="sxs-lookup"><span data-stu-id="9445f-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="9445f-174">Hello urządzenia nie odbiera komunikaty z Centrum IoT, aż pomyślnie subskrybowanych tooits urządzenia punktu końcowego, reprezentowany przez hello `devices/{device_id}/messages/devicebound/#` filtru tematu.</span><span class="sxs-lookup"><span data-stu-id="9445f-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="9445f-175">Po nawiązaniu pomyślnego subskrypcji, urządzenia hello uruchamia odbieranie wiadomości tylko chmury do urządzenia, które zostały wysłane tooit po czasie hello hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9445f-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="9445f-176">Jeśli urządzenie hello nawiązanie połączenia z **CleanSession** zbyt ustawiona flaga**0**, subskrypcji hello jest trwała dla różnych sesji.</span><span class="sxs-lookup"><span data-stu-id="9445f-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="9445f-177">W takim przypadku hello kolejnym nawiązaniu z **CleanSession 0** hello urządzenia odbiera komunikaty oczekujące, które zostały wysłane tooit gdy był on odłączony.</span><span class="sxs-lookup"><span data-stu-id="9445f-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="9445f-178">Jeśli urządzenie hello używa **CleanSession** zbyt ustawiona flaga**1** , nie otrzyma komunikaty z Centrum IoT dopóki ją subskrybuje tooits urządzenia endpoint.</span><span class="sxs-lookup"><span data-stu-id="9445f-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="9445f-179">Centrum IoT zapewnia wiadomości powitania **nazwa tematu** `devices/{device_id}/messages/devicebound/`, lub `devices/{device_id}/messages/devicebound/{property_bag}` , jeśli nie ma żadnych właściwości komunikatu.</span><span class="sxs-lookup"><span data-stu-id="9445f-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="9445f-180">`{property_bag}`zawiera pary klucz wartość zakodowane w adresie url właściwości komunikatu.</span><span class="sxs-lookup"><span data-stu-id="9445f-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="9445f-181">Tylko właściwości aplikacji i użytkownika można ustawić właściwości (takie jak **messageId** lub **correlationId**) znajdują się w zbiorze właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="9445f-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="9445f-182">Nazwy właściwości systemu mają prefiks hello  **$** , właściwości aplikacji za pomocą hello oryginalna nazwa właściwości nie ma prefiksu.</span><span class="sxs-lookup"><span data-stu-id="9445f-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="9445f-183">Gdy aplikacja urządzenia subskrybuje temat tooa z **QoS 2**, Centrum IoT przyznaje maksymalny poziom QoS 1 w hello **SUBACK** pakietów.</span><span class="sxs-lookup"><span data-stu-id="9445f-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="9445f-184">Po tym Centrum IoT zapewnia urządzenia toohello wiadomości przy użyciu QoS 1.</span><span class="sxs-lookup"><span data-stu-id="9445f-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="9445f-185">Podczas pobierania właściwości dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="9445f-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="9445f-186">Po pierwsze urządzenie subskrybuje zbyt`$iothub/twin/res/#`, tooreceive hello operacji odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9445f-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="9445f-187">Następnie wysyła tootopic pusty komunikat `$iothub/twin/GET/?$rid={request id}`, z wypełnione wartością **identyfikator żądania**. Usługa hello wysyła następnie odpowiedź hello urządzenia dwie dane na temat `$iothub/twin/res/{status}/?$rid={request id}`, przy użyciu hello sam  **Identyfikator żądania** jako hello żądania.</span><span class="sxs-lookup"><span data-stu-id="9445f-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="9445f-188">Identyfikator żądania może być wszystkie prawidłowe wartości wartość właściwości komunikatu zgodnie [Centrum IoT wiadomości przewodnik dewelopera][lnk-messaging], i stan zostanie zweryfikowany jako liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="9445f-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="9445f-189">treść odpowiedzi Hello zawiera sekcja właściwości hello Witaj dwie urządzenia:</span><span class="sxs-lookup"><span data-stu-id="9445f-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="9445f-190">Witaj treść wpisu rejestru tożsamości hello ograniczone toohello "właściwości" elementu członkowskiego, na przykład:</span><span class="sxs-lookup"><span data-stu-id="9445f-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

<span data-ttu-id="9445f-191">kody stanu możliwe Hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="9445f-191">hello possible status codes are:</span></span>

|<span data-ttu-id="9445f-192">Stan</span><span class="sxs-lookup"><span data-stu-id="9445f-192">Status</span></span> | <span data-ttu-id="9445f-193">Opis</span><span class="sxs-lookup"><span data-stu-id="9445f-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9445f-194">200</span><span class="sxs-lookup"><span data-stu-id="9445f-194">200</span></span> | <span data-ttu-id="9445f-195">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="9445f-195">Success</span></span> |
| <span data-ttu-id="9445f-196">429</span><span class="sxs-lookup"><span data-stu-id="9445f-196">429</span></span> | <span data-ttu-id="9445f-197">Za dużo żądań (ograniczony), jak na [ograniczania Centrum IoT][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="9445f-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="9445f-198">5**</span><span class="sxs-lookup"><span data-stu-id="9445f-198">5**</span></span> | <span data-ttu-id="9445f-199">Błędy serwera</span><span class="sxs-lookup"><span data-stu-id="9445f-199">Server errors</span></span> |

<span data-ttu-id="9445f-200">Aby uzyskać więcej informacji, zobacz [urządzenia twins przewodnik dewelopera][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="9445f-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="9445f-201">Aktualizacja właściwości zgłoszone dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="9445f-201">Update device twin's reported properties</span></span>

<span data-ttu-id="9445f-202">Witaj poniższa sekwencja zawiera opis jak urządzenie aktualizuje hello zgłosił właściwości w Witaj dwie urządzenie w Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="9445f-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="9445f-203">Urządzenia najpierw zasubskrybować toohello `$iothub/twin/res/#` operacji tematu tooreceive hello odpowiedzi z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9445f-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="9445f-204">Urządzenie wysyła wiadomość zawierającą hello urządzenia dwie aktualizacji toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` tematu.</span><span class="sxs-lookup"><span data-stu-id="9445f-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="9445f-205">Ten komunikat zawiera **identyfikator żądania** wartość.</span><span class="sxs-lookup"><span data-stu-id="9445f-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="9445f-206">Witaj usługi, a następnie wysyła komunikat odpowiedzi, który zawiera hello nową wartość ETag hello kolekcji właściwości zgłoszony na temat `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="9445f-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="9445f-207">Ten komunikat odpowiedzi używa hello sam **identyfikator żądania** jako hello żądania.</span><span class="sxs-lookup"><span data-stu-id="9445f-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="9445f-208">treść komunikatu żądania Hello zawiera dokument JSON, który zawiera nowe wartości dla właściwości zgłoszone (nie właściwości lub metadanych może być modyfikowany).</span><span class="sxs-lookup"><span data-stu-id="9445f-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="9445f-209">Każdy element członkowski w dokumencie JSON hello aktualizacji lub Dodaj hello odpowiadającego mu członka w dokumencie dwie hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9445f-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="9445f-210">Zestaw elementów członkowskich za`null`, usuwa hello hello zawierający obiektu elementu członkowskiego.</span><span class="sxs-lookup"><span data-stu-id="9445f-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="9445f-211">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9445f-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="9445f-212">kody stanu możliwe Hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="9445f-212">hello possible status codes are:</span></span>

|<span data-ttu-id="9445f-213">Stan</span><span class="sxs-lookup"><span data-stu-id="9445f-213">Status</span></span> | <span data-ttu-id="9445f-214">Opis</span><span class="sxs-lookup"><span data-stu-id="9445f-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9445f-215">200</span><span class="sxs-lookup"><span data-stu-id="9445f-215">200</span></span> | <span data-ttu-id="9445f-216">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="9445f-216">Success</span></span> |
| <span data-ttu-id="9445f-217">400</span><span class="sxs-lookup"><span data-stu-id="9445f-217">400</span></span> | <span data-ttu-id="9445f-218">Nieprawidłowe żądanie.</span><span class="sxs-lookup"><span data-stu-id="9445f-218">Bad Request.</span></span> <span data-ttu-id="9445f-219">Nieprawidłowo sformatowany kod JSON</span><span class="sxs-lookup"><span data-stu-id="9445f-219">Malformed JSON</span></span> |
| <span data-ttu-id="9445f-220">429</span><span class="sxs-lookup"><span data-stu-id="9445f-220">429</span></span> | <span data-ttu-id="9445f-221">Za dużo żądań (ograniczony), jak na [ograniczania Centrum IoT][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="9445f-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="9445f-222">5**</span><span class="sxs-lookup"><span data-stu-id="9445f-222">5**</span></span> | <span data-ttu-id="9445f-223">Błędy serwera</span><span class="sxs-lookup"><span data-stu-id="9445f-223">Server errors</span></span> |

<span data-ttu-id="9445f-224">Aby uzyskać więcej informacji, zobacz [urządzenia twins przewodnik dewelopera][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="9445f-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="9445f-225">Odbieranie powiadomienia o aktualizacji odpowiednie właściwości</span><span class="sxs-lookup"><span data-stu-id="9445f-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="9445f-226">Gdy urządzenie jest podłączone, Centrum IoT wysyła powiadomienia toohello tematu `$iothub/twin/PATCH/properties/desired/?$version={new version}`, które zawierają hello zawartość aktualizacji hello wykonywane przez zaplecza rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="9445f-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="9445f-227">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9445f-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="9445f-228">Podobnie jak w przypadku aktualizacji właściwości `null` wartości oznacza, że hello JSON obiektu elementu członkowskiego jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="9445f-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="9445f-229">Centrum IoT generuje powiadomienia o zmianie tylko wtedy, gdy urządzenia są połączone.</span><span class="sxs-lookup"><span data-stu-id="9445f-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="9445f-230">Upewnij się, że hello tooimplement [przepływu ponowne łączenie urządzenia] [ lnk-devguide-twin-reconnection] tookeep hello żądanego właściwości między centrum IoT i hello aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9445f-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="9445f-231">Aby uzyskać więcej informacji, zobacz [urządzenia twins przewodnik dewelopera][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="9445f-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="9445f-232">Metoda bezpośrednia tooa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="9445f-232">Respond tooa direct method</span></span>

<span data-ttu-id="9445f-233">Po pierwsze urządzenie ma toosubscribe zbyt`$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="9445f-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="9445f-234">Centrum IoT wysyła tematu toohello żądania metody `$iothub/methods/POST/{method name}/?$rid={request id}`, poprawne dane JSON lub pustej treści.</span><span class="sxs-lookup"><span data-stu-id="9445f-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="9445f-235">toorespond, urządzenie hello wysyła wiadomość o poprawne dane JSON lub pustej treści tematu toohello `$iothub/methods/res/{status}/?$rid={request id}`, gdzie **identyfikator żądania** ma toomatch hello w hello komunikat żądania, i **stan** ma toobe liczbą całkowitą .</span><span class="sxs-lookup"><span data-stu-id="9445f-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="9445f-236">Aby uzyskać więcej informacji, zobacz [bezpośrednie przewodnik dewelopera metody][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="9445f-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="9445f-237">Dodatkowe zagadnienia</span><span class="sxs-lookup"><span data-stu-id="9445f-237">Additional considerations</span></span>

<span data-ttu-id="9445f-238">Jako ostatecznego wchodzi w grę, jeśli potrzebujesz zachowanie protokołu MQTT hello toocustomize po stronie chmury hello, należy przejrzeć hello [brama protokołu Azure IoT] [ lnk-azure-protocol-gateway] umożliwiająca toodeploy wysokiej wydajności Protokół niestandardowych bramy, która bezpośrednio z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9445f-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="9445f-239">Brama protokołu Azure IoT Hello umożliwia możesz toocustomize hello urządzenia protokołu tooaccommodate brownfield MQTT wdrożenia lub innych niestandardowych protokołów.</span><span class="sxs-lookup"><span data-stu-id="9445f-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="9445f-240">Takie podejście wymaga jednak uruchamiania i działać brama protokołu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="9445f-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9445f-241">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9445f-241">Next steps</span></span>

<span data-ttu-id="9445f-242">toolearn więcej informacji na temat protokołu MQTT hello, zobacz hello [dokumentacji MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="9445f-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="9445f-243">toolearn więcej informacji na temat planowania wdrożenia Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="9445f-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="9445f-244">[Azure certyfikowane dla katalogu urządzenia IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="9445f-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="9445f-245">[Obsługa dodatkowych protokołów.][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="9445f-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="9445f-246">[Porównaj z usługi Event Hubs][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="9445f-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="9445f-247">[Skalowanie, wysokiej dostępności i odzyskiwania po awarii][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="9445f-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="9445f-248">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="9445f-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9445f-249">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="9445f-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="9445f-250">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="9445f-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
