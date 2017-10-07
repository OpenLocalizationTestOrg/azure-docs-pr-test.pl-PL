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
# <a name="how-toosend-email-using-sendgrid-from-java"></a>Jak tooSend SendGrid za pomocą poczty E-mail za pomocą języka Java
W tym przewodniku pokazano, jak tooperform typowych zadań programowania SendGrid poczty e-mail usługi na platformie Azure. Witaj przykłady są napisane w języku Java. Witaj omówione scenariusze obejmują **konstruowania e-mail**, **wysyłania wiadomości e-mail**, **dodawanie załączników**, **za pomocą filtrów**i **aktualizowanie właściwości**. Aby uzyskać więcej informacji na SendGrid i wysyłania wiadomości e-mail, zobacz hello [następne kroki](#next-steps) sekcji.

## <a name="what-is-hello-sendgrid-email-service"></a>Co to jest hello SendGrid usługa poczty E-mail?
Jest SendGrid [e-mail opartej na chmurze usługa] zapewnia niezawodne [dostarczania transakcyjnych wiadomości e-mail], skalowalności i analiz w czasie rzeczywistym oraz elastyczne interfejsów API, które umożliwiają łatwe niestandardowej integracji. Typowe scenariusze użycia SendGrid obejmują:

* Nie są automatycznie wysyłane potwierdzenia toocustomers
* Administrowanie dystrybucji wymieniono wysyłania klientów miesięczne e ulotki i oferty specjalne
* Zbieranie metryk w czasie rzeczywistym dla zablokowanych poczty e-mail i czasu odpowiedzi klienta
* Generowanie raportów toohelp trendów
* Zapytania dotyczące przekazywania klienta
* Powiadomienia e-mail z aplikacji

Aby uzyskać więcej informacji, zobacz <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>Utwórz konto SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>Porady: Użyj hello javax.mail biblioteki
Uzyskaj hello javax.mail biblioteki, na przykład z <http://www.oracle.com/technetwork/java/javamail> i zaimportuj je do kodu. Na ogólne hello proces hello javax.mail biblioteki toosend e-mail za pomocą protokołu SMTP jest toodo hello następujące:

1. Określ wartości SMTP hello, w tym powitania serwera SMTP, który SendGrid jest smtp.sendgrid.net.

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

1. Rozszerzanie hello *javax.mail.Authenticator* klasy w implementacji *getPasswordAuthentication* metody zwrócić SendGrid nazwę użytkownika i hasło.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Tworzenia sesji uwierzytelnionych poczty e-mail za pośrednictwem *javax.mail.Session* obiektu.  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. Utwórz wiadomość i przypisać **do**, **z**, **podmiotu** i zawartości wartości. Przedstawiono to w hello [jak: utworzyć wiadomości E-mail](#how-to-create-an-email) sekcji.
4. Wyślij wiadomość hello za pośrednictwem *javax.mail.Transport* obiektu. Przedstawiono to w hello [jak: Wyślij wiadomość E-mail] [porady: wysyłanie wiadomości E-mail] sekcji.

## <a name="how-to-create-an-email"></a>Porady: Tworzenie wiadomości e-mail
Witaj poniżej pokazano, jak toospecify wartości dla wiadomości e-mail.

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

## <a name="how-to-send-an-email"></a>Porady: wysyłanie wiadomości e-mail
Witaj, po pokazuje, jak toosend wiadomości e-mail.

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Porady: Dodawanie załącznika
Witaj poniższy kod pokazuje sposób tooadd załącznika.

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Porady: użycie filtruje stopki tooenable, śledzenia i analiza
SendGrid udostępnia funkcje dodatkowe poczty e-mail przy użyciu hello *filtry*. Są to ustawienia, które można dodać tooan wiadomości e-mail, aby włączyć określonych funkcji, np. włączenie kliknij śledzenia, Google analytics, subskrypcji śledzenia, i tak dalej. Aby uzyskać pełną listę filtrów, zobacz [ustawienia filtru][Filter Settings].

* Witaj poniżej pokazano, jak tooinsert stopkę filtrowania, którego wynikiem tekst HTML znajdujący się u dołu hello hello wiadomości e-mail wysyłane.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Innym przykładem filtr jest kliknij śledzenia. Załóżmy, że tekst wiadomości e-mail zawiera hiperłącza, takie jak hello poniżej, a ma tootrack powitania kliknij szybkość:

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* tooenable powitania kliknij śledzenia hello Użyj następującego kodu:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Porady: Aktualizacja właściwości wiadomości e-mail
Niektóre właściwości wiadomości e-mail może zostać zastąpiona przy użyciu  **ustawić*właściwości*** lub dołączonych za pomocą  **dodać*właściwości***.

Na przykład toospecify **ReplyTo** adresów, użyj następujących hello:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd **DW** adresatów, użyj hello poniżej:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Porady: Użyj dodatkowych usług SendGrid
SendGrid oferuje API sieci web z aplikacji platformy Azure można dodatkowe funkcje SendGrid tooleverage. Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello hello usługi SendGrid wiadomości E-mail, wykonaj te więcej toolearn łącza.

* Przykład przedstawiający we wdrożeniu Azure przy użyciu SendGrid: [jak toosend poczty e-mail przy użyciu SendGrid za pomocą języka Java w wdrożenia usługi Azure](store-sendgrid-java-how-to-send-email-example.md)
* Zestawu SDK SendGrid Java: <https://sendgrid.com/docs/Code_Examples/java.html>
* Dokumentacja interfejsu API SendGrid: <https://sendgrid.com/docs/API_Reference/index.html>
* Oferta specjalna SendGrid dla klientów platformy Azure: <https://sendgrid.com/windowsazure.html>

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
