---
title: "Jak używać usługi poczty e-mail SendGrid (Node.js) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wysłać wiadomość e-mail z usługi poczty e-mail SendGrid na platformie Azure. Przykłady kodu napisane przy użyciu interfejsu API środowiska Node.js."
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
ms.openlocfilehash: 327cea3a24cc47a9cc463b37cc2346ebc475ef7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="dc91e-104">Sposób wysyłania poczty E-mail przy użyciu SendGrid w oprogramowaniu Node.js</span><span class="sxs-lookup"><span data-stu-id="dc91e-104">How to Send Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="dc91e-105">W tym przewodniku przedstawiono sposób wykonywania typowych zadań programowania usługi poczty e-mail SendGrid na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dc91e-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="dc91e-106">Przykłady są napisane przy użyciu interfejsu API środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="dc91e-106">The samples are written using the Node.js API.</span></span> <span data-ttu-id="dc91e-107">Omówione scenariusze obejmują **konstruowania e-mail**, **wysyłania wiadomości e-mail**, **dodawanie załączników**, **za pomocą filtrów**i **aktualizowanie właściwości**.</span><span class="sxs-lookup"><span data-stu-id="dc91e-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="dc91e-108">Aby uzyskać więcej informacji na SendGrid i wysyłania wiadomości e-mail, zobacz [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="dc91e-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="dc91e-109">Co to jest usługa SendGrid poczty E-mail?</span><span class="sxs-lookup"><span data-stu-id="dc91e-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="dc91e-110">Jest SendGrid [e-mail opartej na chmurze usługa] zapewnia niezawodne [dostarczania transakcyjnych wiadomości e-mail], skalowalności i analiz w czasie rzeczywistym oraz elastyczne interfejsów API, które umożliwiają łatwe niestandardowej integracji.</span><span class="sxs-lookup"><span data-stu-id="dc91e-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="dc91e-111">Typowe scenariusze użycia SendGrid obejmują:</span><span class="sxs-lookup"><span data-stu-id="dc91e-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="dc91e-112">Potwierdzenia są automatycznie wysyłane do klientów</span><span class="sxs-lookup"><span data-stu-id="dc91e-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="dc91e-113">Administrowanie dystrybucji wymieniono wysyłania klientów miesięczne e ulotki i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="dc91e-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="dc91e-114">Zbieranie metryk w czasie rzeczywistym dla zablokowanych poczty e-mail i czasu odpowiedzi klienta</span><span class="sxs-lookup"><span data-stu-id="dc91e-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="dc91e-115">Generowanie raportów, aby ułatwić identyfikację trendów</span><span class="sxs-lookup"><span data-stu-id="dc91e-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="dc91e-116">Zapytania dotyczące przekazywania klienta</span><span class="sxs-lookup"><span data-stu-id="dc91e-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="dc91e-117">Powiadomienia e-mail z aplikacji</span><span class="sxs-lookup"><span data-stu-id="dc91e-117">Email notifications from your application</span></span>

