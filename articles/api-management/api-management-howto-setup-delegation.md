---
title: "aaaHow toodelegate użytkownika rejestracji i produktu subskrypcji"
description: "Dowiedz się, jak toodelegate użytkownika rejestracji i produktu subskrypcji tooa innej firmy w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>Jak toodelegate użytkownika rejestracji i produktu subskrypcji
Delegowanie pozwala toouse istniejącej witryny sieci Web do obsługi tooproducts logowania — w/tworzenia konta i subskrypcji dewelopera jako przeciwieństwie toousing hello wbudowanej funkcji w portalu dla deweloperów hello. To umożliwia dane użytkowników hello tooown witryny sieci Web i sprawdzania poprawności hello tych kroków w niestandardowy sposób.

## <a name="delegate-signin-up"></a>Developer delegowanie logowania i rejestrowania
toodelegate developer tooyour logowania i rejestrowania istniejącej witryny sieci Web w swojej witrynie, który działa jako punkt wejścia dla takiego żądania inicjowanych z poziomu portalu dla deweloperów usługi API Management hello hello konieczne będzie toocreate punktu końcowego specjalne delegowania.

Hello końcowego przepływ pracy będzie wyglądać następująco:

1. Deweloper kliknie łącze logowania lub zapisywania hello na powitania portalu dla deweloperów zarządzanie interfejsami API
2. Przeglądarka jest punkt końcowy delegowania toohello przekierowane
3. Punkt końcowy delegowania w zamian przekierowuje tooor przedstawia interfejsu użytkownika pytaniem, czy użytkownik toosign w lub zapisywania
4. W przypadku powodzenia hello użytkownik jest przekierowane toohello wstecz zarządzanie interfejsami API developer strony portalu uruchomienia z

toobegin, umożliwia pierwszy Konfiguracja interfejsu API zarządzania tooroute żądań za pośrednictwem punktu końcowego delegowania. W portalu wydawcy zarządzanie interfejsami API hello, kliknij polecenie **zabezpieczeń** , a następnie kliknij przycisk hello **delegowania** kartę. Kliknij przycisk tooenable wyboru hello "Delegate logowania & rejestracji".

![Strony delegowania][api-management-delegation-signin-up]

* Zdecyduj, co hello adres URL punktu końcowego specjalne delegowania zostanie i wprowadź go w hello **adres URL punktu końcowego delegowania** pola. 
* W ramach hello **klucz uwierzytelniania delegowania** polu Wprowadź hasło, które będzie używane toocompute tooyou podpisu podane dla tooensure weryfikacji, który hello żądania jest rzeczywiście pochodzi z usługi Azure API Management. Możesz kliknąć hello **Generowanie** toohave przycisk interfejsu API zarządzania losowego generowania klucza dla Ciebie.

Teraz należy toocreate hello **punktu końcowego delegowania**. Tooperform ma wiele akcji:

1. Otrzyma żądanie w hello następującej postaci:
   
   > *http://www.yourwebsite.com/apimdelegation?Operation=SignIn&returnUrl= {adres URL strony źródła} & soli = {ciąg} & sig = {ciąg}*
   > 
   > 
   
    Parametry zapytania w przypadku logowania / tworzenia konta hello:
   
   * **Operacja**: Określa jaki typ żądania delegowania jest — może być tylko **SignIn** w takim przypadku
   * **returnUrl**: hello adres URL strony hello gdzie hello użytkownik kliknął link logowania lub zapisywania
   * **ziarna**: specjalne ciąg zaburzający używane do obliczania skrótu zabezpieczeń
   * **SIG**: obliczona zabezpieczeń toobe wyznaczania wartości skrótu, używany do porównania tooyour własnych obliczoną wartość mieszania
2. Sprawdź, czy Żądanie hello pochodzi z usługi Azure API Management (opcjonalne, lecz zdecydowanie zalecane dla zabezpieczeń)
   
   * Obliczeniowe skrótu HMAC SHA512 ciągu oparte na powitania **returnUrl** i **soli** parametry zapytania ([przykładowy kod podany poniżej]):
     
     > Metoda HMAC (**soli** + "\n" + **returnUrl**)
     > 
     > 
   * Porównaj wartości toohello obliczonego powyżej skrótu hello hello **sig** parametr zapytania. Jeśli skróty dwóch hello są zgodne, przesuń w następnym kroku toohello, w przeciwnym razie odmowy żądania hello.
3. Sprawdź, czy otrzymują żądanie logowania w/logowania — w górę: hello **operacji** parametru zapytania zostanie ustawiona zbyt "**SignIn**".
4. Obecny użytkownik hello przy użyciu interfejsu użytkownika w toosign lub zapisywania
5. Jeśli użytkownik hello jest zarejestrowanie się masz toocreate odpowiadającego mu konta dla nich w usłudze API Management. [Utwórz użytkownika] z hello interfejsu API REST zarządzania interfejsu API. Po tej czynności upewnij się, ustaw toohello identyfikator użytkownika hello, takie same, który znajduje się w magazynie użytkownika lub identyfikator tooan, który użytkownik może przechowywać ścieżkę.
6. Gdy hello pomyślnego uwierzytelnienia użytkownika:
   
   * [żądania tokenu (rejestracji jednokrotnej SSO) single-sign-on] za pośrednictwem hello interfejsu API REST zarządzania interfejsu API
   * Dołącz returnUrl toohello parametru zapytania URL logowania jednokrotnego otrzymany z powyższego wywołania hello interfejsu API:
     
     > https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url np. 
     > 
     > 
   * adres URL utworzony przekierowania hello użytkownika toohello powyżej

