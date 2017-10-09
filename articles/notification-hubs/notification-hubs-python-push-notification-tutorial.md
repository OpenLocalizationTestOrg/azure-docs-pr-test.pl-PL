---
title: "toouse aaaHow usługi Notification Hubs z języka Python"
description: "Dowiedz się, jak toouse usługi Azure Notification Hubs z zaplecza Python."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 5640dd4a-a91e-4aa0-a833-93615bde49b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: python
ms.devlang: php
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 21d5aaf7fc24c9936fac8e0a8de640c66c51ab0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-python"></a>Jak toouse usługi Notification Hubs w języku Python
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Dostęp do wszystkich funkcji centra powiadomień z zaplecza Java/PHP/Python/Ruby przy użyciu interfejsu REST Centrum powiadomień hello zgodnie z opisem w temacie MSDN hello [interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn223264.aspx).

> [!NOTE]
> To jest przykładowy implementacji wykonywania wysyła powiadomienia hello w języku Python i nie hello oficjalnie obsługiwana zestaw SDK Python Centrum powiadomień.
> 
> Ten przykład jest zapisywany przy użyciu języka Python 3.4.
> 
> 

W tym temacie zostanie przedstawiony sposób:

* Tworzenie klienta REST dla funkcji usługi Notification Hubs w języku Python.
* Wysyłanie powiadomień za pomocą hello Python interfejsu toohello interfejsów API REST Centrum powiadomień. 
* Pobierz zrzutu hello REST protokołu HTTP żądania/odpowiedzi w celu debugowania edukacyjnych. 

Możesz wykonać hello [samouczku Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) dla danej platformy przenośne wyboru wdrażanie hello zaplecza części w języku Python.

> [!NOTE]
> zakres Hello próbki hello jest tylko ograniczony toosend powiadomienia i nie wykonuje żadnych zarządzania rejestracji.
> 
> 

