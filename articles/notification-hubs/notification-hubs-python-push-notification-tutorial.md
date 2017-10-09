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
# <a name="how-toouse-notification-hubs-from-python"></a><span data-ttu-id="cb48e-103">Jak toouse usługi Notification Hubs w języku Python</span><span class="sxs-lookup"><span data-stu-id="cb48e-103">How toouse Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="cb48e-104">Dostęp do wszystkich funkcji centra powiadomień z zaplecza Java/PHP/Python/Ruby przy użyciu interfejsu REST Centrum powiadomień hello zgodnie z opisem w temacie MSDN hello [interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb48e-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="cb48e-105">To jest przykładowy implementacji wykonywania wysyła powiadomienia hello w języku Python i nie hello oficjalnie obsługiwana zestaw SDK Python Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="cb48e-105">This is a sample reference implementation for implementing hello notification sends in Python and is not hello officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="cb48e-106">Ten przykład jest zapisywany przy użyciu języka Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="cb48e-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="cb48e-107">W tym temacie zostanie przedstawiony sposób:</span><span class="sxs-lookup"><span data-stu-id="cb48e-107">In this topic we show how to:</span></span>

* <span data-ttu-id="cb48e-108">Tworzenie klienta REST dla funkcji usługi Notification Hubs w języku Python.</span><span class="sxs-lookup"><span data-stu-id="cb48e-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="cb48e-109">Wysyłanie powiadomień za pomocą hello Python interfejsu toohello interfejsów API REST Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="cb48e-109">Send notifications using hello Python interface toohello Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="cb48e-110">Pobierz zrzutu hello REST protokołu HTTP żądania/odpowiedzi w celu debugowania edukacyjnych.</span><span class="sxs-lookup"><span data-stu-id="cb48e-110">Get a dump of hello HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="cb48e-111">Możesz wykonać hello [samouczku Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) dla danej platformy przenośne wyboru wdrażanie hello zaplecza części w języku Python.</span><span class="sxs-lookup"><span data-stu-id="cb48e-111">You can follow hello [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing hello back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="cb48e-112">zakres Hello próbki hello jest tylko ograniczony toosend powiadomienia i nie wykonuje żadnych zarządzania rejestracji.</span><span class="sxs-lookup"><span data-stu-id="cb48e-112">hello scope of hello sample is only limited toosend notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="cb48e-113">Interfejs klienta</span><span class="sxs-lookup"><span data-stu-id="cb48e-113">Client interface</span></span>
<span data-ttu-id="cb48e-114">Interfejs klienta głównego Hello zapewniają hello tych samych metod, które są dostępne w hello [.NET SDK centra powiadomień](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb48e-114">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="cb48e-115">Pozwoli to toodirectly Tłumaczenie wszystkich hello samouczki i przykłady, które są obecnie dostępne w tej witrynie, a zamieszczone przez społeczność hello na powitania internet.</span><span class="sxs-lookup"><span data-stu-id="cb48e-115">This will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="cb48e-116">Można znaleźć w hello cały kod hello [próbki otoki Python REST].</span><span class="sxs-lookup"><span data-stu-id="cb48e-116">You can find all hello code available in hello [Python REST wrapper sample].</span></span>

<span data-ttu-id="cb48e-117">Na przykład toocreate klienta:</span><span class="sxs-lookup"><span data-stu-id="cb48e-117">For example, toocreate a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="cb48e-118">toosend Windows wyskakujących powiadomień:</span><span class="sxs-lookup"><span data-stu-id="cb48e-118">toosend a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="cb48e-119">Wdrażanie</span><span class="sxs-lookup"><span data-stu-id="cb48e-119">Implementation</span></span>
<span data-ttu-id="cb48e-120">Jeśli tak, nie jest jeszcze nie, wykonaj naszych [samouczku Get] ostatniej sekcji toohello, gdzie masz zaplecza tooimplement hello w górę.</span><span class="sxs-lookup"><span data-stu-id="cb48e-120">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>

<span data-ttu-id="cb48e-121">Witaj wszystkie szczegóły tooimplement pełne otoki REST można znaleźć w [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb48e-121">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="cb48e-122">W tej sekcji możemy będzie opisano hello Python stosowania hello główne kroki wymagane tooaccess punkty końcowe REST centra powiadomień i wysyłania powiadomień</span><span class="sxs-lookup"><span data-stu-id="cb48e-122">In this section we will describe hello Python implementation of hello main steps required tooaccess Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="cb48e-123">Przeanalizować parametrów połączenia hello</span><span class="sxs-lookup"><span data-stu-id="cb48e-123">Parse hello connection string</span></span>
2. <span data-ttu-id="cb48e-124">Generuj token autoryzacji hello</span><span class="sxs-lookup"><span data-stu-id="cb48e-124">Generate hello authorization token</span></span>
3. <span data-ttu-id="cb48e-125">Wyślij powiadomienia za pomocą interfejsu API REST protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="cb48e-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="cb48e-126">Przeanalizować parametrów połączenia hello</span><span class="sxs-lookup"><span data-stu-id="cb48e-126">Parse hello connection string</span></span>
<span data-ttu-id="cb48e-127">Oto hello klasy głównym implementującej powitania klienta, którego konstruktor analizuje parametry połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="cb48e-127">Here is hello main class implementing hello client, whose constructor parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="cb48e-128">Utwórz token zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="cb48e-128">Create security token</span></span>
<span data-ttu-id="cb48e-129">Szczegóły Hello tworzenia tokenu zabezpieczeń hello są dostępne [tutaj](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb48e-129">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="cb48e-130">Witaj następujące metody mają toobe dodane toohello **NotificationHub** klasy toocreate hello tokenów na powitania URI bieżącego żądania hello i poświadczeniami hello wyodrębniony z parametrów połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="cb48e-130">hello following methods have toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="cb48e-131">Wyślij powiadomienia za pomocą interfejsu API REST protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="cb48e-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="cb48e-132">Użyj pierwszego, umożliwiają definiowanie Klasa reprezentująca powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="cb48e-132">First, let use define a class representing a notification.</span></span>

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

<span data-ttu-id="cb48e-133">Ta klasa jest kontenerem dla treści natywnych powiadomień lub zbiór właściwości, w przypadku powiadomień szablonu, zestaw nagłówków zawiera formacie (native platformy lub szablonu) i właściwości specyficzne dla platformy (na przykład właściwość wygaśnięcia firmy Apple i nagłówki WNS).</span><span class="sxs-lookup"><span data-stu-id="cb48e-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="cb48e-134">Zobacz toohello [dokumentacja interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn495827.aspx) i hello formaty powiadomień określonych platform dla wszystkich hello dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="cb48e-134">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="cb48e-135">Teraz z tą klasą możemy zapisu hello wysyłania powiadomień metody wewnątrz hello **NotificationHub** klasy.</span><span class="sxs-lookup"><span data-stu-id="cb48e-135">Now with this class, we can write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="cb48e-136">Hello powyżej metod wysyłania POST protokołu HTTP żądania toohello /messages punktu końcowego Centrum powiadomień, z treści poprawne hello i nagłówki toosend hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="cb48e-136">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

### <a name="using-debug-property-tooenable-detailed-logging"></a><span data-ttu-id="cb48e-137">Za pomocą debugowania właściwość tooenable szczegółowe rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="cb48e-137">Using debug property tooenable detailed logging</span></span>
<span data-ttu-id="cb48e-138">Włączanie debugowania właściwość podczas inicjowania hello Centrum powiadomień zostanie zapisu szczegółowe rejestrowanie informacji o hello HTTP żądania i odpowiedzi zrzutu, a także szczegółowe komunikatu powiadomienia wysyłania wyników.</span><span class="sxs-lookup"><span data-stu-id="cb48e-138">Enabling debug property while initializing hello Notification Hub will write out detailed logging information about hello HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="cb48e-139">Ostatnio dodane tej właściwości o nazwie [właściwości TestSend centra powiadomień](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) to zwraca szczegółowe informacje na temat wyniku wysyłania powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="cb48e-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about hello notification send outcome.</span></span> <span data-ttu-id="cb48e-140">toouse jej — inicjowanie przy użyciu następujących hello:</span><span class="sxs-lookup"><span data-stu-id="cb48e-140">toouse it - initialize using hello following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="cb48e-141">Witaj powiadomienia Centrum Wyślij żądanie HTTP URL pobiera w związku z tym dołączane querystring "test".</span><span class="sxs-lookup"><span data-stu-id="cb48e-141">hello Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="cb48e-142"><a name="complete-tutorial"></a>Samouczek hello ukończone</span><span class="sxs-lookup"><span data-stu-id="cb48e-142"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="cb48e-143">Można teraz ukończyć Samouczek wprowadzający hello, wysyłając hello powiadomień z zaplecza Python.</span><span class="sxs-lookup"><span data-stu-id="cb48e-143">Now you can complete hello Get Started tutorial by sending hello notification from a Python back-end.</span></span>

<span data-ttu-id="cb48e-144">Inicjowanie klienta usługi Notification Hubs (zastąpić nazwę Centrum i parametry połączenia hello zgodnie z instrukcją w hello [samouczku Get]):</span><span class="sxs-lookup"><span data-stu-id="cb48e-144">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="cb48e-145">Następnie dodaj kod wysyłania hello w zależności od platform przenośnych docelowych.</span><span class="sxs-lookup"><span data-stu-id="cb48e-145">Then add hello send code depending on your target mobile platform.</span></span> <span data-ttu-id="cb48e-146">W tym przykładzie dodano również wyższej tooenable poziomu metod wysyłania powiadomień z platformą hello np. send_windows_notification dla systemu windows; send_apple_notification (dla apple) itd.</span><span class="sxs-lookup"><span data-stu-id="cb48e-146">This sample also adds higher level methods tooenable sending notifications based on hello platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="cb48e-147">Sklep Windows i Windows Phone 8.1 (z systemem innym niż platformy Silverlight)</span><span class="sxs-lookup"><span data-stu-id="cb48e-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="cb48e-148">Windows Phone 8.0 i 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="cb48e-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="cb48e-149">iOS</span><span class="sxs-lookup"><span data-stu-id="cb48e-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="cb48e-150">Android</span><span class="sxs-lookup"><span data-stu-id="cb48e-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="cb48e-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="cb48e-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="cb48e-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="cb48e-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="cb48e-153">Uruchamianie kodu języka Python powinny być powiadomienie znajdujących się na urządzeniu docelowym.</span><span class="sxs-lookup"><span data-stu-id="cb48e-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="cb48e-154">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="cb48e-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="cb48e-155">Włączenie właściwości debugowania</span><span class="sxs-lookup"><span data-stu-id="cb48e-155">Enabling debug property</span></span>
<span data-ttu-id="cb48e-156">Po włączeniu flagi debugowania podczas inicjowania hello NotificationHub, a następnie zostanie wyświetlony szczegółowe zrzutu żądań i odpowiedzi HTTP, a także NotificationOutcome podobnie następującej hello, gdzie można zrozumieć, jakie nagłówki HTTP są przekazywane w żądaniu hello i jakie HTTP Odebrano odpowiedź z hello Centrum powiadomień:![][1]</span><span class="sxs-lookup"><span data-stu-id="cb48e-156">When you enable debug flag while initializing hello NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like hello following where you can understand what HTTP headers are passed in hello request and what HTTP response was received from hello Notification Hub: ![][1]</span></span>

<span data-ttu-id="cb48e-157">Zobaczysz, np. szczegóły wyniku Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="cb48e-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="cb48e-158">Kiedy wiadomość hello są wysyłane pomyślnie toohello Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="cb48e-158">when hello message is successfully sent toohello Push Notification Service.</span></span> 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* <span data-ttu-id="cb48e-159">Jeśli wystąpiły nie znaleziono celu dla wszystkich powiadomień wypychanych, prawdopodobnie ma następujące hello toosee w odpowiedzi hello, (co oznacza, że nie było żadnej rejestracji znaleziono powiadomień hello toodeliver prawdopodobnie ponieważ rejestracje hello niektóre niedopasowane znaczniki)</span><span class="sxs-lookup"><span data-stu-id="cb48e-159">If there were no targets found for any push notification then you are likely going toosee hello following in hello response (which indicates that there were no registrations found toodeliver hello notification probably because hello registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a><span data-ttu-id="cb48e-160">Wyskakujące powiadomienia tooWindows emisji</span><span class="sxs-lookup"><span data-stu-id="cb48e-160">Broadcast toast notification tooWindows</span></span>
<span data-ttu-id="cb48e-161">Zwróć uwagę, hello nagłówki, które get wysyłane podczas przesyłania klienta tooWindows emisji wyskakujące powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="cb48e-161">Notice hello headers that get sent out when you are sending a broadcast toast notification tooWindows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="cb48e-162">Wyślij powiadomienie, określając tag (lub wyrażenie etykiety)</span><span class="sxs-lookup"><span data-stu-id="cb48e-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="cb48e-163">Nagłówek HTTP tagi hello powiadomienia, pobiera dodanego toohello HTTP żądania (w poniższym przykładzie hello, możemy wysyłania hello tooregistrations tylko powiadomienia o ładunku "Sport")</span><span class="sxs-lookup"><span data-stu-id="cb48e-163">Notice hello Tags HTTP header which gets added toohello HTTP request (in hello example below, we are sending hello notification only tooregistrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="cb48e-164">Wyślij powiadomienie określania wielu tagów</span><span class="sxs-lookup"><span data-stu-id="cb48e-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="cb48e-165">Zwróć uwagę, jak nagłówka HTTP tagi hello zostanie zmieniona, gdy wiele tagów są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="cb48e-165">Notice how hello Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="cb48e-166">Szablonu powiadomień</span><span class="sxs-lookup"><span data-stu-id="cb48e-166">Templated notification</span></span>
<span data-ttu-id="cb48e-167">Należy zauważyć, że hello zmiany nagłówka Format HTTP i hello treści ładunku jest wysyłany jako część treści żądania hello HTTP:</span><span class="sxs-lookup"><span data-stu-id="cb48e-167">Notice that hello Format HTTP header changes and hello payload body is sent as part of hello HTTP request body:</span></span>

<span data-ttu-id="cb48e-168">**Po stronie klienta — zarejestrowanych szablonu**</span><span class="sxs-lookup"><span data-stu-id="cb48e-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="cb48e-169">**Po stronie serwera — wysyłanie hello ładunku**</span><span class="sxs-lookup"><span data-stu-id="cb48e-169">**Server side - sending hello payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="cb48e-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb48e-170">Next Steps</span></span>
<span data-ttu-id="cb48e-171">W tym temacie firma Microsoft pokazano, jak toocreate proste Python REST klienta dla usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="cb48e-171">In this topic we showed how toocreate a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="cb48e-172">W tym miejscu można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cb48e-172">From here you can:</span></span>

* <span data-ttu-id="cb48e-173">Pobierz pełną hello [próbki otoki Python REST], zawierającą cały kod hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="cb48e-173">Download hello full [Python REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="cb48e-174">Kontynuować szkoleniowe dotyczące usługi Notification Hubs znakowanie funkcji w hello [samouczek fundamentalne wiadomości]</span><span class="sxs-lookup"><span data-stu-id="cb48e-174">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="cb48e-175">Kontynuować zapoznawanie funkcji szablonów centra powiadomień w hello [samouczek lokalizowanie wiadomości]</span><span class="sxs-lookup"><span data-stu-id="cb48e-175">Continue learning about Notification Hubs Templates feature in hello [Localizing News tutorial]</span></span>

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

