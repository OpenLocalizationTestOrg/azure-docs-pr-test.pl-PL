---
title: "aaaUnderstand zabezpieczeń Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — jak toocontrol dostępu tooIoT Centrum dla aplikacji dla urządzeń i aplikacji zaplecza. Zawiera informacje na temat tokeny zabezpieczające i pomoc techniczna dla certyfikatów X.509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a><span data-ttu-id="0fa97-104">Kontrola dostępu tooIoT Centrum</span><span class="sxs-lookup"><span data-stu-id="0fa97-104">Control access tooIoT Hub</span></span>

<span data-ttu-id="0fa97-105">W tym artykule opisano opcje hello zabezpieczania Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-105">This article describes hello options for securing your IoT hub.</span></span> <span data-ttu-id="0fa97-106">Centrum IoT używa *uprawnienia* punktu końcowego Centrum IoT toogrant dostępu tooeach.</span><span class="sxs-lookup"><span data-stu-id="0fa97-106">IoT Hub uses *permissions* toogrant access tooeach IoT hub endpoint.</span></span> <span data-ttu-id="0fa97-107">Uprawnienia ograniczyć hello dostępu tooan Centrum IoT oparta na funkcjach.</span><span class="sxs-lookup"><span data-stu-id="0fa97-107">Permissions limit hello access tooan IoT hub based on functionality.</span></span>

<span data-ttu-id="0fa97-108">W tym artykule opisano:</span><span class="sxs-lookup"><span data-stu-id="0fa97-108">This article describes:</span></span>

* <span data-ttu-id="0fa97-109">Witaj różne uprawnienia można przyznanie tooaccess zaplecza aplikacji lub urządzenia tooa Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-109">hello different permissions that you can grant tooa device or back-end app tooaccess your IoT hub.</span></span>
* <span data-ttu-id="0fa97-110">Witaj tokeny proces i hello uwierzytelniania używa tooverify uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-110">hello authentication process and hello tokens it uses tooverify permissions.</span></span>
* <span data-ttu-id="0fa97-111">Jak tooscope poświadczeń toolimit dostęp do toospecific zasobów.</span><span class="sxs-lookup"><span data-stu-id="0fa97-111">How tooscope credentials toolimit access toospecific resources.</span></span>
* <span data-ttu-id="0fa97-112">Obsługa Centrum IoT certyfikatów X.509.</span><span class="sxs-lookup"><span data-stu-id="0fa97-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="0fa97-113">Urządzeń niestandardowych mechanizmów uwierzytelniania, korzystających z istniejących rejestrów tożsamość urządzenia lub schematy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0fa97-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="0fa97-114">Gdy toouse</span><span class="sxs-lookup"><span data-stu-id="0fa97-114">When toouse</span></span>

<span data-ttu-id="0fa97-115">Musisz mieć odpowiednie uprawnienia tooaccess wszelkie punkty końcowe Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-115">You must have appropriate permissions tooaccess any of hello IoT Hub endpoints.</span></span> <span data-ttu-id="0fa97-116">Na przykład urządzenie musi zawierać token zawierający poświadczenia zabezpieczeń, wraz z każdej wiadomości wysyła tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="0fa97-116">For example, a device must include a token containing security credentials along with every message it sends tooIoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="0fa97-117">Kontrola dostępu i uprawnienia</span><span class="sxs-lookup"><span data-stu-id="0fa97-117">Access control and permissions</span></span>