## <a name="client-interface"></a>Interfejs klienta
Interfejs klienta głównego Hello zapewniają hello tych samych metod, które są dostępne w hello [.NET SDK centra powiadomień](http://msdn.microsoft.com/library/jj933431.aspx). Pozwoli to toodirectly Tłumaczenie wszystkich hello samouczki i przykłady, które są obecnie dostępne w tej witrynie, a zamieszczone przez społeczność hello na powitania internet.

Można znaleźć w hello cały kod hello [próbki otoki Python REST].

Na przykład toocreate klienta:

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

toosend Windows wyskakujących powiadomień:

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a>Wdrażanie
Jeśli tak, nie jest jeszcze nie, wykonaj naszych [samouczku Get] ostatniej sekcji toohello, gdzie masz zaplecza tooimplement hello w górę.

Witaj wszystkie szczegóły tooimplement pełne otoki REST można znaleźć w [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). W tej sekcji możemy będzie opisano hello Python stosowania hello główne kroki wymagane tooaccess punkty końcowe REST centra powiadomień i wysyłania powiadomień

1. Przeanalizować parametrów połączenia hello
2. Generuj token autoryzacji hello
3. Wyślij powiadomienia za pomocą interfejsu API REST protokołu HTTP

### <a name="parse-hello-connection-string"></a>Przeanalizować parametrów połączenia hello
Oto hello klasy głównym implementującej powitania klienta, którego konstruktor analizuje parametry połączenia hello:

    class NotificationHub:
        API_VERSION = "?api-version=2013-10"
        DEBUG_SEND = "&test"

        def __init__(self, connection_string=None, hub_name=None, debug=0):
            self.HubName = hub_name
            self.Debug = debug

            # Parse connection string
            parts = connection_string.split(';')
            if len(parts) != 3:
                raise Exception("Invalid ConnectionString.")

            for part in parts:
                if part.startswith('Endpoint'):
                    self.Endpoint = 'https' + part[11:]
                if part.startswith('SharedAccessKeyName'):
                    self.SasKeyName = part[20:]
                if part.startswith('SharedAccessKey'):
                    self.SasKeyValue = part[16:]


### <a name="create-security-token"></a>Utwórz token zabezpieczeń
Szczegóły Hello tworzenia tokenu zabezpieczeń hello są dostępne [tutaj](http://msdn.microsoft.com/library/dn495627.aspx).
Witaj następujące metody mają toobe dodane toohello **NotificationHub** klasy toocreate hello tokenów na powitania URI bieżącego żądania hello i poświadczeniami hello wyodrębniony z parametrów połączenia hello.

    @staticmethod
    def get_expiry():
        # By default returns an expiration of 5 minutes (=300 seconds) from now
        return int(round(time.time() + 300))

    @staticmethod
    def encode_base64(data):
        return base64.b64encode(data)

    def sign_string(self, to_sign):
        key = self.SasKeyValue.encode('utf-8')
        to_sign = to_sign.encode('utf-8')
        signed_hmac_sha256 = hmac.HMAC(key, to_sign, hashlib.sha256)
        digest = signed_hmac_sha256.digest()
        encoded_digest = self.encode_base64(digest)
        return encoded_digest

    def generate_sas_token(self):
        target_uri = self.Endpoint + self.HubName
        my_uri = urllib.parse.quote(target_uri, '').lower()
        expiry = str(self.get_expiry())
        to_sign = my_uri + '\n' + expiry
        signature = urllib.parse.quote(self.sign_string(to_sign))
        auth_format = 'SharedAccessSignature sig={0}&se={1}&skn={2}&sr={3}'
        sas_token = auth_format.format(signature, expiry, self.SasKeyName, my_uri)
        return sas_token

### <a name="send-a-notification-using-http-rest-api"></a>Wyślij powiadomienia za pomocą interfejsu API REST protokołu HTTP
Użyj pierwszego, umożliwiają definiowanie Klasa reprezentująca powiadomienie.

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of hello following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

Ta klasa jest kontenerem dla treści natywnych powiadomień lub zbiór właściwości, w przypadku powiadomień szablonu, zestaw nagłówków zawiera formacie (native platformy lub szablonu) i właściwości specyficzne dla platformy (na przykład właściwość wygaśnięcia firmy Apple i nagłówki WNS).

Zobacz toohello [dokumentacja interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn495827.aspx) i hello formaty powiadomień określonych platform dla wszystkich hello dostępnych opcji.

Teraz z tą klasą możemy zapisu hello wysyłania powiadomień metody wewnątrz hello **NotificationHub** klasy.

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about hello PNS send notification outcome
            url += self.DEBUG_SEND
            print("--- REQUEST ---")
            print("URI: " + url)
            print("Headers: " + json.dumps(headers, sort_keys=True, indent=4, separators=(' ', ': ')))
            print("--- END REQUEST ---\n")

        connection.request('POST', url, payload, headers)
        response = connection.getresponse()

        if self.Debug > 0:
            # print out detailed response information for debugging purpose
            print("\n\n--- RESPONSE ---")
            print(str(response.status) + " " + response.reason)
            print(response.msg)
            print(response.read())
            print("--- END RESPONSE ---")

        elif response.status != 201:
            # Successful outcome of send message is HTTP 201 - Created
            raise Exception(
                "Error sending notification. Received HTTP code " + str(response.status) + " " + response.reason)

        connection.close()

    def send_notification(self, notification, tag_or_tag_expression=None):
        url = self.Endpoint + self.HubName + '/messages' + self.API_VERSION

        json_platforms = ['template', 'apple', 'gcm', 'adm', 'baidu']

        if any(x in notification.format for x in json_platforms):
            content_type = "application/json"
            payload_to_send = json.dumps(notification.payload)
        else:
            content_type = "application/xml"
            payload_to_send = notification.payload

        headers = {
            'Content-type': content_type,
            'Authorization': self.generate_sas_token(),
            'ServiceBusNotification-Format': notification.format
        }

        if isinstance(tag_or_tag_expression, set):
            tag_list = ' || '.join(tag_or_tag_expression)
        else:
            tag_list = tag_or_tag_expression

        # add hello tags/tag expressions toohello headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers toohello headers collection that hello user may have added
        if notification.headers is not None:
            headers.update(notification.headers)

        self.make_http_request(url, payload_to_send, headers)

    def send_apple_notification(self, payload, tags=""):
        nh = Notification("apple", payload)
        self.send_notification(nh, tags)

    def send_gcm_notification(self, payload, tags=""):
        nh = Notification("gcm", payload)
        self.send_notification(nh, tags)

    def send_adm_notification(self, payload, tags=""):
        nh = Notification("adm", payload)
        self.send_notification(nh, tags)

    def send_baidu_notification(self, payload, tags=""):
        nh = Notification("baidu", payload)
        self.send_notification(nh, tags)

    def send_mpns_notification(self, payload, tags=""):
        nh = Notification("windowsphone", payload)

        if "<wp:Toast>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'toast', 'X-NotificationClass': '2'}
        elif "<wp:Tile>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'tile', 'X-NotificationClass': '1'}

        self.send_notification(nh, tags)

    def send_windows_notification(self, payload, tags=""):
        nh = Notification("windows", payload)

        if "<toast>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/toast'}
        elif "<tile>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/tile'}
        elif "<badge>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/badge'}

        self.send_notification(nh, tags)

    def send_template_notification(self, properties, tags=""):
        nh = Notification("template", properties)
        self.send_notification(nh, tags)

Hello powyżej metod wysyłania POST protokołu HTTP żądania toohello /messages punktu końcowego Centrum powiadomień, z treści poprawne hello i nagłówki toosend hello powiadomień.

### <a name="using-debug-property-tooenable-detailed-logging"></a>Za pomocą debugowania właściwość tooenable szczegółowe rejestrowanie
Włączanie debugowania właściwość podczas inicjowania hello Centrum powiadomień zostanie zapisu szczegółowe rejestrowanie informacji o hello HTTP żądania i odpowiedzi zrzutu, a także szczegółowe komunikatu powiadomienia wysyłania wyników. Ostatnio dodane tej właściwości o nazwie [właściwości TestSend centra powiadomień](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) to zwraca szczegółowe informacje na temat wyniku wysyłania powiadomienia hello. toouse jej — inicjowanie przy użyciu następujących hello:

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

Witaj powiadomienia Centrum Wyślij żądanie HTTP URL pobiera w związku z tym dołączane querystring "test". 

## <a name="complete-tutorial"></a>Samouczek hello ukończone
Można teraz ukończyć Samouczek wprowadzający hello, wysyłając hello powiadomień z zaplecza Python.

Inicjowanie klienta usługi Notification Hubs (zastąpić nazwę Centrum i parametry połączenia hello zgodnie z instrukcją w hello [samouczku Get]):

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

Następnie dodaj kod wysyłania hello w zależności od platform przenośnych docelowych. W tym przykładzie dodano również wyższej tooenable poziomu metod wysyłania powiadomień z platformą hello np. send_windows_notification dla systemu windows; send_apple_notification (dla apple) itd. 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Sklep Windows i Windows Phone 8.1 (z systemem innym niż platformy Silverlight)
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 i 8.1 Silverlight
    hub.send_mpns_notification(toast)

### <a name="ios"></a>iOS
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a>Android
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a>Kindle Fire
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a>Baidu
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

Uruchamianie kodu języka Python powinny być powiadomienie znajdujących się na urządzeniu docelowym.

## <a name="examples"></a>Przykłady:
### <a name="enabling-debug-property"></a>Włączenie właściwości debugowania
Po włączeniu flagi debugowania podczas inicjowania hello NotificationHub, a następnie zostanie wyświetlony szczegółowe zrzutu żądań i odpowiedzi HTTP, a także NotificationOutcome podobnie następującej hello, gdzie można zrozumieć, jakie nagłówki HTTP są przekazywane w żądaniu hello i jakie HTTP Odebrano odpowiedź z hello Centrum powiadomień:![][1]

Zobaczysz, np. szczegóły wyniku Centrum powiadomień 

* Kiedy wiadomość hello są wysyłane pomyślnie toohello Push Notification Service. 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* Jeśli wystąpiły nie znaleziono celu dla wszystkich powiadomień wypychanych, prawdopodobnie ma następujące hello toosee w odpowiedzi hello, (co oznacza, że nie było żadnej rejestracji znaleziono powiadomień hello toodeliver prawdopodobnie ponieważ rejestracje hello niektóre niedopasowane znaczniki)
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a>Wyskakujące powiadomienia tooWindows emisji
Zwróć uwagę, hello nagłówki, które get wysyłane podczas przesyłania klienta tooWindows emisji wyskakujące powiadomienie. 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a>Wyślij powiadomienie, określając tag (lub wyrażenie etykiety)
Nagłówek HTTP tagi hello powiadomienia, pobiera dodanego toohello HTTP żądania (w poniższym przykładzie hello, możemy wysyłania hello tooregistrations tylko powiadomienia o ładunku "Sport")

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a>Wyślij powiadomienie określania wielu tagów
Zwróć uwagę, jak nagłówka HTTP tagi hello zostanie zmieniona, gdy wiele tagów są wysyłane. 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a>Szablonu powiadomień
Należy zauważyć, że hello zmiany nagłówka Format HTTP i hello treści ładunku jest wysyłany jako część treści żądania hello HTTP:

**Po stronie klienta — zarejestrowanych szablonu**

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

**Po stronie serwera — wysyłanie hello ładunku**

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a>Następne kroki
W tym temacie firma Microsoft pokazano, jak toocreate proste Python REST klienta dla usługi Notification Hubs. W tym miejscu można wykonywać następujące czynności:

* Pobierz pełną hello [próbki otoki Python REST], zawierającą cały kod hello powyżej.
* Kontynuować szkoleniowe dotyczące usługi Notification Hubs znakowanie funkcji w hello [samouczek fundamentalne wiadomości]
* Kontynuować zapoznawanie funkcji szablonów centra powiadomień w hello [samouczek lokalizowanie wiadomości]

<!-- URLs -->
[próbki otoki Python REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python
[samouczku Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[samouczek fundamentalne wiadomości]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/
[samouczek lokalizowanie wiadomości]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

