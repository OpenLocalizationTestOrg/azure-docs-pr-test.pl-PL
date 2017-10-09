---
title: "Witaj toouse aaaHow SendGrid usługa poczty e-mail (Node.js) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wysłać wiadomość e-mail z hello SendGrid usługa poczty e-mail na platformie Azure. Przykłady kodu napisane przy użyciu hello interfejsu API środowiska Node.js."
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="298be-104">Jak tooSend SendGrid za pomocą poczty E-mail w oprogramowaniu Node.js</span><span class="sxs-lookup"><span data-stu-id="298be-104">How tooSend Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="298be-105">W tym przewodniku pokazano, jak tooperform typowych zadań programowania SendGrid poczty e-mail usługi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="298be-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="298be-106">Hello przykłady są napisane przy użyciu hello interfejsu API środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="298be-106">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="298be-107">Witaj omówione scenariusze obejmują **konstruowania e-mail**, **wysyłania wiadomości e-mail**, **dodawanie załączników**, **za pomocą filtrów**i **aktualizowanie właściwości**.</span><span class="sxs-lookup"><span data-stu-id="298be-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="298be-108">Aby uzyskać więcej informacji na SendGrid i wysyłania wiadomości e-mail, zobacz hello [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="298be-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="298be-109">Co to jest hello SendGrid usługa poczty E-mail?</span><span class="sxs-lookup"><span data-stu-id="298be-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="298be-110">Jest SendGrid [e-mail opartej na chmurze usługa] zapewnia niezawodne [dostarczania transakcyjnych wiadomości e-mail], skalowalności i analiz w czasie rzeczywistym oraz elastyczne interfejsów API, które umożliwiają łatwe niestandardowej integracji.</span><span class="sxs-lookup"><span data-stu-id="298be-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="298be-111">Typowe scenariusze użycia SendGrid obejmują:</span><span class="sxs-lookup"><span data-stu-id="298be-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="298be-112">Nie są automatycznie wysyłane potwierdzenia toocustomers</span><span class="sxs-lookup"><span data-stu-id="298be-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="298be-113">Administrowanie dystrybucji wymieniono wysyłania klientów miesięczne e ulotki i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="298be-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="298be-114">Zbieranie metryk w czasie rzeczywistym dla zablokowanych poczty e-mail i czasu odpowiedzi klienta</span><span class="sxs-lookup"><span data-stu-id="298be-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="298be-115">Generowanie raportów toohelp trendów</span><span class="sxs-lookup"><span data-stu-id="298be-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="298be-116">Zapytania dotyczące przekazywania klienta</span><span class="sxs-lookup"><span data-stu-id="298be-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="298be-117">Powiadomienia e-mail z aplikacji</span><span class="sxs-lookup"><span data-stu-id="298be-117">Email notifications from your application</span></span>

<span data-ttu-id="298be-118">Aby uzyskać więcej informacji, zobacz [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="298be-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="298be-119">Utwórz konto SendGrid</span><span class="sxs-lookup"><span data-stu-id="298be-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a><span data-ttu-id="298be-120">Odwołanie hello SendGrid Node.js modułu</span><span class="sxs-lookup"><span data-stu-id="298be-120">Reference hello SendGrid Node.js Module</span></span>
<span data-ttu-id="298be-121">Moduł SendGrid Hello node.js można zainstalować za pomocą Menedżera pakietów hello węzła (npm) za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="298be-121">hello SendGrid module for Node.js can be installed through hello node package manager (npm) by using hello following command:</span></span>

    npm install sendgrid

<span data-ttu-id="298be-122">Po zakończeniu instalacji można wymagać modułu hello w aplikacji przy użyciu hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="298be-122">After installation, you can require hello module in your application by using hello following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="298be-123">Moduł SendGrid Hello eksportuje hello **SendGrid** i **E-mail** funkcji.</span><span class="sxs-lookup"><span data-stu-id="298be-123">hello SendGrid module exports hello **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="298be-124">**SendGrid** jest odpowiedzialny za wysyłanie poczty e-mail za pośrednictwem interfejsu API sieci Web, podczas gdy **E-mail** hermetyzuje wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="298be-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="298be-125">Porady: Tworzenie wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="298be-125">How to: Create an Email</span></span>
<span data-ttu-id="298be-126">Tworzenie wiadomości e-mail przy użyciu modułu SendGrid hello obejmuje najpierw Tworzenie wiadomości e-mail przy użyciu funkcji poczty E-mail hello, a następnie wysyła je przy użyciu funkcji SendGrid hello.</span><span class="sxs-lookup"><span data-stu-id="298be-126">Creating an email message using hello SendGrid module involves first creating an email message using hello Email function, and then sending it using hello SendGrid function.</span></span> <span data-ttu-id="298be-127">Hello poniżej przedstawiono przykład tworzenia nowej wiadomości przy użyciu funkcji poczty E-mail hello:</span><span class="sxs-lookup"><span data-stu-id="298be-127">hello following is an example of creating a new message using hello Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="298be-128">W przypadku klientów obsługujących go przez ustawienie właściwości html hello, można również określić wiadomości w formacie HTML.</span><span class="sxs-lookup"><span data-stu-id="298be-128">You can also specify an HTML message for clients that support it by setting hello html property.</span></span> <span data-ttu-id="298be-129">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="298be-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="298be-130">Ustawianie właściwości zarówno hello tekst i html udostępnia bezpieczne powrotu do zawartości tekstowej dla klientów, które nie obsługują wiadomości w formacie HTML.</span><span class="sxs-lookup"><span data-stu-id="298be-130">Setting both hello text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="298be-131">Aby uzyskać więcej informacji na wszystkie właściwości obsługiwanych przez hello funkcji poczty E-mail, zobacz [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="298be-131">For more information on all properties supported by hello Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="298be-132">Porady: wysyłanie wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="298be-132">How to: Send an Email</span></span>
<span data-ttu-id="298be-133">Po utworzeniu wiadomość e-mail przy użyciu hello funkcji poczty E-mail, możesz wysłać go za pomocą hello udostępniane przez włączenie interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="298be-133">After creating an email message using hello Email function, you can send it using hello Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="298be-134">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="298be-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="298be-135">Gdy hello powyżej przykłady Pokaż przekazywanie w funkcji i wywołanie zwrotne obiektu poczty e-mail, można również bezpośrednio wywołanie funkcji wysyłania hello, bezpośrednio, określając właściwości wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="298be-135">While hello above examples show passing in an email object and callback function, you can also directly invoke hello send function by directly specifying email properties.</span></span> <span data-ttu-id="298be-136">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="298be-136">For example:</span></span>  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="298be-137">Porady: Dodawanie załącznika</span><span class="sxs-lookup"><span data-stu-id="298be-137">How to: Add an Attachment</span></span>
<span data-ttu-id="298be-138">Załączniki do dodania komunikatu tooa określając hello nazwy pliku i ścieżki w hello **pliki** właściwości.</span><span class="sxs-lookup"><span data-stu-id="298be-138">Attachments can be added tooa message by specifying hello file name(s) and path(s) in hello **files** property.</span></span> <span data-ttu-id="298be-139">Witaj poniższy przykład przedstawia wysyłania załącznika:</span><span class="sxs-lookup"><span data-stu-id="298be-139">hello following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="298be-140">Korzystając z hello **pliki** właściwość, musi być dostępny za pośrednictwem pliku hello [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="298be-140">When using hello **files** property, hello file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="298be-141">Jeśli chcesz tooattach pliku hello znajduje się w usłudze Azure Storage, taki jak kontenera obiektów Blob, należy najpierw skopiować toolocal magazynem hello lub tooan Azure dysku zanim będzie można wysłać jako załącznik przy użyciu hello **pliki** właściwości.</span><span class="sxs-lookup"><span data-stu-id="298be-141">If hello file you wish tooattach is hosted in Azure Storage, such as in a Blob container, you must first copy hello file toolocal storage or tooan Azure drive before it can be sent as an attachment using hello **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a><span data-ttu-id="298be-142">Porady: Użyj filtrów stopki tooEnable i śledzenia</span><span class="sxs-lookup"><span data-stu-id="298be-142">How to: Use Filters tooEnable Footers and Tracking</span></span>
<span data-ttu-id="298be-143">SendGrid udostępnia funkcje dodatkowe poczty e-mail za pośrednictwem hello korzystania z filtrów.</span><span class="sxs-lookup"><span data-stu-id="298be-143">SendGrid provides additional email functionality through hello use of filters.</span></span> <span data-ttu-id="298be-144">Są to ustawienia, które można dodać tooan wiadomości e-mail, aby włączyć określonych funkcji, np. włączenie kliknij śledzenia, Google analytics, subskrypcji śledzenia, i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="298be-144">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="298be-145">Aby uzyskać pełną listę filtrów, zobacz [ustawienia filtru][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="298be-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="298be-146">Filtry mogą być zastosowane tooa wiadomości przy użyciu hello **filtry** właściwości.</span><span class="sxs-lookup"><span data-stu-id="298be-146">Filters can be applied tooa message by using hello **filters** property.</span></span>
<span data-ttu-id="298be-147">Każdy filtr jest określany przez skrót zawierający ustawienia specyficzne dla filtru.</span><span class="sxs-lookup"><span data-stu-id="298be-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="298be-148">Witaj poniższe przykłady pokazują stopki hello i kliknij śledzenia filtrów:</span><span class="sxs-lookup"><span data-stu-id="298be-148">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="298be-149">Stopki</span><span class="sxs-lookup"><span data-stu-id="298be-149">Footer</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a><span data-ttu-id="298be-150">Kliknij przycisk śledzenia</span><span class="sxs-lookup"><span data-stu-id="298be-150">Click Tracking</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a><span data-ttu-id="298be-151">Porady: aktualizowanie właściwości wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="298be-151">How to: Update Email Properties</span></span>
<span data-ttu-id="298be-152">Niektóre właściwości wiadomości e-mail może zostać zastąpiona przy użyciu  **ustawić*właściwości*** lub dołączonych za pomocą  **dodać*właściwości***.</span><span class="sxs-lookup"><span data-stu-id="298be-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="298be-153">Na przykład można dodać dodatkowych adresatów za pomocą</span><span class="sxs-lookup"><span data-stu-id="298be-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="298be-154">lub ustawić filtr przy użyciu</span><span class="sxs-lookup"><span data-stu-id="298be-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="298be-155">Aby uzyskać więcej informacji, zobacz [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="298be-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="298be-156">Porady: Użyj SendGrid dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="298be-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="298be-157">SendGrid oferuje API sieci web z aplikacji platformy Azure można dodatkowe funkcje SendGrid tooleverage.</span><span class="sxs-lookup"><span data-stu-id="298be-157">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="298be-158">Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="298be-158">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="298be-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="298be-159">Next Steps</span></span>
<span data-ttu-id="298be-160">Teraz, kiedy znasz już podstawy hello hello usługi SendGrid wiadomości E-mail, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="298be-160">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="298be-161">Repozytorium modułu SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="298be-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="298be-162">Dokumentacja interfejsu API SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="298be-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="298be-163">Oferta specjalna SendGrid dla klientów platformy Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="298be-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[e-mail opartej na chmurze usługa]: https://sendgrid.com/email-solutions
[dostarczania transakcyjnych wiadomości e-mail]: https://sendgrid.com/transactional-email
