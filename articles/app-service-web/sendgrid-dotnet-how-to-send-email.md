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
# <a name="how-toosend-email-using-sendgrid-with-azure"></a>Jak tooSend SendGrid za pomocą wiadomości E-mail z platformy Azure
## <a name="overview"></a>Omówienie
W tym przewodniku pokazano, jak tooperform typowych zadań programowania SendGrid poczty e-mail usługi na platformie Azure. Przykłady Hello są napisane w języku C\# i obsługuje standardowe 1.3 .NET. omówione scenariusze Hello obejmują konstruowania poczty e-mail, wysyłania wiadomości e-mail, dodawanie załączników i włączanie różnych poczty i ustawienia śledzenia. Aby uzyskać więcej informacji na SendGrid i wysyłania wiadomości e-mail, zobacz hello [następne kroki] [ Next steps] sekcji.

## <a name="what-is-hello-sendgrid-email-service"></a>Co to jest hello SendGrid usługa poczty E-mail?
Jest SendGrid [e-mail opartej na chmurze usługa] zapewnia niezawodne [dostarczania transakcyjnych wiadomości e-mail], skalowalności i analiz w czasie rzeczywistym oraz elastyczne interfejsów API, które umożliwiają łatwe niestandardowej integracji. Typowe przypadki użycia SendGrid obejmują:

* Automatycznego wysyłania potwierdzeń lub toocustomers potwierdzenia zakupu.
* Administrowanie dystrybucji wymieniono wysyłania klientów miesięczne ulotki i promocji.
* Zbieranie metryk w czasie rzeczywistym dla zablokowanych poczty e-mail i zaangażowania klientów.
* Przekazywanie zapytania klientów.
* Przetwarzanie przychodzących wiadomości e-mail.

