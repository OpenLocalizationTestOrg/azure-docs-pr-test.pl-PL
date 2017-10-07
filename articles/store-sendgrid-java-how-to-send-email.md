---
title: "Witaj toouse aaaHow SendGrid usługa poczty e-mail (Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wysłać wiadomość e-mail z hello SendGrid usługa poczty e-mail na platformie Azure. Przykłady kodu napisane w języku Java."
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a><span data-ttu-id="b1cbc-104">Jak tooSend SendGrid za pomocą poczty E-mail za pomocą języka Java</span><span class="sxs-lookup"><span data-stu-id="b1cbc-104">How tooSend Email Using SendGrid from Java</span></span>
<span data-ttu-id="b1cbc-105">W tym przewodniku pokazano, jak tooperform typowych zadań programowania SendGrid poczty e-mail usługi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="b1cbc-106">Witaj przykłady są napisane w języku Java.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-106">hello samples are written in Java.</span></span> <span data-ttu-id="b1cbc-107">Witaj omówione scenariusze obejmują **konstruowania e-mail**, **wysyłania wiadomości e-mail**, **dodawanie załączników**, **za pomocą filtrów**i **aktualizowanie właściwości**.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="b1cbc-108">Aby uzyskać więcej informacji na SendGrid i wysyłania wiadomości e-mail, zobacz hello [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-108">For more information on SendGrid and sending email, see hello [Next steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="b1cbc-109">Co to jest hello SendGrid usługa poczty E-mail?</span><span class="sxs-lookup"><span data-stu-id="b1cbc-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="b1cbc-110">Jest SendGrid [e-mail opartej na chmurze usługa] zapewnia niezawodne [dostarczania transakcyjnych wiadomości e-mail], skalowalności i analiz w czasie rzeczywistym oraz elastyczne interfejsów API, które umożliwiają łatwe niestandardowej integracji.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="b1cbc-111">Typowe scenariusze użycia SendGrid obejmują:</span><span class="sxs-lookup"><span data-stu-id="b1cbc-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="b1cbc-112">Nie są automatycznie wysyłane potwierdzenia toocustomers</span><span class="sxs-lookup"><span data-stu-id="b1cbc-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="b1cbc-113">Administrowanie dystrybucji wymieniono wysyłania klientów miesięczne e ulotki i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="b1cbc-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="b1cbc-114">Zbieranie metryk w czasie rzeczywistym dla zablokowanych poczty e-mail i czasu odpowiedzi klienta</span><span class="sxs-lookup"><span data-stu-id="b1cbc-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="b1cbc-115">Generowanie raportów toohelp trendów</span><span class="sxs-lookup"><span data-stu-id="b1cbc-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="b1cbc-116">Zapytania dotyczące przekazywania klienta</span><span class="sxs-lookup"><span data-stu-id="b1cbc-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="b1cbc-117">Powiadomienia e-mail z aplikacji</span><span class="sxs-lookup"><span data-stu-id="b1cbc-117">Email notifications from your application</span></span>

<span data-ttu-id="b1cbc-118">Aby uzyskać więcej informacji, zobacz <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="b1cbc-119">Utwórz konto SendGrid</span><span class="sxs-lookup"><span data-stu-id="b1cbc-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a><span data-ttu-id="b1cbc-120">Porady: Użyj hello javax.mail biblioteki</span><span class="sxs-lookup"><span data-stu-id="b1cbc-120">How to: Use hello javax.mail libraries</span></span>
<span data-ttu-id="b1cbc-121">Uzyskaj hello javax.mail biblioteki, na przykład z <http://www.oracle.com/technetwork/java/javamail> i zaimportuj je do kodu.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-121">Obtain hello javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="b1cbc-122">Na ogólne hello proces hello javax.mail biblioteki toosend e-mail za pomocą protokołu SMTP jest toodo hello następujące:</span><span class="sxs-lookup"><span data-stu-id="b1cbc-122">At a high-level, hello process for using hello javax.mail library toosend email using SMTP is toodo hello following:</span></span>

1. <span data-ttu-id="b1cbc-123">Określ wartości SMTP hello, w tym powitania serwera SMTP, który SendGrid jest smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-123">Specify hello SMTP values, including hello SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. <span data-ttu-id="b1cbc-124">Rozszerzanie hello *javax.mail.Authenticator* klasy w implementacji *getPasswordAuthentication* metody zwrócić SendGrid nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-124">Extend hello *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="b1cbc-125">Tworzenia sesji uwierzytelnionych poczty e-mail za pośrednictwem *javax.mail.Session* obiektu.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="b1cbc-126">Utwórz wiadomość i przypisać **do**, **z**, **podmiotu** i zawartości wartości.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="b1cbc-127">Przedstawiono to w hello [jak: utworzyć wiadomości E-mail](#how-to-create-an-email) sekcji.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-127">This is shown in hello [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="b1cbc-128">Wyślij wiadomość hello za pośrednictwem *javax.mail.Transport* obiektu.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-128">Send hello message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="b1cbc-129">Przedstawiono to w hello [jak: Wyślij wiadomość E-mail] [porady: wysyłanie wiadomości E-mail] sekcji.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-129">This is shown in hello [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="b1cbc-130">Porady: Tworzenie wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="b1cbc-130">How to: Create an email</span></span>
<span data-ttu-id="b1cbc-131">Witaj poniżej pokazano, jak toospecify wartości dla wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-131">hello following shows how toospecify values for an email.</span></span>

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a><span data-ttu-id="b1cbc-132">Porady: wysyłanie wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="b1cbc-132">How to: Send an email</span></span>
<span data-ttu-id="b1cbc-133">Witaj, po pokazuje, jak toosend wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-133">hello following shows how toosend an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="b1cbc-134">Porady: Dodawanie załącznika</span><span class="sxs-lookup"><span data-stu-id="b1cbc-134">How to: Add an attachment</span></span>
<span data-ttu-id="b1cbc-135">Witaj poniższy kod pokazuje sposób tooadd załącznika.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-135">hello following code shows you how tooadd an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="b1cbc-136">Porady: użycie filtruje stopki tooenable, śledzenia i analiza</span><span class="sxs-lookup"><span data-stu-id="b1cbc-136">How to: Use filters tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="b1cbc-137">SendGrid udostępnia funkcje dodatkowe poczty e-mail przy użyciu hello *filtry*.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-137">SendGrid provides additional email functionality through hello use of *filters*.</span></span> <span data-ttu-id="b1cbc-138">Są to ustawienia, które można dodać tooan wiadomości e-mail, aby włączyć określonych funkcji, np. włączenie kliknij śledzenia, Google analytics, subskrypcji śledzenia, i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-138">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="b1cbc-139">Aby uzyskać pełną listę filtrów, zobacz [ustawienia filtru][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="b1cbc-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="b1cbc-140">Witaj poniżej pokazano, jak tooinsert stopkę filtrowania, którego wynikiem tekst HTML znajdujący się u dołu hello hello wiadomości e-mail wysyłane.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-140">hello following shows how tooinsert a footer filter that results in HTML text appearing at hello bottom of hello email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="b1cbc-141">Innym przykładem filtr jest kliknij śledzenia.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="b1cbc-142">Załóżmy, że tekst wiadomości e-mail zawiera hiperłącza, takie jak hello poniżej, a ma tootrack powitania kliknij szybkość:</span><span class="sxs-lookup"><span data-stu-id="b1cbc-142">Let’s say that your email text contains a hyperlink, such as hello following, and you want tootrack hello click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="b1cbc-143">tooenable powitania kliknij śledzenia hello Użyj następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="b1cbc-143">tooenable hello click tracking, use hello following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="b1cbc-144">Porady: Aktualizacja właściwości wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="b1cbc-144">How to: Update email properties</span></span>
<span data-ttu-id="b1cbc-145">Niektóre właściwości wiadomości e-mail może zostać zastąpiona przy użyciu  **ustawić*właściwości*** lub dołączonych za pomocą  **dodać*właściwości***.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="b1cbc-146">Na przykład toospecify **ReplyTo** adresów, użyj następujących hello:</span><span class="sxs-lookup"><span data-stu-id="b1cbc-146">For example, toospecify **ReplyTo** addresses, use hello following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="b1cbc-147">tooadd **DW** adresatów, użyj hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="b1cbc-147">tooadd a **Cc** recipient, use hello following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="b1cbc-148">Porady: Użyj dodatkowych usług SendGrid</span><span class="sxs-lookup"><span data-stu-id="b1cbc-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="b1cbc-149">SendGrid oferuje API sieci web z aplikacji platformy Azure można dodatkowe funkcje SendGrid tooleverage.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-149">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="b1cbc-150">Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="b1cbc-150">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1cbc-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1cbc-151">Next steps</span></span>
<span data-ttu-id="b1cbc-152">Teraz, kiedy znasz już podstawy hello hello usługi SendGrid wiadomości E-mail, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="b1cbc-152">Now that you’ve learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="b1cbc-153">Przykład przedstawiający we wdrożeniu Azure przy użyciu SendGrid: [jak toosend poczty e-mail przy użyciu SendGrid za pomocą języka Java w wdrożenia usługi Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="b1cbc-153">Sample that demonstrates using SendGrid in an Azure deployment: [How toosend email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="b1cbc-154">Zestawu SDK SendGrid Java: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="b1cbc-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="b1cbc-155">Dokumentacja interfejsu API SendGrid: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="b1cbc-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="b1cbc-156">Oferta specjalna SendGrid dla klientów platformy Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="b1cbc-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[e-mail opartej na chmurze usługa]: https://sendgrid.com/email-solutions
[dostarczania transakcyjnych wiadomości e-mail]: https://sendgrid.com/transactional-email
