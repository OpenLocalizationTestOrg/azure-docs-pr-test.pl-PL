---
title: "Witaj toouse aaaHow SendGrid usługa poczty e-mail (.NET) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wysłać wiadomość e-mail z hello SendGrid usługa poczty e-mail na platformie Azure. Przykłady kodu napisane w hello C# i użyj interfejsu API platformy .NET."
services: app-service-web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: b3d77bb67898b991c7293e6b9086b263f6bcb755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-with-azure"></a><span data-ttu-id="48792-104">Jak tooSend SendGrid za pomocą wiadomości E-mail z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="48792-104">How tooSend Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="48792-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="48792-105">Overview</span></span>
<span data-ttu-id="48792-106">W tym przewodniku pokazano, jak tooperform typowych zadań programowania SendGrid poczty e-mail usługi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="48792-106">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="48792-107">Przykłady Hello są napisane w języku C\# i obsługuje standardowe 1.3 .NET.</span><span class="sxs-lookup"><span data-stu-id="48792-107">hello samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="48792-108">omówione scenariusze Hello obejmują konstruowania poczty e-mail, wysyłania wiadomości e-mail, dodawanie załączników i włączanie różnych poczty i ustawienia śledzenia.</span><span class="sxs-lookup"><span data-stu-id="48792-108">hello scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="48792-109">Aby uzyskać więcej informacji na SendGrid i wysyłania wiadomości e-mail, zobacz hello [następne kroki] [ Next steps] sekcji.</span><span class="sxs-lookup"><span data-stu-id="48792-109">For more information on SendGrid and sending email, see hello [Next steps][Next steps] section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="48792-110">Co to jest hello SendGrid usługa poczty E-mail?</span><span class="sxs-lookup"><span data-stu-id="48792-110">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="48792-111">Jest SendGrid [e-mail opartej na chmurze usługa] zapewnia niezawodne [dostarczania transakcyjnych wiadomości e-mail], skalowalności i analiz w czasie rzeczywistym oraz elastyczne interfejsów API, które umożliwiają łatwe niestandardowej integracji.</span><span class="sxs-lookup"><span data-stu-id="48792-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="48792-112">Typowe przypadki użycia SendGrid obejmują:</span><span class="sxs-lookup"><span data-stu-id="48792-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="48792-113">Automatycznego wysyłania potwierdzeń lub toocustomers potwierdzenia zakupu.</span><span class="sxs-lookup"><span data-stu-id="48792-113">Automatically sending receipts or purchase confirmations toocustomers.</span></span>
* <span data-ttu-id="48792-114">Administrowanie dystrybucji wymieniono wysyłania klientów miesięczne ulotki i promocji.</span><span class="sxs-lookup"><span data-stu-id="48792-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="48792-115">Zbieranie metryk w czasie rzeczywistym dla zablokowanych poczty e-mail i zaangażowania klientów.</span><span class="sxs-lookup"><span data-stu-id="48792-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="48792-116">Przekazywanie zapytania klientów.</span><span class="sxs-lookup"><span data-stu-id="48792-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="48792-117">Przetwarzanie przychodzących wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="48792-117">Processing incoming emails.</span></span>

