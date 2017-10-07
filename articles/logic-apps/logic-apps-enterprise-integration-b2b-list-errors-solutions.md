---
title: "Logiki aplikacji B2B listę błędów i rozwiązania: usługi Azure App Service | Dokumentacja firmy Microsoft"
description: "Logiki aplikacji B2B listę błędów i rozwiązania"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Logiki aplikacji B2B listę błędów i rozwiązania  
Ten artykuł pomaga rozwiązywania problemów, które może się tak dziać w scenariusze B2B aplikacji logiki, a także sugeruje odpowiednie działania w przypadku naprawiania te błędy.


## <a name="agreement-resolution"></a>Rozdzielczość umowy

### <a name="no-agreement-found"></a>* Nie znaleziono umowę. 

|   |   |  
|---|---|
| Opis błędu | Nie znaleziono z parametrami rozpoznawania umowy umowę.|    
| Akcja użytkownika | Umowa Hello powinny zostać dodane toohello konta integracji z tożsamości firm uzgodnione.</br> tożsamości firm Hello powinna być zgodna toohello komunikat wejściowy identyfikatorów|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>* Nie znaleziono z tożsamościami umowę.

|   |   | 
|---|---|
| Opis błędu | Nie znaleziono z tożsamościami umowę: "AS2Identity":: "Partner1" i "AS2Identity":: "Partner3"| 
| Akcja użytkownika | Nieprawidłowy AS2-z lub AS2-tooconfigured umowy. </br> Komunikatów AS2 AS2-z lub identyfikatory toomatch AS2 AS2 tooheaders lub umowy w AS2 komunikatu nagłówków z konfiguracjami umowy |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>* Brak AS2 nagłówki komunikatów  

|   |   |  
|---|---|
| Opis błędu| Nieprawidłowy nagłówek AS2. Jedną z "AS2 — do" lub "AS2 — od" nagłówki są puste| 
| Akcja użytkownika | Odebrano komunikat AS2, która nie zawiera hello AS2-z lub AS2 tooor zarówno nagłówków. </br> Sprawdź komunikat AS2 AS2-z i AS2 tooheaders i popraw je na podstawie umowy konfiguracji |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>* Brakuje treści komunikatu AS2 i nagłówków    

|   |   |  
|---|---|
| Opis błędu| zawartość żądania Hello ma wartość null lub pusty | 
| Akcja użytkownika | Odebrano komunikat AS2, która nie zawiera treść wiadomości powitania |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>* Błąd odszyfrowywania wiadomości AS2

|   |   | 
|---|---|
| Opis błędu |  [przetwarzane błąd: nie powiodło się odszyfrowywania] | 
| Akcja użytkownika | Dodaj @base64ToBinary tooAS2Message przed wysłaniem toopartner 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a>* Błąd odszyfrowywania MDN

|   |   | 
|---|---|
| Opis błędu |  [przetwarzane błąd: nie powiodło się odszyfrowywania] | 
| Akcja użytkownika | Dodaj @base64ToBinary tooMDN przed wysłaniem toopartner 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a>* Brakuje certyfikatu podpisywania

|   |   |  
|---|---|
| Opis błędu| Witaj certyfikat podpisywania nie skonfigurowano dla strony AS2. </br> AS2 — z: partner1 AS2 — do: partner2 | 
| Akcja użytkownika | Skonfiguruj ustawienia umowy AS2 z prawidłowego certyfikatu do podpisu |
|  |  | 

## <a name="x12-and-edifact"></a>X12 i EDIFACT

### <a name="-leading-or-trailing-space-found"></a>* Początkowe lub końcowe miejsca znaleziono    
    
|   |   | 
|---|---|
| Opis błędu | Napotkano błąd podczas analizowania. Witaj transakcji Edifact ustawić o identyfikatorze "123456"zawarte w interchange (bez grupy) o identyfikatorze "987654", identyfikatorem nadawcy "Partner1", identyfikator odbiorcy "Partner2" zostanie wstrzymane z następujących błędów: wiodące końcowe separatora, znaleziono |
| Akcja użytkownika | toobe ustawienia umowy Hello skonfigurowane tooallow spacji wiodących i końcowych miejsca. </br> Edytowanie umowy ustawienia tooallow spacji wiodących i końcowych miejsca |
|   |   |

![Zezwalaj na miejsce](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a>* Zduplikowane wyboru włączył hello umowy

|   |   | 
|---|---| 
| Opis błędu | Zduplikowany numer formantu |
| Akcja użytkownika | Ten błąd wskazuje, że wiadomość hello Odebrano ma numery zduplikowane kontroli. </br> Popraw liczbę kontroli hello i ponownie wyślij wiadomość hello |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a>* Brak schematu hello umowy

|   |   | 
|---|---| 
| Opis błędu | Napotkano błąd podczas analizowania. zestaw transakcji Hello X12 o identyfikatorze '564220001' zawarte w grupy funkcjonalnej o identyfikatorze "56422', w wymiany o identyfikatorze"000056422"o identyfikatorze nadawcy" 12345678", identyfikator odbiorcy" 87654321"zostanie wstrzymane z następujących błędów"wiadomość hello ma ty nieznany dokumentu PE i nie rozwiązało tooany hello istniejących schematów skonfigurowanych w umowie hello " |
| Akcja użytkownika | Konfigurowanie schematu w ustawieniach umowy hello  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a>* Niepoprawny schemat hello umowy

|   |   | 
|---|---| 
| Opis błędu | wiadomości powitania ma nieznany typ dokumentu i nie rozwiązało tooany hello istniejących schematów skonfigurowanych w hello umowy. |
| Akcja użytkownika | Skonfiguruj poprawny schemat w ustawieniach umowy hello  |
|   |   |

## <a name="flat-file"></a>Plik prosty

### <a name="-input-message-with-no-body"></a>* Komunikat wejściowy o nie treści

|   |   | 
|---|---|
| Opis błędu | InvalidTemplate. Nie można tooprocess wyrażeń języka szablonu w danych wejściowych "Flat_File_Decoding" akcji w wierszu "1" i kolumnie "1902": "Wymagana właściwość"content"oczekuje, ale wartość otrzymano wartość null. Ścieżka ".". |
| Akcja użytkownika | Ten błąd oznacza, że komunikat wejściowy hello nie zawiera treści |
|   |   | 

## <a name="learn-more"></a>Dowiedz się więcej
[Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md)
