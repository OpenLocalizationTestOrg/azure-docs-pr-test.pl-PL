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
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a>Jak tooSend SendGrid za pomocą poczty E-mail w oprogramowaniu Node.js
W tym przewodniku pokazano, jak tooperform typowych zadań programowania SendGrid poczty e-mail usługi na platformie Azure. Hello przykłady są napisane przy użyciu hello interfejsu API środowiska Node.js. Witaj omówione scenariusze obejmują **konstruowania e-mail**, **wysyłania wiadomości e-mail**, **dodawanie załączników**, **za pomocą filtrów**i **aktualizowanie właściwości**. Aby uzyskać więcej informacji na SendGrid i wysyłania wiadomości e-mail, zobacz hello [następne kroki](#next-steps) sekcji.

## <a name="what-is-hello-sendgrid-email-service"></a>Co to jest hello SendGrid usługa poczty E-mail?
Jest SendGrid [e-mail opartej na chmurze usługa] zapewnia niezawodne [dostarczania transakcyjnych wiadomości e-mail], skalowalności i analiz w czasie rzeczywistym oraz elastyczne interfejsów API, które umożliwiają łatwe niestandardowej integracji. Typowe scenariusze użycia SendGrid obejmują:

* Nie są automatycznie wysyłane potwierdzenia toocustomers
* Administrowanie dystrybucji wymieniono wysyłania klientów miesięczne e ulotki i oferty specjalne
* Zbieranie metryk w czasie rzeczywistym dla zablokowanych poczty e-mail i czasu odpowiedzi klienta
* Generowanie raportów toohelp trendów
* Zapytania dotyczące przekazywania klienta
* Powiadomienia e-mail z aplikacji

Aby uzyskać więcej informacji, zobacz [https://sendgrid.com](https://sendgrid.com).

## <a name="create-a-sendgrid-account"></a>Utwórz konto SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a>Odwołanie hello SendGrid Node.js modułu
Moduł SendGrid Hello node.js można zainstalować za pomocą Menedżera pakietów hello węzła (npm) za pomocą następującego polecenia hello:

    npm install sendgrid

Po zakończeniu instalacji można wymagać modułu hello w aplikacji przy użyciu hello następującego kodu:

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

Moduł SendGrid Hello eksportuje hello **SendGrid** i **E-mail** funkcji.
**SendGrid** jest odpowiedzialny za wysyłanie poczty e-mail za pośrednictwem interfejsu API sieci Web, podczas gdy **E-mail** hermetyzuje wiadomości e-mail.

## <a name="how-to-create-an-email"></a>Porady: Tworzenie wiadomości E-mail
Tworzenie wiadomości e-mail przy użyciu modułu SendGrid hello obejmuje najpierw Tworzenie wiadomości e-mail przy użyciu funkcji poczty E-mail hello, a następnie wysyła je przy użyciu funkcji SendGrid hello. Hello poniżej przedstawiono przykład tworzenia nowej wiadomości przy użyciu funkcji poczty E-mail hello:

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

W przypadku klientów obsługujących go przez ustawienie właściwości html hello, można również określić wiadomości w formacie HTML. Na przykład:

    html: This is a sample <b>HTML<b> email message.

Ustawianie właściwości zarówno hello tekst i html udostępnia bezpieczne powrotu do zawartości tekstowej dla klientów, które nie obsługują wiadomości w formacie HTML.

Aby uzyskać więcej informacji na wszystkie właściwości obsługiwanych przez hello funkcji poczty E-mail, zobacz [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-send-an-email"></a>Porady: wysyłanie wiadomości E-mail
Po utworzeniu wiadomość e-mail przy użyciu hello funkcji poczty E-mail, możesz wysłać go za pomocą hello udostępniane przez włączenie interfejsu API sieci Web. 

### <a name="web-api"></a>Interfejs API sieci Web
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> Gdy hello powyżej przykłady Pokaż przekazywanie w funkcji i wywołanie zwrotne obiektu poczty e-mail, można również bezpośrednio wywołanie funkcji wysyłania hello, bezpośrednio, określając właściwości wiadomości e-mail. Na przykład:  
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

## <a name="how-to-add-an-attachment"></a>Porady: Dodawanie załącznika
Załączniki do dodania komunikatu tooa określając hello nazwy pliku i ścieżki w hello **pliki** właściwości. Witaj poniższy przykład przedstawia wysyłania załącznika:

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
> Korzystając z hello **pliki** właściwość, musi być dostępny za pośrednictwem pliku hello [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile). Jeśli chcesz tooattach pliku hello znajduje się w usłudze Azure Storage, taki jak kontenera obiektów Blob, należy najpierw skopiować toolocal magazynem hello lub tooan Azure dysku zanim będzie można wysłać jako załącznik przy użyciu hello **pliki** właściwości.
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a>Porady: Użyj filtrów stopki tooEnable i śledzenia
SendGrid udostępnia funkcje dodatkowe poczty e-mail za pośrednictwem hello korzystania z filtrów. Są to ustawienia, które można dodać tooan wiadomości e-mail, aby włączyć określonych funkcji, np. włączenie kliknij śledzenia, Google analytics, subskrypcji śledzenia, i tak dalej. Aby uzyskać pełną listę filtrów, zobacz [ustawienia filtru][Filter Settings].

Filtry mogą być zastosowane tooa wiadomości przy użyciu hello **filtry** właściwości.
Każdy filtr jest określany przez skrót zawierający ustawienia specyficzne dla filtru.
Witaj poniższe przykłady pokazują stopki hello i kliknij śledzenia filtrów:

### <a name="footer"></a>Stopki
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

### <a name="click-tracking"></a>Kliknij przycisk śledzenia
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

## <a name="how-to-update-email-properties"></a>Porady: aktualizowanie właściwości wiadomości E-mail
Niektóre właściwości wiadomości e-mail może zostać zastąpiona przy użyciu  **ustawić*właściwości*** lub dołączonych za pomocą  **dodać*właściwości***. Na przykład można dodać dodatkowych adresatów za pomocą

    email.addTo('jeff@contoso.com');

lub ustawić filtr przy użyciu

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

Aby uzyskać więcej informacji, zobacz [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-use-additional-sendgrid-services"></a>Porady: Użyj SendGrid dodatkowych usług
SendGrid oferuje API sieci web z aplikacji platformy Azure można dodatkowe funkcje SendGrid tooleverage. Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello hello usługi SendGrid wiadomości E-mail, wykonaj te więcej toolearn łącza.

* Repozytorium modułu SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]
* Dokumentacja interfejsu API SendGrid: <https://sendgrid.com/docs>
* Oferta specjalna SendGrid dla klientów platformy Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[e-mail opartej na chmurze usługa]: https://sendgrid.com/email-solutions
[dostarczania transakcyjnych wiadomości e-mail]: https://sendgrid.com/transactional-email