W dodatku toohello **SignIn** operacji, można również wykonywać Zarządzanie kontami po poprzednich kroków hello i przy użyciu jednej z hello następujące operacje.

* **Element ChangePassword**
* **ChangeProfile**
* **CloseAccount**

Należy podać następujące parametry zapytania dla operacji zarządzania kontem hello.

* **Operacja**: Określa typ żądania delegowania jest (Element ChangePassword, ChangeProfile lub CloseAccount)
* **Identyfikator userId**: identyfikator użytkownika hello hello toomanage konta
* **ziarna**: specjalne ciąg zaburzający używane do obliczania skrótu zabezpieczeń
* **SIG**: obliczona zabezpieczeń toobe wyznaczania wartości skrótu, używany do porównania tooyour własnych obliczoną wartość mieszania

## <a name="delegate-product-subscription"></a>Delegowanie subskrypcji produktu
Delegowanie subskrypcji produktu działa podobnie toodelegating użytkownika logowania/w górę. Witaj końcowego przepływu pracy, należy w następujący sposób:

1. Deweloper wybiera produktu w portalu dla deweloperów usługi API Management hello i kliknie przycisk Subskrybuj hello
2. Przeglądarka jest punkt końcowy delegowania toohello przekierowane
3. Punkt końcowy delegowania wykonuje kroki subskrypcji produktu wymagane — to jest uruchomiony tooyou i może pociągać za sobą przekierowania toorequest strony tooanother informacji dotyczących rozliczeń, prosząc dodatkowych pytań lub hello informacje są przechowywane po prostu i nie wymaga żadnych działań użytkownika

Funkcje hello tooenable, na powitania **delegowania** kliknij **delegować subskrypcji produktu**.

Następnie upewnij się, że punkt końcowy delegowania hello wykonuje hello następujące akcje:

1. Otrzyma żądanie w hello następującej postaci:
   
   > *{Operacja} http://www.yourwebsite.com/apimdelegation?Operation= & productId = {toosubscribe produktu do} & userId = {użytkownika zgłaszającego żądanie} & ziarna = {ciąg} & sig = {ciąg}*
   > 
   > 
   
    Parametry zapytania w przypadku subskrypcji produktu hello:
   
   * **Operacja**: Określa, jakiego typu żądanie delegowania jest. Dla subskrypcji produktu żądań hello prawidłowe opcje to:
     * "Subskrypcji": toosubscribe żądania hello tooa użytkownika danego produktu o podany identyfikator (patrz poniżej)
     * "Anuluj subskrypcję": toounsubscribe żądań użytkowników z produktu
     * "Odnowić": toorenew requst subskrypcją (np. może być wygasa)
   * **productId**: toosubscribe do żądany identyfikator hello hello produktu hello użytkownika
   * **Identyfikator userId**: hello identyfikator hello użytkownika, dla którego hello żądań
   * **ziarna**: specjalne ciąg zaburzający używane do obliczania skrótu zabezpieczeń
   * **SIG**: obliczona zabezpieczeń toobe wyznaczania wartości skrótu, używany do porównania tooyour własnych obliczoną wartość mieszania
2. Sprawdź, czy Żądanie hello pochodzi z usługi Azure API Management (opcjonalne, lecz zdecydowanie zalecane dla zabezpieczeń)
   
   * Obliczeniowe SHA512 HMAC ciągu oparte na powitania **productId**, **userId** i **soli** parametry zapytania:
     
     > Metoda HMAC (**soli** + "\n" + **productId** + "\n" + **userId**)
     > 
     > 
   * Porównaj wartości toohello obliczonego powyżej skrótu hello hello **sig** parametr zapytania. Jeśli skróty dwóch hello są zgodne, przesuń w następnym kroku toohello, w przeciwnym razie odmowy żądania hello.
3. Przetwarzania żadnych subskrypcji produktu oparty na typie hello operacji w **operacji** -np. rozliczeń, dalsze pytania itp.
4. W subskrypcji pomyślnie hello użytkownika toohello produktu na Twojej stronie, subskrypcja hello użytkownika toohello interfejsu API produktów do zarządzania przez [hello wywołania interfejsu API REST dla subskrypcji produktu].

## <a name="delegate-example-code"></a> Przykładowy kod
Pokaż przykłady te kodu jak tootake hello *klucz sprawdzania poprawności delegowania*, który wynosi hello delegowania ekranie powitania wydawcy portalu, toocreate HMAC, który jest następnie używany toovalidate hello podpisu, co dowodzi hello ważności hello przekazany returnUrl. Witaj, sam kod działa hello productId i userId nieznaczne modyfikacji.

**C# kodu toogenerate skrót returnUrl**

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

**Skrót toogenerate kodu NodeJS returnUrl**

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na delegowania Zobacz powitania po wideo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[żądania tokenu (rejestracji jednokrotnej SSO) single-sign-on]: http://go.microsoft.com/fwlink/?LinkId=507409
[Utwórz użytkownika]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[hello wywołania interfejsu API REST dla subskrypcji produktu]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[przykładowy kod podany poniżej]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
