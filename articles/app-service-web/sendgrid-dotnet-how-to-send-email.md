---
title: "Jak używać usługi poczty e-mail SendGrid (.NET) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wysłać wiadomość e-mail z usługi poczty e-mail SendGrid na platformie Azure. Przykłady kodu napisane w języku C# i używają interfejsu API platformy .NET."
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
ms.openlocfilehash: b3a48b3c838763b022a18e55817ec7455fe94c85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-send-email-using-sendgrid-with-azure"></a><span data-ttu-id="4bbd8-104">Sposób wysyłania poczty E-mail przy użyciu SendGrid z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4bbd8-104">How to Send Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="4bbd8-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4bbd8-105">Overview</span></span>
<span data-ttu-id="4bbd8-106">W tym przewodniku przedstawiono sposób wykonywania typowych zadań programowania usługi poczty e-mail SendGrid na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-106">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="4bbd8-107">Przykłady są napisane w języku C\# i obsługuje standardowe 1.3 .NET.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-107">The samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="4bbd8-108">Omówione scenariusze obejmują konstruowania poczty e-mail, wysyłania wiadomości e-mail, dodawanie załączników i włączanie różnych poczty i ustawienia śledzenia.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-108">The scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="4bbd8-109">Aby uzyskać więcej informacji na SendGrid i wysyłania wiadomości e-mail, zobacz [następne kroki] [ Next steps] sekcji.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-109">For more information on SendGrid and sending email, see the [Next steps][Next steps] section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="4bbd8-110">Co to jest usługa SendGrid poczty E-mail?</span><span class="sxs-lookup"><span data-stu-id="4bbd8-110">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="4bbd8-111">Jest SendGrid [e-mail opartej na chmurze usługa] zapewnia niezawodne [dostarczania transakcyjnych wiadomości e-mail], skalowalności i analiz w czasie rzeczywistym oraz elastyczne interfejsów API, które umożliwiają łatwe niestandardowej integracji.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="4bbd8-112">Typowe przypadki użycia SendGrid obejmują:</span><span class="sxs-lookup"><span data-stu-id="4bbd8-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="4bbd8-113">Automatycznego wysyłania potwierdzeń lub potwierdzenia zakupu do klientów.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-113">Automatically sending receipts or purchase confirmations to customers.</span></span>
* <span data-ttu-id="4bbd8-114">Administrowanie dystrybucji wymieniono wysyłania klientów miesięczne ulotki i promocji.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="4bbd8-115">Zbieranie metryk w czasie rzeczywistym dla zablokowanych poczty e-mail i zaangażowania klientów.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="4bbd8-116">Przekazywanie zapytania klientów.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="4bbd8-117">Przetwarzanie przychodzących wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-117">Processing incoming emails.</span></span>