<span data-ttu-id="dc91e-118">Aby uzyskać więcej informacji, zobacz [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="dc91e-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="dc91e-119">Utwórz konto SendGrid</span><span class="sxs-lookup"><span data-stu-id="dc91e-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-nodejs-module"></a><span data-ttu-id="dc91e-120">Odwołanie do modułu Node.js SendGrid</span><span class="sxs-lookup"><span data-stu-id="dc91e-120">Reference the SendGrid Node.js Module</span></span>
<span data-ttu-id="dc91e-121">Moduł SendGrid dla środowiska Node.js może być instalowane za pośrednictwem węzeł Menedżera pakietów (npm) przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="dc91e-121">The SendGrid module for Node.js can be installed through the node package manager (npm) by using the following command:</span></span>

    npm install sendgrid

<span data-ttu-id="dc91e-122">Po zakończeniu instalacji można wymagać modułu w aplikacji przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="dc91e-122">After installation, you can require the module in your application by using the following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="dc91e-123">Eksportuje modułu SendGrid **SendGrid** i **E-mail** funkcji.</span><span class="sxs-lookup"><span data-stu-id="dc91e-123">The SendGrid module exports the **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="dc91e-124">**SendGrid** jest odpowiedzialny za wysyłanie poczty e-mail za pośrednictwem interfejsu API sieci Web, podczas gdy **E-mail** hermetyzuje wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="dc91e-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="dc91e-125">Porady: Tworzenie wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="dc91e-125">How to: Create an Email</span></span>
<span data-ttu-id="dc91e-126">Tworzenie wiadomości e-mail przy użyciu modułu SendGrid obejmuje najpierw Tworzenie wiadomości e-mail przy użyciu funkcji poczty E-mail, a następnie wysyła je przy użyciu funkcji SendGrid.</span><span class="sxs-lookup"><span data-stu-id="dc91e-126">Creating an email message using the SendGrid module involves first creating an email message using the Email function, and then sending it using the SendGrid function.</span></span> <span data-ttu-id="dc91e-127">Poniżej przedstawiono przykład tworzenia nowej wiadomości przy użyciu funkcji poczty E-mail:</span><span class="sxs-lookup"><span data-stu-id="dc91e-127">The following is an example of creating a new message using the Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="dc91e-128">Można również określić wiadomości w formacie HTML dla klientów obsługujących go przez ustawienie właściwości html.</span><span class="sxs-lookup"><span data-stu-id="dc91e-128">You can also specify an HTML message for clients that support it by setting the html property.</span></span> <span data-ttu-id="dc91e-129">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="dc91e-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="dc91e-130">Ustawianie właściwości tekst i html zapewnia płynne powrotu do zawartości tekstowej dla klientów, które nie obsługują wiadomości w formacie HTML.</span><span class="sxs-lookup"><span data-stu-id="dc91e-130">Setting both the text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="dc91e-131">Aby uzyskać więcej informacji na wszystkie właściwości obsługiwane przez funkcję poczty E-mail, zobacz [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="dc91e-131">For more information on all properties supported by the Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="dc91e-132">Porady: wysyłanie wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="dc91e-132">How to: Send an Email</span></span>
<span data-ttu-id="dc91e-133">Po utworzeniu wiadomości e-mail przy użyciu funkcji poczty E-mail, możesz wysłać go za pomocą interfejsu API sieci Web udostępniane przez włączenie.</span><span class="sxs-lookup"><span data-stu-id="dc91e-133">After creating an email message using the Email function, you can send it using the Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="dc91e-134">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="dc91e-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="dc91e-135">Gdy w powyższych przykładach pokazano przekazywanie w funkcji i wywołanie zwrotne obiektu poczty e-mail, można również bezpośrednio wywołanie funkcji wysyłania bezpośrednio, określając właściwości wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="dc91e-135">While the above examples show passing in an email object and callback function, you can also directly invoke the send function by directly specifying email properties.</span></span> <span data-ttu-id="dc91e-136">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="dc91e-136">For example:</span></span>  
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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="dc91e-137">Porady: Dodawanie załącznika</span><span class="sxs-lookup"><span data-stu-id="dc91e-137">How to: Add an Attachment</span></span>
<span data-ttu-id="dc91e-138">Można dodawać załączników do wiadomości przez określenie nazwy pliku i ścieżki w **pliki** właściwości.</span><span class="sxs-lookup"><span data-stu-id="dc91e-138">Attachments can be added to a message by specifying the file name(s) and path(s) in the **files** property.</span></span> <span data-ttu-id="dc91e-139">W poniższym przykładzie pokazano, wysyłania załącznika:</span><span class="sxs-lookup"><span data-stu-id="dc91e-139">The following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used to specify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="dc91e-140">Korzystając z **pliki** właściwości, plik musi być dostępny za pośrednictwem [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="dc91e-140">When using the **files** property, the file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="dc91e-141">Jeśli chcesz dołączyć plik znajduje się w usłudze Azure Storage, taki jak kontenera obiektów Blob, należy najpierw skopiować plik do lokalnej pamięci masowej lub dysku platformy Azure przed mógł zostać wysłany jako załącznik przy użyciu **pliki** właściwości.</span><span class="sxs-lookup"><span data-stu-id="dc91e-141">If the file you wish to attach is hosted in Azure Storage, such as in a Blob container, you must first copy the file to local storage or to an Azure drive before it can be sent as an attachment using the **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-to-enable-footers-and-tracking"></a><span data-ttu-id="dc91e-142">Porady: należy używać filtrów do śledzenia i Włącz stopek</span><span class="sxs-lookup"><span data-stu-id="dc91e-142">How to: Use Filters to Enable Footers and Tracking</span></span>
<span data-ttu-id="dc91e-143">SendGrid udostępnia funkcje dodatkowe poczty e-mail przy użyciu filtrów.</span><span class="sxs-lookup"><span data-stu-id="dc91e-143">SendGrid provides additional email functionality through the use of filters.</span></span> <span data-ttu-id="dc91e-144">Są to ustawienia, które mogą zostać dodane do wiadomości e-mail, aby włączyć określonych funkcji, takich jak włączenie kliknij śledzenia, Google analytics, subskrypcji, śledzenia i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="dc91e-144">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="dc91e-145">Aby uzyskać pełną listę filtrów, zobacz [ustawienia filtru][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="dc91e-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="dc91e-146">Filtry można stosować do wiadomości, przy użyciu **filtry** właściwości.</span><span class="sxs-lookup"><span data-stu-id="dc91e-146">Filters can be applied to a message by using the **filters** property.</span></span>
<span data-ttu-id="dc91e-147">Każdy filtr jest określany przez skrót zawierający ustawienia specyficzne dla filtru.</span><span class="sxs-lookup"><span data-stu-id="dc91e-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="dc91e-148">Poniższe przykłady pokazują, stopka i kliknij przycisk śledzenia filtrów:</span><span class="sxs-lookup"><span data-stu-id="dc91e-148">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="dc91e-149">Stopki</span><span class="sxs-lookup"><span data-stu-id="dc91e-149">Footer</span></span>
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

### <a name="click-tracking"></a><span data-ttu-id="dc91e-150">Kliknij przycisk śledzenia</span><span class="sxs-lookup"><span data-stu-id="dc91e-150">Click Tracking</span></span>
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

## <a name="how-to-update-email-properties"></a><span data-ttu-id="dc91e-151">Porady: aktualizowanie właściwości wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="dc91e-151">How to: Update Email Properties</span></span>
<span data-ttu-id="dc91e-152">Niektóre właściwości wiadomości e-mail może zostać zastąpiona przy użyciu * *ustawić*właściwości*** lub dołączonych za pomocą * *dodać*właściwości***.</span><span class="sxs-lookup"><span data-stu-id="dc91e-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="dc91e-153">Na przykład można dodać dodatkowych adresatów za pomocą</span><span class="sxs-lookup"><span data-stu-id="dc91e-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="dc91e-154">lub ustawić filtr przy użyciu</span><span class="sxs-lookup"><span data-stu-id="dc91e-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="dc91e-155">Aby uzyskać więcej informacji, zobacz [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="dc91e-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="dc91e-156">Porady: Użyj SendGrid dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="dc91e-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="dc91e-157">SendGrid oferuje opartych na sieci web interfejsów API, które można wykorzystać dodatkowe funkcje włączenie w aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dc91e-157">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="dc91e-158">Aby uzyskać szczegółowe informacje, zobacz [dokumentacji interfejsu API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="dc91e-158">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc91e-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dc91e-159">Next Steps</span></span>
<span data-ttu-id="dc91e-160">Teraz, kiedy znasz już podstawy usługi poczty E-mail SendGrid, skorzystaj z poniższych linków, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="dc91e-160">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="dc91e-161">Repozytorium modułu SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="dc91e-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="dc91e-162">Dokumentacja interfejsu API SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="dc91e-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="dc91e-163">Oferta specjalna SendGrid dla klientów platformy Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="dc91e-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
<span data-ttu-id="dc91e-164">[Usługa poczty e-mail hostowanego w chmurze]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="dc91e-164">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="dc91e-165">[dostarczanie transakcyjnych wiadomości e-mail]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="dc91e-165">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
