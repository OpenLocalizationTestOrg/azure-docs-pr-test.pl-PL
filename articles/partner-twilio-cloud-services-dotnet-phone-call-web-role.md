---
title: "Porady: tworzenie rozmowy telefonicznej z usługi Twilio (.NET) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wykonać połączenie telefoniczne i wysłać wiadomość SMS z usługi interfejsu API usługi Twilio na platformie Azure. Przykłady kodu napisane w programie .NET."
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 0899a49cbfda775017dab7fc6d8963bbeb86d74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="781cd-104">Jak nawiązać połączenie telefoniczne z rolą sieci web na platformie Azure przy użyciu usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="781cd-104">How to make a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="781cd-105">W tym przewodniku pokazano, jak używać usługi Twilio, aby nawiązać połączenie ze strony sieci web hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="781cd-105">This guide demonstrates how to use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="781cd-106">Wynikowa aplikacji monituje użytkownika o nawiązać połączenie za pomocą podanej liczbie i wiadomości, jak pokazano na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="781cd-106">The resulting application prompts the user to make a call with the given number and message, as shown in the following screenshot.</span></span>

![Formularz wywołania platformy Azure przy użyciu usługi Twilio i platformy ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="781cd-108"><a name="twilio-prereqs"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="781cd-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="781cd-109">Należy wykonać następujące czynności, aby użyć kodu w tym temacie:</span><span class="sxs-lookup"><span data-stu-id="781cd-109">You will need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="781cd-110">Uzyskać konta usługi Twilio i uwierzytelniania tokenu z [usługi Twilio Console][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="781cd-110">Acquire a Twilio account and authentication token from the [Twilio Console][twilio_console].</span></span> <span data-ttu-id="781cd-111">Aby zacząć korzystać z usługi Twilio, zarejestruj się w [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="781cd-111">To get started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="781cd-112">Będziesz w stanie ocenić cennik w [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="781cd-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="781cd-113">Aby uzyskać informacje o interfejsie API dostarczonych przez usługi Twilio, zobacz [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="781cd-113">For information about the API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="781cd-114">Dodaj *biblioteki .NET usługi Twilio* do roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="781cd-114">Add the *Twilio .NET libary* to your web role.</span></span> <span data-ttu-id="781cd-115">Zobacz **do dodania do projektu roli sieci web biblioteki usługi Twilio**w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="781cd-115">See **To add the Twilio libraries to your web role project**, later in this topic.</span></span>

<span data-ttu-id="781cd-116">Należy się zapoznać z tworzeniem podstawowego [roli sieci Web na platformie Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="781cd-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="781cd-117"><a name="howtocreateform"></a>Porady: Tworzenie formularza sieci web nawiązywania połączenia</span><span class="sxs-lookup"><span data-stu-id="781cd-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="781cd-118"><a id="use_nuget"></a>Aby dodać biblioteki usługi Twilio do projektu roli sieci web:</span><span class="sxs-lookup"><span data-stu-id="781cd-118"><a id="use_nuget"></a>To add the Twilio libraries to your web role project:</span></span>

1. <span data-ttu-id="781cd-119">Otwórz rozwiązanie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="781cd-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="781cd-120">Kliknij prawym przyciskiem myszy **odwołania**.</span><span class="sxs-lookup"><span data-stu-id="781cd-120">Right-click **References**.</span></span>
3. <span data-ttu-id="781cd-121">Kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="781cd-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="781cd-122">Kliknij przycisk **Online**.</span><span class="sxs-lookup"><span data-stu-id="781cd-122">Click **Online**.</span></span>
5. <span data-ttu-id="781cd-123">W polu wyszukiwania online, wpisz *usługi twilio*.</span><span class="sxs-lookup"><span data-stu-id="781cd-123">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="781cd-124">Kliknij przycisk **zainstalować** w pakiecie usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="781cd-124">Click **Install** on the Twilio package.</span></span>

<span data-ttu-id="781cd-125">Poniższy kod przedstawia sposób tworzenia formularzy sieci web do pobierania danych użytkownika do nawiązywania połączenia.</span><span class="sxs-lookup"><span data-stu-id="781cd-125">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="781cd-126">W tym przykładzie roli sieci Web programu ASP.NET o nazwie **TwilioCloud** jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="781cd-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <span data-ttu-id="781cd-127"><a id="howtocreatecode"></a>Porady: tworzenie kodu do wywoływania</span><span class="sxs-lookup"><span data-stu-id="781cd-127"><a id="howtocreatecode"></a>How to: Create the code to make the call</span></span>
<span data-ttu-id="781cd-128">Następujący kod, który jest wywoływany, gdy użytkownik zamyka formularz, tworzy komunikat wywołania i generuje wywołania.</span><span class="sxs-lookup"><span data-stu-id="781cd-128">The following code, which is called when the user completes the form, creates the call message and generates the call.</span></span> <span data-ttu-id="781cd-129">W tym przykładzie kodu uruchamianego w program obsługi zdarzeń przycisk w formularzu.</span><span class="sxs-lookup"><span data-stu-id="781cd-129">In this example, the code is run in the onclick event handler of the button on the form.</span></span> <span data-ttu-id="781cd-130">(Użyj swojego konta usługi Twilio i uwierzytelniania tokenu zamiast wartości symbolu zastępczego, przypisane do `accountSID` i `authToken` w poniższym kodzie.)</span><span class="sxs-lookup"><span data-stu-id="781cd-130">(Use your Twilio account and authentication token instead of the placeholder values assigned to `accountSID` and `authToken` in the code below.)</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // the placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of the Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve the account, used later to retrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve the values entered by the user.
                var to = PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using the Twilio message and the user-entered
                // text. You must replace spaces in the user's text with '%20'
                // to make the text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display the endpoint, API version, and the URL for the message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"The URL is {url}");

                // Place the call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="781cd-131">Połączenie jest nawiązywane, a punkt końcowy usługi Twilio, wersja interfejsu API i stan wywołania są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="781cd-131">The call is made, and the Twilio endpoint, API version, and the call status are displayed.</span></span> <span data-ttu-id="781cd-132">Poniższy zrzut ekranu przedstawia Uruchom przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="781cd-132">The following screenshot shows output from a sample run.</span></span>

![Odpowiedź wywołania platformy Azure przy użyciu usługi Twilio i platformy ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="781cd-134">Więcej informacji na temat TwiML można znaleźć w folderze [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="781cd-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="781cd-135">Więcej informacji na temat &lt;powiedzieć&gt; i inne usługi Twilio zlecenia można znaleźć w folderze [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="781cd-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="781cd-136"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="781cd-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="781cd-137">Ten kod został podany pokazanie podstawowe funkcje w roli sieci web platformy ASP.NET na platformie Azure przy użyciu usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="781cd-137">This code was provided to show you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="781cd-138">Przed wdrożeniem na platformie Azure w środowisku produkcyjnym, możesz dodać więcej obsługi błędów lub innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="781cd-138">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="781cd-139">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="781cd-139">For example:</span></span>

* <span data-ttu-id="781cd-140">Zamiast za pomocą formularza sieci web, można użyć magazynu obiektów Blob platformy Azure lub wystąpienie bazy danych SQL Azure do przechowywania numerów telefonów i wywołać tekstu.</span><span class="sxs-lookup"><span data-stu-id="781cd-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance to store phone numbers and call text.</span></span> <span data-ttu-id="781cd-141">Aby dowiedzieć się, jak za pomocą obiektów blob platformy Azure, zobacz [jak używać usługi magazynu obiektów Blob platformy Azure w programie .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="781cd-141">For information about using Blobs in Azure, see [How to use the Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="781cd-142">Aby uzyskać informacje dotyczące korzystania z bazy danych SQL, zobacz [jak używać usługi Azure SQL Database w aplikacjach .NET][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="781cd-142">For information about using SQL Database, see [How to use Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="781cd-143">Można użyć `RoleEnvironment.getConfigurationSettings` można pobrać usługi Twilio Identyfikatora konta oraz uwierzytelniania token z danym wdrożeniu ustawień konfiguracji, zamiast kodować wartości w formularzu.</span><span class="sxs-lookup"><span data-stu-id="781cd-143">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in your form.</span></span> <span data-ttu-id="781cd-144">Aby uzyskać informacje o `RoleEnvironment` , zobacz [Namespace Microsoft.WindowsAzure.ServiceRuntime][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="781cd-144">For information about the `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="781cd-145">Zapoznaj się ze wskazówkami zabezpieczeń usługi Twilio w [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="781cd-145">Read the Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="781cd-146">Dowiedz się więcej na temat usługi Twilio w [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="781cd-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="781cd-147"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="781cd-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="781cd-148">Jak używać usługi Twilio głosu i SMS funkcji z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="781cd-148">How to use Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
