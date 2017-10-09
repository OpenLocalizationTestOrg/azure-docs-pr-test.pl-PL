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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>Jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji PHP na platformie Azure połączeń telefonicznych
Witaj poniższym przykładzie pokazano korzystania z usługi Twilio toomake wywołanie ze strony sieci web PHP hostowana na platformie Azure. Wynikowa aplikacji Hello monitują użytkownika hello wartości rozmowy telefonicznej, pokazane na powitania po zrzut ekranu.

![Formularz wywołania platformy Azure przy użyciu usługi Twilio i PHP][twilio_php]

Będą potrzebne następujące hello toodo toouse hello kodu w tym temacie:

1. Uzyskać konta usługi Twilio i uwierzytelniania tokenu z Twojej [usługi Twilio Console][twilio_console]. tooget wprowadzenie do usługi Twilio, ocenę cennik w [http://www.twilio.com/pricing][twilio_pricing]. Można założyć konto próbne w [https://www.twilio.com/try-twilio][try_twilio].
2. Uzyskaj hello [biblioteki usługi Twilio dla PHP](https://github.com/twilio/twilio-php) lub zainstaluj go w pakiecie GRUSZKOWA. Aby uzyskać więcej informacji, zobacz hello [plik readme](https://github.com/twilio/twilio-php/blob/master/README.md).
3. Zainstaluj hello Azure SDK dla programu PHP. Omówienie hello zestawu SDK i instrukcje dotyczące instalacji, zobacz [ustawienia hello Azure SDK dla języka PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>Tworzenie formularza sieci web nawiązywania połączenia
powitania po HTML kodu pokazuje sposób toobuild strony sieci web (**callform.html**), który pobiera dane użytkownika dla wywołania:

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

## <a name="create-hello-code-toomake-hello-call"></a>Utwórz hello kodu toomake hello wywołania
Witaj następującego kodu pokazuje sposób toobuild **makecall.php**, nazywany gdy hello użytkownik prześle formularz hello wyświetlanych przez **callform.html**. Kod Hello pokazano poniżej tworzy wiadomości powitania wywołania i generuje hello wywołania. Można również, czy toouse Twojego konta usługi Twilio i uwierzytelniania tokenu z hello [usługi Twilio Console] [ twilio_console] zamiast symbole zastępcze hello przypisane zbyt**$sid** i **$token** w kodzie hello poniżej.

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

Ponadto toomaking hello wywołania **makecall.php** Wyświetla niektóre metadane wywołanie, jak przedstawiono na poniższym obrazie hello. Aby uzyskać więcej informacji o metadanych wywołanie, zobacz [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].

![Odpowiedź wywołania platformy Azure przy użyciu usługi Twilio i PHP][twilio_php_response]

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello
Witaj, następnym krokiem jest toodeploy Twojego tooAzure aplikacji witryny sieci Web. Witaj następujące artykuły zawierają hello informacje dotyczące tworzenia witryny sieci Web i wdrażanie kodu za pomocą narzędzia Git, FTP lub WebMatrix (choć nie wszystkie informacje w każdym artykule są odpowiednie):

* [Utwórz witrynę sieci Web Azure PHP MySQL i wdrożyć przy użyciu narzędzia Git](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [Tworzenie witryny sieci Web platformy Azure PHP MySQL i wdrażanie za pomocą protokołu FTP](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>Następne kroki
Ten kod został podany tooshow możesz podstawowe funkcje w kodzie PHP na platformie Azure przy użyciu usługi Twilio. Przed wdrożeniem tooAzure w środowisku produkcyjnym, możesz tooadd więcej obsługi błędów lub innych funkcji. Na przykład:

* Zamiast za pomocą formularza sieci web, możesz użyć obiektów blob magazynu Azure lub numery telefonów toostore bazy danych SQL i wywołać tekstu. Aby dowiedzieć się, jak za pomocą obiektów blob magazynu Azure w kodzie PHP, zobacz [przy użyciu usługi Azure Storage z aplikacji PHP][howto_blob_storage_php]. Aby uzyskać informacje dotyczące korzystania z bazy danych SQL w języku PHP, zobacz [przy użyciu bazy danych SQL z aplikacji PHP][howto_sql_azure_php].
* Witaj **makecall.php** kod zawiera adres URL udostępniony do usługi Twilio ([http://twimlets.com/message][twimlet_message_url]) tooprovide odpowiedzi usługi Twilio Markup Language (TwiML), który informuje usługi Twilio jak tooproceed z wywołaniem hello. Na przykład może zawierać hello TwiML, która jest zwracana `<Say>` czasownika, który powoduje tekst jest rozmowy toohello wywołania adresata. Zamiast przy użyciu adresu URL dostarczony do usługi Twilio hello, można zbudować żądania własnych tooTwilio toorespond usługi; Aby uzyskać więcej informacji, zobacz [jak tooUse usługi Twilio głosowe i możliwości programu SMS w kodzie PHP][howto_twilio_voice_sms_php]. Więcej informacji na temat TwiML można znaleźć w folderze [http://www.twilio.com/docs/api/twiml][twiml]oraz dodatkowe informacje o `<Say>` i inne usługi Twilio zlecenia można znaleźć w folderze [http:// www.twilio.com/docs/API/twiml/Say][twilio_say].
* Przeczytaj wytyczne dotyczące zabezpieczeń usługi Twilio hello na [https://www.twilio.com/docs/security][twilio_docs_security].

Aby uzyskać dodatkowe informacje na temat usługi Twilio, zobacz [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Zobacz też
* [Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku PHP](partner-twilio-php-how-to-use-voice-sms.md)

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
