---
title: aaaTemplates
description: "W tym temacie wyjaśniono szablonów usługi Azure notification hubs."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a><span data-ttu-id="9527e-103">Szablony</span><span class="sxs-lookup"><span data-stu-id="9527e-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="9527e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9527e-104">Overview</span></span>
<span data-ttu-id="9527e-105">Szablony Włącz klienta aplikacji toospecify hello formacie hello powiadomienia musi tooreceive.</span><span class="sxs-lookup"><span data-stu-id="9527e-105">Templates enable a client application toospecify hello exact format of hello notifications it wants tooreceive.</span></span> <span data-ttu-id="9527e-106">Za pomocą szablonów, aplikacji może realizować kilka różnych korzyści, w tym następujące hello:</span><span class="sxs-lookup"><span data-stu-id="9527e-106">Using templates, an app can realize several different benefits, including hello following :</span></span>

* <span data-ttu-id="9527e-107">Niezależne od platformy wewnętrznej bazie danych</span><span class="sxs-lookup"><span data-stu-id="9527e-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="9527e-108">Spersonalizowanych powiadomień</span><span class="sxs-lookup"><span data-stu-id="9527e-108">Personalized notifications</span></span>
* <span data-ttu-id="9527e-109">Niezależność od wersji klienta</span><span class="sxs-lookup"><span data-stu-id="9527e-109">Client-version independence</span></span>
* <span data-ttu-id="9527e-110">Łatwe lokalizacji</span><span class="sxs-lookup"><span data-stu-id="9527e-110">Easy localization</span></span>

