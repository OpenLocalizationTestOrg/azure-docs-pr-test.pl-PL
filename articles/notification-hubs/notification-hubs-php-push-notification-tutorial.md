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
# <a name="how-toouse-notification-hubs-from-php"></a>Jak toouse usługi Notification Hubs za pomocą języka PHP
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Dostęp do wszystkich funkcji centra powiadomień z zaplecza Ruby-Java/PHP przy użyciu interfejsu REST Centrum powiadomień hello zgodnie z opisem w temacie MSDN hello [interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn223264.aspx).

W tym temacie zostanie przedstawiony sposób:

* Tworzenie klienta REST dla funkcji usługi Notification Hubs w języku PHP;
* Wykonaj hello [samouczku Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) dla danej platformy przenośne wyboru wdrażanie hello zaplecza części w kodzie PHP.

## <a name="client-interface"></a>Interfejs klienta
Interfejs klienta głównego Hello zapewniają hello tych samych metod, które są dostępne w hello [.NET SDK centra powiadomień](http://msdn.microsoft.com/library/jj933431.aspx), umożliwi toodirectly Tłumaczenie wszystkich hello samouczki i przykłady, które są obecnie dostępne w tej witrynie i zamieszczone przez społeczność hello na powitania internet.

Można znaleźć w hello cały kod hello [próbki otoki PHP REST].

Na przykład toocreate klienta:

    $hub = new NotificationHub("connection string", "hubname");    

toosend natywnych powiadomień systemu iOS:

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a>Wdrażanie
Jeśli tak, nie jest jeszcze nie, wykonaj naszych [samouczku Get] ostatniej sekcji toohello, gdzie masz zaplecza tooimplement hello w górę.
Ponadto jeśli chcesz, można użyć hello kodu z hello [próbki otoki PHP REST] i przejść bezpośrednio toohello [hello ukończenia samouczka](#complete-tutorial) sekcji.

Witaj wszystkie szczegóły tooimplement pełne otoki REST można znaleźć w [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). W tej sekcji zostaną przedstawione hello PHP stosowania hello główne kroki wymagane tooaccess punkty końcowe REST centra powiadomień:

1. Przeanalizować parametrów połączenia hello
2. Generuj token autoryzacji hello
3. Wykonywać wywołania hello HTTP

### <a name="parse-hello-connection-string"></a>Przeanalizować parametrów połączenia hello
Oto hello klasy głównym implementującej powitania klienta, którego konstruktor, który analizuje parametry połączenia hello:

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


### <a name="create-security-token"></a>Utwórz token zabezpieczeń
Szczegóły Hello tworzenia tokenu zabezpieczeń hello są dostępne [tutaj](http://msdn.microsoft.com/library/dn495627.aspx).
Hello następującą metodę został dodany toobe toohello **NotificationHub** klasy toocreate hello tokenów na powitania URI bieżącego żądania hello i poświadczeniami hello wyodrębniony z parametrów połączenia hello.

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

### <a name="send-a-notification"></a>Wyślij powiadomienie
Najpierw należy zdefiniować Daj nam Klasa reprezentująca powiadomienie.

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

Ta klasa jest kontenerem dla treści natywnych powiadomień, lub zbiór właściwości, w przypadku szablonu powiadomienia i zestaw nagłówków zawiera formacie (native platformy lub szablonu) i właściwości specyficzne dla platformy (na przykład właściwość wygaśnięcia firmy Apple i WNS nagłówki).

Zobacz toohello [dokumentacja interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn495827.aspx) i hello formaty powiadomień określonych platform dla wszystkich hello dostępnych opcji.

Dzięki tej klasy, możemy teraz zapisać hello wysyłania powiadomień metody wewnątrz hello **NotificationHub** klasy.

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

Hello powyżej metod wysyłania POST protokołu HTTP żądania toohello /messages punktu końcowego Centrum powiadomień, z treści poprawne hello i nagłówki toosend hello powiadomień.

## <a name="complete-tutorial"></a>Samouczek hello ukończone
Można teraz ukończyć Samouczek wprowadzający hello, wysyłając hello powiadomień z zaplecza PHP.

Inicjowanie klienta usługi Notification Hubs (zastąpić nazwę Centrum i parametry połączenia hello zgodnie z instrukcją w hello [samouczku Get]):

    $hub = new NotificationHub("connection string", "hubname");    

Następnie dodaj kod wysyłania hello w zależności od platform przenośnych docelowych.

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Sklep Windows i Windows Phone 8.1 (z systemem innym niż platformy Silverlight)
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a>iOS
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a>Android
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 i 8.1 Silverlight
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


### <a name="kindle-fire"></a>Kindle Fire
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

Uruchamianie kodu PHP powinny być teraz powiadomienie znajdujących się na urządzeniu docelowym.

## <a name="next-steps"></a>Następne kroki
W tym temacie firma Microsoft pokazano, jak toocreate proste Java REST klienta dla usługi Notification Hubs. W tym miejscu można wykonywać następujące czynności:

* Pobierz pełną hello [próbki otoki PHP REST], zawierającą cały kod hello powyżej.
* Kontynuować szkoleniowe dotyczące usługi Notification Hubs znakowanie funkcji w hello [samouczek wiadomości krytyczne]
* Dowiedz się więcej o wypychanie powiadomień tooindividual użytkowników [Powiadom użytkowników samouczka]

Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka PHP](/develop/php/).

[próbki otoki PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[samouczku Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