<span data-ttu-id="0fa97-118">Można przyznać [uprawnienia](#iot-hub-permissions) w hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="0fa97-118">You can grant [permissions](#iot-hub-permissions) in hello following ways:</span></span>

* <span data-ttu-id="0fa97-119">**Zasady dostępu do udostępnionego Centrum IoT na poziomie**.</span><span class="sxs-lookup"><span data-stu-id="0fa97-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="0fa97-120">Zasady dostępu współdzielonego, można przyznać dowolną kombinację [uprawnienia](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="0fa97-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="0fa97-121">Zasady można definiować w hello [portalu Azure][lnk-management-portal], lub programowo, używając hello [interfejsy API REST dostawcy zasobów Centrum IoT][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="0fa97-121">You can define policies in hello [Azure portal][lnk-management-portal], or programmatically by using hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="0fa97-122">Nowo utworzone Centrum IoT ma hello następujące zasady domyślne:</span><span class="sxs-lookup"><span data-stu-id="0fa97-122">A newly created IoT hub has hello following default policies:</span></span>

  * <span data-ttu-id="0fa97-123">**iothubowner**: zasady z wszystkie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="0fa97-124">**Usługa**: zasady z **ServiceConnect** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="0fa97-125">**urządzenie**: zasady z **DeviceConnect** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="0fa97-126">**registryRead**: zasady z **RegistryRead** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="0fa97-127">**registryReadWrite**: zasady z **RegistryRead** i RegistryWrite uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="0fa97-128">**Poświadczenia zabezpieczeń na urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="0fa97-128">**Per-device security credentials**.</span></span> <span data-ttu-id="0fa97-129">Zawiera każdego centrum IoT [rejestru tożsamości][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="0fa97-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="0fa97-130">Dla każdego urządzenia w rejestrze tej tożsamości można skonfigurować poświadczenia zabezpieczeń, które przyznać **DeviceConnect** uprawnień zakresie punkty końcowe toohello odpowiednie urządzenie.</span><span class="sxs-lookup"><span data-stu-id="0fa97-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped toohello corresponding device endpoints.</span></span>

<span data-ttu-id="0fa97-131">Na przykład w typowej rozwiązania IoT:</span><span class="sxs-lookup"><span data-stu-id="0fa97-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="0fa97-132">składnika zarządzania urządzeniami Hello używa hello *registryReadWrite* zasad.</span><span class="sxs-lookup"><span data-stu-id="0fa97-132">hello device management component uses hello *registryReadWrite* policy.</span></span>
* <span data-ttu-id="0fa97-133">składnik procesora zdarzeń Hello używa hello *usługi* zasad.</span><span class="sxs-lookup"><span data-stu-id="0fa97-133">hello event processor component uses hello *service* policy.</span></span>
* <span data-ttu-id="0fa97-134">składnika logiki biznesowej urządzenia środowiska wykonawczego Hello używa hello *usługi* zasad.</span><span class="sxs-lookup"><span data-stu-id="0fa97-134">hello run-time device business logic component uses hello *service* policy.</span></span>
* <span data-ttu-id="0fa97-135">Poszczególne urządzenia łączą, przy użyciu poświadczeń przechowywanych w rejestrze tożsamości Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-135">Individual devices connect using credentials stored in hello IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="0fa97-136">Zobacz [uprawnienia](#iot-hub-permissions) Aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0fa97-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="0fa97-137">Authentication</span><span class="sxs-lookup"><span data-stu-id="0fa97-137">Authentication</span></span>

<span data-ttu-id="0fa97-138">Centrum IoT Azure udziela dostępu tooendpoints weryfikując token przed hello udostępnionych zasady dostępu i poświadczenia zabezpieczeń rejestru tożsamości.</span><span class="sxs-lookup"><span data-stu-id="0fa97-138">Azure IoT Hub grants access tooendpoints by verifying a token against hello shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="0fa97-139">Poświadczenia zabezpieczeń, takie jak klucze symetryczne, nigdy nie są przesyłane przez sieć hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-139">Security credentials, such as symmetric keys, are never sent over hello wire.</span></span>

> [!NOTE]
> <span data-ttu-id="0fa97-140">Witaj Centrum IoT Azure dostawcy zasobów jest chronione przy użyciu subskrypcji platformy Azure, są wszystkich dostawców w hello [usługi Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="0fa97-140">hello Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in hello [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="0fa97-141">Aby uzyskać więcej informacji o tym, jak tooconstruct i używania tokenów zabezpieczających, zobacz [tokeny zabezpieczające Centrum IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="0fa97-141">For more information about how tooconstruct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="0fa97-142">Szczegóły protokołu</span><span class="sxs-lookup"><span data-stu-id="0fa97-142">Protocol specifics</span></span>

<span data-ttu-id="0fa97-143">Każdy obsługiwanych protokołów, takich jak MQTT, AMQP i HTTP, transport tokenów na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="0fa97-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="0fa97-144">Używając MQTT hello CONNECT pakiet ma hello deviceId jak hello ClientId, {iothubhostname} / {deviceId} hello pole nazwy użytkownika i tokenu sygnatury dostępu Współdzielonego, w polu hasła hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-144">When using MQTT, hello CONNECT packet has hello deviceId as hello ClientId, {iothubhostname}/{deviceId} in hello Username field, and a SAS token in hello Password field.</span></span> <span data-ttu-id="0fa97-145">{iothubhostname} powinna hello pełne CName z Centrum IoT hello (na przykład devices.net contoso.azure).</span><span class="sxs-lookup"><span data-stu-id="0fa97-145">{iothubhostname} should be hello full CName of hello IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="0fa97-146">Korzystając z [AMQP][lnk-amqp], obsługuje Centrum IoT [zwykły SASL] [ lnk-sasl-plain] i [AMQP oświadczenia na podstawie-zabezpieczeń] [ lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="0fa97-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="0fa97-147">Jeśli używasz protokołu AMQP oświadczenia na podstawie — zabezpieczeń, określa hello standardowe jak tootransmit tych tokenów.</span><span class="sxs-lookup"><span data-stu-id="0fa97-147">If you use AMQP claims-based-security, hello standard specifies how tootransmit these tokens.</span></span>

<span data-ttu-id="0fa97-148">Dla zwykłego SASL hello **username** może być:</span><span class="sxs-lookup"><span data-stu-id="0fa97-148">For SASL PLAIN, hello **username** can be:</span></span>

* <span data-ttu-id="0fa97-149">`{policyName}@sas.root.{iothubName}`Jeśli przy użyciu tokenów poziomie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="0fa97-150">`{deviceId}@sas.{iothubname}`Jeśli przy użyciu tokenów zakres urządzeń.</span><span class="sxs-lookup"><span data-stu-id="0fa97-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="0fa97-151">W obu przypadkach pole hasła hello zawiera hello token, zgodnie z opisem w [tokeny zabezpieczające Centrum IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="0fa97-151">In both cases, hello password field contains hello token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="0fa97-152">HTTP wykonuje uwierzytelnianie przy tym nieprawidłowy token w hello **autoryzacji** nagłówek żądania.</span><span class="sxs-lookup"><span data-stu-id="0fa97-152">HTTP implements authentication by including a valid token in hello **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="0fa97-153">Przykład</span><span class="sxs-lookup"><span data-stu-id="0fa97-153">Example</span></span>

<span data-ttu-id="0fa97-154">Nazwa użytkownika (DeviceId jest rozróżniana wielkość liter):`iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="0fa97-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="0fa97-155">Hasło (token Generowanie sygnatury dostępu Współdzielonego z hello [explorer urządzenia] [ lnk-device-explorer] narzędzie):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="0fa97-155">Password (Generate SAS token with hello [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="0fa97-156">Witaj [Azure IoT SDK] [ lnk-sdks] automatycznie generować tokeny podczas łączenia toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="0fa97-156">hello [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting toohello service.</span></span> <span data-ttu-id="0fa97-157">W niektórych przypadkach hello Azure IoT SDK nie obsługują wszystkie protokoły hello lub wszystkich metod uwierzytelniania hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-157">In some cases, hello Azure IoT SDKs do not support all hello protocols or all hello authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="0fa97-158">Uwagi dotyczące SASL zwykły</span><span class="sxs-lookup"><span data-stu-id="0fa97-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="0fa97-159">Korzystając z protokołu AMQP zwykły SASL, klienta nawiązującego połączenie tooan Centrum IoT można użyć jednego tokenu dla każdego połączenia TCP.</span><span class="sxs-lookup"><span data-stu-id="0fa97-159">When using SASL PLAIN with AMQP, a client connecting tooan IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="0fa97-160">Po wygaśnięciu tokenu hello hello połączenie TCP zakończy połączenie z usługą hello i wyzwala ponownego połączenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-160">When hello token expires, hello TCP connection disconnects from hello service and triggers a reconnect.</span></span> <span data-ttu-id="0fa97-161">To zachowanie, gdy nie powodować problemy dla aplikacji zaplecza, jest uszkodzenia aplikacji urządzenia dla hello z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="0fa97-161">This behavior, while not problematic for a back-end app, is damaging for a device app for hello following reasons:</span></span>

* <span data-ttu-id="0fa97-162">Bramy ze łączyć imieniu wiele urządzeń.</span><span class="sxs-lookup"><span data-stu-id="0fa97-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="0fa97-163">Przy użyciu zwykłego SASL, mają toocreate różne połączenia TCP dla każdego urządzenia łączenie tooan Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-163">When using SASL PLAIN, they have toocreate a distinct TCP connection for each device connecting tooan IoT hub.</span></span> <span data-ttu-id="0fa97-164">W tym scenariuszu znacznie zwiększa hello zużycia energii i zasobów sieciowych i zwiększa hello opóźnienie połączenia każdego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-164">This scenario considerably increases hello consumption of power and networking resources, and increases hello latency of each device connection.</span></span>
* <span data-ttu-id="0fa97-165">Ograniczone zasobów urządzeń dotkną hello zwiększone użycie tooreconnect zasobów po każdym wygaśnięcia tokenu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-165">Resource-constrained devices are adversely affected by hello increased use of resources tooreconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="0fa97-166">Zakres poświadczeń na poziomie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="0fa97-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="0fa97-167">Zakres zasad zabezpieczeń na poziomie Centrum IoT można określić, tworząc tokenów z ograniczeniami identyfikator URI zasobu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="0fa97-168">Na przykład wiadomości powitania od punktu końcowego toosend urządzenia do chmury przy użyciu urządzenia jest **/devices/ {deviceId} / wiadomości/zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="0fa97-168">For example, hello endpoint toosend device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="0fa97-169">Można także użyć zasady dostępu współdzielonego z poziomu Centrum IoT z **DeviceConnect** toosign uprawnienia tokenu, w których resourceURI jest **/devices/ {deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="0fa97-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions toosign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="0fa97-170">Ta metoda tworzy token, który jest tylko komunikaty toosend można używać w imieniu urządzenia **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="0fa97-170">This approach creates a token that is only usable toosend messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="0fa97-171">Mechanizm ten jest podobny toohello [zasad wydawcy usługi Event Hubs][lnk-event-hubs-publisher-policy]i umożliwia tooimplement niestandardowe metody uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0fa97-171">This mechanism is similar toohello [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you tooimplement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="0fa97-172">Tokeny zabezpieczające</span><span class="sxs-lookup"><span data-stu-id="0fa97-172">Security tokens</span></span>

<span data-ttu-id="0fa97-173">Centrum IoT używa zabezpieczeń tokeny tooauthenticate urządzeń i usług tooavoid wysyłania kluczy umieszczonego hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-173">IoT Hub uses security tokens tooauthenticate devices and services tooavoid sending keys on hello wire.</span></span> <span data-ttu-id="0fa97-174">Ponadto tokeny zabezpieczające są ograniczone w czas ważności i zakres.</span><span class="sxs-lookup"><span data-stu-id="0fa97-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="0fa97-175">[Zestawy Azure SDK IoT] [ lnk-sdks] automatycznie generować tokeny bez konieczności żadnej specjalnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0fa97-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="0fa97-176">Niektóre scenariusze wymaga toogenerate i korzystać bezpośrednio tokenów zabezpieczających.</span><span class="sxs-lookup"><span data-stu-id="0fa97-176">Some scenarios do require you toogenerate and use security tokens directly.</span></span> <span data-ttu-id="0fa97-177">Takie scenariusze obejmują:</span><span class="sxs-lookup"><span data-stu-id="0fa97-177">Such scenarios include:</span></span>

* <span data-ttu-id="0fa97-178">Witaj bezpośredniego użycia hello powierzchni MQTT AMQP i HTTP.</span><span class="sxs-lookup"><span data-stu-id="0fa97-178">hello direct use of hello MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="0fa97-179">Witaj implementacji wzorca usługi tokenu hello, zgodnie z objaśnieniem w [uwierzytelnianie urządzenia niestandardowe][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="0fa97-179">hello implementation of hello token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="0fa97-180">Centrum IoT umożliwia również tooauthenticate urządzenia z Centrum IoT przy użyciu [certyfikatów X.509][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="0fa97-180">IoT Hub also allows devices tooauthenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="0fa97-181">Struktura tokenu zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="0fa97-181">Security token structure</span></span>

<span data-ttu-id="0fa97-182">Należy używać zabezpieczeń tokeny toogrant ograniczonym czasie dostępu usługi i toodevices toospecific funkcji w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-182">You use security tokens toogrant time-bounded access toodevices and services toospecific functionality in IoT Hub.</span></span> <span data-ttu-id="0fa97-183">tooget autoryzacji tooconnect tooIoT koncentratora, urządzeń i usług musi wysyłanie tokenów zabezpieczających, podpisany dostępu współdzielonego lub klucza symetrycznego.</span><span class="sxs-lookup"><span data-stu-id="0fa97-183">tooget authorization tooconnect tooIoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="0fa97-184">Klucze te są przechowywane za pomocą tożsamości urządzenia w rejestrze tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-184">These keys are stored with a device identity in hello identity registry.</span></span>

<span data-ttu-id="0fa97-185">Podpisany token dostępu współdzielonego przyznaje klucza dostępu tooall hello funkcji skojarzonych z uprawnieniami zasad dostępu hello udostępnionych.</span><span class="sxs-lookup"><span data-stu-id="0fa97-185">A token signed with a shared access key grants access tooall hello functionality associated with hello shared access policy permissions.</span></span> <span data-ttu-id="0fa97-186">Podpisany token hello symetrycznego klucza przyznaje tylko urządzenia tożsamości **DeviceConnect** uprawnienie hello skojarzone tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-186">A token signed with a device identity's symmetric key only grants hello **DeviceConnect** permission for hello associated device identity.</span></span>

<span data-ttu-id="0fa97-187">token zabezpieczający Hello ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="0fa97-187">hello security token has hello following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="0fa97-188">Poniżej przedstawiono hello oczekiwanych wartości:</span><span class="sxs-lookup"><span data-stu-id="0fa97-188">Here are hello expected values:</span></span>

| <span data-ttu-id="0fa97-189">Wartość</span><span class="sxs-lookup"><span data-stu-id="0fa97-189">Value</span></span> | <span data-ttu-id="0fa97-190">Opis</span><span class="sxs-lookup"><span data-stu-id="0fa97-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0fa97-191">{sygnatury}</span><span class="sxs-lookup"><span data-stu-id="0fa97-191">{signature}</span></span> |<span data-ttu-id="0fa97-192">Ciąg HMAC SHA256 podpisu formularza hello: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="0fa97-192">An HMAC-SHA256 signature string of hello form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="0fa97-193">**Ważne**: klucz hello jest zdekodować z formatu base64 i użyć jako klucza tooperform hello HMAC SHA256 obliczeń.</span><span class="sxs-lookup"><span data-stu-id="0fa97-193">**Important**: hello key is decoded from base64 and used as key tooperform hello HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="0fa97-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="0fa97-194">{resourceURI}</span></span> |<span data-ttu-id="0fa97-195">Prefiks identyfikatora URI (według segmentu) hello punktów końcowych, które mogą być udostępniane z tym tokenem, począwszy od nazwy hosta Centrum IoT hello (nie protocol).</span><span class="sxs-lookup"><span data-stu-id="0fa97-195">URI prefix (by segment) of hello endpoints that can be accessed with this token, starting with host name of hello IoT hub (no protocol).</span></span> <span data-ttu-id="0fa97-196">Na przykład: `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="0fa97-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="0fa97-197">{wygaśnięcia}</span><span class="sxs-lookup"><span data-stu-id="0fa97-197">{expiry}</span></span> |<span data-ttu-id="0fa97-198">Ciągi UTF8 liczbę sekund od czasu UTC 00:00:00 epoki hello na 1 stycznia 1970.</span><span class="sxs-lookup"><span data-stu-id="0fa97-198">UTF8 strings for number of seconds since hello epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="0fa97-199">{URL-zakodowane resourceURI}</span><span class="sxs-lookup"><span data-stu-id="0fa97-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="0fa97-200">Małe przypadek kodowania adresów URL identyfikator URI zasobu małe litery hello</span><span class="sxs-lookup"><span data-stu-id="0fa97-200">Lower case URL-encoding of hello lower case resource URI</span></span> |
| <span data-ttu-id="0fa97-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="0fa97-201">{policyName}</span></span> |<span data-ttu-id="0fa97-202">Nazwa Hello hello udostępnionego toowhich zasad dostępu, który odwołuje się ten token.</span><span class="sxs-lookup"><span data-stu-id="0fa97-202">hello name of hello shared access policy toowhich this token refers.</span></span> <span data-ttu-id="0fa97-203">Brak w przypadku hello token odwołuje się poświadczenia toodevice rejestru.</span><span class="sxs-lookup"><span data-stu-id="0fa97-203">Absent if hello token refers toodevice-registry credentials.</span></span> |

<span data-ttu-id="0fa97-204">**Uwaga na prefiksie**: Prefiks URI hello jest obliczana przez segment, a nie przez znak.</span><span class="sxs-lookup"><span data-stu-id="0fa97-204">**Note on prefix**: hello URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="0fa97-205">Na przykład `/a/b` był prefiksem dla `/a/b/c` , ale nie dla `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="0fa97-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="0fa97-206">Witaj następujący fragment kodu Node.js zawiera funkcji o nazwie **generateSasToken** czy oblicza hello tokenu z wejść hello `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="0fa97-206">hello following Node.js snippet shows a function called **generateSasToken** that computes hello token from hello inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="0fa97-207">Hello kolejnych sekcjach szczegółowo opisano sposób tooinitialize hello różnych komponentów o inny token hello przypadki użycia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-207">hello next sections detail how tooinitialize hello different inputs for hello different token use cases.</span></span>

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

<span data-ttu-id="0fa97-208">Jako porównanie hello równoważne toogenerate kodu języka Python, który token zabezpieczający jest:</span><span class="sxs-lookup"><span data-stu-id="0fa97-208">As a comparison, hello equivalent Python code toogenerate a security token is:</span></span>

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> <span data-ttu-id="0fa97-209">Ponieważ hello czas ważności tokenu hello jest weryfikowane na komputerach Centrum IoT, odejście hello zegara hello hello maszyny, które generuje hello token musi być minimalny.</span><span class="sxs-lookup"><span data-stu-id="0fa97-209">Since hello time validity of hello token is validated on IoT Hub machines, hello drift on hello clock of hello machine that generates hello token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="0fa97-210">Używanie tokeny sygnatury dostępu Współdzielonego w aplikacji urządzeń</span><span class="sxs-lookup"><span data-stu-id="0fa97-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="0fa97-211">Istnieją dwa sposoby tooobtain **DeviceConnect** uprawnienia z Centrum IoT z tokenów zabezpieczających: Użyj [klucza symetrycznego urządzenia z rejestru tożsamości hello](#use-a-symmetric-key-in-the-identity-registry), lub użyj [udostępniony klucz dostępu](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="0fa97-211">There are two ways tooobtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from hello identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="0fa97-212">Należy pamiętać, że wszystkie funkcje dostępne z urządzeń jest udostępniany przez projekt w punktach końcowych z prefiksem `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="0fa97-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0fa97-213">Jedynym sposobem Hello, że Centrum IoT uwierzytelnia określonego urządzenia używa hello klucza symetrycznego tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-213">hello only way that IoT Hub authenticates a specific device is using hello device identity symmetric key.</span></span> <span data-ttu-id="0fa97-214">W przypadkach, gdy zasady dostępu współdzielonego jest używane tooaccess funkcjonalności, hello rozwiązania należy wziąć pod uwagę wystawiania tokenu zabezpieczającego hello jako zaufany podskładnika składnika hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-214">In cases when a shared access policy is used tooaccess device functionality, hello solution must consider hello component issuing hello security token as a trusted subcomponent.</span></span>

<span data-ttu-id="0fa97-215">punkty końcowe skierowane do urządzenia Hello są (niezależnie od protokołu hello):</span><span class="sxs-lookup"><span data-stu-id="0fa97-215">hello device-facing endpoints are (irrespective of hello protocol):</span></span>

| <span data-ttu-id="0fa97-216">Endpoint</span><span class="sxs-lookup"><span data-stu-id="0fa97-216">Endpoint</span></span> | <span data-ttu-id="0fa97-217">Funkcjonalność</span><span class="sxs-lookup"><span data-stu-id="0fa97-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="0fa97-218">Wysyłanie wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="0fa97-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="0fa97-219">Komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a><span data-ttu-id="0fa97-220">Użyj klucza symetrycznego w rejestrze tożsamości hello</span><span class="sxs-lookup"><span data-stu-id="0fa97-220">Use a symmetric key in hello identity registry</span></span>

<span data-ttu-id="0fa97-221">Podczas korzystania z urządzenia tożsamości toogenerate klucza symetrycznego token, hello Nazwa_zasady (`skn`) element hello token zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="0fa97-221">When using a device identity's symmetric key toogenerate a token, hello policyName (`skn`) element of hello token is omitted.</span></span>

<span data-ttu-id="0fa97-222">Na przykład token utworzony tooaccess wszystkie funkcje urządzenia powinien mieć hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="0fa97-222">For example, a token created tooaccess all device functionality should have hello following parameters:</span></span>

* <span data-ttu-id="0fa97-223">Identyfikator URI zasobu: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="0fa97-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="0fa97-224">Klucz podpisujący: dowolnego klucza symetrycznego dla hello `{device id}` tożsamości,</span><span class="sxs-lookup"><span data-stu-id="0fa97-224">signing key: any symmetric key for hello `{device id}` identity,</span></span>
* <span data-ttu-id="0fa97-225">Brak nazwy zasad</span><span class="sxs-lookup"><span data-stu-id="0fa97-225">no policy name,</span></span>
* <span data-ttu-id="0fa97-226">wszelkie czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-226">any expiration time.</span></span>

<span data-ttu-id="0fa97-227">Przykładem przy użyciu hello poprzedzających funkcja Node.js może być:</span><span class="sxs-lookup"><span data-stu-id="0fa97-227">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="0fa97-228">Witaj, zapewniającej dostęp do funkcji tooall device1 nastąpiłoby:</span><span class="sxs-lookup"><span data-stu-id="0fa97-228">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="0fa97-229">Jego jest możliwe toogenerate token sygnatury dostępu Współdzielonego przy użyciu platformy .NET hello [explorer urządzenia] [ lnk-device-explorer] narzędzie lub hello i platform, na podstawie węzła [explorer Centrum iothub] [ lnk-iothub-explorer] narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-229">It is possible toogenerate a SAS token using hello .NET [device explorer][lnk-device-explorer] tool or hello cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="0fa97-230">Użyj zasad dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="0fa97-230">Use a shared access policy</span></span>

<span data-ttu-id="0fa97-231">Podczas tworzenia tokenu z zasad dostępu współdzielonego, ustaw hello `skn` pole Nazwa toohello hello zasad.</span><span class="sxs-lookup"><span data-stu-id="0fa97-231">When you create a token from a shared access policy, set hello `skn` field toohello name of hello policy.</span></span> <span data-ttu-id="0fa97-232">Ta zasada musi udzielić hello **DeviceConnect** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-232">This policy must grant hello **DeviceConnect** permission.</span></span>

<span data-ttu-id="0fa97-233">Witaj dwa główne scenariusze korzystania z funkcji urządzenia tooaccess zasady dostępu współdzielonego są:</span><span class="sxs-lookup"><span data-stu-id="0fa97-233">hello two main scenarios for using shared access policies tooaccess device functionality are:</span></span>

* <span data-ttu-id="0fa97-234">[chmury bramy protokołu][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="0fa97-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="0fa97-235">[token usługi] [ lnk-custom-auth] używane tooimplement schematy uwierzytelniania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="0fa97-235">[token services][lnk-custom-auth] used tooimplement custom authentication schemes.</span></span>

<span data-ttu-id="0fa97-236">Od hello zasady dostępu współdzielonego może potencjalnie przyznanie dostępu tooconnect jako dowolnego urządzenia podczas tworzenia tokenów zabezpieczających jest ważne toouse hello poprawne zasobów identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="0fa97-236">Since hello shared access policy can potentially grant access tooconnect as any device, it is important toouse hello correct resource URI when creating security tokens.</span></span> <span data-ttu-id="0fa97-237">To ustawienie jest szczególnie ważne w przypadku tokenów usług, które mają tooscope hello token tooa określonego urządzenia przy użyciu identyfikatora URI zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-237">This setting is especially important for token services, which have tooscope hello token tooa specific device using hello resource URI.</span></span> <span data-ttu-id="0fa97-238">Ten punkt jest mniej istotne dla bramy protokołu, ponieważ są one już pośredniczących ruchu dla wszystkich urządzeń.</span><span class="sxs-lookup"><span data-stu-id="0fa97-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="0fa97-239">Na przykład usługi tokenu przy użyciu wstępnie utworzonej hello udostępnionych zasady dostępu o nazwie **urządzenia** utworzyć token z hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="0fa97-239">As an example, a token service using hello pre-created shared access policy called **device** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="0fa97-240">Identyfikator URI zasobu: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="0fa97-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="0fa97-241">Klucz podpisujący: jeden z kluczy hello hello `device` zasad,</span><span class="sxs-lookup"><span data-stu-id="0fa97-241">signing key: one of hello keys of hello `device` policy,</span></span>
* <span data-ttu-id="0fa97-242">Nazwa zasad: `device`,</span><span class="sxs-lookup"><span data-stu-id="0fa97-242">policy name: `device`,</span></span>
* <span data-ttu-id="0fa97-243">wszelkie czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-243">any expiration time.</span></span>

<span data-ttu-id="0fa97-244">Przykładem przy użyciu hello poprzedzających funkcja Node.js może być:</span><span class="sxs-lookup"><span data-stu-id="0fa97-244">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="0fa97-245">Witaj, zapewniającej dostęp do funkcji tooall device1 nastąpiłoby:</span><span class="sxs-lookup"><span data-stu-id="0fa97-245">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="0fa97-246">Brama protokołu można użyć hello token takie same dla wszystkich urządzeń, wystarczy wybrać ustawienie zbyt hello identyfikator URI zasobu`myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="0fa97-246">A protocol gateway could use hello same token for all devices simply setting hello resource URI too`myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="0fa97-247">Używaj tokenów zabezpieczeń z składniki usługi</span><span class="sxs-lookup"><span data-stu-id="0fa97-247">Use security tokens from service components</span></span>

<span data-ttu-id="0fa97-248">Składniki usługi można generować tylko tokeny zabezpieczające, za pomocą zasad dostępu współdzielonego udzielanie hello odpowiednie uprawnienia, zgodnie z objaśnieniem wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0fa97-248">Service components can only generate security tokens using shared access policies granting hello appropriate permissions as explained previously.</span></span>

<span data-ttu-id="0fa97-249">Poniżej przedstawiono funkcje usługi hello narażone na powitania punktów końcowych:</span><span class="sxs-lookup"><span data-stu-id="0fa97-249">Here is hello service functions exposed on hello endpoints:</span></span>

| <span data-ttu-id="0fa97-250">Endpoint</span><span class="sxs-lookup"><span data-stu-id="0fa97-250">Endpoint</span></span> | <span data-ttu-id="0fa97-251">Funkcjonalność</span><span class="sxs-lookup"><span data-stu-id="0fa97-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="0fa97-252">Tworzenie, aktualizowanie, pobrać i usuwania tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="0fa97-253">Komunikaty urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="0fa97-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="0fa97-254">Otrzymasz opinię komunikatów chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="0fa97-255">Wysyłanie wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="0fa97-256">Na przykład usługi generowania przy użyciu wstępnie utworzonej hello udostępnionych zasady dostępu o nazwie **registryRead** utworzyć token z hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="0fa97-256">As an example, a service generating using hello pre-created shared access policy called **registryRead** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="0fa97-257">Identyfikator URI zasobu: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="0fa97-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="0fa97-258">Klucz podpisujący: jeden z kluczy hello hello `registryRead` zasad,</span><span class="sxs-lookup"><span data-stu-id="0fa97-258">signing key: one of hello keys of hello `registryRead` policy,</span></span>
* <span data-ttu-id="0fa97-259">Nazwa zasad: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="0fa97-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="0fa97-260">wszelkie czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="0fa97-261">wynik Hello, którym przyznano dostęp tooread wszystkich tożsamości urządzenia, będzie:</span><span class="sxs-lookup"><span data-stu-id="0fa97-261">hello result, which would grant access tooread all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="0fa97-262">Obsługiwane certyfikaty X.509</span><span class="sxs-lookup"><span data-stu-id="0fa97-262">Supported X.509 certificates</span></span>

<span data-ttu-id="0fa97-263">Można użyć dowolnego tooauthenticate certyfikatu X.509 urządzenie z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-263">You can use any X.509 certificate tooauthenticate a device with IoT Hub.</span></span> <span data-ttu-id="0fa97-264">Certyfikaty obejmują:</span><span class="sxs-lookup"><span data-stu-id="0fa97-264">Certificates include:</span></span>

* <span data-ttu-id="0fa97-265">**Istniejący certyfikat X.509**.</span><span class="sxs-lookup"><span data-stu-id="0fa97-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="0fa97-266">Urządzenie może już być skojarzone z nim certyfikatu X.509.</span><span class="sxs-lookup"><span data-stu-id="0fa97-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="0fa97-267">Witaj urządzenie może używać tego certyfikatu tooauthenticate z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-267">hello device can use this certificate tooauthenticate with IoT Hub.</span></span>
* <span data-ttu-id="0fa97-268">**A własnym wygenerowany i X-509 certyfikat z podpisem własnym**.</span><span class="sxs-lookup"><span data-stu-id="0fa97-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="0fa97-269">Producenta urządzenia lub wewnętrznych narzędzia wdrażania można wygenerować tych certyfikatów i przechowywać hello odpowiadające im klucze prywatne (i certyfikatu) na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-269">A device manufacturer or in-house deployer can generate these certificates and store hello corresponding private key (and certificate) on hello device.</span></span> <span data-ttu-id="0fa97-270">Można użyć narzędzia, takie jak [OpenSSL] [ lnk-openssl] i [Windows SelfSignedCertificate] [ lnk-selfsigned] narzędzie do tego celu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="0fa97-271">**Podpisany przez urząd certyfikacji certyfikatu X.509**.</span><span class="sxs-lookup"><span data-stu-id="0fa97-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="0fa97-272">tooidentify urządzenia oraz uwierzytelniania go z Centrum IoT, można użyć certyfikatu X.509 wygenerowany i podpisany przez urząd certyfikacji (CA).</span><span class="sxs-lookup"><span data-stu-id="0fa97-272">tooidentify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="0fa97-273">Centrum IoT sprawdza tylko tym palca hello przedstawione zgodny z odciskiem palca hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="0fa97-273">IoT Hub only verifies that hello thumbprint presented matches hello configured thumbprint.</span></span> <span data-ttu-id="0fa97-274">Centrum IotHub nie można zweryfikować łańcucha certyfikatów hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-274">IotHub does not validate hello certificate chain.</span></span>

<span data-ttu-id="0fa97-275">Urządzenie może użyć certyfikatu X.509 lub tokenu zabezpieczającego dla uwierzytelniania, ale nie oba.</span><span class="sxs-lookup"><span data-stu-id="0fa97-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="0fa97-276">Zarejestruj certyfikat X.509 dla urządzenia</span><span class="sxs-lookup"><span data-stu-id="0fa97-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="0fa97-277">Witaj [Azure IoT usługi SDK dla języka C#] [ lnk-service-sdk] (wersja 1.0.8+) obsługuje rejestrowanie urządzenia, który używa certyfikatu X.509 do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0fa97-277">hello [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="0fa97-278">Innych interfejsów API, takich jak importu/eksportu urządzeń obsługuje także certyfikaty X.509.</span><span class="sxs-lookup"><span data-stu-id="0fa97-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="0fa97-279">C\# pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="0fa97-279">C\# Support</span></span>

<span data-ttu-id="0fa97-280">Witaj **RegistryManager** klasa udostępnia tooregister sposób programowy urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-280">hello **RegistryManager** class provides a programmatic way tooregister a device.</span></span> <span data-ttu-id="0fa97-281">W szczególności hello **AddDeviceAsync** i **UpdateDeviceAsync** metody umożliwiają tooregister i zaktualizować urządzenie w hello rejestru tożsamości Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-281">In particular, hello **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you tooregister and update a device in hello IoT Hub identity registry.</span></span> <span data-ttu-id="0fa97-282">Te dwie metody przyjmują **urządzenia** wystąpienia jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="0fa97-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="0fa97-283">Witaj **urządzenia** klasa zawiera **uwierzytelniania** właściwość, która umożliwia toospecify podstawowych i pomocniczych X.509 odciski palców certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-283">hello **Device** class includes an **Authentication** property that allows you toospecify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="0fa97-284">Odcisk palca Hello reprezentuje wartości skrótu SHA-1 certyfikatu X.509 hello (przechowywane przy użyciu kodowania binarnego DER).</span><span class="sxs-lookup"><span data-stu-id="0fa97-284">hello thumbprint represents a SHA-1 hash of hello X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="0fa97-285">Masz hello możliwość określenia podstawowego odcisk palca lub dodatkowej odcisk palca lub oba.</span><span class="sxs-lookup"><span data-stu-id="0fa97-285">You have hello option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="0fa97-286">Odciski palców podstawowych i pomocniczych są obsługiwane toohandle certyfikatu przerzucania scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="0fa97-286">Primary and secondary thumbprints are supported toohandle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="0fa97-287">Centrum IoT nie wymagają lub zapisać całą hello X.509 certyfikatu, tylko hello odcisk palca.</span><span class="sxs-lookup"><span data-stu-id="0fa97-287">IoT Hub does not require or store hello entire X.509 certificate, only hello thumbprint.</span></span>

<span data-ttu-id="0fa97-288">Poniżej przedstawiono przykładowe C\# kodu tooregister fragment urządzenia przy użyciu certyfikatu X.509:</span><span class="sxs-lookup"><span data-stu-id="0fa97-288">Here is a sample C\# code snippet tooregister a device using an X.509 certificate:</span></span>

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="0fa97-289">Użyj certyfikatu X.509 podczas operacji w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="0fa97-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="0fa97-290">Witaj [urządzenia Azure IoT SDK dla platformy .NET] [ lnk-client-sdk] (wersja 1.0.11+) obsługuje hello przy użyciu certyfikatów X.509.</span><span class="sxs-lookup"><span data-stu-id="0fa97-290">hello [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports hello use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="0fa97-291">C\# pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="0fa97-291">C\# Support</span></span>

<span data-ttu-id="0fa97-292">Witaj klasy **DeviceAuthenticationWithX509Certificate** obsługuje hello tworzenie **DeviceClient** wystąpienia za pomocą certyfikatu X.509.</span><span class="sxs-lookup"><span data-stu-id="0fa97-292">hello class **DeviceAuthenticationWithX509Certificate** supports hello creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="0fa97-293">Certyfikat X.509 Hello musi być w formacie PFX (nazywany również PKCS #12) hello, który zawiera klucz prywatny hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-293">hello X.509 certificate must be in hello PFX (also called PKCS #12) format that includes hello private key.</span></span>

<span data-ttu-id="0fa97-294">Oto fragment kodu próbki:</span><span class="sxs-lookup"><span data-stu-id="0fa97-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="0fa97-295">Uwierzytelnianie urządzeń niestandardowych</span><span class="sxs-lookup"><span data-stu-id="0fa97-295">Custom device authentication</span></span>

<span data-ttu-id="0fa97-296">Można użyć hello Centrum IoT [rejestru tożsamości] [ lnk-identity-registry] dostępu i poświadczenia zabezpieczeń na urządzenie tooconfigure można kontrolować przy użyciu [tokenów] [ lnk-sas-tokens] .</span><span class="sxs-lookup"><span data-stu-id="0fa97-296">You can use hello IoT Hub [identity registry][lnk-identity-registry] tooconfigure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="0fa97-297">Jeśli rozwiązania IoT już schemat rejestru i/lub uwierzytelnianie tożsamości niestandardowej, należy rozważyć utworzenie *token usługi* toointegrate tej infrastruktury z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* toointegrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="0fa97-298">W ten sposób można użyć innych funkcji IoT w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="0fa97-299">Token usługi to usługa w chmurze niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="0fa97-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="0fa97-300">Używa Centrum IoT *udostępnionych zasad dostępu* z **DeviceConnect** toocreate uprawnienia *zakres urządzeń* tokenów.</span><span class="sxs-lookup"><span data-stu-id="0fa97-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions toocreate *device-scoped* tokens.</span></span> <span data-ttu-id="0fa97-301">Tokeny te umożliwiają Centrum IoT tooyour tooconnect urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-301">These tokens enable a device tooconnect tooyour IoT hub.</span></span>

![Kroki hello usługi tokenu wzorca][img-tokenservice]

<span data-ttu-id="0fa97-303">Oto główne kroki hello hello usługi tokenu wzorca:</span><span class="sxs-lookup"><span data-stu-id="0fa97-303">Here are hello main steps of hello token service pattern:</span></span>

1. <span data-ttu-id="0fa97-304">Tworzenie zasad dostępu do udostępnionego Centrum IoT z **DeviceConnect** uprawnienia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="0fa97-305">Te zasady można tworzyć w hello [portalu Azure] [ lnk-management-portal] lub programowo.</span><span class="sxs-lookup"><span data-stu-id="0fa97-305">You can create this policy in hello [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="0fa97-306">Hello usługi tokenu używa tej zasady tokeny hello toosign tworzonego.</span><span class="sxs-lookup"><span data-stu-id="0fa97-306">hello token service uses this policy toosign hello tokens it creates.</span></span>
1. <span data-ttu-id="0fa97-307">Gdy urządzenie musi tooaccess Centrum IoT, żądań podpisany token z usługą tokenu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-307">When a device needs tooaccess your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="0fa97-308">Hello urządzenia mogą uwierzytelniać za pomocą tożsamości urządzenia hello toodetermine schemat tożsamość niestandardowa rejestru/uwierzytelniania używany toocreate hello token hello usługi tokenu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-308">hello device can authenticate with your custom identity registry/authentication scheme toodetermine hello device identity that hello token service uses toocreate hello token.</span></span>
1. <span data-ttu-id="0fa97-309">Usługa tokenu Hello zwraca token.</span><span class="sxs-lookup"><span data-stu-id="0fa97-309">hello token service returns a token.</span></span> <span data-ttu-id="0fa97-310">Witaj token jest tworzona przy użyciu `/devices/{deviceId}` jako `resourceURI`, z `deviceId` jako urządzenie hello jest uwierzytelniane.</span><span class="sxs-lookup"><span data-stu-id="0fa97-310">hello token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as hello device being authenticated.</span></span> <span data-ttu-id="0fa97-311">Usługa tokenu Hello używa hello dostępu współdzielonego zasad tooconstruct hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-311">hello token service uses hello shared access policy tooconstruct hello token.</span></span>
1. <span data-ttu-id="0fa97-312">Witaj urządzenie używa tokenu hello bezpośrednio z Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-312">hello device uses hello token directly with hello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="0fa97-313">Można użyć klasy .NET hello [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] lub hello Klasa Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate tokenu w usłudze tokenu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-313">You can use hello .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or hello Java class [IotHubServiceSasToken][lnk-java-sas] toocreate a token in your token service.</span></span>

<span data-ttu-id="0fa97-314">Usługa tokenu Hello można ustawić wygaśnięcia tokenu hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="0fa97-314">hello token service can set hello token expiration as desired.</span></span> <span data-ttu-id="0fa97-315">Po wygaśnięciu tokenu hello Centrum IoT hello serwery hello połączenie z urządzeniem.</span><span class="sxs-lookup"><span data-stu-id="0fa97-315">When hello token expires, hello IoT hub severs hello device connection.</span></span> <span data-ttu-id="0fa97-316">Następnie hello urządzenia należy zażądać nowego tokenu z usługi tokenu hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-316">Then, hello device must request a new token from hello token service.</span></span> <span data-ttu-id="0fa97-317">Czas wygaśnięcia krótki zwiększa obciążenie hello hello urządzeniu i na powitania usługi tokenu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-317">A short expiry time increases hello load on both hello device and hello token service.</span></span>

<span data-ttu-id="0fa97-318">Dla koncentratora tooyour tooconnect urządzenia, należy nadal go dodać toohello rejestru tożsamości Centrum IoT — mimo że hello urządzenie korzysta z tokenu i nie tooconnect klucza urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-318">For a device tooconnect tooyour hub, you must still add it toohello IoT Hub identity registry — even though hello device is using a token and not a device key tooconnect.</span></span> <span data-ttu-id="0fa97-319">W związku z tym można kontynuować kontroli dostępu na urządzeniu toouse przez włączenie lub wyłączenie tożsamości urządzenia w hello [rejestru tożsamości][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="0fa97-319">Therefore, you can continue toouse per-device access control by enabling or disabling device identities in hello [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="0fa97-320">Takie podejście zmniejsza ryzyko hello używania tokenów z wygaśnięcia długi czas.</span><span class="sxs-lookup"><span data-stu-id="0fa97-320">This approach mitigates hello risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="0fa97-321">Porównanie z bramą niestandardowych</span><span class="sxs-lookup"><span data-stu-id="0fa97-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="0fa97-322">Wzorzec usługi tokenu Hello jest hello zalecany sposób tooimplement schemat rejestru/uwierzytelniania tożsamość niestandardowa z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-322">hello token service pattern is hello recommended way tooimplement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="0fa97-323">Ten wzorzec jest zalecane, ponieważ Centrum IoT nadal toohandle większość hello rozwiązania ruchu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-323">This pattern is recommended because IoT Hub continues toohandle most of hello solution traffic.</span></span> <span data-ttu-id="0fa97-324">Jednak jeśli schemat uwierzytelniania niestandardowego hello więc jest sprzężony z protokołem hello, mogą wymagać *bram* tooprocess wszystkie hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-324">However, if hello custom authentication scheme is so intertwined with hello protocol, you may require a *custom gateway* tooprocess all hello traffic.</span></span> <span data-ttu-id="0fa97-325">Przykładem takiej sytuacji jest przy użyciu[zabezpieczeń TLS (Transport Layer) i kluczy wstępnych (PSKs)][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="0fa97-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="0fa97-326">Aby uzyskać więcej informacji, zobacz hello [bramy protokołu] [ lnk-protocols] tematu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-326">For more information, see hello [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="0fa97-327">Tematy odwołań:</span><span class="sxs-lookup"><span data-stu-id="0fa97-327">Reference topics:</span></span>

<span data-ttu-id="0fa97-328">Witaj następujące tematy dokumentacji zapewniają więcej informacji na temat kontrolowania dostępu tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0fa97-328">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="0fa97-329">Centrum IoT uprawnień</span><span class="sxs-lookup"><span data-stu-id="0fa97-329">IoT Hub permissions</span></span>

<span data-ttu-id="0fa97-330">Witaj Poniższa tabela zawiera listę uprawnień hello można użyć Centrum IoT tooyour dostępu toocontrol.</span><span class="sxs-lookup"><span data-stu-id="0fa97-330">hello following table lists hello permissions you can use toocontrol access tooyour IoT hub.</span></span>

| <span data-ttu-id="0fa97-331">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="0fa97-331">Permission</span></span> | <span data-ttu-id="0fa97-332">Uwagi</span><span class="sxs-lookup"><span data-stu-id="0fa97-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="0fa97-333">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="0fa97-333">**RegistryRead**</span></span> |<span data-ttu-id="0fa97-334">Przyznaje dostęp do odczytu toohello tożsamości rejestru.</span><span class="sxs-lookup"><span data-stu-id="0fa97-334">Grants read access toohello identity registry.</span></span> <span data-ttu-id="0fa97-335">Aby uzyskać więcej informacji, zobacz [rejestru tożsamości][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="0fa97-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="0fa97-336">To uprawnienie jest używany przez usługi w chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="0fa97-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="0fa97-337">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="0fa97-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="0fa97-338">Udziela dostępu odczytu i zapisu toohello rejestrze tożsamości.</span><span class="sxs-lookup"><span data-stu-id="0fa97-338">Grants read and write access toohello identity registry.</span></span> <span data-ttu-id="0fa97-339">Aby uzyskać więcej informacji, zobacz [rejestru tożsamości][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="0fa97-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="0fa97-340">To uprawnienie jest używany przez usługi w chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="0fa97-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="0fa97-341">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="0fa97-341">**ServiceConnect**</span></span> |<span data-ttu-id="0fa97-342">Przyznaje dostęp komunikacji usługi połączonej toocloud i monitorowania punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="0fa97-342">Grants access toocloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="0fa97-343">Przyznaje uprawnienia tooreceive urządzenia do chmury wiadomości wysyłania wiadomości chmury do urządzenia i pobrać hello odpowiadającego potwierdzeń dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-343">Grants permission tooreceive device-to-cloud messages, send cloud-to-device messages, and retrieve hello corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="0fa97-344">Przyznaje uprawnienia tooretrieve dostarczanie potwierdzeń pliku operacji przekazywania.</span><span class="sxs-lookup"><span data-stu-id="0fa97-344">Grants permission tooretrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="0fa97-345">Przyznaje uprawnienia tooaccess urządzenia twins tooupdate tagów i odpowiednie właściwości pobierania właściwości zgłoszone, a następnie uruchom zapytania.</span><span class="sxs-lookup"><span data-stu-id="0fa97-345">Grants permission tooaccess device twins tooupdate tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="0fa97-346">To uprawnienie jest używany przez usługi w chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="0fa97-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="0fa97-347">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="0fa97-347">**DeviceConnect**</span></span> |<span data-ttu-id="0fa97-348">Udziela dostępu do punktów końcowych toodevice uwzględniającym.</span><span class="sxs-lookup"><span data-stu-id="0fa97-348">Grants access toodevice-facing endpoints.</span></span> <br/><span data-ttu-id="0fa97-349">Przyznaje uprawnienia toosend urządzenia do chmury wiadomości i odbieranie wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-349">Grants permission toosend device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="0fa97-350">Przyznaje uprawnienia tooperform przekazywania pliku z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-350">Grants permission tooperform file upload from a device.</span></span> <br/><span data-ttu-id="0fa97-351">Przyznaje uprawnienia tooreceive urządzenia potrzebne dwie właściwości powiadomień i aktualizacji urządzenia dwie właściwości zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="0fa97-351">Grants permission tooreceive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="0fa97-352">Przyznaje uprawnienia tooperform pliku operacji przekazywania.</span><span class="sxs-lookup"><span data-stu-id="0fa97-352">Grants permission tooperform file uploads.</span></span> <br/><span data-ttu-id="0fa97-353">To uprawnienie jest używany przez urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0fa97-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="0fa97-354">Odwołanie dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="0fa97-354">Additional reference material</span></span>

<span data-ttu-id="0fa97-355">Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:</span><span class="sxs-lookup"><span data-stu-id="0fa97-355">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="0fa97-356">[Punkty końcowe Centrum IoT] [ lnk-endpoints] opisuje hello różnych punktów końcowych, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="0fa97-356">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="0fa97-357">[Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziały hello i ograniczanie zachowań stosowane toohello usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0fa97-357">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="0fa97-358">[Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] list hello języka różnych zestawów SDK, można użyć podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0fa97-358">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="0fa97-359">[Język zapytań Centrum IoT] [ lnk-query] opisuje tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend hello.</span><span class="sxs-lookup"><span data-stu-id="0fa97-359">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="0fa97-360">[Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zamieszczono więcej informacji o obsłudze Centrum IoT hello MQTT protokołu.</span><span class="sxs-lookup"><span data-stu-id="0fa97-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fa97-361">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0fa97-361">Next steps</span></span>

<span data-ttu-id="0fa97-362">Teraz wiesz już, jak toocontrol uzyskują dostęp do Centrum IoT, może Cię zainteresować następujące tematy przewodnik dewelopera Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="0fa97-362">Now you have learned how toocontrol access IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="0fa97-363">[Urządzenie twins toosynchronize stanu i konfiguracji][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="0fa97-363">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="0fa97-364">[Wywoływanie metody bezpośrednio na urządzeniu][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="0fa97-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="0fa97-365">[Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="0fa97-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="0fa97-366">Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello następujące samouczki Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="0fa97-366">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="0fa97-367">[Rozpoczynanie pracy z Centrum IoT Azure][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="0fa97-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="0fa97-368">[Jak komunikaty toosend chmury do urządzenia z Centrum IoT][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="0fa97-368">[How toosend cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="0fa97-369">[Jak tooprocess Centrum IoT urządzenia do chmury wiadomości][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="0fa97-369">[How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