Aby uzyskać więcej informacji, odwiedź stronę [https://sendgrid.com](https://sendgrid.com) lub jego SendGrid [biblioteki C#] [ sendgrid-csharp] repozytorium GitHub.

## <a name="create-a-sendgrid-account"></a>Utwórz konto SendGrid
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a>Odwołanie hello SendGrid Biblioteka klas programu .NET
Witaj [pakietu SendGrid NuGet](https://www.nuget.org/packages/Sendgrid) jest hello Najprostszym sposobem tooget hello SendGrid interfejsu API i tooconfigure wszystkie zależności aplikacji. NuGet jest dostępne w programie Microsoft Visual Studio 2015 oraz powyżej rozszerzenia umożliwia łatwe tooinstall i aktualizacji biblioteki i narzędzia Visual Studio.

> [!NOTE]
> tooinstall NuGet, jeśli używasz programu Visual Studio w wersji starszej niż Visual Studio 2015, odwiedź stronę [http://www.nuget.org](http://www.nuget.org)i kliknij przycisk hello **instalowania NuGet** przycisku.
>
>

Witaj tooinstall pakietu SendGrid NuGet w aplikacji hello następujące:

1. Polecenie **nowy projekt** i wybierz **szablonu**.

   ![Tworzenie nowego projektu][create-new-project]
2. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **odwołania**, następnie kliknij przycisk **Zarządzaj pakietami NuGet**.

   ![Pakiet SendGrid NuGet][SendGrid-NuGet-package]
3. Wyszukaj **SendGrid** i wybierz hello **SendGrid** element na liście wyników.
4. Wybierz hello najnowsza stabilna wersja pakietu Nuget hello z hello wersja listy rozwijanej toobe stanie toowork z modelu obiektu hello i interfejsów API przedstawiona w tym artykule.

   ![Pakietu SendGrid][sendgrid-package]
5. Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.

Biblioteka klas programu .NET w SendGrid jest nazywany **SendGrid**. Ten przewodnik zawiera następujące przestrzenie nazw hello:

* **SendGrid** do komunikowania się z jego SendGrid interfejsu API.
* **SendGrid.Helpers.Mail** dla pomocnika tooeasily metod tworzenia SendGridMessage obiektów, które określają sposób toosend wiadomości e-mail.

Dodaj hello następującego kodu przestrzeni nazw deklaracje toohello top dla dowolnego pliku C# w którym chcesz tooprogrammatically dostępu hello SendGrid poczty e-mail usługi.

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a>Porady: Tworzenie wiadomości E-mail
Użyj hello **SendGridMessage** obiekt toocreate wiadomości e-mail. Po utworzeniu obiektu wiadomość hello można ustawić właściwości i metod, w tym hello nadawcą wiadomości e-mail, hello adresata poczty e-mail i hello temat i treść wiadomości e-mail hello.

Witaj poniższym przykładzie pokazano, jak toocreate obiektu całkowicie wypełnione poczty e-mail:

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

Aby uzyskać więcej informacji na temat wszystkich właściwości i metod obsługiwanych przez **SendGrid** typu, zobacz [sendgrid csharp] [ sendgrid-csharp] w witrynie GitHub.

## <a name="how-to-send-an-email"></a>Porady: wysyłanie wiadomości E-mail
Po utworzeniu wiadomości e-mail, możesz wysłać go przy użyciu interfejsu API w SendGrid. Alternatywnie można użyć [. Utworzony przez sieć w bibliotece][NET-library].

Wysyłanie poczty e-mail wymaga podania klucza interfejsu API SendGrid. Aby uzyskać szczegółowe informacje na temat tooconfigure klucze interfejsu API, odwiedź stronę klucze interfejsu API w SendGrid [dokumentacji][documentation].

Te poświadczenia mogą być przechowywane w portalu Azure, klikając pozycję Ustawienia aplikacji i dodawanie hello pary klucz wartość w ustawieniach aplikacji.

 ![Ustawienia aplikacji Azure][azure_app_settings]

 Następnie użytkownik może uzyskiwać do nich dostęp w następujący sposób:

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

Hello następujące przykłady przedstawiają sposób toosend komunikat przy użyciu hello interfejsu API sieci Web.

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

## <a name="how-to-add-an-attachment"></a>Porady: Dodawanie załącznika
Załączniki mogą być dodawane tooa wiadomości przez wywołanie hello **AddAttachment** — metoda i minimalny zestaw Określanie hello nazwę pliku i kodowany w standardzie Base64 zawartości można mają tooattach. Może zawierać wiele załączników za hello lub wywołaniem tej metody, gdy dla każdego pliku chcesz tooattach **AddAttachments** metody. Hello poniższy przykład przedstawia, dodawanie komunikat tooa załącznika:

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a>Porady: Użyj stopki tooenable ustawienia poczty, śledzenia i analiza
SendGrid udostępnia funkcje dodatkowe poczty e-mail przy użyciu hello ustawienia śledzenia i ustawienia poczty. Te ustawienia można dodać tooan e-mail wiadomość tooenable określone funkcje, takie jak kliknij śledzenia, Google analytics, subskrypcji, śledzenia i tak dalej. Aby uzyskać pełną listę aplikacji, zobacz hello [dokumentacji ustawienia][settings-documentation].

Aplikacje, które mogą być stosowane za**SendGrid** przy użyciu metod zaimplementowanych jako część hello wiadomości e-mail **SendGridMessage** klasy. Witaj poniższe przykłady pokazują stopki hello i kliknij śledzenia filtrów:

Witaj poniższe przykłady pokazują stopki hello i kliknij śledzenia filtrów:

### <a name="footer-settings"></a>Ustawienia stopki
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a>Kliknij przycisk śledzenia
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a>Porady: Użyj SendGrid dodatkowych usług
SendGrid oferuje kilka interfejsów API i elementów webhook, których można używać tooleverage dodatkowe funkcje aplikacji Azure. Aby uzyskać więcej informacji, zobacz hello [dokumentacja interfejsu API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello hello usługi SendGrid wiadomości E-mail, wykonaj te więcej toolearn łącza.

* SendGrid C\# repozytorium biblioteki: [sendgrid csharp][sendgrid-csharp]
* Dokumentacja interfejsu API SendGrid: <https://sendgrid.com/docs>

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