<span data-ttu-id="48792-118">Aby uzyskać więcej informacji, odwiedź stronę [https://sendgrid.com](https://sendgrid.com) lub jego SendGrid [biblioteki C#] [ sendgrid-csharp] repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="48792-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="48792-119">Utwórz konto SendGrid</span><span class="sxs-lookup"><span data-stu-id="48792-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a><span data-ttu-id="48792-120">Odwołanie hello SendGrid Biblioteka klas programu .NET</span><span class="sxs-lookup"><span data-stu-id="48792-120">Reference hello SendGrid .NET Class Library</span></span>
<span data-ttu-id="48792-121">Witaj [pakietu SendGrid NuGet](https://www.nuget.org/packages/Sendgrid) jest hello Najprostszym sposobem tooget hello SendGrid interfejsu API i tooconfigure wszystkie zależności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="48792-121">hello [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is hello easiest way tooget hello SendGrid API and tooconfigure your application with all dependencies.</span></span> <span data-ttu-id="48792-122">NuGet jest dostępne w programie Microsoft Visual Studio 2015 oraz powyżej rozszerzenia umożliwia łatwe tooinstall i aktualizacji biblioteki i narzędzia Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="48792-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy tooinstall and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="48792-123">tooinstall NuGet, jeśli używasz programu Visual Studio w wersji starszej niż Visual Studio 2015, odwiedź stronę [http://www.nuget.org](http://www.nuget.org)i kliknij przycisk hello **instalowania NuGet** przycisku.</span><span class="sxs-lookup"><span data-stu-id="48792-123">tooinstall NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click hello **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="48792-124">Witaj tooinstall pakietu SendGrid NuGet w aplikacji hello następujące:</span><span class="sxs-lookup"><span data-stu-id="48792-124">tooinstall hello SendGrid NuGet package in your application, do hello following:</span></span>

1. <span data-ttu-id="48792-125">Polecenie **nowy projekt** i wybierz **szablonu**.</span><span class="sxs-lookup"><span data-stu-id="48792-125">Click on **New Project** and select a **Template**.</span></span>

   ![Tworzenie nowego projektu][create-new-project]
2. <span data-ttu-id="48792-127">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **odwołania**, następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="48792-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![Pakiet SendGrid NuGet][SendGrid-NuGet-package]
3. <span data-ttu-id="48792-129">Wyszukaj **SendGrid** i wybierz hello **SendGrid** element na liście wyników.</span><span class="sxs-lookup"><span data-stu-id="48792-129">Search for **SendGrid** and select hello **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="48792-130">Wybierz hello najnowsza stabilna wersja pakietu Nuget hello z hello wersja listy rozwijanej toobe stanie toowork z modelu obiektu hello i interfejsów API przedstawiona w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="48792-130">Select hello latest stable version of hello Nuget package from hello version dropdown toobe able toowork with hello object model and APIs demonstrated in this article.</span></span>

   ![Pakietu SendGrid][sendgrid-package]
5. <span data-ttu-id="48792-132">Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="48792-132">Click **Install** toocomplete hello installation, and then close this dialog.</span></span>

<span data-ttu-id="48792-133">Biblioteka klas programu .NET w SendGrid jest nazywany **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="48792-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="48792-134">Ten przewodnik zawiera następujące przestrzenie nazw hello:</span><span class="sxs-lookup"><span data-stu-id="48792-134">It contains hello following namespaces:</span></span>

* <span data-ttu-id="48792-135">**SendGrid** do komunikowania się z jego SendGrid interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="48792-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="48792-136">**SendGrid.Helpers.Mail** dla pomocnika tooeasily metod tworzenia SendGridMessage obiektów, które określają sposób toosend wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="48792-136">**SendGrid.Helpers.Mail** for helper methods tooeasily create SendGridMessage objects that specify how toosend emails.</span></span>

<span data-ttu-id="48792-137">Dodaj hello następującego kodu przestrzeni nazw deklaracje toohello top dla dowolnego pliku C# w którym chcesz tooprogrammatically dostępu hello SendGrid poczty e-mail usługi.</span><span class="sxs-lookup"><span data-stu-id="48792-137">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access hello SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="48792-138">Porady: Tworzenie wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="48792-138">How to: Create an Email</span></span>
<span data-ttu-id="48792-139">Użyj hello **SendGridMessage** obiekt toocreate wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="48792-139">Use hello **SendGridMessage** object toocreate an email message.</span></span> <span data-ttu-id="48792-140">Po utworzeniu obiektu wiadomość hello można ustawić właściwości i metod, w tym hello nadawcą wiadomości e-mail, hello adresata poczty e-mail i hello temat i treść wiadomości e-mail hello.</span><span class="sxs-lookup"><span data-stu-id="48792-140">Once hello message object is created, you can set properties and methods, including hello email sender, hello email recipient, and hello subject and body of hello email.</span></span>

<span data-ttu-id="48792-141">Witaj poniższym przykładzie pokazano, jak toocreate obiektu całkowicie wypełnione poczty e-mail:</span><span class="sxs-lookup"><span data-stu-id="48792-141">hello following example demonstrates how toocreate a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing hello SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="48792-142">Aby uzyskać więcej informacji na temat wszystkich właściwości i metod obsługiwanych przez **SendGrid** typu, zobacz [sendgrid csharp] [ sendgrid-csharp] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="48792-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="48792-143">Porady: wysyłanie wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="48792-143">How to: Send an Email</span></span>
<span data-ttu-id="48792-144">Po utworzeniu wiadomości e-mail, możesz wysłać go przy użyciu interfejsu API w SendGrid.</span><span class="sxs-lookup"><span data-stu-id="48792-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="48792-145">Alternatywnie można użyć [. Utworzony przez sieć w bibliotece][NET-library].</span><span class="sxs-lookup"><span data-stu-id="48792-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="48792-146">Wysyłanie poczty e-mail wymaga podania klucza interfejsu API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="48792-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="48792-147">Aby uzyskać szczegółowe informacje na temat tooconfigure klucze interfejsu API, odwiedź stronę klucze interfejsu API w SendGrid [dokumentacji][documentation].</span><span class="sxs-lookup"><span data-stu-id="48792-147">If you need details about how tooconfigure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="48792-148">Te poświadczenia mogą być przechowywane w portalu Azure, klikając pozycję Ustawienia aplikacji i dodawanie hello pary klucz wartość w ustawieniach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="48792-148">You may store these credentials via your Azure Portal by clicking Application settings and adding hello key/value pairs under App settings.</span></span>

 ![Ustawienia aplikacji Azure][azure_app_settings]

 <span data-ttu-id="48792-150">Następnie użytkownik może uzyskiwać do nich dostęp w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="48792-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="48792-151">Hello następujące przykłady przedstawiają sposób toosend komunikat przy użyciu hello interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="48792-151">hello following examples show how toosend a message using hello Web API.</span></span>

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from hello SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="48792-152">Porady: Dodawanie załącznika</span><span class="sxs-lookup"><span data-stu-id="48792-152">How to: Add an attachment</span></span>
<span data-ttu-id="48792-153">Załączniki mogą być dodawane tooa wiadomości przez wywołanie hello **AddAttachment** — metoda i minimalny zestaw Określanie hello nazwę pliku i kodowany w standardzie Base64 zawartości można mają tooattach.</span><span class="sxs-lookup"><span data-stu-id="48792-153">Attachments can be added tooa message by calling hello **AddAttachment** method and minimally specifying hello file name and Base64 encoded content you want tooattach.</span></span> <span data-ttu-id="48792-154">Może zawierać wiele załączników za hello lub wywołaniem tej metody, gdy dla każdego pliku chcesz tooattach **AddAttachments** metody.</span><span class="sxs-lookup"><span data-stu-id="48792-154">You can include multiple attachments by calling this method once for each file you wish tooattach or by using hello **AddAttachments** method.</span></span> <span data-ttu-id="48792-155">Hello poniższy przykład przedstawia, dodawanie komunikat tooa załącznika:</span><span class="sxs-lookup"><span data-stu-id="48792-155">hello following example demonstrates adding an attachment tooa message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="48792-156">Porady: Użyj stopki tooenable ustawienia poczty, śledzenia i analiza</span><span class="sxs-lookup"><span data-stu-id="48792-156">How to: Use mail settings tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="48792-157">SendGrid udostępnia funkcje dodatkowe poczty e-mail przy użyciu hello ustawienia śledzenia i ustawienia poczty.</span><span class="sxs-lookup"><span data-stu-id="48792-157">SendGrid provides additional email functionality through hello use of mail settings and tracking settings.</span></span> <span data-ttu-id="48792-158">Te ustawienia można dodać tooan e-mail wiadomość tooenable określone funkcje, takie jak kliknij śledzenia, Google analytics, subskrypcji, śledzenia i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="48792-158">These settings can be added tooan email message tooenable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="48792-159">Aby uzyskać pełną listę aplikacji, zobacz hello [dokumentacji ustawienia][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="48792-159">For a full list of apps, see hello [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="48792-160">Aplikacje, które mogą być stosowane za**SendGrid** przy użyciu metod zaimplementowanych jako część hello wiadomości e-mail **SendGridMessage** klasy.</span><span class="sxs-lookup"><span data-stu-id="48792-160">Apps can be applied too**SendGrid** email messages using methods implemented as part of hello **SendGridMessage** class.</span></span> <span data-ttu-id="48792-161">Witaj poniższe przykłady pokazują stopki hello i kliknij śledzenia filtrów:</span><span class="sxs-lookup"><span data-stu-id="48792-161">hello following examples demonstrate hello footer and click tracking filters:</span></span>

<span data-ttu-id="48792-162">Witaj poniższe przykłady pokazują stopki hello i kliknij śledzenia filtrów:</span><span class="sxs-lookup"><span data-stu-id="48792-162">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="48792-163">Ustawienia stopki</span><span class="sxs-lookup"><span data-stu-id="48792-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="48792-164">Kliknij przycisk śledzenia</span><span class="sxs-lookup"><span data-stu-id="48792-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="48792-165">Porady: Użyj SendGrid dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="48792-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="48792-166">SendGrid oferuje kilka interfejsów API i elementów webhook, których można używać tooleverage dodatkowe funkcje aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="48792-166">SendGrid offers several APIs and webhooks that you can use tooleverage additional functionality within your Azure application.</span></span> <span data-ttu-id="48792-167">Aby uzyskać więcej informacji, zobacz hello [dokumentacja interfejsu API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="48792-167">For more details, see hello [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="48792-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48792-168">Next steps</span></span>
<span data-ttu-id="48792-169">Teraz, kiedy znasz już podstawy hello hello usługi SendGrid wiadomości E-mail, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="48792-169">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="48792-170">SendGrid C\# repozytorium biblioteki: [sendgrid csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="48792-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="48792-171">Dokumentacja interfejsu API SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="48792-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is hello SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference hello SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters tooEnable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: ./media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: ./media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: ./media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: ./media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

[e-mail opartej na chmurze usługa]: https://sendgrid.com/solutions
[dostarczania transakcyjnych wiadomości e-mail]: https://sendgrid.com/use-cases/transactional-email

