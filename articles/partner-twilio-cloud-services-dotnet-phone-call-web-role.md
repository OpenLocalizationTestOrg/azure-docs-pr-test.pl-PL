---
title: "toomake aaaHow rozmowy telefonicznej z usługi Twilio (.NET) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak komunikatów toomake połączeń telefonicznych i Wyślij wiadomość SMS z usługi interfejsu API usługi Twilio hello na platformie Azure. Przykłady kodu napisane w programie .NET."
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
ms.openlocfilehash: 857d89961c563a51fef944f4a72828036af79b43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="3b1ee-104">Jak toomake rozmowy telefonicznej przy użyciu usługi Twilio w roli sieci web na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3b1ee-104">How toomake a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="3b1ee-105">W tym przewodniku pokazano, jak toomake usługi Twilio toouse wywołanie ze strony sieci web hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-105">This guide demonstrates how toouse Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="3b1ee-106">wynikowej aplikacji Hello monity toomake użytkownika hello wywołania z hello podany numer i komunikat, jak pokazano w powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-106">hello resulting application prompts hello user toomake a call with hello given number and message, as shown in hello following screenshot.</span></span>

![Formularz wywołania platformy Azure przy użyciu usługi Twilio i platformy ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="3b1ee-108"><a name="twilio-prereqs"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3b1ee-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="3b1ee-109">Konieczne będzie toodo hello następujące toouse hello kodu w tym temacie:</span><span class="sxs-lookup"><span data-stu-id="3b1ee-109">You will need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="3b1ee-110">Uzyskać konta usługi Twilio i uwierzytelniania tokenu z hello [usługi Twilio Console][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-110">Acquire a Twilio account and authentication token from hello [Twilio Console][twilio_console].</span></span> <span data-ttu-id="3b1ee-111">tooget wprowadzenie do usługi Twilio, zaloguj na [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-111">tooget started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="3b1ee-112">Będziesz w stanie ocenić cennik w [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="3b1ee-113">Informacje hello udostępniane przez usługi Twilio interfejsu API, zobacz [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-113">For information about hello API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="3b1ee-114">Dodaj hello *biblioteki .NET usługi Twilio* tooyour roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-114">Add hello *Twilio .NET libary* tooyour web role.</span></span> <span data-ttu-id="3b1ee-115">Zobacz **usługi Twilio hello tooadd biblioteki projektu roli sieć web tooyour**w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-115">See **tooadd hello Twilio libraries tooyour web role project**, later in this topic.</span></span>

<span data-ttu-id="3b1ee-116">Należy się zapoznać z tworzeniem podstawowego [roli sieci Web na platformie Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="3b1ee-117"><a name="howtocreateform"></a>Porady: Tworzenie formularza sieci web nawiązywania połączenia</span><span class="sxs-lookup"><span data-stu-id="3b1ee-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="3b1ee-118"><a id="use_nuget"></a>tooadd hello usługi Twilio biblioteki tooyour projektu roli sieć web:</span><span class="sxs-lookup"><span data-stu-id="3b1ee-118"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour web role project:</span></span>

1. <span data-ttu-id="3b1ee-119">Otwórz rozwiązanie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="3b1ee-120">Kliknij prawym przyciskiem myszy **odwołania**.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-120">Right-click **References**.</span></span>
3. <span data-ttu-id="3b1ee-121">Kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="3b1ee-122">Kliknij przycisk **Online**.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-122">Click **Online**.</span></span>
5. <span data-ttu-id="3b1ee-123">W hello wyszukiwania online wpisz *usługi twilio*.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-123">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="3b1ee-124">Kliknij przycisk **zainstalować** na powitania pakietu usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-124">Click **Install** on hello Twilio package.</span></span>

<span data-ttu-id="3b1ee-125">Witaj następującego kodu pokazuje, jak dane użytkownika tooretrieve wywołania formularza toocreate sieci web.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-125">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="3b1ee-126">W tym przykładzie roli sieci Web programu ASP.NET o nazwie **TwilioCloud** jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

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

## <span data-ttu-id="3b1ee-127"><a id="howtocreatecode"></a>Porady: tworzenie hello kodu toomake hello rozmowy</span><span class="sxs-lookup"><span data-stu-id="3b1ee-127"><a id="howtocreatecode"></a>How to: Create hello code toomake hello call</span></span>
<span data-ttu-id="3b1ee-128">Witaj następujący kod, który jest wywoływany, gdy użytkownik hello kończy formularz hello, tworzy wiadomości powitania wywołania i generuje hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-128">hello following code, which is called when hello user completes hello form, creates hello call message and generates hello call.</span></span> <span data-ttu-id="3b1ee-129">W tym przykładzie kodu hello jest uruchomiony w hello program obsługi zdarzeń przycisk hello hello formularza.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-129">In this example, hello code is run in hello onclick event handler of hello button on hello form.</span></span> <span data-ttu-id="3b1ee-130">(Użyj swojego konta usługi Twilio i uwierzytelniania tokenu zamiast symbole zastępcze hello przypisane zbyt`accountSID` i `authToken` w kodzie hello poniżej.)</span><span class="sxs-lookup"><span data-stu-id="3b1ee-130">(Use your Twilio account and authentication token instead of hello placeholder values assigned too`accountSID` and `authToken` in hello code below.)</span></span>

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
            // hello placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of hello Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve hello account, used later tooretrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve hello values entered by hello user.
                var too= PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using hello Twilio message and hello user-entered
                // text. You must replace spaces in hello user's text with '%20'
                // toomake hello text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display hello endpoint, API version, and hello URL for hello message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"hello URL is {url}");

                // Place hello call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="3b1ee-131">Wywołanie Hello, a punkt końcowy usługi Twilio hello, wersja interfejsu API i stan wywołania hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-131">hello call is made, and hello Twilio endpoint, API version, and hello call status are displayed.</span></span> <span data-ttu-id="3b1ee-132">Witaj poniższych zrzut ekranu przedstawia w danych wyjściowych z próbkę Uruchom.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-132">hello following screenshot shows output from a sample run.</span></span>

![Odpowiedź wywołania platformy Azure przy użyciu usługi Twilio i platformy ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="3b1ee-134">Więcej informacji na temat TwiML można znaleźć w folderze [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="3b1ee-135">Więcej informacji na temat &lt;powiedzieć&gt; i inne usługi Twilio zlecenia można znaleźć w folderze [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="3b1ee-136"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3b1ee-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="3b1ee-137">Ten kod został podany tooshow możesz podstawowe funkcje w roli sieci web platformy ASP.NET na platformie Azure przy użyciu usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-137">This code was provided tooshow you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="3b1ee-138">Przed wdrożeniem tooAzure w środowisku produkcyjnym, możesz tooadd więcej obsługi błędów lub innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-138">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="3b1ee-139">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="3b1ee-139">For example:</span></span>

* <span data-ttu-id="3b1ee-140">Zamiast za pomocą formularza sieci web, można użyć magazynu obiektów Blob platformy Azure lub numery telefonów toostore wystąpienia bazy danych SQL Azure i wywołać tekstu.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance toostore phone numbers and call text.</span></span> <span data-ttu-id="3b1ee-141">Aby dowiedzieć się, jak za pomocą obiektów blob platformy Azure, zobacz [jak toouse hello usługi magazynu obiektów Blob platformy Azure w programie .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-141">For information about using Blobs in Azure, see [How toouse hello Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="3b1ee-142">Aby uzyskać informacje dotyczące korzystania z bazy danych SQL, zobacz [jak toouse Azure SQL bazy danych w aplikacjach .NET][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-142">For information about using SQL Database, see [How toouse Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="3b1ee-143">Można użyć `RoleEnvironment.getConfigurationSettings` identyfikator konta usługi Twilio hello tooretrieve i uwierzytelniania token z danym wdrożeniu ustawień konfiguracji, zamiast kodować hello wartości w formularzu.</span><span class="sxs-lookup"><span data-stu-id="3b1ee-143">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in your form.</span></span> <span data-ttu-id="3b1ee-144">Aby uzyskać informacje na temat hello `RoleEnvironment` , zobacz [Namespace Microsoft.WindowsAzure.ServiceRuntime][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-144">For information about hello `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="3b1ee-145">Przeczytaj wytyczne dotyczące zabezpieczeń usługi Twilio hello na [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-145">Read hello Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="3b1ee-146">Dowiedz się więcej na temat usługi Twilio w [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="3b1ee-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="3b1ee-147"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3b1ee-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="3b1ee-148">Jak toouse usługi Twilio głosu i SMS funkcji z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3b1ee-148">How toouse Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

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
