---
title: "Jak używać usługi poczty e-mail SendGrid (Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wysłać wiadomość e-mail z usługi poczty e-mail SendGrid na platformie Azure. Przykłady kodu napisane w języku Java."
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
ms.openlocfilehash: 85a0e302626ca14ac039ee6f662f372ddbeb62c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java"></a><span data-ttu-id="fffa9-104">Sposób wysyłania poczty E-mail przy użyciu SendGrid za pomocą języka Java</span><span class="sxs-lookup"><span data-stu-id="fffa9-104">How to Send Email Using SendGrid from Java</span></span>
<span data-ttu-id="fffa9-105">W tym przewodniku przedstawiono sposób wykonywania typowych zadań programowania usługi poczty e-mail SendGrid na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fffa9-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="fffa9-106">Przykłady są napisane w języku Java.</span><span class="sxs-lookup"><span data-stu-id="fffa9-106">The samples are written in Java.</span></span> <span data-ttu-id="fffa9-107">Omówione scenariusze obejmują **konstruowania e-mail**, **wysyłania wiadomości e-mail**, **dodawanie załączników**, **za pomocą filtrów**i **aktualizowanie właściwości**.</span><span class="sxs-lookup"><span data-stu-id="fffa9-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="fffa9-108">Aby uzyskać więcej informacji na SendGrid i wysyłania wiadomości e-mail, zobacz [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fffa9-108">For more information on SendGrid and sending email, see the [Next steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="fffa9-109">Co to jest usługa SendGrid poczty E-mail?</span><span class="sxs-lookup"><span data-stu-id="fffa9-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="fffa9-110">Jest SendGrid [e-mail opartej na chmurze usługa] zapewnia niezawodne [dostarczania transakcyjnych wiadomości e-mail], skalowalności i analiz w czasie rzeczywistym oraz elastyczne interfejsów API, które umożliwiają łatwe niestandardowej integracji.</span><span class="sxs-lookup"><span data-stu-id="fffa9-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="fffa9-111">Typowe scenariusze użycia SendGrid obejmują:</span><span class="sxs-lookup"><span data-stu-id="fffa9-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="fffa9-112">Potwierdzenia są automatycznie wysyłane do klientów</span><span class="sxs-lookup"><span data-stu-id="fffa9-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="fffa9-113">Administrowanie dystrybucji wymieniono wysyłania klientów miesięczne e ulotki i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="fffa9-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="fffa9-114">Zbieranie metryk w czasie rzeczywistym dla zablokowanych poczty e-mail i czasu odpowiedzi klienta</span><span class="sxs-lookup"><span data-stu-id="fffa9-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="fffa9-115">Generowanie raportów, aby ułatwić identyfikację trendów</span><span class="sxs-lookup"><span data-stu-id="fffa9-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="fffa9-116">Zapytania dotyczące przekazywania klienta</span><span class="sxs-lookup"><span data-stu-id="fffa9-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="fffa9-117">Powiadomienia e-mail z aplikacji</span><span class="sxs-lookup"><span data-stu-id="fffa9-117">Email notifications from your application</span></span>

<span data-ttu-id="fffa9-118">Aby uzyskać więcej informacji, zobacz <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="fffa9-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="fffa9-119">Utwórz konto SendGrid</span><span class="sxs-lookup"><span data-stu-id="fffa9-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-the-javaxmail-libraries"></a><span data-ttu-id="fffa9-120">Porady: Użyj biblioteki javax.mail</span><span class="sxs-lookup"><span data-stu-id="fffa9-120">How to: Use the javax.mail libraries</span></span>
<span data-ttu-id="fffa9-121">Na przykład uzyskać bibliotek javax.mail z <http://www.oracle.com/technetwork/java/javamail> i zaimportuj je do kodu.</span><span class="sxs-lookup"><span data-stu-id="fffa9-121">Obtain the javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="fffa9-122">W wysokiego poziomu proces za pomocą biblioteki javax.mail do wysyłania wiadomości e-mail za pomocą protokołu SMTP jest wykonanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="fffa9-122">At a high-level, the process for using the javax.mail library to send email using SMTP is to do the following:</span></span>

1. <span data-ttu-id="fffa9-123">Określ wartości SMTP, w tym do serwera SMTP, który SendGrid jest smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="fffa9-123">Specify the SMTP values, including the SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

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

1. <span data-ttu-id="fffa9-124">Rozszerzanie *javax.mail.Authenticator* klasy w implementacji *getPasswordAuthentication* metody zwrócić SendGrid nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="fffa9-124">Extend the *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="fffa9-125">Tworzenia sesji uwierzytelnionych poczty e-mail za pośrednictwem *javax.mail.Session* obiektu.</span><span class="sxs-lookup"><span data-stu-id="fffa9-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="fffa9-126">Utwórz wiadomość i przypisać **do**, **z**, **podmiotu** i zawartości wartości.</span><span class="sxs-lookup"><span data-stu-id="fffa9-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="fffa9-127">Przedstawiono to w [jak: utworzyć wiadomości E-mail](#how-to-create-an-email) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fffa9-127">This is shown in the [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="fffa9-128">Wysłać komunikatu za pośrednictwem *javax.mail.Transport* obiektu.</span><span class="sxs-lookup"><span data-stu-id="fffa9-128">Send the message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="fffa9-129">Przedstawiono to w [jak: Wyślij wiadomość E-mail] [porady: wysyłanie wiadomości E-mail] sekcji.</span><span class="sxs-lookup"><span data-stu-id="fffa9-129">This is shown in the [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="fffa9-130">Porady: Tworzenie wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="fffa9-130">How to: Create an email</span></span>
<span data-ttu-id="fffa9-131">Poniżej przedstawiono sposób określania wartości dla wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="fffa9-131">The following shows how to specify values for an email.</span></span>

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

## <a name="how-to-send-an-email"></a><span data-ttu-id="fffa9-132">Porady: wysyłanie wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="fffa9-132">How to: Send an email</span></span>
<span data-ttu-id="fffa9-133">Poniżej przedstawiono sposób wysyłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="fffa9-133">The following shows how to send an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect the transport object.
    transport.connect();
    // Send the message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close the connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="fffa9-134">Porady: Dodawanie załącznika</span><span class="sxs-lookup"><span data-stu-id="fffa9-134">How to: Add an attachment</span></span>
<span data-ttu-id="fffa9-135">Poniższy kod przedstawia sposób dodawania załącznika.</span><span class="sxs-lookup"><span data-stu-id="fffa9-135">The following code shows you how to add an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify the local file to attach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses the local file name as the attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="fffa9-136">Porady: Użyj filtrów, aby włączyć stopki, śledzenia i analiza</span><span class="sxs-lookup"><span data-stu-id="fffa9-136">How to: Use filters to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="fffa9-137">SendGrid udostępnia funkcje dodatkowe poczty e-mail za pośrednictwem *filtry*.</span><span class="sxs-lookup"><span data-stu-id="fffa9-137">SendGrid provides additional email functionality through the use of *filters*.</span></span> <span data-ttu-id="fffa9-138">Są to ustawienia, które mogą zostać dodane do wiadomości e-mail, aby włączyć określonych funkcji, takich jak włączenie kliknij śledzenia, Google analytics, subskrypcji, śledzenia i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="fffa9-138">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="fffa9-139">Aby uzyskać pełną listę filtrów, zobacz [ustawienia filtru][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="fffa9-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="fffa9-140">Poniżej przedstawiono sposób wstawiania stopki filtr, który powoduje znajdujących się w dolnej części wiadomości e-mail wysyłane tekstu w formacie HTML.</span><span class="sxs-lookup"><span data-stu-id="fffa9-140">The following shows how to insert a footer filter that results in HTML text appearing at the bottom of the email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="fffa9-141">Innym przykładem filtr jest kliknij śledzenia.</span><span class="sxs-lookup"><span data-stu-id="fffa9-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="fffa9-142">Załóżmy, że tekst wiadomości e-mail zawiera hiperłącza, takie jak wymienione poniżej, i chcesz śledzić tempo kliknij:</span><span class="sxs-lookup"><span data-stu-id="fffa9-142">Let’s say that your email text contains a hyperlink, such as the following, and you want to track the click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is the body of the message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="fffa9-143">Aby włączyć kliknij śledzenia, należy użyć poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="fffa9-143">To enable the click tracking, use the following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="fffa9-144">Porady: Aktualizacja właściwości wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="fffa9-144">How to: Update email properties</span></span>
<span data-ttu-id="fffa9-145">Niektóre właściwości wiadomości e-mail może zostać zastąpiona przy użyciu  **ustawić*właściwości*** lub dołączonych za pomocą  **dodać*właściwości***.</span><span class="sxs-lookup"><span data-stu-id="fffa9-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="fffa9-146">Na przykład, aby określić **ReplyTo** adresów, należy użyć następującego:</span><span class="sxs-lookup"><span data-stu-id="fffa9-146">For example, to specify **ReplyTo** addresses, use the following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="fffa9-147">Aby dodać **DW** adresata, należy użyć następującego:</span><span class="sxs-lookup"><span data-stu-id="fffa9-147">To add a **Cc** recipient, use the following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="fffa9-148">Porady: Użyj dodatkowych usług SendGrid</span><span class="sxs-lookup"><span data-stu-id="fffa9-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="fffa9-149">SendGrid oferuje opartych na sieci web interfejsów API, które można wykorzystać dodatkowe funkcje włączenie w aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fffa9-149">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="fffa9-150">Aby uzyskać szczegółowe informacje, zobacz [dokumentacji interfejsu API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="fffa9-150">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="fffa9-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fffa9-151">Next steps</span></span>
<span data-ttu-id="fffa9-152">Teraz, kiedy znasz już podstawy usługi poczty E-mail SendGrid, skorzystaj z poniższych linków, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="fffa9-152">Now that you’ve learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="fffa9-153">Przykład przedstawiający we wdrożeniu Azure przy użyciu SendGrid: [sposób wysyłania poczty e-mail przy użyciu SendGrid za pomocą języka Java w wdrożenia usługi Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="fffa9-153">Sample that demonstrates using SendGrid in an Azure deployment: [How to send email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="fffa9-154">Zestawu SDK SendGrid Java: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="fffa9-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="fffa9-155">Dokumentacja interfejsu API SendGrid: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="fffa9-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="fffa9-156">Oferta specjalna SendGrid dla klientów platformy Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="fffa9-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
<span data-ttu-id="fffa9-157">[e-mail opartej na chmurze usługa]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="fffa9-157">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="fffa9-158">[dostarczania transakcyjnych wiadomości e-mail]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="fffa9-158">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
