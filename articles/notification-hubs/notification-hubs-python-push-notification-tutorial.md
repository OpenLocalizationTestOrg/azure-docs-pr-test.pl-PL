---
title: "Jak używać usługi Notification Hubs z języka Python"
description: "Dowiedz się, jak używać usługi Azure Notification Hubs z zaplecza Python."
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
ms.openlocfilehash: 9ceedb9940759427fc8cec74a1307e42472563a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-python"></a><span data-ttu-id="a3e1c-103">Jak używać usługi Notification Hubs w języku Python</span><span class="sxs-lookup"><span data-stu-id="a3e1c-103">How to use Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="a3e1c-104">Dostęp do wszystkich funkcji centra powiadomień z zaplecza Java/PHP/Python/Ruby przy użyciu interfejsu REST Centrum powiadomień, zgodnie z opisem w temacie MSDN [interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3e1c-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="a3e1c-105">To jest przykładowy implementacji wykonywania wysyła powiadomienia w języku Python i nie jest oficjalnie obsługiwana SDK Python Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-105">This is a sample reference implementation for implementing the notification sends in Python and is not the officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="a3e1c-106">Ten przykład jest zapisywany przy użyciu języka Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="a3e1c-107">W tym temacie zostanie przedstawiony sposób:</span><span class="sxs-lookup"><span data-stu-id="a3e1c-107">In this topic we show how to:</span></span>

