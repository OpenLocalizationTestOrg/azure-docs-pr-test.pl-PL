---
title: "toouse aaaHow usługi Notification Hubs za pomocą języka PHP"
description: "Dowiedz się, jak toouse usługi Azure Notification Hubs z zaplecza PHP."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="f55e0-103">Jak toouse usługi Notification Hubs za pomocą języka PHP</span><span class="sxs-lookup"><span data-stu-id="f55e0-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="f55e0-104">Dostęp do wszystkich funkcji centra powiadomień z zaplecza Ruby-Java/PHP przy użyciu interfejsu REST Centrum powiadomień hello zgodnie z opisem w temacie MSDN hello [interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="f55e0-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="f55e0-105">W tym temacie zostanie przedstawiony sposób:</span><span class="sxs-lookup"><span data-stu-id="f55e0-105">In this topic we show how to:</span></span>

* <span data-ttu-id="f55e0-106">Tworzenie klienta REST dla funkcji usługi Notification Hubs w języku PHP;</span><span class="sxs-lookup"><span data-stu-id="f55e0-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="f55e0-107">Wykonaj hello [samouczku Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) dla danej platformy przenośne wyboru wdrażanie hello zaplecza części w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="f55e0-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="f55e0-108">Interfejs klienta</span><span class="sxs-lookup"><span data-stu-id="f55e0-108">Client interface</span></span>
<span data-ttu-id="f55e0-109">Interfejs klienta głównego Hello zapewniają hello tych samych metod, które są dostępne w hello [.NET SDK centra powiadomień](http://msdn.microsoft.com/library/jj933431.aspx), umożliwi toodirectly Tłumaczenie wszystkich hello samouczki i przykłady, które są obecnie dostępne w tej witrynie i zamieszczone przez społeczność hello na powitania internet.</span><span class="sxs-lookup"><span data-stu-id="f55e0-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="f55e0-110">Można znaleźć w hello cały kod hello [próbki otoki PHP REST].</span><span class="sxs-lookup"><span data-stu-id="f55e0-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="f55e0-111">Na przykład toocreate klienta:</span><span class="sxs-lookup"><span data-stu-id="f55e0-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="f55e0-112">toosend natywnych powiadomień systemu iOS:</span><span class="sxs-lookup"><span data-stu-id="f55e0-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="f55e0-113">Wdrażanie</span><span class="sxs-lookup"><span data-stu-id="f55e0-113">Implementation</span></span>
<span data-ttu-id="f55e0-114">Jeśli tak, nie jest jeszcze nie, wykonaj naszych [samouczku Get] ostatniej sekcji toohello, gdzie masz zaplecza tooimplement hello w górę.</span><span class="sxs-lookup"><span data-stu-id="f55e0-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="f55e0-115">Ponadto jeśli chcesz, można użyć hello kodu z hello [próbki otoki PHP REST] i przejść bezpośrednio toohello [hello ukończenia samouczka](#complete-tutorial) sekcji.</span><span class="sxs-lookup"><span data-stu-id="f55e0-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="f55e0-116">Witaj wszystkie szczegóły tooimplement pełne otoki REST można znaleźć w [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="f55e0-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="f55e0-117">W tej sekcji zostaną przedstawione hello PHP stosowania hello główne kroki wymagane tooaccess punkty końcowe REST centra powiadomień:</span><span class="sxs-lookup"><span data-stu-id="f55e0-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="f55e0-118">Przeanalizować parametrów połączenia hello</span><span class="sxs-lookup"><span data-stu-id="f55e0-118">Parse hello connection string</span></span>
2. <span data-ttu-id="f55e0-119">Generuj token autoryzacji hello</span><span class="sxs-lookup"><span data-stu-id="f55e0-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="f55e0-120">Wykonywać wywołania hello HTTP</span><span class="sxs-lookup"><span data-stu-id="f55e0-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="f55e0-121">Przeanalizować parametrów połączenia hello</span><span class="sxs-lookup"><span data-stu-id="f55e0-121">Parse hello connection string</span></span>
<span data-ttu-id="f55e0-122">Oto hello klasy głównym implementującej powitania klienta, którego konstruktor, który analizuje parametry połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="f55e0-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a><span data-ttu-id="f55e0-123">Utwórz token zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="f55e0-123">Create security token</span></span>
<span data-ttu-id="f55e0-124">Szczegóły Hello tworzenia tokenu zabezpieczeń hello są dostępne [tutaj](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="f55e0-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="f55e0-125">Hello następującą metodę został dodany toobe toohello **NotificationHub** klasy toocreate hello tokenów na powitania URI bieżącego żądania hello i poświadczeniami hello wyodrębniony z parametrów połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="f55e0-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a><span data-ttu-id="f55e0-126">Wyślij powiadomienie</span><span class="sxs-lookup"><span data-stu-id="f55e0-126">Send a notification</span></span>
<span data-ttu-id="f55e0-127">Najpierw należy zdefiniować Daj nam Klasa reprezentująca powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="f55e0-127">First, let us define a class representing a notification.</span></span>

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

<span data-ttu-id="f55e0-128">Ta klasa jest kontenerem dla treści natywnych powiadomień, lub zbiór właściwości, w przypadku szablonu powiadomienia i zestaw nagłówków zawiera formacie (native platformy lub szablonu) i właściwości specyficzne dla platformy (na przykład właściwość wygaśnięcia firmy Apple i WNS nagłówki).</span><span class="sxs-lookup"><span data-stu-id="f55e0-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="f55e0-129">Zobacz toohello [dokumentacja interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn495827.aspx) i hello formaty powiadomień określonych platform dla wszystkich hello dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="f55e0-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="f55e0-130">Dzięki tej klasy, możemy teraz zapisać hello wysyłania powiadomień metody wewnątrz hello **NotificationHub** klasy.</span><span class="sxs-lookup"><span data-stu-id="f55e0-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send hello request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

<span data-ttu-id="f55e0-131">Hello powyżej metod wysyłania POST protokołu HTTP żądania toohello /messages punktu końcowego Centrum powiadomień, z treści poprawne hello i nagłówki toosend hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="f55e0-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="f55e0-132"><a name="complete-tutorial"></a>Samouczek hello ukończone</span><span class="sxs-lookup"><span data-stu-id="f55e0-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="f55e0-133">Można teraz ukończyć Samouczek wprowadzający hello, wysyłając hello powiadomień z zaplecza PHP.</span><span class="sxs-lookup"><span data-stu-id="f55e0-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="f55e0-134">Inicjowanie klienta usługi Notification Hubs (zastąpić nazwę Centrum i parametry połączenia hello zgodnie z instrukcją w hello [samouczku Get]):</span><span class="sxs-lookup"><span data-stu-id="f55e0-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="f55e0-135">Następnie dodaj kod wysyłania hello w zależności od platform przenośnych docelowych.</span><span class="sxs-lookup"><span data-stu-id="f55e0-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="f55e0-136">Sklep Windows i Windows Phone 8.1 (z systemem innym niż platformy Silverlight)</span><span class="sxs-lookup"><span data-stu-id="f55e0-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="f55e0-137">iOS</span><span class="sxs-lookup"><span data-stu-id="f55e0-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="f55e0-138">Android</span><span class="sxs-lookup"><span data-stu-id="f55e0-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="f55e0-139">Windows Phone 8.0 i 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="f55e0-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a><span data-ttu-id="f55e0-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="f55e0-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="f55e0-141">Uruchamianie kodu PHP powinny być teraz powiadomienie znajdujących się na urządzeniu docelowym.</span><span class="sxs-lookup"><span data-stu-id="f55e0-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f55e0-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f55e0-142">Next Steps</span></span>
<span data-ttu-id="f55e0-143">W tym temacie firma Microsoft pokazano, jak toocreate proste Java REST klienta dla usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="f55e0-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="f55e0-144">W tym miejscu można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f55e0-144">From here you can:</span></span>

* <span data-ttu-id="f55e0-145">Pobierz pełną hello [próbki otoki PHP REST], zawierającą cały kod hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="f55e0-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="f55e0-146">Kontynuować szkoleniowe dotyczące usługi Notification Hubs znakowanie funkcji w hello [samouczek wiadomości krytyczne]</span><span class="sxs-lookup"><span data-stu-id="f55e0-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="f55e0-147">Dowiedz się więcej o wypychanie powiadomień tooindividual użytkowników [Powiadom użytkowników samouczka]</span><span class="sxs-lookup"><span data-stu-id="f55e0-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="f55e0-148">Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f55e0-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[próbki otoki PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[samouczku Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

