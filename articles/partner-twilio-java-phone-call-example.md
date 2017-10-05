---
title: "Porady: tworzenie rozmowy telefonicznej z usługi Twilio (Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak nawiązać połączenie telefoniczne ze strony sieci web w aplikacji Java na platformie Azure przy użyciu usługi Twilio."
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
ms.openlocfilehash: 04ecb80a2a9e15b549b47138caf71c7e64bda500
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="b10e2-103">Porady: tworzenie rozmowę telefoniczną w aplikacji Java na platformie Azure przy użyciu usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="b10e2-103">How to Make a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="b10e2-104">Poniższy przykład pokazuje, jak można użyć usługi Twilio, aby nawiązać połączenie ze strony sieci web hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b10e2-104">The following example shows you how you can use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="b10e2-105">Wynikowa aplikacja pojawi się monit dla wartości rozmowy telefonicznej, jak pokazano na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="b10e2-105">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Formularz wywołania platformy Azure przy użyciu usługi Twilio i Java][twilio_java]

<span data-ttu-id="b10e2-107">Należy wykonać następujące czynności, aby użyć kodu w tym temacie:</span><span class="sxs-lookup"><span data-stu-id="b10e2-107">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="b10e2-108">Uzyskać konta usługi Twilio i uwierzytelniania tokenu.</span><span class="sxs-lookup"><span data-stu-id="b10e2-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="b10e2-109">Aby zacząć korzystać z usługi Twilio, ocenę cennik w [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="b10e2-109">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="b10e2-110">Możesz utworzyć konto w [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="b10e2-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="b10e2-111">Aby uzyskać informacje o interfejsie API dostarczonych przez usługi Twilio, zobacz [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="b10e2-111">For information about the API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="b10e2-112">Uzyskaj usługi Twilio JAR.</span><span class="sxs-lookup"><span data-stu-id="b10e2-112">Obtain the Twilio JAR.</span></span> <span data-ttu-id="b10e2-113">W [https://github.com/twilio/twilio-java][twilio_java_github], możesz pobrać źródeł GitHub i tworzyć własne JAR lub pobrać wbudowanych JAR (z lub bez zależności).</span><span class="sxs-lookup"><span data-stu-id="b10e2-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="b10e2-114">Kod w tym temacie została opracowana za pomocą wbudowanych JAR TwilioJava 3.3.8 z zależności.</span><span class="sxs-lookup"><span data-stu-id="b10e2-114">The code in this topic was written using the pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="b10e2-115">Dodaj JAR do ścieżki kompilacji języka Java.</span><span class="sxs-lookup"><span data-stu-id="b10e2-115">Add the JAR to your Java build path.</span></span>
4. <span data-ttu-id="b10e2-116">Jeśli używasz programu Eclipse do tworzenia aplikacji w języku Java, w pliku wdrożenia aplikacji (plik WAR) za pomocą funkcji zestawu wdrożenia w środowisku Eclipse należy umieścić JAR usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="b10e2-116">If you are using Eclipse to create this Java application, include the Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="b10e2-117">Jeśli nie używasz programu Eclipse do tworzenia aplikacji w języku Java, upewnij się, JAR usługi Twilio jest uwzględniony w obrębie tego samego elementu role Azure jako aplikacji w języku Java i dodawany do ścieżki klasy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b10e2-117">If you are not using Eclipse to create this Java application, ensure the Twilio JAR is included within the same Azure role as your Java application, and added to the class path of your application.</span></span>
5. <span data-ttu-id="b10e2-118">Upewnij się Twojego magazynu kluczy cacerts zawiera certyfikat urzędu certyfikacji Secure firmy Equifax z 67:CB:9 odcisk palca MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (numer seryjny jest 35:DE:F4:CF i odcisk palca SHA1 D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="b10e2-118">Ensure your cacerts keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="b10e2-119">Jest to certyfikat urzędu certyfikacji dla [https://api.twilio.com] [ twilio_api_service] usługi, która jest wywoływana, gdy używasz interfejsów API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="b10e2-119">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="b10e2-120">Informacje o dodawaniu tego certyfikatu urzędu certyfikacji do magazynu cacert Twojego JDK, zobacz [Dodawanie certyfikatu do magazynu certyfikatów urzędu certyfikacji Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="b10e2-120">For information about adding this CA certificate to your JDK's cacert store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="b10e2-121">Ponadto znajomość informacji w [utworzenie Hello World aplikacji przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse][azure_java_eclipse_hello_world], lub z innych technik do hostowania aplikacji Java na platformie Azure, jeśli nie używasz programu Eclipse jest zdecydowanie zalecane.</span><span class="sxs-lookup"><span data-stu-id="b10e2-121">Additionally, familiarity with the information at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="b10e2-122">Tworzenie formularza sieci web nawiązywania połączenia</span><span class="sxs-lookup"><span data-stu-id="b10e2-122">Create a web form for making a call</span></span>
<span data-ttu-id="b10e2-123">Poniższy kod przedstawia sposób tworzenia formularzy sieci web do pobierania danych użytkownika do nawiązywania połączenia.</span><span class="sxs-lookup"><span data-stu-id="b10e2-123">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="b10e2-124">Dla celów tego przykładu nowy projekt dynamicznej sieci web o nazwie **TwilioCloud**, został utworzony i **callform.jsp** został dodany jako plik JSP.</span><span class="sxs-lookup"><span data-stu-id="b10e2-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

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
           <td><input type="text" size=400 name="callText" value="Hello. This is the call text. Good bye." />
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

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="b10e2-125">Utwórz kod, aby wykonać wywołanie</span><span class="sxs-lookup"><span data-stu-id="b10e2-125">Create the code to make the call</span></span>
<span data-ttu-id="b10e2-126">Następujący kod, który jest wywoływany, gdy użytkownik zamyka formularz, wyświetlane przez callform.jsp, tworzy komunikat wywołania i generuje wywołania.</span><span class="sxs-lookup"><span data-stu-id="b10e2-126">The following code, which is called when the user completes the form displayed by callform.jsp, creates the call message and generates the call.</span></span> <span data-ttu-id="b10e2-127">Do celów tego przykładu, nosi nazwę pliku JSP **makecall.jsp** i została dodana do **TwilioCloud** projektu.</span><span class="sxs-lookup"><span data-stu-id="b10e2-127">For purposes of this example, the JSP file is named **makecall.jsp** and was added to the **TwilioCloud** project.</span></span> <span data-ttu-id="b10e2-128">(Użyj swojego konta usługi Twilio i uwierzytelniania tokenu zamiast wartości symbolu zastępczego, przypisane do **accountSID** i **parametru authToken** w poniższym kodzie.)</span><span class="sxs-lookup"><span data-stu-id="b10e2-128">(Use your Twilio account and authentication token instead of the placeholder values assigned to **accountSID** and **authToken** in the code below.)</span></span>

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
         // of the placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of the Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve the account, used later to retrieve the CallFactory.
         Account account = client.getAccount();

         // Display the client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display the API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve the values entered by the user.
         String callTo = request.getParameter("callTo");  
         // The Outgoing Caller ID, used for the From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in the user's text with '%20', 
         // to make the text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using the Twilio message and the user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display the message URL.
         out.println("<p>");
         out.println("The URL is " + Url);
         out.println("</p>");

         // Place the call From, To and URL values into a hash map. 
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

<span data-ttu-id="b10e2-129">Oprócz wywołania, makecall.jsp Wyświetla punktu końcowego usługi Twilio, wersja interfejsu API i stan połączenia.</span><span class="sxs-lookup"><span data-stu-id="b10e2-129">In addition to making the call, makecall.jsp displays the Twilio endpoint, API version, and the call status.</span></span> <span data-ttu-id="b10e2-130">Przykładem jest na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="b10e2-130">An example is the following screen shot:</span></span>

![Odpowiedź wywołania platformy Azure przy użyciu usługi Twilio i Java][twilio_java_response]

## <a name="run-the-application"></a><span data-ttu-id="b10e2-132">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b10e2-132">Run the application</span></span>
<span data-ttu-id="b10e2-133">Poniżej przedstawiono ogólne kroki do uruchamiania aplikacji; Szczegóły dla tych kroków można znaleźć w [utworzenie Hello World aplikacji przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="b10e2-133">Following are the high-level steps to run your application; details for these steps can be found at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="b10e2-134">Eksportowanie z WAR TwilioCloud do platformy Azure **approot** folderu.</span><span class="sxs-lookup"><span data-stu-id="b10e2-134">Export your TwilioCloud WAR to the Azure **approot** folder.</span></span> 
2. <span data-ttu-id="b10e2-135">Modyfikowanie **startup.cmd** rozpakować z WAR TwilioCloud.</span><span class="sxs-lookup"><span data-stu-id="b10e2-135">Modify **startup.cmd** to unzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="b10e2-136">Skompiluj aplikację w emulatorze obliczeń.</span><span class="sxs-lookup"><span data-stu-id="b10e2-136">Compile your application for the compute emulator.</span></span>
4. <span data-ttu-id="b10e2-137">Uruchomić wdrożenia w emulatorze obliczeń.</span><span class="sxs-lookup"><span data-stu-id="b10e2-137">Start your deployment in the compute emulator.</span></span>
5. <span data-ttu-id="b10e2-138">Otwórz przeglądarkę, a następnie uruchom **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="b10e2-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="b10e2-139">Wprowadź wartości w formularzu, kliknij polecenie **wykonać to wywołanie**i wyświetlić wyniki w makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="b10e2-139">Enter values in the form, click **Make this call**, and then see the results in makecall.jsp.</span></span>

<span data-ttu-id="b10e2-140">Gdy wszystko będzie gotowe do wdrożenia na platformie Azure, skompiluj ponownie do wdrożenia w chmurze, wdrażanie na platformie Azure, i uruchom http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp w przeglądarce (Zastąp wartość dla *your_hosted_name*).</span><span class="sxs-lookup"><span data-stu-id="b10e2-140">When you are ready to deploy to Azure, recompile for deployment to the cloud, deploy to Azure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in the browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b10e2-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b10e2-141">Next steps</span></span>
<span data-ttu-id="b10e2-142">Ten kod został podany pokazanie podstawowych funkcji przy użyciu usługi Twilio w języku Java na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b10e2-142">This code was provided to show you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="b10e2-143">Przed wdrożeniem na platformie Azure w środowisku produkcyjnym, możesz dodać więcej obsługi błędów lub innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="b10e2-143">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="b10e2-144">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b10e2-144">For example:</span></span>

* <span data-ttu-id="b10e2-145">Zamiast za pomocą formularza sieci web, można użyć obiektów blob magazynu Azure lub bazy danych SQL do przechowywania numerów telefonów i wywołać tekstu.</span><span class="sxs-lookup"><span data-stu-id="b10e2-145">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="b10e2-146">Aby dowiedzieć się, jak za pomocą obiektów blob magazynu Azure w języku Java, zobacz [jak używać usługi magazynu obiektów Blob w języku Java][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="b10e2-146">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="b10e2-147">Aby uzyskać informacje dotyczące korzystania z bazy danych SQL w języku Java, zobacz [przy użyciu bazy danych SQL w języku Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="b10e2-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="b10e2-148">Można użyć **RoleEnvironment.getConfigurationSettings** można pobrać usługi Twilio Identyfikatora konta oraz uwierzytelniania token z danym wdrożeniu ustawień konfiguracji, zamiast kodować wartości makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="b10e2-148">You could use **RoleEnvironment.getConfigurationSettings** to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in makecall.jsp.</span></span> <span data-ttu-id="b10e2-149">Informacje o **RoleEnvironment** , zobacz [za pomocą biblioteki środowiska uruchomieniowego usługi Azure w JSP] [ azure_runtime_jsp] i dokumentacji pakietu środowiska uruchomieniowego usługi Azure w [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="b10e2-149">For information about the **RoleEnvironment** class, see [Using the Azure Service Runtime Library in JSP][azure_runtime_jsp] and the Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="b10e2-150">Kod makecall.jsp przypisuje adres URL udostępniony do usługi Twilio, [http://twimlets.com/message][twimlet_message_url], do **adres Url** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="b10e2-150">The makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], to the **Url** variable.</span></span> <span data-ttu-id="b10e2-151">Ten adres URL zawiera odpowiedzi usługi Twilio Markup Language (TwiML), który informuje usługi Twilio sposób postępowania z wywołaniem.</span><span class="sxs-lookup"><span data-stu-id="b10e2-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="b10e2-152">Na przykład może zawierać TwiML, która jest zwracana  **&lt;powiedzieć&gt;**  zlecenia, który daje w tekście jest używany do adresata wywołania.</span><span class="sxs-lookup"><span data-stu-id="b10e2-152">For example, the TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="b10e2-153">Zamiast używać adresu URL dostarczony do usługi Twilio, można zbudować usługi na odpowiedź na żądanie dla usługi Twilio; Aby uzyskać więcej informacji, zobacz [sposobu użycia usługi Twilio, głosowe i możliwości programu SMS w języku Java][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="b10e2-153">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="b10e2-154">Więcej informacji na temat TwiML można znaleźć w folderze [http://www.twilio.com/docs/api/twiml][twiml]i więcej informacji na temat  **&lt;powiedzieć&gt;**  i inne usługi Twilio zlecenia można znaleźć w folderze [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="b10e2-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="b10e2-155">Zapoznaj się ze wskazówkami zabezpieczeń usługi Twilio w [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="b10e2-155">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="b10e2-156">Aby uzyskać dodatkowe informacje na temat usługi Twilio, zobacz [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="b10e2-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="b10e2-157">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b10e2-157">See Also</span></span>
* <span data-ttu-id="b10e2-158">[Jak używać usługi Twilio głosowe i możliwości programu SMS w języku Java][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="b10e2-158">[How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="b10e2-159">[Dodawanie certyfikatu do magazynu certyfikatów urzędu certyfikacji Java][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="b10e2-159">[Adding a Certificate to the Java CA Certificate Store][add_ca_cert]</span></span>

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