* <span data-ttu-id="a3e1c-108">Tworzenie klienta REST dla funkcji usługi Notification Hubs w języku Python.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="a3e1c-109">Wysyłanie powiadomień za pomocą interfejsu Python do interfejsów API REST Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-109">Send notifications using the Python interface to the Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="a3e1c-110">Pobierz zrzutu REST protokołu HTTP żądania/odpowiedzi w celu debugowania edukacyjnych.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-110">Get a dump of the HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="a3e1c-111">Możesz wykonać [samouczku Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) dla platformy przenośne wyboru wdrażanie części zaplecza w języku Python.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-111">You can follow the [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing the back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="a3e1c-112">Zakres próbki jest ograniczona tylko do wysyłania powiadomień i nie wykonuje żadnych zarządzania rejestracji.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-112">The scope of the sample is only limited to send notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="a3e1c-113">Interfejs klienta</span><span class="sxs-lookup"><span data-stu-id="a3e1c-113">Client interface</span></span>
<span data-ttu-id="a3e1c-114">Interfejs klienta głównego zapewniają te same metody, które są dostępne w [.NET SDK centra powiadomień](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3e1c-114">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="a3e1c-115">Umożliwi to bezpośrednio tłumaczenie samouczki i przykłady, które są obecnie dostępne w tej witrynie, a zamieszczone przez społeczność w Internecie.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-115">This will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="a3e1c-116">Możesz znaleźć kod dostępne w [próbki otoki Python REST].</span><span class="sxs-lookup"><span data-stu-id="a3e1c-116">You can find all the code available in the [Python REST wrapper sample].</span></span>

<span data-ttu-id="a3e1c-117">Na przykład można utworzyć klienta:</span><span class="sxs-lookup"><span data-stu-id="a3e1c-117">For example, to create a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="a3e1c-118">Aby wysłać powiadomienie wyskakujące systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="a3e1c-118">To send a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="a3e1c-119">Wdrażanie</span><span class="sxs-lookup"><span data-stu-id="a3e1c-119">Implementation</span></span>
<span data-ttu-id="a3e1c-120">Jeśli tak, nie jest jeszcze nie, wykonaj naszych [samouczku Get] w górę do ostatniej sekcji, w którym należy implementować zaplecza.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-120">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>

<span data-ttu-id="a3e1c-121">Wszystkie szczegóły, aby zaimplementować pełne otoki REST można znaleźć w [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3e1c-121">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="a3e1c-122">W tej sekcji zostaną przedstawione implementacji Python głównych kroków wymaganych dostęp punkty końcowe REST centra powiadomień do wysyłania powiadomień</span><span class="sxs-lookup"><span data-stu-id="a3e1c-122">In this section we will describe the Python implementation of the main steps required to access Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="a3e1c-123">Analizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="a3e1c-123">Parse the connection string</span></span>
2. <span data-ttu-id="a3e1c-124">Wygeneruj token autoryzacji</span><span class="sxs-lookup"><span data-stu-id="a3e1c-124">Generate the authorization token</span></span>
3. <span data-ttu-id="a3e1c-125">Wyślij powiadomienia za pomocą interfejsu API REST protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="a3e1c-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="a3e1c-126">Analizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="a3e1c-126">Parse the connection string</span></span>
<span data-ttu-id="a3e1c-127">W tym miejscu jest główna klasa implementacji klienta, którego konstruktor analizuje parametry połączenia:</span><span class="sxs-lookup"><span data-stu-id="a3e1c-127">Here is the main class implementing the client, whose constructor parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="a3e1c-128">Utwórz token zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="a3e1c-128">Create security token</span></span>
<span data-ttu-id="a3e1c-129">Szczegóły dotyczące tworzenia tokenu zabezpieczeń są dostępne [tutaj](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3e1c-129">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="a3e1c-130">Następujące metody muszą być dodane do **NotificationHub** do utworzenia tokenu na podstawie identyfikatora URI bieżącego żądania i poświadczenia wyodrębniony z ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-130">The following methods have to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="a3e1c-131">Wyślij powiadomienia za pomocą interfejsu API REST protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="a3e1c-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="a3e1c-132">Użyj pierwszego, umożliwiają definiowanie Klasa reprezentująca powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of the following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="a3e1c-133">Ta klasa jest kontenerem dla treści natywnych powiadomień lub zbiór właściwości, w przypadku powiadomień szablonu, zestaw nagłówków zawiera formacie (native platformy lub szablonu) i właściwości specyficzne dla platformy (na przykład właściwość wygaśnięcia firmy Apple i nagłówki WNS).</span><span class="sxs-lookup"><span data-stu-id="a3e1c-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="a3e1c-134">Zapoznaj się z [dokumentacja interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn495827.aspx) i formaty na platformach powiadomienia określonych dla wszystkich dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-134">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="a3e1c-135">Teraz z tą klasą możemy zapisu wysyłania powiadomień metody wewnątrz **NotificationHub** klasy.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-135">Now with this class, we can write the send notification methods inside of the **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about the PNS send notification outcome
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

        # add the tags/tag expressions to the headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers to the headers collection that the user may have added
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

<span data-ttu-id="a3e1c-136">Powyżej metod Wyślij żądanie HTTP POST do punktu końcowego /messages Centrum powiadomień, z poprawną treści i nagłówków, aby wysłać powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-136">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

### <a name="using-debug-property-to-enable-detailed-logging"></a><span data-ttu-id="a3e1c-137">Aby włączyć szczegółowe rejestrowanie przy użyciu właściwości debugowania</span><span class="sxs-lookup"><span data-stu-id="a3e1c-137">Using debug property to enable detailed logging</span></span>
<span data-ttu-id="a3e1c-138">Włączanie debugowania właściwość podczas inicjowania Centrum powiadomień będą zapisywane szczegółowe rejestrowanie informacji o informacje dotyczące żądania HTTP i zrzutu odpowiedzi, a także szczegółowe komunikatu powiadomienia wysyłania wyników.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-138">Enabling debug property while initializing the Notification Hub will write out detailed logging information about the HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="a3e1c-139">Ostatnio dodane tej właściwości o nazwie [właściwości TestSend centra powiadomień](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) to zwraca szczegółowe informacje na temat wyniku wysyłania powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about the notification send outcome.</span></span> <span data-ttu-id="a3e1c-140">Aby użyć go - zainicjować za pomocą następujących:</span><span class="sxs-lookup"><span data-stu-id="a3e1c-140">To use it - initialize using the following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="a3e1c-141">Wyślij Centrum powiadomień żądanie adresu URL HTTP pobiera w związku z tym dołączane querystring "test".</span><span class="sxs-lookup"><span data-stu-id="a3e1c-141">The Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="a3e1c-142"><a name="complete-tutorial"></a>Ukończ samouczek</span><span class="sxs-lookup"><span data-stu-id="a3e1c-142"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="a3e1c-143">Teraz możesz ukończyć Samouczek wprowadzający przez wysyłanie powiadomień z zaplecza Python.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-143">Now you can complete the Get Started tutorial by sending the notification from a Python back-end.</span></span>

<span data-ttu-id="a3e1c-144">Inicjowanie klienta usługi Notification Hubs (zastąpić nazwę Centrum i parametry połączenia, zgodnie z instrukcją w [samouczku Get]):</span><span class="sxs-lookup"><span data-stu-id="a3e1c-144">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="a3e1c-145">Następnie dodaj kod wysyłania, w zależności od platform przenośnych docelowych.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-145">Then add the send code depending on your target mobile platform.</span></span> <span data-ttu-id="a3e1c-146">W tym przykładzie dodano również wyższym poziomie metody w celu umożliwienia wysyłania powiadomień z platformą np. send_windows_notification dla systemu windows; send_apple_notification (dla apple) itd.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-146">This sample also adds higher level methods to enable sending notifications based on the platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="a3e1c-147">Sklep Windows i Windows Phone 8.1 (z systemem innym niż platformy Silverlight)</span><span class="sxs-lookup"><span data-stu-id="a3e1c-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="a3e1c-148">Windows Phone 8.0 i 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="a3e1c-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="a3e1c-149">iOS</span><span class="sxs-lookup"><span data-stu-id="a3e1c-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="a3e1c-150">Android</span><span class="sxs-lookup"><span data-stu-id="a3e1c-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="a3e1c-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="a3e1c-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="a3e1c-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="a3e1c-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="a3e1c-153">Uruchamianie kodu języka Python powinny być powiadomienie znajdujących się na urządzeniu docelowym.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="a3e1c-154">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="a3e1c-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="a3e1c-155">Włączenie właściwości debugowania</span><span class="sxs-lookup"><span data-stu-id="a3e1c-155">Enabling debug property</span></span>
<span data-ttu-id="a3e1c-156">Po włączeniu flagi debugowania podczas inicjowania NotificationHub, a następnie zobaczysz szczegółowe żądania HTTP i zrzutu odpowiedzi, a także NotificationOutcome podobnie do następującej gdzie można zrozumieć, jakie nagłówki HTTP są przekazywane w żądaniu, a otrzymano jaką odpowiedź HTTP z Centrum powiadomień:![][1]</span><span class="sxs-lookup"><span data-stu-id="a3e1c-156">When you enable debug flag while initializing the NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like the following where you can understand what HTTP headers are passed in the request and what HTTP response was received from the Notification Hub: ![][1]</span></span>

<span data-ttu-id="a3e1c-157">Zobaczysz, np. szczegóły wyniku Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="a3e1c-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="a3e1c-158">gdy komunikat jest wysyłany pomyślnie Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-158">when the message is successfully sent to the Push Notification Service.</span></span> 
  
        <Outcome>The Notification was successfully sent to the Push Notification System</Outcome>
* <span data-ttu-id="a3e1c-159">Jeśli nie było żadnych elementów docelowych znaleziono dla wszystkich powiadomień wypychanych następnie prawdopodobnie zamierzasz zobacz następujące tematy w odpowiedzi (co oznacza, że nie było żadnej rejestracji znaleźć do dostarczenia powiadomienia prawdopodobnie ponieważ rejestracje niektóre tagi niezgodne)</span><span class="sxs-lookup"><span data-stu-id="a3e1c-159">If there were no targets found for any push notification then you are likely going to see the following in the response (which indicates that there were no registrations found to deliver the notification probably because the registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-to-windows"></a><span data-ttu-id="a3e1c-160">Emisji wyskakujące powiadomienie do systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a3e1c-160">Broadcast toast notification to Windows</span></span>
<span data-ttu-id="a3e1c-161">Zwróć uwagę, nagłówki, które get wysyłane podczas przesyłania emisji wyskakujących powiadomień na klientach z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-161">Notice the headers that get sent out when you are sending a broadcast toast notification to Windows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="a3e1c-162">Wyślij powiadomienie, określając tag (lub wyrażenie etykiety)</span><span class="sxs-lookup"><span data-stu-id="a3e1c-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="a3e1c-163">Zwróć uwagę, nagłówek HTTP tagi, które pobiera dodane do żądania HTTP (w poniższym przykładzie mamy wysyłania powiadomienia tylko do rejestracji z ładunku "Sport")</span><span class="sxs-lookup"><span data-stu-id="a3e1c-163">Notice the Tags HTTP header which gets added to the HTTP request (in the example below, we are sending the notification only to registrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="a3e1c-164">Wyślij powiadomienie określania wielu tagów</span><span class="sxs-lookup"><span data-stu-id="a3e1c-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="a3e1c-165">Zwróć uwagę, jak nagłówka HTTP tagi zostanie zmieniona, gdy wiele tagów są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-165">Notice how the Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="a3e1c-166">Szablonu powiadomień</span><span class="sxs-lookup"><span data-stu-id="a3e1c-166">Templated notification</span></span>
<span data-ttu-id="a3e1c-167">Zwróć uwagę, że zmiany nagłówka formatu HTTP i treści ładunku jest wysyłany jako część treści żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="a3e1c-167">Notice that the Format HTTP header changes and the payload body is sent as part of the HTTP request body:</span></span>

<span data-ttu-id="a3e1c-168">**Po stronie klienta — zarejestrowanych szablonu**</span><span class="sxs-lookup"><span data-stu-id="a3e1c-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="a3e1c-169">**Po stronie serwera — wysyłanie ładunku**</span><span class="sxs-lookup"><span data-stu-id="a3e1c-169">**Server side - sending the payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="a3e1c-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a3e1c-170">Next Steps</span></span>
<span data-ttu-id="a3e1c-171">W tym temacie firma Microsoft pokazano, jak utworzyć prosty Python REST klienta usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-171">In this topic we showed how to create a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="a3e1c-172">W tym miejscu można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a3e1c-172">From here you can:</span></span>

* <span data-ttu-id="a3e1c-173">Pobierz pełny [próbki otoki Python REST], który zawiera kod powyżej.</span><span class="sxs-lookup"><span data-stu-id="a3e1c-173">Download the full [Python REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="a3e1c-174">Kontynuować szkoleniowe dotyczące usługi Notification Hubs znakowanie funkcja [samouczek fundamentalne wiadomości]</span><span class="sxs-lookup"><span data-stu-id="a3e1c-174">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="a3e1c-175">Kontynuować zapoznawanie funkcji szablonów centra powiadomień w [samouczek lokalizowanie wiadomości]</span><span class="sxs-lookup"><span data-stu-id="a3e1c-175">Continue learning about Notification Hubs Templates feature in the [Localizing News tutorial]</span></span>

<!-- URLs -->
<span data-ttu-id="a3e1c-176">[próbki otoki Python REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span><span class="sxs-lookup"><span data-stu-id="a3e1c-176">[Python REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span></span>
<span data-ttu-id="a3e1c-177">[samouczku Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="a3e1c-177">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="a3e1c-178">[samouczek fundamentalne wiadomości]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="a3e1c-178">[Breaking News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span></span>
<span data-ttu-id="a3e1c-179">[samouczek lokalizowanie wiadomości]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="a3e1c-179">[Localizing News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