<span data-ttu-id="9527e-111">Ta sekcja zawiera dwa szczegółowe przykłady sposobu toouse szablony toosend niezależny od platformy powiadomienia przeznaczonych dla wszystkich urządzeń na platformach i toopersonalize emisji urządzenia tooeach powiadomień.</span><span class="sxs-lookup"><span data-stu-id="9527e-111">This section provides two in-depth examples of how toouse templates toosend platform-agnostic notifications targeting all your devices across platforms, and toopersonalize broadcast notification tooeach device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="9527e-112">Za pomocą szablonów i platform</span><span class="sxs-lookup"><span data-stu-id="9527e-112">Using templates cross-platform</span></span>
<span data-ttu-id="9527e-113">powiadomienia wypychane toosend standardowy sposób Hello jest toosend do każdego powiadomienia, który jest wysyłany, toobe określonych ładunku tooplatform usługi powiadomień (WNS, APNS).</span><span class="sxs-lookup"><span data-stu-id="9527e-113">hello standard way toosend push notifications is toosend, for each notification that is toobe sent, a specific payload tooplatform notification services (WNS, APNS).</span></span> <span data-ttu-id="9527e-114">Na przykład toosend alertu tooAPNS ładunek hello jest obiekt Json hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="9527e-114">For example, toosend an alert tooAPNS, hello payload is a Json object of hello following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="9527e-115">toosend podobny komunikat powiadomienia wyskakującego w aplikacji Sklepu Windows hello ładunek XML wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="9527e-115">toosend a similar toast message on a Windows Store application, hello XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="9527e-116">Podobne ładunki można tworzyć dla usługi MPNS (Windows Phone) i usługi GCM platform (Android).</span><span class="sxs-lookup"><span data-stu-id="9527e-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="9527e-117">To wymaganie wymusza hello aplikacji zaplecza tooproduce różnych ładunków dla każdej platformy i efektywnie sprawia, że zaplecza hello odpowiedzialny za część warstwy prezentacji hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9527e-117">This requirement forces hello app backend tooproduce different payloads for each platform, and effectively makes hello backend responsible for part of hello presentation layer of hello app.</span></span> <span data-ttu-id="9527e-118">Niektóre problemy obejmują lokalizacja i układy graficznego (szczególnie w przypadku aplikacji ze Sklepu Windows obejmujących powiadomień dla różnych typów Kafelki).</span><span class="sxs-lookup"><span data-stu-id="9527e-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="9527e-119">Witaj usługi Notification Hubs szablonu funkcja umożliwia aplikacji toocreate specjalne rejestracje klienta, nazywane rejestracji szablonu, które obejmują dodatkowo toohello zestawu tagów, szablon.</span><span class="sxs-lookup"><span data-stu-id="9527e-119">hello Notification Hubs template feature enables a client app toocreate special registrations, called template registrations, which include, in addition toohello set of tags, a template.</span></span> <span data-ttu-id="9527e-120">funkcji szablonu usługi Notification Hubs Hello umożliwia urządzenia klienckie aplikacji tooassociate z szablonami czy korzystasz z urządzenia (preferowane) lub rejestracji.</span><span class="sxs-lookup"><span data-stu-id="9527e-120">hello Notification Hubs template feature enables a client app tooassociate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="9527e-121">Podana hello poprzedzających przykłady ładunku, hello tylko informacje niezależne od platformy jest hello rzeczywiste komunikat alertu (Witaj!).</span><span class="sxs-lookup"><span data-stu-id="9527e-121">Given hello preceding payload examples, hello only platform-independent information is hello actual alert message (Hello!).</span></span> <span data-ttu-id="9527e-122">Szablon jest zestaw instrukcji dla hello Centrum powiadomień w sposób tooformat niezależne od platformy wiadomość hello rejestrację, aplikacja określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="9527e-122">A template is a set of instructions for hello Notification Hub on how tooformat a platform-independent message for hello registration of that specific client app.</span></span> <span data-ttu-id="9527e-123">W hello poprzedzających przykład, komunikat niezależny platformy hello jest jednej właściwości: **wiadomość = Hello!**.</span><span class="sxs-lookup"><span data-stu-id="9527e-123">In hello preceding example, hello platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="9527e-124">Witaj, na poniższej ilustracji przedstawiono hello powyżej proces:</span><span class="sxs-lookup"><span data-stu-id="9527e-124">hello following picture illustrates hello above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="9527e-125">Szablon Hello rejestracji aplikacji klienta z systemem iOS hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="9527e-125">hello template for hello iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="9527e-126">odpowiedni szablon powitania klienta w Sklepie Windows Hello jest:</span><span class="sxs-lookup"><span data-stu-id="9527e-126">hello corresponding template for hello Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="9527e-127">Należy zauważyć, że rzeczywista wiadomość hello zastępuje hello wyrażenia $(komunikat).</span><span class="sxs-lookup"><span data-stu-id="9527e-127">Notice that hello actual message is substituted for hello expression $(message).</span></span> <span data-ttu-id="9527e-128">To wyrażenie powoduje, że hello Centrum powiadomień przy każdym wysyła toothis wiadomości w określonej rejestracji, toobuild komunikat, który wykonuje go i przełączników w wartości typowych hello.</span><span class="sxs-lookup"><span data-stu-id="9527e-128">This expression instructs hello Notification Hub, whenever it sends a message toothis particular registration, toobuild a message that follows it and switches in hello common value.</span></span>

