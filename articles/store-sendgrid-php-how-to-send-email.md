---
title: "Witaj toouse aaaHow SendGrid usługa poczty e-mail (PHP) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wysłać wiadomość e-mail z hello SendGrid usługa poczty e-mail na platformie Azure. Przykłady kodu napisane w języku PHP."
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a><span data-ttu-id="ac64b-104">Jak tooUse hello SendGrid usługa poczty E-mail za pomocą języka PHP</span><span class="sxs-lookup"><span data-stu-id="ac64b-104">How tooUse hello SendGrid Email Service from PHP</span></span>
<span data-ttu-id="ac64b-105">W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello SendGrid poczty e-mail usługi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ac64b-105">This guide demonstrates how tooperform common programming tasks with hello SendGrid email service on Azure.</span></span> <span data-ttu-id="ac64b-106">Przykłady Hello są zapisywane w kodzie PHP.</span><span class="sxs-lookup"><span data-stu-id="ac64b-106">hello samples are written in PHP.</span></span>
<span data-ttu-id="ac64b-107">Witaj omówione scenariusze obejmują **konstruowania e-mail**, **wysyłania wiadomości e-mail**, i **dodawanie załączników**.</span><span class="sxs-lookup"><span data-stu-id="ac64b-107">hello scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="ac64b-108">Aby uzyskać więcej informacji na SendGrid i wysyłania wiadomości e-mail, zobacz hello [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ac64b-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="ac64b-109">Co to jest hello SendGrid usługa poczty E-mail?</span><span class="sxs-lookup"><span data-stu-id="ac64b-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="ac64b-110">Jest SendGrid [e-mail opartej na chmurze usługa] zapewnia niezawodne [dostarczania transakcyjnych wiadomości e-mail], skalowalności i analiz w czasie rzeczywistym oraz elastyczne interfejsów API, które umożliwiają łatwe niestandardowej integracji.</span><span class="sxs-lookup"><span data-stu-id="ac64b-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="ac64b-111">Typowe scenariusze użycia SendGrid obejmują:</span><span class="sxs-lookup"><span data-stu-id="ac64b-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="ac64b-112">Nie są automatycznie wysyłane potwierdzenia toocustomers</span><span class="sxs-lookup"><span data-stu-id="ac64b-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="ac64b-113">Administrowanie dystrybucji wymieniono wysyłania klientów miesięczne e ulotki i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="ac64b-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="ac64b-114">Zbieranie metryk w czasie rzeczywistym dla zablokowanych poczty e-mail i czasu odpowiedzi klienta</span><span class="sxs-lookup"><span data-stu-id="ac64b-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="ac64b-115">Generowanie raportów toohelp trendów</span><span class="sxs-lookup"><span data-stu-id="ac64b-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="ac64b-116">Zapytania dotyczące przekazywania klienta</span><span class="sxs-lookup"><span data-stu-id="ac64b-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="ac64b-117">Powiadomienia e-mail z aplikacji</span><span class="sxs-lookup"><span data-stu-id="ac64b-117">Email notifications from your application</span></span>

<span data-ttu-id="ac64b-118">Aby uzyskać więcej informacji, zobacz [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="ac64b-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="ac64b-119">Utwórz konto SendGrid</span><span class="sxs-lookup"><span data-stu-id="ac64b-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="ac64b-120">Przy użyciu SendGrid z aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="ac64b-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="ac64b-121">Włączenie w aplikacji Azure PHP korzystania z żadnych specjalnych konfiguracji lub kodowania.</span><span class="sxs-lookup"><span data-stu-id="ac64b-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="ac64b-122">Ponieważ usługa jest SendGrid, jest dostępny w hello dokładnie tak samo z aplikacji w chmurze jak mogą z aplikacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="ac64b-122">Because SendGrid is a service, it can be accessed in exactly hello same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="ac64b-123">Porady: wysyłanie wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="ac64b-123">How to: Send an Email</span></span>
<span data-ttu-id="ac64b-124">Możesz wysłać wiadomości e-mail przy użyciu protokołu SMTP lub hello udostępniane przez włączenie interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ac64b-124">You can send email using either SMTP or hello Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="ac64b-125">INTERFEJS API SMTP</span><span class="sxs-lookup"><span data-stu-id="ac64b-125">SMTP API</span></span>
<span data-ttu-id="ac64b-126">toosend poczty e-mail przy użyciu hello SendGrid SMTP API, użyj *programu Swift poczty*, biblioteki platformy składników do wysyłania wiadomości e-mail z aplikacji PHP.</span><span class="sxs-lookup"><span data-stu-id="ac64b-126">toosend email using hello SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="ac64b-127">Możesz pobrać hello *programu Swift poczty* biblioteki z [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (Użyj [Composer] tooinstall SWIFT programu poczty).</span><span class="sxs-lookup"><span data-stu-id="ac64b-127">You can download hello *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] tooinstall Swift Mailer).</span></span> <span data-ttu-id="ac64b-128">Wysyłanie wiadomości e-mail z biblioteką hello obejmuje utworzenie wystąpienia <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_programu poczty</span>, i <span class="auto-style2">Swift\_wiadomości </span> klas, ustawienie odpowiednie właściwości i wywoływania <span class="auto-style2">Swift\_Mailer::send</span> metody.</span><span class="sxs-lookup"><span data-stu-id="ac64b-128">Sending email with hello library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a><span data-ttu-id="ac64b-129">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="ac64b-129">Web API</span></span>
<span data-ttu-id="ac64b-130">Użyj tego PHP [curl funkcja] [ curl function] toosend e-mail przy użyciu hello SendGrid interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ac64b-130">Use PHP's [curl function][curl function] toosend email using hello SendGrid Web API.</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

<span data-ttu-id="ac64b-131">Włączenie tego interfejsu API sieci Web jest bardzo podobne tooa interfejsu API REST, chociaż nie jest rzeczywiście interfejsu API RESTful ponieważ w większości wywołania zarówno GET i POST zlecenia, które mogą być używane zamiennie.</span><span class="sxs-lookup"><span data-stu-id="ac64b-131">SendGrid's Web API is very similar tooa REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="ac64b-132">Porady: Dodawanie załącznika</span><span class="sxs-lookup"><span data-stu-id="ac64b-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="ac64b-133">INTERFEJS API SMTP</span><span class="sxs-lookup"><span data-stu-id="ac64b-133">SMTP API</span></span>
<span data-ttu-id="ac64b-134">Wysyłanie załączników za pomocą interfejsu API SMTP hello obejmuje jeden dodatkowy wiersz kodu toohello przykładowy skrypt do wysyłania wiadomości e-mail z programu Swift poczty.</span><span class="sxs-lookup"><span data-stu-id="ac64b-134">Sending an attachment using hello SMTP API involves one additional line of code toohello example script for sending an email with Swift Mailer.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

<span data-ttu-id="ac64b-135">dodatkowe wiersz kodu Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="ac64b-135">hello additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="ac64b-136">Ten wiersz kodu wywołania hello attach — metoda na <span class="auto-style2">Swift\_komunikat</span> obiektu i używa metody statycznej <span class="auto-style2">fromPath</span> na <span class="auto-style2">Swift\_załącznika</span>klasy tooget i Dołącz plik tooa wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ac64b-136">This line of code calls hello attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class tooget and attach a file tooa message.</span></span>

### <a name="web-api"></a><span data-ttu-id="ac64b-137">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="ac64b-137">Web API</span></span>
<span data-ttu-id="ac64b-138">Wysyłanie załączników za pomocą interfejsu API sieci Web hello jest bardzo podobne toosending e-mail przy użyciu hello interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ac64b-138">Sending an attachment using hello Web API is very similar toosending an email using hello Web API.</span></span> <span data-ttu-id="ac64b-139">Pamiętaj jednak, w następującym przykładzie hello hello Tablica parametrów musi zawierać ten element:</span><span class="sxs-lookup"><span data-stu-id="ac64b-139">However, note that in hello example that follows, hello parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="ac64b-140">Przykład:</span><span class="sxs-lookup"><span data-stu-id="ac64b-140">Example:</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="ac64b-141">Porady: Użyj filtrów stopki tooEnable, śledzenia i analiza</span><span class="sxs-lookup"><span data-stu-id="ac64b-141">How to: Use Filters tooEnable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="ac64b-142">SendGrid udostępnia funkcje dodatkowe poczty e-mail przy użyciu hello "filtrów".</span><span class="sxs-lookup"><span data-stu-id="ac64b-142">SendGrid provides additional email functionality through hello use of 'filters'.</span></span> <span data-ttu-id="ac64b-143">Są to ustawienia, które można dodać tooan wiadomości e-mail, aby włączyć określonych funkcji, np. włączenie kliknij śledzenia, Google analytics, subskrypcji śledzenia, i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="ac64b-143">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="ac64b-144">Filtry można zastosowane tooa wiadomości przy użyciu hello filtry właściwości.</span><span class="sxs-lookup"><span data-stu-id="ac64b-144">Filters can be applied tooa message by using hello filters property.</span></span> <span data-ttu-id="ac64b-145">Każdy filtr jest określany przez skrót zawierający ustawienia specyficzne dla filtru.</span><span class="sxs-lookup"><span data-stu-id="ac64b-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="ac64b-146">Poniższy przykład umożliwia hello stopki filtru i określa, że wiadomość SMS, który ma być dołączany toohello dołu hello wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="ac64b-146">The following example enables hello footer filter and specifies a text message that will be appended toohello bottom of hello email message.</span></span>
<span data-ttu-id="ac64b-147">W tym przykładzie używamy [sendgrid php biblioteki].</span><span class="sxs-lookup"><span data-stu-id="ac64b-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="ac64b-148">Użyj [Composer] tooinstall biblioteki:</span><span class="sxs-lookup"><span data-stu-id="ac64b-148">Use [Composer] tooinstall library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="ac64b-149">Przykład:</span><span class="sxs-lookup"><span data-stu-id="ac64b-149">Example:</span></span>    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a><span data-ttu-id="ac64b-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac64b-150">Next Steps</span></span>
<span data-ttu-id="ac64b-151">Teraz, kiedy znasz już podstawy hello hello usługi SendGrid wiadomości E-mail, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="ac64b-151">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="ac64b-152">Dokumentacja SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="ac64b-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="ac64b-153">Biblioteka SendGrid PHP: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="ac64b-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="ac64b-154">Oferta specjalna SendGrid dla klientów platformy Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="ac64b-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="ac64b-155">Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="ac64b-155">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[e-mail opartej na chmurze usługa]: https://sendgrid.com/email-solutions
[dostarczania transakcyjnych wiadomości e-mail]: https://sendgrid.com/transactional-email
[sendgrid php biblioteki]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[Composer]: https://getcomposer.org/download/
