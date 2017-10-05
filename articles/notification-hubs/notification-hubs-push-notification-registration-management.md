---
title: "Zarządzanie rejestracji"
description: "W tym temacie wyjaśniono, jak zarejestrować urządzenia z usługą notification hubs w celu odbierania powiadomień wypychanych."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: a1a349150ef4c7837932706f0c4fcc8d022ec7ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="registration-management"></a><span data-ttu-id="e3b88-103">Zarządzanie rejestracją</span><span class="sxs-lookup"><span data-stu-id="e3b88-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="e3b88-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e3b88-104">Overview</span></span>
<span data-ttu-id="e3b88-105">W tym temacie wyjaśniono, jak zarejestrować urządzenia z usługą notification hubs w celu odbierania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="e3b88-105">This topic explains how to register devices with notification hubs in order to receive push notifications.</span></span> <span data-ttu-id="e3b88-106">Temat opisuje rejestracji na wysokim poziomie, a następnie wprowadza dwa główne wzorce do rejestracji urządzeń: rejestrację z urządzenia bezpośrednio w Centrum powiadomień i rejestrowanie za pomocą wewnętrznej bazy danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-106">The topic describes registrations at a high level, then introduces the two main patterns for registering devices: registering from the device directly to the notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="e3b88-107">Co to jest rejestracja urządzenia</span><span class="sxs-lookup"><span data-stu-id="e3b88-107">What is device registration</span></span>
<span data-ttu-id="e3b88-108">Rejestracja urządzenia z Centrum powiadomień odbywa się przy użyciu **rejestracji** lub **instalacji**.</span><span class="sxs-lookup"><span data-stu-id="e3b88-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="e3b88-109">Rejestracje</span><span class="sxs-lookup"><span data-stu-id="e3b88-109">Registrations</span></span>
<span data-ttu-id="e3b88-110">Rejestracja kojarzy dojścia usługi powiadomień platformy (PNS) dla urządzenia z tagami i prawdopodobnie szablonu.</span><span class="sxs-lookup"><span data-stu-id="e3b88-110">A registration associates the Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="e3b88-111">Dojście systemu powiadomień platformy można ChannelURI, token urządzenia lub identyfikator rejestracji usługi GCM.</span><span class="sxs-lookup"><span data-stu-id="e3b88-111">The PNS handle could be a ChannelURI, device token, or GCM registration id.</span></span> <span data-ttu-id="e3b88-112">Tagi są używane do kierowania powiadomień do poprawny zestaw dojść urządzeń.</span><span class="sxs-lookup"><span data-stu-id="e3b88-112">Tags are used to route notifications to the correct set of device handles.</span></span> <span data-ttu-id="e3b88-113">Aby uzyskać więcej informacji, zobacz [routingu i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="e3b88-113">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="e3b88-114">Szablony są używane do implementowania na rejestracji przekształcenia.</span><span class="sxs-lookup"><span data-stu-id="e3b88-114">Templates are used to implement per-registration transformation.</span></span> <span data-ttu-id="e3b88-115">Aby uzyskać więcej informacji, zobacz [szablony](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="e3b88-115">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="e3b88-116">Instalacje</span><span class="sxs-lookup"><span data-stu-id="e3b88-116">Installations</span></span>
<span data-ttu-id="e3b88-117">Instalacja jest rozszerzonych właściwości powiązanych z rejestrację, która zawiera zbiór wypychania.</span><span class="sxs-lookup"><span data-stu-id="e3b88-117">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="e3b88-118">Jest to najnowsze i najlepsze rozwiązanie z rejestracją urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e3b88-118">It is the latest and best approach to registering your devices.</span></span> <span data-ttu-id="e3b88-119">Jednak nie jest obsługiwany przez klienta po stronie zestawu SDK programu .NET ([SDK Centrum powiadomień dla wewnętrznej bazy danych operacji](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) jeszcze.</span><span class="sxs-lookup"><span data-stu-id="e3b88-119">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="e3b88-120">Oznacza to, w przypadku rejestracji na urządzeniu klienckim, należy użyć [interfejsu API REST centra powiadomień](https://msdn.microsoft.com/library/mt621153.aspx) podejście do obsługi instalacji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-120">This means if you are registering from the client device itself, you would have to use the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach to support installations.</span></span> <span data-ttu-id="e3b88-121">Jeśli używasz usługi wewnętrznej bazy danych powinno być możliwe do użycia [SDK Centrum powiadomień dla wewnętrznej bazy danych operacji](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="e3b88-121">If you are using a backend service, you should be able to use [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="e3b88-122">Poniżej przedstawiono niektóre kluczowe zalety korzystania z instalacji:</span><span class="sxs-lookup"><span data-stu-id="e3b88-122">The following are some key advantages to using installations:</span></span>

* <span data-ttu-id="e3b88-123">Tworzenie lub aktualizowanie instalacji jest w pełni idempotentności.</span><span class="sxs-lookup"><span data-stu-id="e3b88-123">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="e3b88-124">Dlatego możesz ponowić próbę jej bez żadnych problemów dotyczących rejestracji duplikatów.</span><span class="sxs-lookup"><span data-stu-id="e3b88-124">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="e3b88-125">Model instalacji ułatwia czy poszczególnych wypchnięć - przeznaczonych dla określonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e3b88-125">The installation model makes it easy to do individual pushes - targeting specific device.</span></span> <span data-ttu-id="e3b88-126">Tag systemu **"$InstallationId: [identyfikator installationId]"** jest automatycznie dodawany z każdej instalacji na podstawie rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-126">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="e3b88-127">Dlatego należy wywołać Wyślij do tego znacznika do określonego urządzenia bez konieczności dodatkowe kodowania.</span><span class="sxs-lookup"><span data-stu-id="e3b88-127">So you can call a send to this tag to target a specific device without having to do any additional coding.</span></span>
* <span data-ttu-id="e3b88-128">Przy użyciu instalacji umożliwia także aktualizacje częściowe rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-128">Using installations also enables you to do partial registration updates.</span></span> <span data-ttu-id="e3b88-129">Zażądano częściowej aktualizacji instalacji z metody poprawki przy użyciu [standard JSON poprawki](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="e3b88-129">The partial update of an installation is requested with a PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="e3b88-130">Jest to szczególnie przydatne, jeśli chcesz zaktualizować tagów do rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-130">This is particularly useful when you want to update tags on the registration.</span></span> <span data-ttu-id="e3b88-131">Nie trzeba rozwiń całego rejestracji, a następnie ponownie Wyślij ponownie wszystkie poprzednie tagi.</span><span class="sxs-lookup"><span data-stu-id="e3b88-131">You don't have to pull down the entire registration and then resend all the previous tags again.</span></span>

<span data-ttu-id="e3b88-132">Instalacja produktu może zawierać następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="e3b88-132">An installation can contain the the following properties.</span></span> <span data-ttu-id="e3b88-133">Aby uzyskać pełną listę można znaleźć właściwości instalacji, [utworzyć ani zastąpić instalacji z interfejsu API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) lub [właściwości instalacji](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) dla.</span><span class="sxs-lookup"><span data-stu-id="e3b88-133">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for the .</span></span>

    // Example installation format to show some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



<span data-ttu-id="e3b88-134">Należy pamiętać, że rejestracji i instalacje domyślnie nie wygasają już.</span><span class="sxs-lookup"><span data-stu-id="e3b88-134">It is important to note that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="e3b88-135">Rejestracje i instalacji musi zawierać prawidłowe dojście systemu powiadomień platformy dla każdego urządzenia/kanału.</span><span class="sxs-lookup"><span data-stu-id="e3b88-135">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="e3b88-136">Ponieważ dojść systemu powiadomień platformy można uzyskać tylko w aplikacji klienta, na urządzeniu, jeden wzorzec jest zarejestrować bezpośrednio na tym urządzeniu z aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="e3b88-136">Because PNS handles can only be obtained in a client app on the device, one pattern is to register directly on that device with the client app.</span></span> <span data-ttu-id="e3b88-137">Z drugiej strony, zagadnienia dotyczące zabezpieczeń i powiązane z tagami logiki biznesowej może być konieczne umożliwia zarządzanie rejestracją urządzeń w aplikacji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="e3b88-137">On the other hand, security considerations and business logic related to tags might require you to manage device registration in the app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="e3b88-138">Szablony</span><span class="sxs-lookup"><span data-stu-id="e3b88-138">Templates</span></span>
<span data-ttu-id="e3b88-139">Jeśli chcesz użyć [szablony](notification-hubs-templates-cross-platform-push-messages.md), instalacja urządzenia również przechowywać wszystkie szablony skojarzone z tym urządzeniem w formacie JSON formatu (Zobacz przykład powyżej).</span><span class="sxs-lookup"><span data-stu-id="e3b88-139">If you want to use [Templates](notification-hubs-templates-cross-platform-push-messages.md), the device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="e3b88-140">Nazwy szablonów pomocy różnych szablonów docelowego dla tego samego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e3b88-140">The template names help target different templates for the same device.</span></span>

<span data-ttu-id="e3b88-141">Należy pamiętać, że każda nazwa szablonu jest mapowana treści szablonu i opcjonalny zestaw tagów.</span><span class="sxs-lookup"><span data-stu-id="e3b88-141">Note that each template name maps to a template body and an optional set of tags.</span></span> <span data-ttu-id="e3b88-142">Ponadto każdej z platform może mieć właściwości dodatkowe szablonu.</span><span class="sxs-lookup"><span data-stu-id="e3b88-142">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="e3b88-143">Dla Sklepu Windows (przy użyciu usługi WNS) i Windows Phone 8 (przy użyciu usługi MPNS) dodatkowe ustawienia nagłówków może być częścią szablonu.</span><span class="sxs-lookup"><span data-stu-id="e3b88-143">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of the template.</span></span> <span data-ttu-id="e3b88-144">W przypadku usługi APNs można ustawić właściwości wygaśnięcia stałą lub wyrażeniem szablonu.</span><span class="sxs-lookup"><span data-stu-id="e3b88-144">In the case of APNs, you can set an expiry property to either a constant or to a template expression.</span></span> <span data-ttu-id="e3b88-145">Aby uzyskać pełną listę można znaleźć właściwości instalacji, [Tworzenie lub Zastąp instalacji REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="e3b88-145">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="e3b88-146">Dodatkowej Kafelki aplikacji do Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="e3b88-146">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="e3b88-147">Dla aplikacji ze Sklepu Windows klienta wysyłanie powiadomień do dodatkowej Kafelki jest taka sama jak ich wysłaniem do główną.</span><span class="sxs-lookup"><span data-stu-id="e3b88-147">For Windows Store client applications, sending notifications to secondary tiles is the same as sending them to the primary one.</span></span> <span data-ttu-id="e3b88-148">Ta jest obsługiwana w przypadku instalacji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-148">This is also supported in installations.</span></span> <span data-ttu-id="e3b88-149">Należy zauważyć, że dodatkowej Kafelki różnych ChannelUri, która zestawu SDK w aplikacji klienta obsługuje przezroczysty.</span><span class="sxs-lookup"><span data-stu-id="e3b88-149">Note that secondary tiles have a different ChannelUri, which the SDK on your client app handles transparently.</span></span>

<span data-ttu-id="e3b88-150">Słownik SecondaryTiles używa tego samego TileId, który służy do tworzenia obiektu SecondaryTiles w aplikacji ze Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="e3b88-150">The SecondaryTiles dictionary uses the same TileId that is used to create the SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="e3b88-151">Podobnie jak w przypadku podstawowego ChannelUri, ChannelUris dodatkowej Kafelki można zmienić w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="e3b88-151">As with the primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="e3b88-152">Aby zachować instalacje zaktualizowano Centrum powiadomień, urządzenia należy odświeżyć je bieżącego ChannelUris dodatkowej kafelków.</span><span class="sxs-lookup"><span data-stu-id="e3b88-152">In order to keep the installations in the notification hub updated, the device must refresh them with the current ChannelUris of the secondary tiles.</span></span>

## <a name="registration-management-from-the-device"></a><span data-ttu-id="e3b88-153">Zarządzanie rejestrację z urządzenia</span><span class="sxs-lookup"><span data-stu-id="e3b88-153">Registration management from the device</span></span>
<span data-ttu-id="e3b88-154">Podczas zarządzania rejestracji urządzeń z aplikacji klienta, wewnętrznej bazy danych tylko jest odpowiedzialny za wysyłanie powiadomień.</span><span class="sxs-lookup"><span data-stu-id="e3b88-154">When managing device registration from client apps, the backend is only responsible for sending notifications.</span></span> <span data-ttu-id="e3b88-155">Aplikacje klienta aktualności dojść systemu powiadomień platformy i zarejestruj tagów.</span><span class="sxs-lookup"><span data-stu-id="e3b88-155">Client apps keep PNS handles up to date, and register tags.</span></span> <span data-ttu-id="e3b88-156">Poniżej przedstawiono tego wzorca.</span><span class="sxs-lookup"><span data-stu-id="e3b88-156">The following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="e3b88-157">Urządzenia najpierw pobiera dojście systemu powiadomień platformy z systemu powiadomień platformy, a następnie rejestruje bezpośrednio z Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="e3b88-157">The device first retrieves the PNS handle from the PNS, then registers with the notification hub directly.</span></span> <span data-ttu-id="e3b88-158">Po pomyślnym rejestracji zaplecze aplikacji może wysłać powiadomienia targeting tej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-158">After the registration is successful, the app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="e3b88-159">Aby uzyskać więcej informacji na temat wysyłania powiadomień, zobacz [routingu i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="e3b88-159">For more information about how to send notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="e3b88-160">Należy pamiętać, że w takim przypadku użyjesz nasłuchiwał tylko prawa dostępu z urządzenia z usługi notification hubs.</span><span class="sxs-lookup"><span data-stu-id="e3b88-160">Note that in this case, you will use only Listen rights to access your notification hubs from the device.</span></span> <span data-ttu-id="e3b88-161">Aby uzyskać więcej informacji, zobacz [zabezpieczeń](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="e3b88-161">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="e3b88-162">Rejestracja urządzenia jest najprostszą metodą, ale ma kilka wad.</span><span class="sxs-lookup"><span data-stu-id="e3b88-162">Registering from the device is the simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="e3b88-163">Pierwszy wadą jest to, że aplikacja kliencka aktualizować tylko jego tagi, gdy aplikacja jest aktywna.</span><span class="sxs-lookup"><span data-stu-id="e3b88-163">The first drawback is that a client app can only update its tags when the app is active.</span></span> <span data-ttu-id="e3b88-164">Na przykład jeśli użytkownik ma dwa urządzenia, które rejestrować tagi związane z zespołów sport przy pierwszym urządzeniem rejestruje dodatkowe tagów (na przykład Seahawks), drugiego urządzenia nie otrzymają powiadomienia o Seahawks momentu aplikacji na drugiego urządzenia wykonywane po raz drugi.</span><span class="sxs-lookup"><span data-stu-id="e3b88-164">For example, if a user has two devices that register tags related to sport teams, when the first device registers for an additional tag (for example, Seahawks), the second device will not receive the notifications about the Seahawks until the app on the second device is executed a second time.</span></span> <span data-ttu-id="e3b88-165">Ogólnie rzecz biorąc gdy tagi jest narażony na wielu urządzeniach, zarządzanie tagów z wewnętrznej bazy danych jest pożądane opcji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-165">More generally, when tags are affected by multiple devices, managing tags from the backend is a desirable option.</span></span>
<span data-ttu-id="e3b88-166">Drugi zwrot management rejestracji w aplikacji klienta jest, ponieważ aplikacje mogą być zaatakowane, zabezpieczanie rejestracji w znacznikach wymaga szczególną uwagę, zgodnie z objaśnieniem w sekcji "zabezpieczenia na poziomie tagu."</span><span class="sxs-lookup"><span data-stu-id="e3b88-166">The second drawback of registration management from the client app is that, since apps can be hacked, securing the registration to specific tags requires extra care, as explained in the section “Tag-level security.”</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="e3b88-167">Przykładowy kod zarejestrować się w Centrum powiadomień z urządzeniem przy użyciu instalacji</span><span class="sxs-lookup"><span data-stu-id="e3b88-167">Example code to register with a notification hub from a device using an installation</span></span>
<span data-ttu-id="e3b88-168">W tej chwili ta jest obsługiwana tylko przy użyciu [interfejsu API REST centra powiadomień](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3b88-168">At this time, this is only supported using the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="e3b88-169">Można również użyć przy użyciu metody poprawki [standard JSON poprawki](https://tools.ietf.org/html/rfc6902) aktualizacji instalacji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-169">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine the targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="e3b88-170">Przykładowy kod zarejestrować się w Centrum powiadomień z urządzenia przy użyciu rejestracji</span><span class="sxs-lookup"><span data-stu-id="e3b88-170">Example code to register with a notification hub from a device using a registration</span></span>
<span data-ttu-id="e3b88-171">Te metody Utwórz lub zaktualizuj rejestracji dla urządzenia, na którym są one nazywane.</span><span class="sxs-lookup"><span data-stu-id="e3b88-171">These methods create or update a registration for the device on which they are called.</span></span> <span data-ttu-id="e3b88-172">Oznacza to, że aby można było zaktualizować, dojście lub znaczniki, musi zastąpić cały rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-172">This means that in order to update the handle or the tags, you must overwrite the entire registration.</span></span> <span data-ttu-id="e3b88-173">Należy pamiętać, że rejestracje przejściowy, dlatego powinien zawsze mieć niezawodny magazyn z bieżącym tagi, które wymaga określonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e3b88-173">Remember that registrations are transient, so you should always have a reliable store with the current tags that a specific device needs.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // The Device id from the PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from the client itself, then store this registration id in device
    // storage. Then when the app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="e3b88-174">Zarządzanie rejestracji z poziomu zaplecza</span><span class="sxs-lookup"><span data-stu-id="e3b88-174">Registration management from a backend</span></span>
<span data-ttu-id="e3b88-175">Zarządzanie rejestracje z wewnętrznej bazy danych wymaga zapisywania dodatkowy kod.</span><span class="sxs-lookup"><span data-stu-id="e3b88-175">Managing registrations from the backend requires writing additional code.</span></span> <span data-ttu-id="e3b88-176">Zaktualizowane systemu powiadomień platformy dojścia do wewnętrznej bazy danych zawsze uruchomieniu aplikacji (wraz z tagami i szablonów) i wewnętrznej bazy danych należy zaktualizować ta dojścia w Centrum powiadomień, należy podać aplikacji z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e3b88-176">The app from the device must provide the updated PNS handle to the backend every time the app starts (along with tags and templates), and the backend must update this handle on the notification hub.</span></span> <span data-ttu-id="e3b88-177">Poniżej przedstawiono w tym projekcie.</span><span class="sxs-lookup"><span data-stu-id="e3b88-177">The following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="e3b88-178">Zalety zarządzania z wewnętrznej bazy danych rejestracji obejmują możliwość modyfikowania tagów do rejestracji, nawet wtedy, gdy jest nieaktywne z odpowiedniej aplikacji na urządzeniu i uwierzytelniania aplikacji klienckiej przed dodaniem tag do rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-178">The advantages of managing registrations from the backend include the ability to modify tags to registrations even when the corresponding app on the device is inactive, and to authenticate the client app before adding a tag to its registration.</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="e3b88-179">Przykładowy kod zarejestrować się w Centrum powiadomień z zaplecza, przy użyciu instalacji</span><span class="sxs-lookup"><span data-stu-id="e3b88-179">Example code to register with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="e3b88-180">Urządzenie klienckie nadal pobiera jego dojście systemu powiadomień platformy i właściwości instalacji w odpowiednich jako przed i wywołuje niestandardowego interfejsu API do wewnętrznej bazy danych, można dokonać rejestracji i autoryzować tagi itp. Wewnętrznej bazy danych można wykorzystać [SDK Centrum powiadomień dla wewnętrznej bazy danych operacji](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="e3b88-180">The client device still gets its PNS handle and relevant installation properties as before and calls a custom API on the backend that can perform the registration and authorize tags etc. The backend can leverage the [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="e3b88-181">Można również użyć przy użyciu metody poprawki [standard JSON poprawki](https://tools.ietf.org/html/rfc6902) aktualizacji instalacji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-181">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on the backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In the backend we can control if a user is allowed to add tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="e3b88-182">Przykładowy kod zarejestrować się w Centrum powiadomień z urządzenia przy użyciu identyfikatora rejestracji</span><span class="sxs-lookup"><span data-stu-id="e3b88-182">Example code to register with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="e3b88-183">Z poziomu zaplecza aplikacji można wykonywać podstawowe operacje CRUDS rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-183">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="e3b88-184">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e3b88-184">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of the correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


<span data-ttu-id="e3b88-185">Wewnętrznej bazy danych musi obsługiwać współbieżności między aktualizacjami rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-185">The backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="e3b88-186">Usługa Service Bus udostępnia optymistyczne sterowanie współbieżnością zarządzania rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-186">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="e3b88-187">Na poziomie protokołu HTTP ten sposób jest implementowany z użyciem ETag na operacji zarządzania rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3b88-187">At the HTTP level, this is implemented with the use of ETag on registration management operations.</span></span> <span data-ttu-id="e3b88-188">Ta funkcja służy niewidocznie SDKs firmy Microsoft, które zgłosić wyjątek, jeśli aktualizacji zostało odrzucone ze względów współbieżności.</span><span class="sxs-lookup"><span data-stu-id="e3b88-188">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="e3b88-189">Zaplecze aplikacji jest odpowiedzialny za obsługę tych wyjątków i ponawianie próby aktualizacji, jeśli jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="e3b88-189">The app backend is responsible for handling these exceptions and retrying the update if required.</span></span>

