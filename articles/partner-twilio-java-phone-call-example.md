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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="c4a12-103">Jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji Java na platformie Azure połączeń telefonicznych</span><span class="sxs-lookup"><span data-stu-id="c4a12-103">How tooMake a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="c4a12-104">Witaj poniższym przykładzie pokazano korzystania z usługi Twilio toomake wywołanie ze strony sieci web hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c4a12-104">hello following example shows you how you can use Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="c4a12-105">Wynikowa aplikacji Hello monitują użytkownika hello wartości rozmowy telefonicznej, pokazane na powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="c4a12-105">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Formularz wywołania platformy Azure przy użyciu usługi Twilio i Java][twilio_java]

<span data-ttu-id="c4a12-107">Będą potrzebne następujące hello toodo toouse hello kodu w tym temacie:</span><span class="sxs-lookup"><span data-stu-id="c4a12-107">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="c4a12-108">Uzyskać konta usługi Twilio i uwierzytelniania tokenu.</span><span class="sxs-lookup"><span data-stu-id="c4a12-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="c4a12-109">tooget wprowadzenie do usługi Twilio, ocenę cennik w [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="c4a12-109">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="c4a12-110">Możesz utworzyć konto w [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="c4a12-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="c4a12-111">Informacje hello udostępniane przez usługi Twilio interfejsu API, zobacz [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="c4a12-111">For information about hello API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="c4a12-112">Uzyskaj hello JAR usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="c4a12-112">Obtain hello Twilio JAR.</span></span> <span data-ttu-id="c4a12-113">W [https://github.com/twilio/twilio-java][twilio_java_github], możesz pobrać hello GitHub źródeł i tworzyć własne JAR lub pobrać wbudowanych JAR (z lub bez zależności).</span><span class="sxs-lookup"><span data-stu-id="c4a12-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="c4a12-114">Kod Hello w tym temacie została opracowana za pomocą hello wstępnie skompilowany JAR TwilioJava 3.3.8 z zależności.</span><span class="sxs-lookup"><span data-stu-id="c4a12-114">hello code in this topic was written using hello pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="c4a12-115">Dodaj tooyour JAR hello ścieżka kompilacji języka Java.</span><span class="sxs-lookup"><span data-stu-id="c4a12-115">Add hello JAR tooyour Java build path.</span></span>
4. <span data-ttu-id="c4a12-116">Jeśli używasz programu Eclipse toocreate tej aplikacji Java, obejmują hello usługi Twilio JAR w pliku wdrożenia aplikacji (plik WAR) za pomocą funkcji zestawu wdrożenia w środowisku Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c4a12-116">If you are using Eclipse toocreate this Java application, include hello Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="c4a12-117">Jeśli nie używasz Eclipse toocreate tej aplikacji Java, upewnij się, hello JAR usługi Twilio jest uwzględniona w obrębie hello tej samej roli Azure jako ścieżki Java toohello aplikacji i dodać klasy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4a12-117">If you are not using Eclipse toocreate this Java application, ensure hello Twilio JAR is included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>
5. <span data-ttu-id="c4a12-118">Upewnij się Twojego magazynu kluczy cacerts zawiera certyfikat urzędu certyfikacji Secure firmy Equifax hello z 67:CB:9 odcisk palca MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (serial numer jest 35:DE:F4:CF i odcisk palca hello SHA1 D2:32:09:AD:23:D hello 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="c4a12-118">Ensure your cacerts keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="c4a12-119">Jest to hello certyfikat urzędu certyfikacji dla hello [https://api.twilio.com] [ twilio_api_service] usługi, która jest wywoływana, gdy używasz interfejsów API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="c4a12-119">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="c4a12-120">Uzyskać informacji o dodawaniu tego urzędu certyfikacji certyfikatu tooyour JDK firmy cacert magazynu, zobacz [Dodawanie toohello certyfikatu z magazynu certyfikatów urzędu certyfikacji Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="c4a12-120">For information about adding this CA certificate tooyour JDK's cacert store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="c4a12-121">Ponadto znajomość hello informacji w [tworzenie hello Hello World aplikacji przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse][azure_java_eclipse_hello_world], lub z innych technik do hostowania aplikacji Java na platformie Azure, jeśli użytkownik nie są używane w środowisku Eclipse, zdecydowanie zaleca się.</span><span class="sxs-lookup"><span data-stu-id="c4a12-121">Additionally, familiarity with hello information at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="c4a12-122">Tworzenie formularza sieci web nawiązywania połączenia</span><span class="sxs-lookup"><span data-stu-id="c4a12-122">Create a web form for making a call</span></span>
<span data-ttu-id="c4a12-123">Witaj następującego kodu pokazuje, jak dane użytkownika tooretrieve wywołania formularza toocreate sieci web.</span><span class="sxs-lookup"><span data-stu-id="c4a12-123">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="c4a12-124">Dla celów tego przykładu nowy projekt dynamicznej sieci web o nazwie **TwilioCloud**, został utworzony i **callform.jsp** został dodany jako plik JSP.</span><span class="sxs-lookup"><span data-stu-id="c4a12-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

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

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="c4a12-125">Utwórz hello kodu toomake hello wywołania</span><span class="sxs-lookup"><span data-stu-id="c4a12-125">Create hello code toomake hello call</span></span>
<span data-ttu-id="c4a12-126">Witaj następujący kod, który jest wywoływany, gdy użytkownik hello kończy formularz hello wyświetlanych przez callform.jsp, tworzy wiadomości powitania wywołania i generuje hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="c4a12-126">hello following code, which is called when hello user completes hello form displayed by callform.jsp, creates hello call message and generates hello call.</span></span> <span data-ttu-id="c4a12-127">Do celów tego przykładu, nosi nazwę pliku JSP hello **makecall.jsp** i została dodana toohello **TwilioCloud** projektu.</span><span class="sxs-lookup"><span data-stu-id="c4a12-127">For purposes of this example, hello JSP file is named **makecall.jsp** and was added toohello **TwilioCloud** project.</span></span> <span data-ttu-id="c4a12-128">(Użyj swojego konta usługi Twilio i uwierzytelniania tokenu zamiast symbole zastępcze hello przypisane zbyt**accountSID** i **parametru authToken** hello kodu poniżej.)</span><span class="sxs-lookup"><span data-stu-id="c4a12-128">(Use your Twilio account and authentication token instead of hello placeholder values assigned too**accountSID** and **authToken** in hello code below.)</span></span>

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

<span data-ttu-id="c4a12-129">Ponadto toomaking hello wywołanie, makecall.jsp Wyświetla punktu końcowego usługi Twilio hello, wersja interfejsu API i stan wywołania hello.</span><span class="sxs-lookup"><span data-stu-id="c4a12-129">In addition toomaking hello call, makecall.jsp displays hello Twilio endpoint, API version, and hello call status.</span></span> <span data-ttu-id="c4a12-130">Przykładem jest powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="c4a12-130">An example is hello following screen shot:</span></span>

![Odpowiedź wywołania platformy Azure przy użyciu usługi Twilio i Java][twilio_java_response]

## <a name="run-hello-application"></a><span data-ttu-id="c4a12-132">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="c4a12-132">Run hello application</span></span>
<span data-ttu-id="c4a12-133">Poniżej są hello toorun ogólne kroki aplikacji; Szczegóły dla tych kroków można znaleźć w [tworzenie hello Hello World aplikacji przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="c4a12-133">Following are hello high-level steps toorun your application; details for these steps can be found at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="c4a12-134">Eksportuj toohello Twojego TwilioCloud WAR Azure **approot** folderu.</span><span class="sxs-lookup"><span data-stu-id="c4a12-134">Export your TwilioCloud WAR toohello Azure **approot** folder.</span></span> 
2. <span data-ttu-id="c4a12-135">Modyfikowanie **startup.cmd** toounzip Twojego WAR TwilioCloud.</span><span class="sxs-lookup"><span data-stu-id="c4a12-135">Modify **startup.cmd** toounzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="c4a12-136">Kompilowanie aplikacji hello emulatora obliczeń.</span><span class="sxs-lookup"><span data-stu-id="c4a12-136">Compile your application for hello compute emulator.</span></span>
4. <span data-ttu-id="c4a12-137">Uruchom wdrożenia w hello emulatora obliczeń.</span><span class="sxs-lookup"><span data-stu-id="c4a12-137">Start your deployment in hello compute emulator.</span></span>
5. <span data-ttu-id="c4a12-138">Otwórz przeglądarkę, a następnie uruchom **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="c4a12-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="c4a12-139">Wprowadź wartości w postaci hello, kliknij polecenie **wykonać to wywołanie**i wyświetlić wyniki hello w makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="c4a12-139">Enter values in hello form, click **Make this call**, and then see hello results in makecall.jsp.</span></span>

<span data-ttu-id="c4a12-140">Gdy wszystko jest gotowe toodeploy tooAzure, skompiluj ponownie chmury toohello wdrożenia, wdrażanie tooAzure i uruchom http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp w przeglądarce hello (Zastąp wartość dla *your_hosted_name*).</span><span class="sxs-lookup"><span data-stu-id="c4a12-140">When you are ready toodeploy tooAzure, recompile for deployment toohello cloud, deploy tooAzure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in hello browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4a12-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c4a12-141">Next steps</span></span>
<span data-ttu-id="c4a12-142">Ten kod został podany tooshow możesz podstawowych funkcji przy użyciu usługi Twilio w języku Java na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c4a12-142">This code was provided tooshow you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="c4a12-143">Przed wdrożeniem tooAzure w środowisku produkcyjnym, możesz tooadd więcej obsługi błędów lub innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="c4a12-143">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="c4a12-144">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c4a12-144">For example:</span></span>

* <span data-ttu-id="c4a12-145">Zamiast za pomocą formularza sieci web, możesz użyć obiektów blob magazynu Azure lub numery telefonów toostore bazy danych SQL i wywołać tekstu.</span><span class="sxs-lookup"><span data-stu-id="c4a12-145">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="c4a12-146">Aby dowiedzieć się, jak za pomocą obiektów blob magazynu Azure w języku Java, zobacz [jak tooUse hello usługi magazynu obiektów Blob w języku Java][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="c4a12-146">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="c4a12-147">Aby uzyskać informacje dotyczące korzystania z bazy danych SQL w języku Java, zobacz [przy użyciu bazy danych SQL w języku Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="c4a12-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="c4a12-148">Można użyć **RoleEnvironment.getConfigurationSettings** identyfikator konta usługi Twilio hello tooretrieve i uwierzytelniania token z danym wdrożeniu ustawień konfiguracji, zamiast kodować wartości hello makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="c4a12-148">You could use **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in makecall.jsp.</span></span> <span data-ttu-id="c4a12-149">Informacji o hello **RoleEnvironment** , zobacz [Using hello Biblioteka środowiska uruchomieniowego usługi Azure w JSP] [ azure_runtime_jsp] i dokumentacji pakietu środowiska uruchomieniowego usługi Azure hello [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="c4a12-149">For information about hello **RoleEnvironment** class, see [Using hello Azure Service Runtime Library in JSP][azure_runtime_jsp] and hello Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="c4a12-150">Kod makecall.jsp Hello przypisuje adres URL udostępniony do usługi Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **adres Url** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="c4a12-150">hello makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span></span> <span data-ttu-id="c4a12-151">Ten adres URL zawiera odpowiedzi usługi Twilio Markup Language (TwiML), który informuje usługi Twilio, jak wywołać tooproceed z hello.</span><span class="sxs-lookup"><span data-stu-id="c4a12-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="c4a12-152">Na przykład może zawierać hello TwiML, która jest zwracana  **&lt;powiedzieć&gt;**  czasownika, który powoduje tekst jest rozmowy toohello wywołania adresata.</span><span class="sxs-lookup"><span data-stu-id="c4a12-152">For example, hello TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="c4a12-153">Zamiast przy użyciu adresu URL dostarczony do usługi Twilio hello, można zbudować żądania własnych tooTwilio toorespond usługi; Aby uzyskać więcej informacji, zobacz [jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku Java][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="c4a12-153">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="c4a12-154">Więcej informacji na temat TwiML można znaleźć w folderze [http://www.twilio.com/docs/api/twiml][twiml]i więcej informacji na temat  **&lt;powiedzieć&gt;**  i inne usługi Twilio zlecenia można znaleźć w folderze [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="c4a12-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="c4a12-155">Przeczytaj wytyczne dotyczące zabezpieczeń usługi Twilio hello na [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="c4a12-155">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="c4a12-156">Aby uzyskać dodatkowe informacje na temat usługi Twilio, zobacz [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="c4a12-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="c4a12-157">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c4a12-157">See Also</span></span>
* <span data-ttu-id="c4a12-158">[Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku Java][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="c4a12-158">[How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="c4a12-159">[Dodawanie certyfikatu toohello magazynu certyfikatów urzędu certyfikacji Java][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="c4a12-159">[Adding a Certificate toohello Java CA Certificate Store][add_ca_cert]</span></span>

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