<span data-ttu-id="4bbd8-118">Aby uzyskać więcej informacji, odwiedź stronę [https://sendgrid.com](https://sendgrid.com) lub jego SendGrid [biblioteki C#] [ sendgrid-csharp] repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="4bbd8-119">Utwórz konto SendGrid</span><span class="sxs-lookup"><span data-stu-id="4bbd8-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-net-class-library"></a><span data-ttu-id="4bbd8-120">Odwołanie w bibliotece klas programu .NET SendGrid</span><span class="sxs-lookup"><span data-stu-id="4bbd8-120">Reference the SendGrid .NET Class Library</span></span>
<span data-ttu-id="4bbd8-121">[Pakietu SendGrid NuGet](https://www.nuget.org/packages/Sendgrid) jest najprostszym sposobem, można pobrać interfejsu API SendGrid i skonfigurowania aplikacji ze wszystkich zależności.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-121">The [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is the easiest way to get the SendGrid API and to configure your application with all dependencies.</span></span> <span data-ttu-id="4bbd8-122">NuGet to rozszerzenie programu Visual Studio, dołączone do programu Microsoft Visual Studio 2015 i powyżej, który ułatwia instalacji i aktualizacji biblioteki i narzędzia.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy to install and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="4bbd8-123">Aby zainstalować NuGet, jeśli używasz programu Visual Studio w wersji starszej niż Visual Studio 2015, odwiedź [http://www.nuget.org](http://www.nuget.org)i kliknij przycisk **instalowania NuGet** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-123">To install NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click the **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="4bbd8-124">Aby zainstalować pakiet NuGet włączenie w aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4bbd8-124">To install the SendGrid NuGet package in your application, do the following:</span></span>

1. <span data-ttu-id="4bbd8-125">Polecenie **nowy projekt** i wybierz **szablonu**.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-125">Click on **New Project** and select a **Template**.</span></span>

   ![Tworzenie nowego projektu][create-new-project]
2. <span data-ttu-id="4bbd8-127">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **odwołania**, następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![Pakiet SendGrid NuGet][SendGrid-NuGet-package]
3. <span data-ttu-id="4bbd8-129">Wyszukaj **SendGrid** i wybierz **SendGrid** element na liście wyników.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-129">Search for **SendGrid** and select the **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="4bbd8-130">Wybierz z listy rozwijanej wersji, aby mieć możliwość pracy z modelem obiektów najnowsza stabilna wersja pakietu Nuget i interfejsów API przedstawiona w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-130">Select the latest stable version of the Nuget package from the version dropdown to be able to work with the object model and APIs demonstrated in this article.</span></span>

   ![Pakietu SendGrid][sendgrid-package]
5. <span data-ttu-id="4bbd8-132">Kliknij przycisk **zainstalować** do ukończenia instalacji, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-132">Click **Install** to complete the installation, and then close this dialog.</span></span>

<span data-ttu-id="4bbd8-133">Biblioteka klas programu .NET w SendGrid jest nazywany **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="4bbd8-134">Ten przewodnik zawiera następujące przestrzenie nazw:</span><span class="sxs-lookup"><span data-stu-id="4bbd8-134">It contains the following namespaces:</span></span>

* <span data-ttu-id="4bbd8-135">**SendGrid** do komunikowania się z jego SendGrid interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="4bbd8-136">**SendGrid.Helpers.Mail** dla metody pomocnicze łatwe tworzenie SendGridMessage obiektów, które określają sposób wysyłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-136">**SendGrid.Helpers.Mail** for helper methods to easily create SendGridMessage objects that specify how to send emails.</span></span>

<span data-ttu-id="4bbd8-137">Dodaj następujące deklaracje przestrzeni nazw kod na początku dowolnego pliku C# ma do uzyskania programowego dostępu do usługi poczty e-mail SendGrid.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-137">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access the SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="4bbd8-138">Porady: Tworzenie wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="4bbd8-138">How to: Create an Email</span></span>
<span data-ttu-id="4bbd8-139">Użyj **SendGridMessage** obiekt, aby utworzyć wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-139">Use the **SendGridMessage** object to create an email message.</span></span> <span data-ttu-id="4bbd8-140">Po utworzeniu obiektu wiadomości, można ustawić właściwości i metod, w tym nadawcą wiadomości e-mail adresata poczty e-mail oraz temat i treść wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-140">Once the message object is created, you can set properties and methods, including the email sender, the email recipient, and the subject and body of the email.</span></span>

<span data-ttu-id="4bbd8-141">Poniższy przykład przedstawia sposób tworzenia obiektu całkowicie wypełnione poczty e-mail:</span><span class="sxs-lookup"><span data-stu-id="4bbd8-141">The following example demonstrates how to create a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing the SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="4bbd8-142">Aby uzyskać więcej informacji na temat wszystkich właściwości i metod obsługiwanych przez **SendGrid** typu, zobacz [sendgrid csharp] [ sendgrid-csharp] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="4bbd8-143">Porady: wysyłanie wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="4bbd8-143">How to: Send an Email</span></span>
<span data-ttu-id="4bbd8-144">Po utworzeniu wiadomości e-mail, możesz wysłać go przy użyciu interfejsu API w SendGrid.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="4bbd8-145">Alternatywnie można użyć [. Utworzony przez sieć w bibliotece][NET-library].</span><span class="sxs-lookup"><span data-stu-id="4bbd8-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="4bbd8-146">Wysyłanie poczty e-mail wymaga podania klucza interfejsu API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="4bbd8-147">Aby uzyskać szczegółowe informacje o sposobie konfigurowania klucze interfejsu API, odwiedź stronę klucze interfejsu API w SendGrid [dokumentacji][documentation].</span><span class="sxs-lookup"><span data-stu-id="4bbd8-147">If you need details about how to configure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="4bbd8-148">Te poświadczenia mogą być przechowywane za pośrednictwem portalu Azure, klikając ustawienia aplikacji i dodawanie pary klucz wartość w ustawieniach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-148">You may store these credentials via your Azure Portal by clicking Application settings and adding the key/value pairs under App settings.</span></span>

 ![Ustawienia aplikacji Azure][azure_app_settings]

 <span data-ttu-id="4bbd8-150">Następnie użytkownik może uzyskiwać do nich dostęp w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4bbd8-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="4bbd8-151">Poniższe przykłady przedstawiają sposób wysyłania wiadomości przy użyciu interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-151">The following examples show how to send a message using the Web API.</span></span>

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
                    Subject = "Hello World from the SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="4bbd8-152">Porady: Dodawanie załącznika</span><span class="sxs-lookup"><span data-stu-id="4bbd8-152">How to: Add an attachment</span></span>
<span data-ttu-id="4bbd8-153">Można dodać załączników do wiadomości przez wywołanie metody **AddAttachment** — metoda i minimalny zestaw określania nazwy pliku i kodowany w standardzie Base64 zawartości możesz chcesz dołączyć.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-153">Attachments can be added to a message by calling the **AddAttachment** method and minimally specifying the file name and Base64 encoded content you want to attach.</span></span> <span data-ttu-id="4bbd8-154">Może zawierać wiele załączników przez wywołanie tej metody, gdy dla każdego pliku chcesz dołączyć lub za pomocą **AddAttachments** metody.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-154">You can include multiple attachments by calling this method once for each file you wish to attach or by using the **AddAttachments** method.</span></span> <span data-ttu-id="4bbd8-155">W poniższym przykładzie pokazano, dodawanie załączników do wiadomości:</span><span class="sxs-lookup"><span data-stu-id="4bbd8-155">The following example demonstrates adding an attachment to a message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="4bbd8-156">Porady: Użyj ustawienia poczty, aby włączyć stopki, śledzenia i analiza</span><span class="sxs-lookup"><span data-stu-id="4bbd8-156">How to: Use mail settings to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="4bbd8-157">SendGrid udostępnia funkcje dodatkowe poczty e-mail przy użyciu ustawienia śledzenia i ustawienia poczty.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-157">SendGrid provides additional email functionality through the use of mail settings and tracking settings.</span></span> <span data-ttu-id="4bbd8-158">Te ustawienia można dodać do wiadomości e-mail, aby włączyć określonych funkcji, takich jak kliknij śledzenia, Google analytics, subskrypcji, śledzenia i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-158">These settings can be added to an email message to enable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="4bbd8-159">Aby uzyskać pełną listę aplikacji, zobacz [dokumentacji ustawienia][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="4bbd8-159">For a full list of apps, see the [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="4bbd8-160">Aplikacje mogą być stosowane do **SendGrid** przy użyciu metod zaimplementowanych jako część wiadomości e-mail **SendGridMessage** klasy.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-160">Apps can be applied to **SendGrid** email messages using methods implemented as part of the **SendGridMessage** class.</span></span> <span data-ttu-id="4bbd8-161">Poniższe przykłady pokazują, stopka i kliknij przycisk śledzenia filtrów:</span><span class="sxs-lookup"><span data-stu-id="4bbd8-161">The following examples demonstrate the footer and click tracking filters:</span></span>

<span data-ttu-id="4bbd8-162">Poniższe przykłady pokazują, stopka i kliknij przycisk śledzenia filtrów:</span><span class="sxs-lookup"><span data-stu-id="4bbd8-162">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="4bbd8-163">Ustawienia stopki</span><span class="sxs-lookup"><span data-stu-id="4bbd8-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="4bbd8-164">Kliknij przycisk śledzenia</span><span class="sxs-lookup"><span data-stu-id="4bbd8-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="4bbd8-165">Porady: Użyj SendGrid dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="4bbd8-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="4bbd8-166">SendGrid oferuje kilka interfejsów API i elementów webhook, który można wykorzystać dodatkowe funkcje aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-166">SendGrid offers several APIs and webhooks that you can use to leverage additional functionality within your Azure application.</span></span> <span data-ttu-id="4bbd8-167">Aby uzyskać więcej informacji, zobacz [dokumentacja interfejsu API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="4bbd8-167">For more details, see the [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bbd8-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4bbd8-168">Next steps</span></span>
<span data-ttu-id="4bbd8-169">Teraz, kiedy znasz już podstawy usługi poczty E-mail SendGrid, skorzystaj z poniższych linków, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="4bbd8-169">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="4bbd8-170">SendGrid C\# repozytorium biblioteki: [sendgrid csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="4bbd8-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="4bbd8-171">Dokumentacja interfejsu API SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="4bbd8-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is the SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference the SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters to Enable Footers, Tracking, and Analytics]: #usefilters
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

<span data-ttu-id="4bbd8-172">[e-mail opartej na chmurze usługa]: https://sendgrid.com/solutions</span><span class="sxs-lookup"><span data-stu-id="4bbd8-172">[cloud-based email service]: https://sendgrid.com/solutions</span></span>
<span data-ttu-id="4bbd8-173">[dostarczania transakcyjnych wiadomości e-mail]: https://sendgrid.com/use-cases/transactional-email</span><span class="sxs-lookup"><span data-stu-id="4bbd8-173">[transactional email delivery]: https://sendgrid.com/use-cases/transactional-email</span></span>

