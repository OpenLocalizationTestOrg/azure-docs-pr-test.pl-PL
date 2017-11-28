---
title: "aaaRegistration zarządzania"
description: "W tym temacie wyjaśniono, jak tooregister urządzeniami przy użyciu usługi notification hubs w kolejności tooreceive powiadomienia wypychane."
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
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a><span data-ttu-id="1b166-103">Zarządzanie rejestracją</span><span class="sxs-lookup"><span data-stu-id="1b166-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="1b166-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1b166-104">Overview</span></span>
<span data-ttu-id="1b166-105">W tym temacie wyjaśniono, jak tooregister urządzeniami przy użyciu usługi notification hubs w kolejności tooreceive powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="1b166-105">This topic explains how tooregister devices with notification hubs in order tooreceive push notifications.</span></span> <span data-ttu-id="1b166-106">Hello tematu opisano rejestracji na wysokim poziomie, a następnie wprowadza hello dwa główne wzorców do rejestracji urządzeń: rejestrowanie na urządzeniu hello bezpośrednio toohello Centrum powiadomień i rejestrowanie za pomocą wewnętrznej bazy danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b166-106">hello topic describes registrations at a high level, then introduces hello two main patterns for registering devices: registering from hello device directly toohello notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="1b166-107">Co to jest rejestracja urządzenia</span><span class="sxs-lookup"><span data-stu-id="1b166-107">What is device registration</span></span>
<span data-ttu-id="1b166-108">Rejestracja urządzenia z Centrum powiadomień odbywa się przy użyciu **rejestracji** lub **instalacji**.</span><span class="sxs-lookup"><span data-stu-id="1b166-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="1b166-109">Rejestracje</span><span class="sxs-lookup"><span data-stu-id="1b166-109">Registrations</span></span>
<span data-ttu-id="1b166-110">Rejestracja kojarzy powitalne obsługi usługi powiadomień platformy (PNS) dla urządzeń z tagami i prawdopodobnie szablonu.</span><span class="sxs-lookup"><span data-stu-id="1b166-110">A registration associates hello Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="1b166-111">dojście systemu powiadomień platformy Hello można ChannelURI, token urządzenia lub identyfikator rejestracji usługi GCM. Tagi są używane tooroute powiadomienia toohello poprawny zestaw dojść urządzeń.</span><span class="sxs-lookup"><span data-stu-id="1b166-111">hello PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used tooroute notifications toohello correct set of device handles.</span></span> <span data-ttu-id="1b166-112">Aby uzyskać więcej informacji, zobacz [routingu i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="1b166-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="1b166-113">Szablony są używane tooimplement na rejestracji przekształcenia.</span><span class="sxs-lookup"><span data-stu-id="1b166-113">Templates are used tooimplement per-registration transformation.</span></span> <span data-ttu-id="1b166-114">Aby uzyskać więcej informacji, zobacz [szablony](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="1b166-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="1b166-115">Instalacje</span><span class="sxs-lookup"><span data-stu-id="1b166-115">Installations</span></span>
<span data-ttu-id="1b166-116">Instalacja jest rozszerzonych właściwości powiązanych z rejestrację, która zawiera zbiór wypychania.</span><span class="sxs-lookup"><span data-stu-id="1b166-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="1b166-117">Jest hello tooregistering najnowsze i najlepsze rozwiązania z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1b166-117">It is hello latest and best approach tooregistering your devices.</span></span> <span data-ttu-id="1b166-118">Jednak nie jest obsługiwany przez klienta po stronie zestawu SDK programu .NET ([SDK Centrum powiadomień dla wewnętrznej bazy danych operacji](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) jeszcze.</span><span class="sxs-lookup"><span data-stu-id="1b166-118">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="1b166-119">Oznacza to, w przypadku rejestracji powitania klienta urządzenia, konieczne będzie toouse hello [interfejsu API REST centra powiadomień](https://msdn.microsoft.com/library/mt621153.aspx) podejścia toosupport instalacji.</span><span class="sxs-lookup"><span data-stu-id="1b166-119">This means if you are registering from hello client device itself, you would have toouse hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach toosupport installations.</span></span> <span data-ttu-id="1b166-120">Jeśli używasz usługi wewnętrznej bazy danych powinno być możliwe toouse [SDK Centrum powiadomień dla wewnętrznej bazy danych operacji](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="1b166-120">If you are using a backend service, you should be able toouse [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="1b166-121">Witaj poniżej przedstawiono niektóre instalacje toousing podstawowych zalet:</span><span class="sxs-lookup"><span data-stu-id="1b166-121">hello following are some key advantages toousing installations:</span></span>

* <span data-ttu-id="1b166-122">Tworzenie lub aktualizowanie instalacji jest w pełni idempotentności.</span><span class="sxs-lookup"><span data-stu-id="1b166-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="1b166-123">Dlatego możesz ponowić próbę jej bez żadnych problemów dotyczących rejestracji duplikatów.</span><span class="sxs-lookup"><span data-stu-id="1b166-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="1b166-124">model instalacji Hello umożliwia łatwe toodo poszczególnych wypchnięć - przeznaczonych dla określonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1b166-124">hello installation model makes it easy toodo individual pushes - targeting specific device.</span></span> <span data-ttu-id="1b166-125">Tag systemu **"$InstallationId: [identyfikator installationId]"** jest automatycznie dodawany z każdej instalacji na podstawie rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1b166-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="1b166-126">Dlatego można wywołać wysyłania toothis tag tootarget określonego urządzenia bez konieczności toodo dodatkowy kod.</span><span class="sxs-lookup"><span data-stu-id="1b166-126">So you can call a send toothis tag tootarget a specific device without having toodo any additional coding.</span></span>
* <span data-ttu-id="1b166-127">Przy użyciu instalacji umożliwia również należy toodo rejestracji częściowej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="1b166-127">Using installations also enables you toodo partial registration updates.</span></span> <span data-ttu-id="1b166-128">Witaj częściowej aktualizacji instalacji zażądano za pomocą metody poprawki przy użyciu hello [standard JSON poprawki](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="1b166-128">hello partial update of an installation is requested with a PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="1b166-129">Jest to szczególnie przydatne, należy tagi tooupdate na powitania rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1b166-129">This is particularly useful when you want tooupdate tags on hello registration.</span></span> <span data-ttu-id="1b166-130">Nie masz toopull dół całej rejestracji hello i ponownie Wyślij wszystkie tagi poprzedniej hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="1b166-130">You don't have toopull down hello entire registration and then resend all hello previous tags again.</span></span>

<span data-ttu-id="1b166-131">Instalacja produktu może zawierać hello hello następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="1b166-131">An installation can contain hello hello following properties.</span></span> <span data-ttu-id="1b166-132">Aby uzyskać pełną listę, zobacz właściwości instalacji hello [utworzyć ani zastąpić instalacji z interfejsu API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) lub [właściwości instalacji](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) dla hello.</span><span class="sxs-lookup"><span data-stu-id="1b166-132">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for hello .</span></span>

    // Example installation format tooshow some supported properties
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



<span data-ttu-id="1b166-133">Jest ważne toonote, którego rejestracji i instalacje domyślnie nie wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="1b166-133">It is important toonote that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="1b166-134">Rejestracje i instalacji musi zawierać prawidłowe dojście systemu powiadomień platformy dla każdego urządzenia/kanału.</span><span class="sxs-lookup"><span data-stu-id="1b166-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="1b166-135">Ponieważ dojść systemu powiadomień platformy można uzyskać tylko w aplikacji klienta na powitania urządzeniu, jeden wzorzec jest tooregister bezpośrednio na tym urządzeniu z powitania klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b166-135">Because PNS handles can only be obtained in a client app on hello device, one pattern is tooregister directly on that device with hello client app.</span></span> <span data-ttu-id="1b166-136">Na powitania inne strony, zagadnienia dotyczące zabezpieczeń i logiki biznesowej związanych z tootags może wymagać toomanage rejestracji urządzeń w zaplecze aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1b166-136">On hello other hand, security considerations and business logic related tootags might require you toomanage device registration in hello app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="1b166-137">Szablony</span><span class="sxs-lookup"><span data-stu-id="1b166-137">Templates</span></span>
<span data-ttu-id="1b166-138">Jeśli chcesz, aby toouse [szablony](notification-hubs-templates-cross-platform-push-messages.md), instalacja urządzenia hello również przechowywać wszystkie szablony skojarzone z tym urządzeniem w formacie JSON formatu (Zobacz przykład powyżej).</span><span class="sxs-lookup"><span data-stu-id="1b166-138">If you want toouse [Templates](notification-hubs-templates-cross-platform-push-messages.md), hello device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="1b166-139">Witaj nazwy szablonów pomocy target różnych szablonów dla hello tego samego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1b166-139">hello template names help target different templates for hello same device.</span></span>

<span data-ttu-id="1b166-140">Należy pamiętać, że nazwa każdego szablonu mapuje treści szablonu tooa i opcjonalny zestaw tagów.</span><span class="sxs-lookup"><span data-stu-id="1b166-140">Note that each template name maps tooa template body and an optional set of tags.</span></span> <span data-ttu-id="1b166-141">Ponadto każdej z platform może mieć właściwości dodatkowe szablonu.</span><span class="sxs-lookup"><span data-stu-id="1b166-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="1b166-142">Dla Sklepu Windows (przy użyciu usługi WNS) i Windows Phone 8 (przy użyciu usługi MPNS) dodatkowych zestawu nagłówków może być częścią hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="1b166-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of hello template.</span></span> <span data-ttu-id="1b166-143">W przypadku hello APN można ustawić tooeither właściwości wygaśnięcia stałą lub tooa wyrażenia szablonu.</span><span class="sxs-lookup"><span data-stu-id="1b166-143">In hello case of APNs, you can set an expiry property tooeither a constant or tooa template expression.</span></span> <span data-ttu-id="1b166-144">Aby uzyskać pełną listę, zobacz właściwości instalacji hello [Tworzenie lub Zastąp instalacji REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="1b166-144">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="1b166-145">Dodatkowej Kafelki aplikacji do Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="1b166-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="1b166-146">Dla aplikacji ze Sklepu Windows klienta wysyłania powiadomień jest Kafelki toosecondary hello takie same jak wysyłanie ich toohello główną.</span><span class="sxs-lookup"><span data-stu-id="1b166-146">For Windows Store client applications, sending notifications toosecondary tiles is hello same as sending them toohello primary one.</span></span> <span data-ttu-id="1b166-147">Ta jest obsługiwana w przypadku instalacji.</span><span class="sxs-lookup"><span data-stu-id="1b166-147">This is also supported in installations.</span></span> <span data-ttu-id="1b166-148">Należy zauważyć, że dodatkowej Kafelki różnych ChannelUri, które hello zestawu SDK w aplikacji klienta obsługuje przezroczysty.</span><span class="sxs-lookup"><span data-stu-id="1b166-148">Note that secondary tiles have a different ChannelUri, which hello SDK on your client app handles transparently.</span></span>

<span data-ttu-id="1b166-149">używa słownika SecondaryTiles Hello hello tego samego TileId, który jest obiektem SecondaryTiles hello toocreate używane w aplikacji ze Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="1b166-149">hello SecondaryTiles dictionary uses hello same TileId that is used toocreate hello SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="1b166-150">Zgodnie z hello ChannelUri podstawowego, ChannelUris dodatkowej Kafelki można zmienić w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="1b166-150">As with hello primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="1b166-151">W przypadku kolejności tookeep hello instalacji w Centrum powiadomień hello zaktualizowane hello urządzenia należy odświeżyć je z hello bieżącego ChannelUris hello dodatkowej kafelków.</span><span class="sxs-lookup"><span data-stu-id="1b166-151">In order tookeep hello installations in hello notification hub updated, hello device must refresh them with hello current ChannelUris of hello secondary tiles.</span></span>

## <a name="registration-management-from-hello-device"></a><span data-ttu-id="1b166-152">Zarządzanie rejestrację z urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="1b166-152">Registration management from hello device</span></span>
<span data-ttu-id="1b166-153">Podczas zarządzania rejestracji urządzeń z aplikacji klienta, hello wewnętrznej bazy danych tylko jest odpowiedzialny za wysyłanie powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1b166-153">When managing device registration from client apps, hello backend is only responsible for sending notifications.</span></span> <span data-ttu-id="1b166-154">Aplikacje klienta zachować dojść systemu powiadomień platformy się toodate i zarejestruj tagów.</span><span class="sxs-lookup"><span data-stu-id="1b166-154">Client apps keep PNS handles up toodate, and register tags.</span></span> <span data-ttu-id="1b166-155">Witaj, na poniższej ilustracji przedstawiono ten wzorzec.</span><span class="sxs-lookup"><span data-stu-id="1b166-155">hello following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="1b166-156">urządzenie Hello najpierw pobiera powitalne systemu powiadomień platformy obsługi z hello systemu powiadomień platformy, a następnie rejestruje z Centrum powiadomień hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="1b166-156">hello device first retrieves hello PNS handle from hello PNS, then registers with hello notification hub directly.</span></span> <span data-ttu-id="1b166-157">Po pomyślnym rejestracji hello zaplecza aplikacji hello można wysłać powiadomienia targeting tej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1b166-157">After hello registration is successful, hello app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="1b166-158">Aby uzyskać więcej informacji o tym, jak toosend powiadomień, zobacz [routingu i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="1b166-158">For more information about how toosend notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="1b166-159">Należy pamiętać, że w takim przypadku użyjesz nasłuchiwał tylko tooaccess praw użytkownika usługi notification hubs z hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1b166-159">Note that in this case, you will use only Listen rights tooaccess your notification hubs from hello device.</span></span> <span data-ttu-id="1b166-160">Aby uzyskać więcej informacji, zobacz [zabezpieczeń](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="1b166-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="1b166-161">Rejestracja urządzenia hello jest hello najprostszą metodą, ale ma kilka wad.</span><span class="sxs-lookup"><span data-stu-id="1b166-161">Registering from hello device is hello simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="1b166-162">Witaj pierwszy wadą jest to, że aplikacja kliencka tylko aktualizowania jego tagi, gdy aplikacja hello jest aktywna.</span><span class="sxs-lookup"><span data-stu-id="1b166-162">hello first drawback is that a client app can only update its tags when hello app is active.</span></span> <span data-ttu-id="1b166-163">Na przykład jeśli użytkownik ma dwa urządzenia zarejestrować zespoły toosport powiązane tagi, gdy hello pierwszego urządzenia rejestruje dodatkowe tagów (na przykład Seahawks), hello drugiego urządzenia nie otrzymają powiadomienia hello o hello Seahawks do aplikacji hello na powitania drugie urządzenie jest wykonywany po raz drugi.</span><span class="sxs-lookup"><span data-stu-id="1b166-163">For example, if a user has two devices that register tags related toosport teams, when hello first device registers for an additional tag (for example, Seahawks), hello second device will not receive hello notifications about hello Seahawks until hello app on hello second device is executed a second time.</span></span> <span data-ttu-id="1b166-164">Ogólnie rzecz biorąc gdy tagi jest narażony na wielu urządzeniach, zarządzanie tagów z zaplecza hello jest pożądane opcji.</span><span class="sxs-lookup"><span data-stu-id="1b166-164">More generally, when tags are affected by multiple devices, managing tags from hello backend is a desirable option.</span></span>
<span data-ttu-id="1b166-165">drugi zwrot zarządzania rejestracji z powitania klienta aplikacji Hello jest, ponieważ aplikacje mogą być zaatakowane, zabezpieczanie rejestracji hello tagi toospecific wymaga szczególną uwagę, zgodnie z objaśnieniem w hello sekcję "zabezpieczenia poziomu znacznika."</span><span class="sxs-lookup"><span data-stu-id="1b166-165">hello second drawback of registration management from hello client app is that, since apps can be hacked, securing hello registration toospecific tags requires extra care, as explained in hello section “Tag-level security.”</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="1b166-166">Przykład kodu tooregister z Centrum powiadomień z urządzeniem przy użyciu instalacji</span><span class="sxs-lookup"><span data-stu-id="1b166-166">Example code tooregister with a notification hub from a device using an installation</span></span>
<span data-ttu-id="1b166-167">W tej chwili obsługiwane wyłącznie przy użyciu hello [interfejsu API REST centra powiadomień](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b166-167">At this time, this is only supported using hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="1b166-168">Umożliwia także metodę PATCH hello przy użyciu hello [standard JSON poprawki](https://tools.ietf.org/html/rfc6902) aktualizowania hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="1b166-168">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

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

        // Determine hello targetUri that we will sign
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



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="1b166-169">Przykład kodu tooregister z Centrum powiadomień z urządzenia przy użyciu rejestracji</span><span class="sxs-lookup"><span data-stu-id="1b166-169">Example code tooregister with a notification hub from a device using a registration</span></span>
<span data-ttu-id="1b166-170">Te metody Utwórz lub zaktualizuj rejestracji dla urządzenia hello, na którym są one nazywane.</span><span class="sxs-lookup"><span data-stu-id="1b166-170">These methods create or update a registration for hello device on which they are called.</span></span> <span data-ttu-id="1b166-171">Oznacza to, że w kolejności tooupdate hello dojścia lub hello tagów, musi zastąpić hello całego rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1b166-171">This means that in order tooupdate hello handle or hello tags, you must overwrite hello entire registration.</span></span> <span data-ttu-id="1b166-172">Należy pamiętać, że rejestracje przejściowe, więc powinien zawsze mieć niezawodnej magazynu z hello bieżącego tagi, które wymaga określonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1b166-172">Remember that registrations are transient, so you should always have a reliable store with hello current tags that a specific device needs.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
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


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="1b166-173">Zarządzanie rejestracji z poziomu zaplecza</span><span class="sxs-lookup"><span data-stu-id="1b166-173">Registration management from a backend</span></span>
<span data-ttu-id="1b166-174">Zarządzanie rejestracje z zaplecza hello wymaga zapisywania dodatkowy kod.</span><span class="sxs-lookup"><span data-stu-id="1b166-174">Managing registrations from hello backend requires writing additional code.</span></span> <span data-ttu-id="1b166-175">Witaj aplikacji z urządzenia hello podać hello zaktualizowane zaplecza toohello dojście systemu powiadomień platformy w każdym uruchomieniu aplikacji hello (wraz z tagami i szablonów) i hello wewnętrznej bazy danych należy zaktualizować ta dojścia na powitania Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1b166-175">hello app from hello device must provide hello updated PNS handle toohello backend every time hello app starts (along with tags and templates), and hello backend must update this handle on hello notification hub.</span></span> <span data-ttu-id="1b166-176">Witaj, na poniższej ilustracji przedstawiono ten projekt.</span><span class="sxs-lookup"><span data-stu-id="1b166-176">hello following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="1b166-177">Zalety Hello Zarządzanie rejestracje z zaplecza hello obejmują hello możliwości toomodify tagi tooregistrations nawet wtedy, gdy hello odpowiednich aplikacji na urządzeniu hello jest nieaktywny i tooauthenticate powitania klienta aplikacji przed dodaniem rejestracji tooits tagu.</span><span class="sxs-lookup"><span data-stu-id="1b166-177">hello advantages of managing registrations from hello backend include hello ability toomodify tags tooregistrations even when hello corresponding app on hello device is inactive, and tooauthenticate hello client app before adding a tag tooits registration.</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="1b166-178">Przykład kodu tooregister z Centrum powiadomień z zaplecza, przy użyciu instalacji</span><span class="sxs-lookup"><span data-stu-id="1b166-178">Example code tooregister with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="1b166-179">powitania klienta urządzenia nadal pobiera jego dojście systemu powiadomień platformy i właściwości instalacji w odpowiednich jak wcześniej, a następnie wywołania niestandardowego interfejsu API hello wewnętrznej bazy danych, można dokonać rejestracji hello i autoryzować znaczniki wewnętrznej bazy danych itp. hello można wykorzystać hello [SDK Centrum powiadomień dla operacje zaplecza](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="1b166-179">hello client device still gets its PNS handle and relevant installation properties as before and calls a custom API on hello backend that can perform hello registration and authorize tags etc. hello backend can leverage hello [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="1b166-180">Umożliwia także metodę PATCH hello przy użyciu hello [standard JSON poprawki](https://tools.ietf.org/html/rfc6902) aktualizowania hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="1b166-180">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
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


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="1b166-181">Przykład kodu tooregister z Centrum powiadomień z urządzenia przy użyciu identyfikatora rejestracji</span><span class="sxs-lookup"><span data-stu-id="1b166-181">Example code tooregister with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="1b166-182">Z poziomu zaplecza aplikacji można wykonywać podstawowe operacje CRUDS rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1b166-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="1b166-183">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1b166-183">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
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


<span data-ttu-id="1b166-184">Witaj wewnętrznej bazy danych musi obsługiwać współbieżności między aktualizacjami rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1b166-184">hello backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="1b166-185">Usługa Service Bus udostępnia optymistyczne sterowanie współbieżnością zarządzania rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1b166-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="1b166-186">Na poziomie hello HTTP ten sposób jest implementowany z użyciem hello ETag na operacji zarządzania rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1b166-186">At hello HTTP level, this is implemented with hello use of ETag on registration management operations.</span></span> <span data-ttu-id="1b166-187">Ta funkcja służy niewidocznie SDKs firmy Microsoft, które zgłosić wyjątek, jeśli aktualizacji zostało odrzucone ze względów współbieżności.</span><span class="sxs-lookup"><span data-stu-id="1b166-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="1b166-188">zaplecze aplikacji Hello jest odpowiedzialny za obsługę tych wyjątków i ponowienie próby hello aktualizacji, jeśli jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="1b166-188">hello app backend is responsible for handling these exceptions and retrying hello update if required.</span></span>

