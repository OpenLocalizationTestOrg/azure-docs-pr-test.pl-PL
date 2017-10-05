---
title: "Jak używać usługi Notification Hubs za pomocą języka PHP"
description: "Dowiedz się, jak używać usługi Azure Notification Hubs z zaplecza PHP."
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
ms.openlocfilehash: c27b6308ff528224a0398e0ff40537db05417bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-php"></a><span data-ttu-id="f2d8d-103">Jak używać usługi Notification Hubs za pomocą języka PHP</span><span class="sxs-lookup"><span data-stu-id="f2d8d-103">How to use Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="f2d8d-104">Dostęp do wszystkich funkcji centra powiadomień z zaplecza Ruby-Java/PHP przy użyciu interfejsu REST Centrum powiadomień, zgodnie z opisem w temacie MSDN [interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2d8d-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="f2d8d-105">W tym temacie zostanie przedstawiony sposób:</span><span class="sxs-lookup"><span data-stu-id="f2d8d-105">In this topic we show how to:</span></span>

* <span data-ttu-id="f2d8d-106">Tworzenie klienta REST dla funkcji usługi Notification Hubs w języku PHP;</span><span class="sxs-lookup"><span data-stu-id="f2d8d-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="f2d8d-107">Postępuj zgodnie z [samouczku Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) dla platformy przenośne wyboru wdrażanie części zaplecza w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-107">Follow the [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing the back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="f2d8d-108">Interfejs klienta</span><span class="sxs-lookup"><span data-stu-id="f2d8d-108">Client interface</span></span>
<span data-ttu-id="f2d8d-109">Interfejs klienta głównego zapewniają te same metody, które są dostępne w [.NET SDK centra powiadomień](http://msdn.microsoft.com/library/jj933431.aspx), to umożliwi bezpośrednio tłumaczenie samouczki i przykłady, które są obecnie dostępne w tej witrynie, a zamieszczone przez społeczności w Internecie.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-109">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="f2d8d-110">Możesz znaleźć kod dostępne w [próbki otoki PHP REST].</span><span class="sxs-lookup"><span data-stu-id="f2d8d-110">You can find all the code available in the [PHP REST wrapper sample].</span></span>

<span data-ttu-id="f2d8d-111">Na przykład można utworzyć klienta:</span><span class="sxs-lookup"><span data-stu-id="f2d8d-111">For example, to create a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="f2d8d-112">Aby wysłać iOS natywnych powiadomień:</span><span class="sxs-lookup"><span data-stu-id="f2d8d-112">To send an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="f2d8d-113">Wdrażanie</span><span class="sxs-lookup"><span data-stu-id="f2d8d-113">Implementation</span></span>
<span data-ttu-id="f2d8d-114">Jeśli tak, nie jest jeszcze nie, wykonaj naszych [samouczku Get] w górę do ostatniej sekcji, w którym należy implementować zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-114">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>
<span data-ttu-id="f2d8d-115">Ponadto jeśli chcesz służy kod z [próbki otoki PHP REST] i przejść bezpośrednio do [Ukończ samouczek](#complete-tutorial) sekcji.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-115">Also, if you want you can use the code from the [PHP REST wrapper sample] and go directly to the [Complete the tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="f2d8d-116">Wszystkie szczegóły, aby zaimplementować pełne otoki REST można znaleźć w [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2d8d-116">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="f2d8d-117">W tej sekcji zostaną przedstawione wykonania PHP główne kroki wymagane do uzyskania dostępu punkty końcowe REST centra powiadomień:</span><span class="sxs-lookup"><span data-stu-id="f2d8d-117">In this section we will describe the PHP implementation of the main steps required to access Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="f2d8d-118">Analizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="f2d8d-118">Parse the connection string</span></span>
2. <span data-ttu-id="f2d8d-119">Wygeneruj token autoryzacji</span><span class="sxs-lookup"><span data-stu-id="f2d8d-119">Generate the authorization token</span></span>
3. <span data-ttu-id="f2d8d-120">Wykonaj wywołanie HTTP</span><span class="sxs-lookup"><span data-stu-id="f2d8d-120">Perform the HTTP call</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="f2d8d-121">Analizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="f2d8d-121">Parse the connection string</span></span>
<span data-ttu-id="f2d8d-122">W tym miejscu jest główna klasa implementacji klienta, którego konstruktora, która analizuje parametry połączenia:</span><span class="sxs-lookup"><span data-stu-id="f2d8d-122">Here is the main class implementing the client, whose constructor that parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="f2d8d-123">Utwórz token zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="f2d8d-123">Create security token</span></span>
<span data-ttu-id="f2d8d-124">Szczegóły dotyczące tworzenia tokenu zabezpieczeń są dostępne [tutaj](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2d8d-124">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="f2d8d-125">Następująca metoda musi być dodany do **NotificationHub** do utworzenia tokenu na podstawie identyfikatora URI bieżącego żądania i poświadczenia wyodrębniony z ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-125">The following method has to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="f2d8d-126">Wyślij powiadomienie</span><span class="sxs-lookup"><span data-stu-id="f2d8d-126">Send a notification</span></span>
<span data-ttu-id="f2d8d-127">Najpierw należy zdefiniować Daj nam Klasa reprezentująca powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="f2d8d-128">Ta klasa jest kontenerem dla treści natywnych powiadomień, lub zbiór właściwości, w przypadku szablonu powiadomienia i zestaw nagłówków zawiera formacie (native platformy lub szablonu) i właściwości specyficzne dla platformy (na przykład właściwość wygaśnięcia firmy Apple i WNS nagłówki).</span><span class="sxs-lookup"><span data-stu-id="f2d8d-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="f2d8d-129">Zapoznaj się z [dokumentacja interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn495827.aspx) i formaty na platformach powiadomienia określonych dla wszystkich dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-129">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="f2d8d-130">Dzięki tej klasy, możemy teraz zapisać wysyłania powiadomień metody wewnątrz **NotificationHub** klasy.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-130">Armed with this class, we can now write the send notification methods inside of the **NotificationHub** class.</span></span>

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

        // Send the request
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

<span data-ttu-id="f2d8d-131">Powyżej metod Wyślij żądanie HTTP POST do punktu końcowego /messages Centrum powiadomień, z poprawną treści i nagłówków, aby wysłać powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-131">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

## <span data-ttu-id="f2d8d-132"><a name="complete-tutorial"></a>Ukończ samouczek</span><span class="sxs-lookup"><span data-stu-id="f2d8d-132"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="f2d8d-133">Teraz możesz ukończyć Samouczek wprowadzający przez wysyłanie powiadomień z zaplecza PHP.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-133">Now you can complete the Get Started tutorial by sending the notification from a PHP back-end.</span></span>

<span data-ttu-id="f2d8d-134">Inicjowanie klienta usługi Notification Hubs (zastąpić nazwę Centrum i parametry połączenia, zgodnie z instrukcją w [samouczku Get]):</span><span class="sxs-lookup"><span data-stu-id="f2d8d-134">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="f2d8d-135">Następnie dodaj kod wysyłania, w zależności od platform przenośnych docelowych.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-135">Then add the send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="f2d8d-136">Sklep Windows i Windows Phone 8.1 (z systemem innym niż platformy Silverlight)</span><span class="sxs-lookup"><span data-stu-id="f2d8d-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="f2d8d-137">iOS</span><span class="sxs-lookup"><span data-stu-id="f2d8d-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="f2d8d-138">Android</span><span class="sxs-lookup"><span data-stu-id="f2d8d-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="f2d8d-139">Windows Phone 8.0 i 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="f2d8d-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="f2d8d-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="f2d8d-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="f2d8d-141">Uruchamianie kodu PHP powinny być teraz powiadomienie znajdujących się na urządzeniu docelowym.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2d8d-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2d8d-142">Next Steps</span></span>
<span data-ttu-id="f2d8d-143">W tym temacie firma Microsoft pokazano, jak utworzyć prosty Java REST klienta usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-143">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="f2d8d-144">W tym miejscu można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f2d8d-144">From here you can:</span></span>

* <span data-ttu-id="f2d8d-145">Pobierz pełny [próbki otoki PHP REST], który zawiera kod powyżej.</span><span class="sxs-lookup"><span data-stu-id="f2d8d-145">Download the full [PHP REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="f2d8d-146">Kontynuować szkoleniowe dotyczące usługi Notification Hubs znakowanie funkcji [samouczka wiadomości krytyczne]</span><span class="sxs-lookup"><span data-stu-id="f2d8d-146">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="f2d8d-147">Dowiedz się więcej o wypychanie powiadomień do poszczególnych użytkowników [Powiadom użytkowników samouczka]</span><span class="sxs-lookup"><span data-stu-id="f2d8d-147">Learn about pushing notifications to individual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="f2d8d-148">Aby uzyskać więcej informacji, zobacz też [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f2d8d-148">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="f2d8d-149">[próbki otoki PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span><span class="sxs-lookup"><span data-stu-id="f2d8d-149">[PHP REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span></span>
<span data-ttu-id="f2d8d-150">[samouczku Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span><span class="sxs-lookup"><span data-stu-id="f2d8d-150">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span></span>

