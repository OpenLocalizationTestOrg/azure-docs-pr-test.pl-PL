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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a>Jak toomake rozmowy telefonicznej przy użyciu usługi Twilio w roli sieci web na platformie Azure
W tym przewodniku pokazano, jak toomake usługi Twilio toouse wywołanie ze strony sieci web hostowanej na platformie Azure. wynikowej aplikacji Hello monity toomake użytkownika hello wywołania z hello podany numer i komunikat, jak pokazano w powitania po zrzut ekranu.

![Formularz wywołania platformy Azure przy użyciu usługi Twilio i platformy ASP.NET][twilio_dotnet_basic_form]

## <a name="twilio-prereqs"></a>Wymagania wstępne
Konieczne będzie toodo hello następujące toouse hello kodu w tym temacie:

1. Uzyskać konta usługi Twilio i uwierzytelniania tokenu z hello [usługi Twilio Console][twilio_console]. tooget wprowadzenie do usługi Twilio, zaloguj na [https://www.twilio.com/try-twilio][try_twilio]. Będziesz w stanie ocenić cennik w [http://www.twilio.com/pricing][twilio_pricing]. Informacje hello udostępniane przez usługi Twilio interfejsu API, zobacz [http://www.twilio.com/voice/api][twilio_api].
2. Dodaj hello *biblioteki .NET usługi Twilio* tooyour roli sieci web. Zobacz **usługi Twilio hello tooadd biblioteki projektu roli sieć web tooyour**w dalszej części tego tematu.

Należy się zapoznać z tworzeniem podstawowego [roli sieci Web na platformie Azure][azure_webroles_get_started].

## <a name="howtocreateform"></a>Porady: Tworzenie formularza sieci web nawiązywania połączenia
<a id="use_nuget"></a>tooadd hello usługi Twilio biblioteki tooyour projektu roli sieć web:

1. Otwórz rozwiązanie w programie Visual Studio.
2. Kliknij prawym przyciskiem myszy **odwołania**.
3. Kliknij przycisk **Zarządzaj pakietami NuGet**.
4. Kliknij przycisk **Online**.
5. W hello wyszukiwania online wpisz *usługi twilio*.
6. Kliknij przycisk **zainstalować** na powitania pakietu usługi Twilio.

Witaj następującego kodu pokazuje, jak dane użytkownika tooretrieve wywołania formularza toocreate sieci web. W tym przykładzie roli sieci Web programu ASP.NET o nazwie **TwilioCloud** jest tworzony.

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

## <a id="howtocreatecode"></a>Porady: tworzenie hello kodu toomake hello rozmowy
Witaj następujący kod, który jest wywoływany, gdy użytkownik hello kończy formularz hello, tworzy wiadomości powitania wywołania i generuje hello wywołania. W tym przykładzie kodu hello jest uruchomiony w hello program obsługi zdarzeń przycisk hello hello formularza. (Użyj swojego konta usługi Twilio i uwierzytelniania tokenu zamiast symbole zastępcze hello przypisane zbyt`accountSID` i `authToken` w kodzie hello poniżej.)

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

Wywołanie Hello, a punkt końcowy usługi Twilio hello, wersja interfejsu API i stan wywołania hello są wyświetlane. Witaj poniższych zrzut ekranu przedstawia w danych wyjściowych z próbkę Uruchom.

![Odpowiedź wywołania platformy Azure przy użyciu usługi Twilio i platformy ASP.NET][twilio_dotnet_basic_form_output]

Więcej informacji na temat TwiML można znaleźć w folderze [http://www.twilio.com/docs/api/twiml][twiml]. Więcej informacji na temat &lt;powiedzieć&gt; i inne usługi Twilio zlecenia można znaleźć w folderze [http://www.twilio.com/docs/api/twiml/say][twilio_say].

## <a id="nextsteps"></a>Następne kroki
Ten kod został podany tooshow możesz podstawowe funkcje w roli sieci web platformy ASP.NET na platformie Azure przy użyciu usługi Twilio. Przed wdrożeniem tooAzure w środowisku produkcyjnym, możesz tooadd więcej obsługi błędów lub innych funkcji. Na przykład:

* Zamiast za pomocą formularza sieci web, można użyć magazynu obiektów Blob platformy Azure lub numery telefonów toostore wystąpienia bazy danych SQL Azure i wywołać tekstu. Aby dowiedzieć się, jak za pomocą obiektów blob platformy Azure, zobacz [jak toouse hello usługi magazynu obiektów Blob platformy Azure w programie .NET][howto_blob_storage_dotnet]. Aby uzyskać informacje dotyczące korzystania z bazy danych SQL, zobacz [jak toouse Azure SQL bazy danych w aplikacjach .NET][howto_sql_azure_dotnet].
* Można użyć `RoleEnvironment.getConfigurationSettings` identyfikator konta usługi Twilio hello tooretrieve i uwierzytelniania token z danym wdrożeniu ustawień konfiguracji, zamiast kodować hello wartości w formularzu. Aby uzyskać informacje na temat hello `RoleEnvironment` , zobacz [Namespace Microsoft.WindowsAzure.ServiceRuntime][azure_runtime_ref_dotnet].
* Przeczytaj wytyczne dotyczące zabezpieczeń usługi Twilio hello na [https://www.twilio.com/docs/security][twilio_docs_security].
* Dowiedz się więcej na temat usługi Twilio w [https://www.twilio.com/docs][twilio_docs].

## <a name="seealso"></a>Zobacz też
* [Jak toouse usługi Twilio głosu i SMS funkcji z platformy Azure](twilio-dotnet-how-to-use-for-voice-sms.md)

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
