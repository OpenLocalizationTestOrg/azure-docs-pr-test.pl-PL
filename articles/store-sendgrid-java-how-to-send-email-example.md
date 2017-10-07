---
title: aaastore-sendgrid-Java-How-to-send-email-example
description: "W jaki sposób toosend poczty e-mail przy użyciu SendGrid za pomocą języka Java we wdrożeniu usługi Azure"
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a>Jak tooSend SendGrid za pomocą poczty E-mail za pomocą języka Java we wdrożeniu usługi Azure
Witaj poniższym przykładzie pokazano sposób korzystania z wiadomości e-mail toosend SendGrid ze strony sieci web hostowanej na platformie Azure. wynikowej aplikacji Hello monitują użytkownika hello wartości poczty e-mail, jak pokazano w powitania po zrzut ekranu.

![Formularz poczty e-mail][emailform]

Hello wynikowa poczty e-mail będzie wyglądać podobnie toohello po zrzut ekranu.

![Wiadomości e-mail][emailsent]

Będą potrzebne następujące hello toodo toouse hello kodu w tym temacie:

1. Uzyskaj hello słoików javax.mail, na przykład z <http://www.oracle.com/technetwork/java/javamail/index.html>.
2. Dodaj tooyour słoików hello ścieżka kompilacji języka Java.
3. Jeśli używasz programu Eclipse toocreate tej aplikacji Java, hello SendGrid biblioteki można uwzględnić w pliku wdrożenia aplikacji (plik WAR) za pomocą funkcji zestawu wdrożenia w środowisku Eclipse. Jeśli nie używasz Eclipse toocreate tej aplikacji Java, upewnij się, bibliotek hello znajdują się w obrębie hello tej samej roli Azure jako ścieżki Java toohello aplikacji i dodać klasy aplikacji.

Musi również mieć własne SendGrid nazwy użytkownika i hasła, toobe toosend stanie hello w wiadomości e-mail. tooget wprowadzenie SendGrid, zobacz [jak toosend poczty e-mail przy użyciu SendGrid za pomocą języka Java](store-sendgrid-java-how-to-send-email.md).

Ponadto znajomość hello informacji w [tworzenia aplikacji Hello World na platformie Azure w programie Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), lub z innych technik do hostowania aplikacji Java na platformie Azure, jeśli nie używasz programu Eclipse jest zdecydowanie zalecane.

## <a name="create-a-web-form-for-sending-email"></a>Tworzenie formularza sieci web do wysyłania wiadomości e-mail
Witaj następującego kodu pokazuje, jak dane użytkownika tooretrieve do wysyłania wiadomości e-mail formularza toocreate sieci web. Dla celów tej zawartości, nosi nazwę pliku JSP hello **emailform.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a>Utworzyć hello kodu toosend hello w wiadomości e-mail
Witaj następujący kod, który jest wywoływana po wypełnieniu formularza hello w emailform.jsp, tworzy hello wiadomości e-mail i wysyła je. Dla celów tej zawartości, nosi nazwę pliku JSP hello **sendemail.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

Ponadto toosending hello poczty e-mail, emailform.jsp zawiera wynik dla użytkownika hello; Przykładem jest powitania po zrzut ekranu:

![Wysyłanie poczty wyników][emailresult]

## <a name="next-steps"></a>Następne kroki
Wdrażanie emulatora obliczeń toohello Twojej aplikacji i w przeglądarce, uruchom emailform.jsp, wprowadź wartości w postaci hello, kliknij przycisk **wysłać tę wiadomość e-mail**, a następnie sprawdź wyniki w sendemail.jsp.

Ten kod został podany tooshow należy jak toouse SendGrid w języku Java na platformie Azure. Przed wdrożeniem tooAzure w środowisku produkcyjnym, możesz tooadd więcej obsługi błędów lub innych funkcji. Na przykład: 

* Można użyć obiektów blob magazynu Azure lub adresy e-mail toostore bazy danych SQL i wiadomości e-mail zamiast za pomocą formularza sieci web. Aby dowiedzieć się, jak za pomocą obiektów blob magazynu Azure w języku Java, zobacz [jak tooUse hello usługi magazynu obiektów Blob w języku Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/). Aby uzyskać informacje dotyczące korzystania z bazy danych SQL w języku Java, zobacz [przy użyciu bazy danych SQL w języku Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).
* Można użyć `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid użytkownika i hasło w danym wdrożeniu ustawień konfiguracji, zamiast hello tooretrieve formularza sieci web tych wartości. Informacji o hello `RoleEnvironment` , zobacz [Using hello Biblioteka środowiska uruchomieniowego usługi Azure w JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) i dokumentacji pakietu środowiska uruchomieniowego usługi Azure hello <http://dl.windowsazure.com/javadoc>.
* Aby uzyskać więcej informacji o używaniu SendGrid w języku Java, zobacz [jak toosend poczty e-mail przy użyciu SendGrid za pomocą języka Java](store-sendgrid-java-how-to-send-email.md).

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
