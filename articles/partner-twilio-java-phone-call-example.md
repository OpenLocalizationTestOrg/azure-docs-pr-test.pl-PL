---
title: "tooMake aaaHow rozmowy telefonicznej z usługi Twilio (Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wywołać toomake telefonu ze strony sieci web w aplikacji Java na platformie Azure przy użyciu usługi Twilio."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a>Jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji Java na platformie Azure połączeń telefonicznych
Witaj poniższym przykładzie pokazano korzystania z usługi Twilio toomake wywołanie ze strony sieci web hostowanej na platformie Azure. Wynikowa aplikacji Hello monitują użytkownika hello wartości rozmowy telefonicznej, pokazane na powitania po zrzut ekranu.

![Formularz wywołania platformy Azure przy użyciu usługi Twilio i Java][twilio_java]

Będą potrzebne następujące hello toodo toouse hello kodu w tym temacie:

1. Uzyskać konta usługi Twilio i uwierzytelniania tokenu. tooget wprowadzenie do usługi Twilio, ocenę cennik w [http://www.twilio.com/pricing][twilio_pricing]. Możesz utworzyć konto w [https://www.twilio.com/try-twilio][try_twilio]. Informacje hello udostępniane przez usługi Twilio interfejsu API, zobacz [http://www.twilio.com/api][twilio_api].
2. Uzyskaj hello JAR usługi Twilio. W [https://github.com/twilio/twilio-java][twilio_java_github], możesz pobrać hello GitHub źródeł i tworzyć własne JAR lub pobrać wbudowanych JAR (z lub bez zależności).
   Kod Hello w tym temacie została opracowana za pomocą hello wstępnie skompilowany JAR TwilioJava 3.3.8 z zależności.
3. Dodaj tooyour JAR hello ścieżka kompilacji języka Java.
4. Jeśli używasz programu Eclipse toocreate tej aplikacji Java, obejmują hello usługi Twilio JAR w pliku wdrożenia aplikacji (plik WAR) za pomocą funkcji zestawu wdrożenia w środowisku Eclipse. Jeśli nie używasz Eclipse toocreate tej aplikacji Java, upewnij się, hello JAR usługi Twilio jest uwzględniona w obrębie hello tej samej roli Azure jako ścieżki Java toohello aplikacji i dodać klasy aplikacji.
5. Upewnij się Twojego magazynu kluczy cacerts zawiera certyfikat urzędu certyfikacji Secure firmy Equifax hello z 67:CB:9 odcisk palca MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (serial numer jest 35:DE:F4:CF i odcisk palca hello SHA1 D2:32:09:AD:23:D hello 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Jest to hello certyfikat urzędu certyfikacji dla hello [https://api.twilio.com] [ twilio_api_service] usługi, która jest wywoływana, gdy używasz interfejsów API usługi Twilio. Uzyskać informacji o dodawaniu tego urzędu certyfikacji certyfikatu tooyour JDK firmy cacert magazynu, zobacz [Dodawanie toohello certyfikatu z magazynu certyfikatów urzędu certyfikacji Java][add_ca_cert].

Ponadto znajomość hello informacji w [tworzenie hello Hello World aplikacji przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse][azure_java_eclipse_hello_world], lub z innych technik do hostowania aplikacji Java na platformie Azure, jeśli użytkownik nie są używane w środowisku Eclipse, zdecydowanie zaleca się.

## <a name="create-a-web-form-for-making-a-call"></a>Tworzenie formularza sieci web nawiązywania połączenia
Witaj następującego kodu pokazuje, jak dane użytkownika tooretrieve wywołania formularza toocreate sieci web. Dla celów tego przykładu nowy projekt dynamicznej sieci web o nazwie **TwilioCloud**, został utworzony i **callform.jsp** został dodany jako plik JSP.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toomake-hello-call"></a>Utwórz hello kodu toomake hello wywołania
Witaj następujący kod, który jest wywoływany, gdy użytkownik hello kończy formularz hello wyświetlanych przez callform.jsp, tworzy wiadomości powitania wywołania i generuje hello wywołania. Do celów tego przykładu, nosi nazwę pliku JSP hello **makecall.jsp** i została dodana toohello **TwilioCloud** projektu. (Użyj swojego konta usługi Twilio i uwierzytelniania tokenu zamiast symbole zastępcze hello przypisane zbyt**accountSID** i **parametru authToken** hello kodu poniżej.)

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

Ponadto toomaking hello wywołanie, makecall.jsp Wyświetla punktu końcowego usługi Twilio hello, wersja interfejsu API i stan wywołania hello. Przykładem jest powitania po zrzut ekranu:

![Odpowiedź wywołania platformy Azure przy użyciu usługi Twilio i Java][twilio_java_response]

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello
Poniżej są hello toorun ogólne kroki aplikacji; Szczegóły dla tych kroków można znaleźć w [tworzenie hello Hello World aplikacji przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse][azure_java_eclipse_hello_world].

1. Eksportuj toohello Twojego TwilioCloud WAR Azure **approot** folderu. 
2. Modyfikowanie **startup.cmd** toounzip Twojego WAR TwilioCloud.
3. Kompilowanie aplikacji hello emulatora obliczeń.
4. Uruchom wdrożenia w hello emulatora obliczeń.
5. Otwórz przeglądarkę, a następnie uruchom **http://localhost:8080/TwilioCloud/callform.jsp**.
6. Wprowadź wartości w postaci hello, kliknij polecenie **wykonać to wywołanie**i wyświetlić wyniki hello w makecall.jsp.

Gdy wszystko jest gotowe toodeploy tooAzure, skompiluj ponownie chmury toohello wdrożenia, wdrażanie tooAzure i uruchom http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp w przeglądarce hello (Zastąp wartość dla *your_hosted_name*).

## <a name="next-steps"></a>Następne kroki
Ten kod został podany tooshow możesz podstawowych funkcji przy użyciu usługi Twilio w języku Java na platformie Azure. Przed wdrożeniem tooAzure w środowisku produkcyjnym, możesz tooadd więcej obsługi błędów lub innych funkcji. Na przykład:

* Zamiast za pomocą formularza sieci web, możesz użyć obiektów blob magazynu Azure lub numery telefonów toostore bazy danych SQL i wywołać tekstu. Aby dowiedzieć się, jak za pomocą obiektów blob magazynu Azure w języku Java, zobacz [jak tooUse hello usługi magazynu obiektów Blob w języku Java][howto_blob_storage_java]. Aby uzyskać informacje dotyczące korzystania z bazy danych SQL w języku Java, zobacz [przy użyciu bazy danych SQL w języku Java][howto_sql_azure_java].
* Można użyć **RoleEnvironment.getConfigurationSettings** identyfikator konta usługi Twilio hello tooretrieve i uwierzytelniania token z danym wdrożeniu ustawień konfiguracji, zamiast kodować wartości hello makecall.jsp. Informacji o hello **RoleEnvironment** , zobacz [Using hello Biblioteka środowiska uruchomieniowego usługi Azure w JSP] [ azure_runtime_jsp] i dokumentacji pakietu środowiska uruchomieniowego usługi Azure hello [http://dl.windowsazure.com/javadoc][azure_javadoc].
* Kod makecall.jsp Hello przypisuje adres URL udostępniony do usługi Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **adres Url** zmiennej. Ten adres URL zawiera odpowiedzi usługi Twilio Markup Language (TwiML), który informuje usługi Twilio, jak wywołać tooproceed z hello. Na przykład może zawierać hello TwiML, która jest zwracana  **&lt;powiedzieć&gt;**  czasownika, który powoduje tekst jest rozmowy toohello wywołania adresata. Zamiast przy użyciu adresu URL dostarczony do usługi Twilio hello, można zbudować żądania własnych tooTwilio toorespond usługi; Aby uzyskać więcej informacji, zobacz [jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku Java][howto_twilio_voice_sms_java]. Więcej informacji na temat TwiML można znaleźć w folderze [http://www.twilio.com/docs/api/twiml][twiml]i więcej informacji na temat  **&lt;powiedzieć&gt;**  i inne usługi Twilio zlecenia można znaleźć w folderze [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Przeczytaj wytyczne dotyczące zabezpieczeń usługi Twilio hello na [https://www.twilio.com/docs/security][twilio_docs_security].

Aby uzyskać dodatkowe informacje na temat usługi Twilio, zobacz [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Zobacz też
* [Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku Java][howto_twilio_voice_sms_java]
* [Dodawanie certyfikatu toohello magazynu certyfikatów urzędu certyfikacji Java][add_ca_cert]

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
