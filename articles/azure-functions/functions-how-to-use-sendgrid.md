---
title: "toouse aaaHow SendGrid w usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Pokazuje sposób toouse SendGrid w funkcji platformy Azure"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a>Jak toouse SendGrid w funkcji platformy Azure

## <a name="sendgrid-overview"></a>Omówienie SendGrid

Azure Functions obsługuje SendGrid output tooenable powiązania wiadomości e-mail toosend funkcji przy użyciu kilku wierszy kodu i konta SendGrid.

toouse API SendGrid hello w funkcji platformy Azure, musi mieć [konta SendGrid](http://SendGrid.com). Ponadto musi mieć klucz interfejsu API SendGrid. Zaloguj się za tooyour SendGrid konta i kliknij przycisk **ustawienia** następnie **klucz interfejsu API** klucza toogenerate interfejsu API. Zachowanie dostęp do tego klucza, jak używasz w nadchodzących kroku.

Wszystko jest teraz gotowy toocreate aplikacji funkcji platformy Azure.

## <a name="create-an-azure-function-app"></a>Tworzenie aplikacji funkcji platformy Azure 

Aplikacje funkcji platformy Azure są kontenerami dla co najmniej jedną funkcję platformy Azure. Środowisko Azure functions to właśnie tę — funkcja. Każdej funkcji platformy Azure jest wiązana tooone wyzwalacza jest zdarzenie, które powoduje, że toorun funkcja hello.
Każdej funkcji mogą zawierać dowolną liczbę danych wejściowych lub wyjściowych powiązania. Powiązania są usług używanych w funkcji. SendGrid jest wyjścia powiązanie, możesz użyć toosend wiadomości e-mail. 

1. Zaloguj się za toohello portalu Azure i [tworzenie aplikacji platformy Azure funkcja](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) lub Otwórz istniejącą aplikację w funkcji. 
2. Tworzenie funkcji platformy Azure. tookeep prostotę, wybierz ręczne wyzwalacza i C#. 

 ![Tworzenie funkcji platformy Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a>Konfigurowanie SendGrid do użycia w aplikacji Azure — funkcja

Klucz interfejsu API SendGrid musi być przechowywany jako toouse ustawienie aplikacji w funkcji. Hello ApiKey nie jest rzeczywista klucza interfejsu API SendGrid, ale ustawienie aplikacji definiować reprezentujące rzeczywistego klucza interfejsu API. Przechowywanie klucza w ten sposób jest zabezpieczeń, ponieważ jest oddzielony od dowolnego kodu lub pliki, które może być wyewidencjonowany do kontroli kodu źródłowego.

- Utwórz **AppSettings** klucza w aplikacji funkcji **ustawienia aplikacji**.

 ![Tworzenie funkcji platformy Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a>Skonfiguruj SendGrid powiązania danych wyjściowych

SendGrid jest dostępna jako platformy Azure funkcja powiązania wyjściowego. toocreate SendGrid powiązania wyjściowego:

1. Przejdź toohello **integracji** kartę funkcji hello w hello portalu Azure.
2. Kliknij przycisk **nowe dane wyjściowe** toocreate SendGrid powiązania wyjściowego.
3. Wypełnij hello **klucz interfejsu API** i **Nazwa parametru komunikatu** właściwości. Jeśli chcesz, możesz wprowadzić teraz hello inne właściwości lub ich zamiast tego kodu. Te ustawienia mogą być używane jako domyślne.

 ![Skonfiguruj SendGrid powiązania danych wyjściowych](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

Dodawanie funkcji tooa powiązania tworzy plik o nazwie **function.json** w folderze z funkcji. Ten plik zawiera wszystkie hello tych samych informacji, zobacz w hello Azure funkcja **integracji** karcie, ale w formacie Json formatowania. Ustawienie hello **ApiKey**, **komunikat**, i **z** pola utworzenie hello następujące wpisy w hello **function.json** pliku: 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

Jeśli wolisz, użytkownik może modyfikować tego pliku samodzielnie bezpośrednio.

Teraz, gdy zostanie utworzony i skonfigurowany hello aplikacji funkcji i funkcji, można napisać hello kodu toosend wiadomości e-mail.

## <a name="write-code-that-creates-and-sends-email"></a>Pisanie kodu, który tworzy i wysyła wiadomości e-mail

Witaj SendGrid API zawiera wszystkie hello polecenia należy toocreate i wysłać wiadomość e-mail.  

- Zastąp kod hello w funkcji hello hello następującego kodu:

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

Powiadomienie hello pierwszy wiersz zawiera hello ```#r``` dyrektywy, który odwołuje się do zestawu SendGrid hello. Następnie można użyć ```using``` toomore instrukcji łatwo uzyskiwać dostęp do obiektów hello w tej przestrzeni nazw. W kodzie hello tworzenia wystąpień ```Mail```, ```Personalization```, i ```Content``` obiektów z hello SendGrid interfejsu API, tworzące hello poczty e-mail. Po powrocie wiadomość hello SendGrid dostarcza ją. 

Witaj sygnatura funkcji zawiera również dodatkową parametru typu out ```Mail``` o nazwie ```message```. Zarówno wejściowa i wyjściowa express powiązań, same jako parametry funkcji w kodzie. 

2. Testowanie kodu, klikając **testu** i wprowadzić komunikat w hello **treść żądania** pola, a następnie klikając hello **Uruchom** przycisku.

 ![Testowanie kodu](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. Sprawdź, czy SendGrid wysyłane wiadomości e-mail hello tooverify wiadomości e-mail. Należy go toohello adresu w kodzie hello z kroku 1 i zawierać wiadomości powitania od hello **treść żądania**.

## <a name="next-steps"></a>Następne kroki
W tym artykule wykazała, jak toouse hello SendGrid usługa toocreate i wysyłania wiadomości e-mail. toolearn więcej informacji na temat przy użyciu usługi Azure Functions w aplikacjach, zobacz następujące tematy hello: 

- [Najlepsze rozwiązania dotyczące usługi Azure Functions](functions-best-practices.md) wymieniono niektóre najlepszych praktyk toouse podczas tworzenia usługi Azure Functions.

- [Dokumentacja dla deweloperów usługi Azure funkcji](functions-reference.md) programisty dokumentacja dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.

- [Testowanie usługi Azure Functions](functions-test-a-function.md) opis różnych narzędzi i technik testowania funkcji.