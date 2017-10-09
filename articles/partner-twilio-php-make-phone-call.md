---
title: "toomake aaaHow rozmowy telefonicznej z usługi Twilio (PHP) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak komunikatów toomake połączeń telefonicznych i Wyślij wiadomość SMS z usługi interfejsu API usługi Twilio hello na platformie Azure. Przykłady są przeznaczone dla aplikacji PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="599c7-104">Jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji PHP na platformie Azure połączeń telefonicznych</span><span class="sxs-lookup"><span data-stu-id="599c7-104">How tooMake a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="599c7-105">Witaj poniższym przykładzie pokazano korzystania z usługi Twilio toomake wywołanie ze strony sieci web PHP hostowana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="599c7-105">hello following example shows you how you can use Twilio toomake a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="599c7-106">Wynikowa aplikacji Hello monitują użytkownika hello wartości rozmowy telefonicznej, pokazane na powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="599c7-106">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Formularz wywołania platformy Azure przy użyciu usługi Twilio i PHP][twilio_php]

<span data-ttu-id="599c7-108">Będą potrzebne następujące hello toodo toouse hello kodu w tym temacie:</span><span class="sxs-lookup"><span data-stu-id="599c7-108">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="599c7-109">Uzyskać konta usługi Twilio i uwierzytelniania tokenu z Twojej [usługi Twilio Console][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="599c7-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="599c7-110">tooget wprowadzenie do usługi Twilio, ocenę cennik w [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="599c7-110">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="599c7-111">Można założyć konto próbne w [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="599c7-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="599c7-112">Uzyskaj hello [biblioteki usługi Twilio dla PHP](https://github.com/twilio/twilio-php) lub zainstaluj go w pakiecie GRUSZKOWA.</span><span class="sxs-lookup"><span data-stu-id="599c7-112">Obtain hello [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="599c7-113">Aby uzyskać więcej informacji, zobacz hello [plik readme](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="599c7-113">For more information, see hello [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="599c7-114">Zainstaluj hello Azure SDK dla programu PHP.</span><span class="sxs-lookup"><span data-stu-id="599c7-114">Install hello Azure SDK for PHP.</span></span> <span data-ttu-id="599c7-115">Omówienie hello zestawu SDK i instrukcje dotyczące instalacji, zobacz [ustawienia hello Azure SDK dla języka PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="599c7-115">For an overview of hello SDK and instructions on installing it, see [Set up hello Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="599c7-116">Tworzenie formularza sieci web nawiązywania połączenia</span><span class="sxs-lookup"><span data-stu-id="599c7-116">Create a web form for making a call</span></span>
<span data-ttu-id="599c7-117">powitania po HTML kodu pokazuje sposób toobuild strony sieci web (**callform.html**), który pobiera dane użytkownika dla wywołania:</span><span class="sxs-lookup"><span data-stu-id="599c7-117">hello following HTML code shows how toobuild a web page (**callform.html**) that retrieves user data for making a call:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="599c7-118">Utwórz hello kodu toomake hello wywołania</span><span class="sxs-lookup"><span data-stu-id="599c7-118">Create hello code toomake hello call</span></span>
<span data-ttu-id="599c7-119">Witaj następującego kodu pokazuje sposób toobuild **makecall.php**, nazywany gdy hello użytkownik prześle formularz hello wyświetlanych przez **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="599c7-119">hello following code shows how toobuild **makecall.php**, which is called when hello user submits hello form displayed by **callform.html**.</span></span> <span data-ttu-id="599c7-120">Kod Hello pokazano poniżej tworzy wiadomości powitania wywołania i generuje hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="599c7-120">hello code shown below creates hello call message and generates hello call.</span></span> <span data-ttu-id="599c7-121">Można również, czy toouse Twojego konta usługi Twilio i uwierzytelniania tokenu z hello [usługi Twilio Console] [ twilio_console] zamiast symbole zastępcze hello przypisane zbyt**$sid** i **$token** w kodzie hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="599c7-121">Also, be sure toouse your Twilio account and authentication token from hello [Twilio Console][twilio_console] instead of hello placeholder values assigned too**$sid** and **$token** in hello code below.</span></span>

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

<span data-ttu-id="599c7-122">Ponadto toomaking hello wywołania **makecall.php** Wyświetla niektóre metadane wywołanie, jak przedstawiono na poniższym obrazie hello.</span><span class="sxs-lookup"><span data-stu-id="599c7-122">In addition toomaking hello call, **makecall.php** displays some call metadata, as is shown in hello image below.</span></span> <span data-ttu-id="599c7-123">Aby uzyskać więcej informacji o metadanych wywołanie, zobacz [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="599c7-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Odpowiedź wywołania platformy Azure przy użyciu usługi Twilio i PHP][twilio_php_response]

## <a name="run-hello-application"></a><span data-ttu-id="599c7-125">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="599c7-125">Run hello application</span></span>
<span data-ttu-id="599c7-126">Witaj, następnym krokiem jest toodeploy Twojego tooAzure aplikacji witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="599c7-126">hello next step is toodeploy your application tooAzure Websites.</span></span> <span data-ttu-id="599c7-127">Witaj następujące artykuły zawierają hello informacje dotyczące tworzenia witryny sieci Web i wdrażanie kodu za pomocą narzędzia Git, FTP lub WebMatrix (choć nie wszystkie informacje w każdym artykule są odpowiednie):</span><span class="sxs-lookup"><span data-stu-id="599c7-127">hello following articles contain hello information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="599c7-128">Utwórz witrynę sieci Web Azure PHP MySQL i wdrożyć przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="599c7-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="599c7-129">Tworzenie witryny sieci Web platformy Azure PHP MySQL i wdrażanie za pomocą protokołu FTP</span><span class="sxs-lookup"><span data-stu-id="599c7-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="599c7-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="599c7-130">Next steps</span></span>
<span data-ttu-id="599c7-131">Ten kod został podany tooshow możesz podstawowe funkcje w kodzie PHP na platformie Azure przy użyciu usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="599c7-131">This code was provided tooshow you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="599c7-132">Przed wdrożeniem tooAzure w środowisku produkcyjnym, możesz tooadd więcej obsługi błędów lub innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="599c7-132">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="599c7-133">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="599c7-133">For example:</span></span>

* <span data-ttu-id="599c7-134">Zamiast za pomocą formularza sieci web, możesz użyć obiektów blob magazynu Azure lub numery telefonów toostore bazy danych SQL i wywołać tekstu.</span><span class="sxs-lookup"><span data-stu-id="599c7-134">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="599c7-135">Aby dowiedzieć się, jak za pomocą obiektów blob magazynu Azure w kodzie PHP, zobacz [przy użyciu usługi Azure Storage z aplikacji PHP][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="599c7-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="599c7-136">Aby uzyskać informacje dotyczące korzystania z bazy danych SQL w języku PHP, zobacz [przy użyciu bazy danych SQL z aplikacji PHP][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="599c7-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="599c7-137">Witaj **makecall.php** kod zawiera adres URL udostępniony do usługi Twilio ([http://twimlets.com/message][twimlet_message_url]) tooprovide odpowiedzi usługi Twilio Markup Language (TwiML), który informuje usługi Twilio jak tooproceed z wywołaniem hello.</span><span class="sxs-lookup"><span data-stu-id="599c7-137">hello **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="599c7-138">Na przykład może zawierać hello TwiML, która jest zwracana `<Say>` czasownika, który powoduje tekst jest rozmowy toohello wywołania adresata.</span><span class="sxs-lookup"><span data-stu-id="599c7-138">For example, hello TwiML that is returned can contain a `<Say>` verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="599c7-139">Zamiast przy użyciu adresu URL dostarczony do usługi Twilio hello, można zbudować żądania własnych tooTwilio toorespond usługi; Aby uzyskać więcej informacji, zobacz [jak tooUse usługi Twilio głosowe i możliwości programu SMS w kodzie PHP][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="599c7-139">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="599c7-140">Więcej informacji na temat TwiML można znaleźć w folderze [http://www.twilio.com/docs/api/twiml][twiml]oraz dodatkowe informacje o `<Say>` i inne usługi Twilio zlecenia można znaleźć w folderze [http:// www.twilio.com/docs/API/twiml/Say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="599c7-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="599c7-141">Przeczytaj wytyczne dotyczące zabezpieczeń usługi Twilio hello na [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="599c7-141">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="599c7-142">Aby uzyskać dodatkowe informacje na temat usługi Twilio, zobacz [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="599c7-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="599c7-143">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="599c7-143">See Also</span></span>
* [<span data-ttu-id="599c7-144">Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku PHP</span><span class="sxs-lookup"><span data-stu-id="599c7-144">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