<span data-ttu-id="9527e-129">Podczas pracy z modelem instalacji klucz "Szablony" instalacji hello przechowuje JSON wielu szablonów.</span><span class="sxs-lookup"><span data-stu-id="9527e-129">If you are working with Installation model, hello installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="9527e-130">Podczas pracy z modelem rejestracji powitania klienta aplikacji można utworzyć wiele rejestracji w kolejności toouse wielu szablonów; na przykład szablon komunikaty alertów i szablon do aktualizacji kafelka.</span><span class="sxs-lookup"><span data-stu-id="9527e-130">If you are working with Registration model, hello client application can create multiple registrations in order toouse multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="9527e-131">Aplikacje klienckie można również mieszać rejestracje natywnego (rejestracje z szablonu) i rejestracji szablonu.</span><span class="sxs-lookup"><span data-stu-id="9527e-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="9527e-132">Witaj Centrum powiadomień wysyła jedno powiadomienie dla każdego szablonu bez uwzględniania czy należą toohello tej samej aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="9527e-132">hello Notification Hub sends one notification for each template without considering whether they belong toohello same client app.</span></span> <span data-ttu-id="9527e-133">To zachowanie może być używane tootranslate niezależne od platformy powiadomień na więcej powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="9527e-133">This behavior can be used tootranslate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="9527e-134">Na przykład Witaj tej samej toohello komunikat niezależny platformy Centrum powiadomień można bezproblemowo przekształcana alert wyskakujące i aktualizacji kafelka, bez konieczności toobe zaplecza hello świadomy naruszenia.</span><span class="sxs-lookup"><span data-stu-id="9527e-134">For example, hello same platform independent message toohello Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring hello backend toobe aware of it.</span></span> <span data-ttu-id="9527e-135">Należy pamiętać, że niektóre platformy (na przykład iOS) może Zwiń wiele toohello powiadomienia o tym samym urządzeniu, jeśli są one wysyłane w krótkim czasie.</span><span class="sxs-lookup"><span data-stu-id="9527e-135">Note that some platforms (for example, iOS) might collapse multiple notifications toohello same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="9527e-136">Za pomocą szablonów na potrzeby personalizacji</span><span class="sxs-lookup"><span data-stu-id="9527e-136">Using templates for personalization</span></span>
<span data-ttu-id="9527e-137">Inną zaletą toousing szablonów jest hello toouse możliwości usługi Notification Hubs tooperform na rejestracji personalizacji powiadomień.</span><span class="sxs-lookup"><span data-stu-id="9527e-137">Another advantage toousing templates is hello ability toouse Notification Hubs tooperform per-registration personalization of notifications.</span></span> <span data-ttu-id="9527e-138">Rozważmy na przykład aplikację pogodzie, która wyświetla kafelka z pogodą hello z określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="9527e-138">For example, consider a weather app that displays a tile with hello weather conditions at a specific location.</span></span> <span data-ttu-id="9527e-139">Użytkownik może wybrać między stopni c lub f i prognozy pojedyncze lub pięć dni.</span><span class="sxs-lookup"><span data-stu-id="9527e-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="9527e-140">Za pomocą szablonów, każdej instalacji aplikacji klienta można zarejestrować formatu hello wymagane (1-dniowego Celsjusz, 1-dniowego f, 5 dni c, 5 dni Stopnie Fahrenheita), i mieć hello Wyślij pojedynczy komunikat, który zawiera wszystkie informacje hello wymagane toofill tych wewnętrznej bazy danych Szablony (na przykład pięciodniowego prognozy z stopni c i f).</span><span class="sxs-lookup"><span data-stu-id="9527e-140">Using templates, each client app installation can register for hello format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have hello backend send a single message that contains all hello information required toofill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="9527e-141">Szablon Hello hello jeden dzień prognozy z c temperatury jest następująca:</span><span class="sxs-lookup"><span data-stu-id="9527e-141">hello template for hello one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="9527e-142">toohello wysłano wiadomość Hello Centrum powiadomień zawiera wszystkie hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="9527e-142">hello message sent toohello Notification Hub contains all hello following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="9527e-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="9527e-143">day1_image</span></span></td><td><span data-ttu-id="9527e-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="9527e-144">day2_image</span></span></td><td><span data-ttu-id="9527e-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="9527e-145">day3_image</span></span></td><td><span data-ttu-id="9527e-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="9527e-146">day4_image</span></span></td><td><span data-ttu-id="9527e-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="9527e-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="9527e-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="9527e-148">day1_tempC</span></span></td><td><span data-ttu-id="9527e-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="9527e-149">day2_tempC</span></span></td><td><span data-ttu-id="9527e-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="9527e-150">day3_tempC</span></span></td><td><span data-ttu-id="9527e-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="9527e-151">day4_tempC</span></span></td><td><span data-ttu-id="9527e-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="9527e-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="9527e-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="9527e-153">day1_tempF</span></span></td><td><span data-ttu-id="9527e-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="9527e-154">day2_tempF</span></span></td><td><span data-ttu-id="9527e-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="9527e-155">day3_tempF</span></span></td><td><span data-ttu-id="9527e-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="9527e-156">day4_tempF</span></span></td><td><span data-ttu-id="9527e-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="9527e-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="9527e-158">Za pomocą tego wzorca, hello wewnętrznej bazy danych tylko wysyła pojedynczą wiadomość bez opcji personalizacji określonych toostore dla użytkowników aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9527e-158">By using this pattern, hello backend only sends a single message without having toostore specific personalization options for hello app users.</span></span> <span data-ttu-id="9527e-159">Witaj, na poniższej ilustracji przedstawiono w tym scenariuszu:</span><span class="sxs-lookup"><span data-stu-id="9527e-159">hello following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a><span data-ttu-id="9527e-160">Jak szablony tooregister</span><span class="sxs-lookup"><span data-stu-id="9527e-160">How tooregister templates</span></span>
<span data-ttu-id="9527e-161">tooregister z szablonów przy użyciu modelu instalacji hello (preferowane) lub hello modelu rejestracji, zobacz [zarządzania rejestracji](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="9527e-161">tooregister with templates using hello Installation model (preferred), or hello Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="9527e-162">Język wyrażeń</span><span class="sxs-lookup"><span data-stu-id="9527e-162">Template expression language</span></span>
<span data-ttu-id="9527e-163">Szablony są ograniczone tooXML lub formatowania dokumentu JSON.</span><span class="sxs-lookup"><span data-stu-id="9527e-163">Templates are limited tooXML or JSON document formats.</span></span> <span data-ttu-id="9527e-164">Ponadto tylko można umieścić wyrażenia w szczególności miejscach; na przykład atrybutów węzła lub wartości XML ciągu wartości właściwości dla formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="9527e-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="9527e-165">Witaj poniższej tabeli przedstawiono dozwolone w szablonach języka hello:</span><span class="sxs-lookup"><span data-stu-id="9527e-165">hello following table shows hello language allowed in templates:</span></span>

| <span data-ttu-id="9527e-166">wyrażenie</span><span class="sxs-lookup"><span data-stu-id="9527e-166">Expression</span></span> | <span data-ttu-id="9527e-167">Opis</span><span class="sxs-lookup"><span data-stu-id="9527e-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9527e-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="9527e-168">$(prop)</span></span> |<span data-ttu-id="9527e-169">Właściwości zdarzenia tooan odwołania o hello podanej nazwie.</span><span class="sxs-lookup"><span data-stu-id="9527e-169">Reference tooan event property with hello given name.</span></span> <span data-ttu-id="9527e-170">Nazwy właściwości nie jest rozróżniana.</span><span class="sxs-lookup"><span data-stu-id="9527e-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="9527e-171">Tego wyrażenia rozpoznaje do wartości tekstowej właściwości hello lub pusty ciąg, jeśli nie ma właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="9527e-171">This expression resolves into hello property’s text value or into an empty string if hello property is not present.</span></span> |
| <span data-ttu-id="9527e-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="9527e-172">$(prop, n)</span></span> |<span data-ttu-id="9527e-173">Jak powyżej, ale hello tekst jest jawnie przycinana n znaków, na przykład $(tytuł, 20) klipy zawartość hello hello tytuł właściwości na 20 znaków.</span><span class="sxs-lookup"><span data-stu-id="9527e-173">As above, but hello text is explicitly clipped at n characters, for example $(title, 20) clips hello contents of hello title property at 20 characters.</span></span> |
| <span data-ttu-id="9527e-174">. (prop, n)</span><span class="sxs-lookup"><span data-stu-id="9527e-174">.(prop, n)</span></span> |<span data-ttu-id="9527e-175">Jako powyżej, ale hello tekstu z wielokropkiem jest sufiksem, jak ma zostać przycięta.</span><span class="sxs-lookup"><span data-stu-id="9527e-175">As above, but hello text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="9527e-176">Całkowity rozmiar hello Hello przycinana ciągu i sufiks hello nie przekracza n znaków.</span><span class="sxs-lookup"><span data-stu-id="9527e-176">hello total size of hello clipped string and hello suffix does not exceed n characters.</span></span> <span data-ttu-id="9527e-177">. (tytuł, 20) z właściwości wejściowej "Jest wiersz tytułu hello" skutkuje **jest tytuł hello...**</span><span class="sxs-lookup"><span data-stu-id="9527e-177">.(title, 20) with an input property of “This is hello title line” results in **This is hello title...**</span></span> |
| <span data-ttu-id="9527e-178">%(Prop)</span><span class="sxs-lookup"><span data-stu-id="9527e-178">%(prop)</span></span> |<span data-ttu-id="9527e-179">Podobne too$(name), chyba że te dane wyjściowe hello jest kodowany w formacie identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="9527e-179">Similar too$(name) except that hello output is URI-encoded.</span></span> |
| <span data-ttu-id="9527e-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="9527e-180">#(prop)</span></span> |<span data-ttu-id="9527e-181">Używane w szablonach JSON (na przykład dla systemów iOS i Android szablonów).</span><span class="sxs-lookup"><span data-stu-id="9527e-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="9527e-182">Ta funkcja działa dokładnie hello takie same jak $(prop) wcześniej określony, z wyjątkiem przypadków, gdy używane w szablonach JSON (na przykład szablony Apple).</span><span class="sxs-lookup"><span data-stu-id="9527e-182">This function works exactly hello same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="9527e-183">W tym przypadku, jeśli ta funkcja nie jest ujęta w "{","}" (na przykład "myJsonProperty": "#(nazwa)"), a jego wartość numer tooa w formacie Javascript, na przykład regexp: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, a następnie hello dane wyjściowe JSON jest liczbą.</span><span class="sxs-lookup"><span data-stu-id="9527e-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates tooa number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then hello output JSON is a number.</span></span><br><br><span data-ttu-id="9527e-184">Na przykład "badge:"#(nazwa)"staje się"badge": 40 (a nie"40").</span><span class="sxs-lookup"><span data-stu-id="9527e-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="9527e-185">"tekst" lub "text"</span><span class="sxs-lookup"><span data-stu-id="9527e-185">‘text’ or “text”</span></span> |<span data-ttu-id="9527e-186">Literału.</span><span class="sxs-lookup"><span data-stu-id="9527e-186">A literal.</span></span> <span data-ttu-id="9527e-187">Literały zawiera dowolny tekst ujęty w pojedynczym lub podwójnym cudzysłowie.</span><span class="sxs-lookup"><span data-stu-id="9527e-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="9527e-188">Wyr1 + Wyr2</span><span class="sxs-lookup"><span data-stu-id="9527e-188">expr1 + expr2</span></span> |<span data-ttu-id="9527e-189">operator łączenia Hello Sprzęganie dwóch wyrażeń w jednym ciągu.</span><span class="sxs-lookup"><span data-stu-id="9527e-189">hello concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="9527e-190">Witaj wyrażenia może być dowolny z hello poprzedzających formularzy.</span><span class="sxs-lookup"><span data-stu-id="9527e-190">hello expressions can be any of hello preceding forms.</span></span>

<span data-ttu-id="9527e-191">Używając łączenia hello całego wyrażenia musi być ujęty w {}.</span><span class="sxs-lookup"><span data-stu-id="9527e-191">When using concatenation, hello entire expression must be surrounded with {}.</span></span> <span data-ttu-id="9527e-192">Na przykład {$(prop) + "-" + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="9527e-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="9527e-193">Na przykład hello następujący element nie jest prawidłowy szablon XML:</span><span class="sxs-lookup"><span data-stu-id="9527e-193">For example, hello following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="9527e-194">Jak wyjaśniono łączenia, używając wyrażenia musi być ujęte w nawiasach klamrowych.</span><span class="sxs-lookup"><span data-stu-id="9527e-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="9527e-195">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9527e-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

