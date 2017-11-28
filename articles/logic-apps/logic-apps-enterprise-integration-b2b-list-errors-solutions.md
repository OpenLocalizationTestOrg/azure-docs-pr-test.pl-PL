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
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="52bb6-103">Logiki aplikacji B2B listę błędów i rozwiązania</span><span class="sxs-lookup"><span data-stu-id="52bb6-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="52bb6-104">Ten artykuł pomaga rozwiązywania problemów, które może się tak dziać w scenariusze B2B aplikacji logiki, a także sugeruje odpowiednie działania w przypadku naprawiania te błędy.</span><span class="sxs-lookup"><span data-stu-id="52bb6-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="52bb6-105">Rozdzielczość umowy</span><span class="sxs-lookup"><span data-stu-id="52bb6-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="52bb6-106">* Nie znaleziono umowę.</span><span class="sxs-lookup"><span data-stu-id="52bb6-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="52bb6-107">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-107">Error description</span></span> | <span data-ttu-id="52bb6-108">Nie znaleziono z parametrami rozpoznawania umowy umowę.</span><span class="sxs-lookup"><span data-stu-id="52bb6-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="52bb6-109">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-109">User action</span></span> | <span data-ttu-id="52bb6-110">Umowa Hello powinny zostać dodane toohello konta integracji z tożsamości firm uzgodnione.</span><span class="sxs-lookup"><span data-stu-id="52bb6-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="52bb6-111">tożsamości firm Hello powinna być zgodna toohello komunikat wejściowy identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="52bb6-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="52bb6-112">* Nie znaleziono z tożsamościami umowę.</span><span class="sxs-lookup"><span data-stu-id="52bb6-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="52bb6-113">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-113">Error description</span></span> | <span data-ttu-id="52bb6-114">Nie znaleziono z tożsamościami umowę: "AS2Identity":: "Partner1" i "AS2Identity":: "Partner3"</span><span class="sxs-lookup"><span data-stu-id="52bb6-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="52bb6-115">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-115">User action</span></span> | <span data-ttu-id="52bb6-116">Nieprawidłowy AS2-z lub AS2-tooconfigured umowy.</span><span class="sxs-lookup"><span data-stu-id="52bb6-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="52bb6-117">Komunikatów AS2 AS2-z lub identyfikatory toomatch AS2 AS2 tooheaders lub umowy w AS2 komunikatu nagłówków z konfiguracjami umowy</span><span class="sxs-lookup"><span data-stu-id="52bb6-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="52bb6-118">AS2</span><span class="sxs-lookup"><span data-stu-id="52bb6-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="52bb6-119">* Brak AS2 nagłówki komunikatów</span><span class="sxs-lookup"><span data-stu-id="52bb6-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="52bb6-120">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-120">Error description</span></span>| <span data-ttu-id="52bb6-121">Nieprawidłowy nagłówek AS2.</span><span class="sxs-lookup"><span data-stu-id="52bb6-121">Invalid AS2 headers.</span></span> <span data-ttu-id="52bb6-122">Jedną z "AS2 — do" lub "AS2 — od" nagłówki są puste</span><span class="sxs-lookup"><span data-stu-id="52bb6-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="52bb6-123">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-123">User action</span></span> | <span data-ttu-id="52bb6-124">Odebrano komunikat AS2, która nie zawiera hello AS2-z lub AS2 tooor zarówno nagłówków.</span><span class="sxs-lookup"><span data-stu-id="52bb6-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="52bb6-125">Sprawdź komunikat AS2 AS2-z i AS2 tooheaders i popraw je na podstawie umowy konfiguracji</span><span class="sxs-lookup"><span data-stu-id="52bb6-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="52bb6-126">* Brakuje treści komunikatu AS2 i nagłówków</span><span class="sxs-lookup"><span data-stu-id="52bb6-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="52bb6-127">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-127">Error description</span></span>| <span data-ttu-id="52bb6-128">zawartość żądania Hello ma wartość null lub pusty</span><span class="sxs-lookup"><span data-stu-id="52bb6-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="52bb6-129">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-129">User action</span></span> | <span data-ttu-id="52bb6-130">Odebrano komunikat AS2, która nie zawiera treść wiadomości powitania</span><span class="sxs-lookup"><span data-stu-id="52bb6-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="52bb6-131">* Błąd odszyfrowywania wiadomości AS2</span><span class="sxs-lookup"><span data-stu-id="52bb6-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="52bb6-132">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-132">Error description</span></span> |  <span data-ttu-id="52bb6-133">[przetwarzane błąd: nie powiodło się odszyfrowywania]</span><span class="sxs-lookup"><span data-stu-id="52bb6-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="52bb6-134">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-134">User action</span></span> | <span data-ttu-id="52bb6-135">Dodaj @base64ToBinary tooAS2Message przed wysłaniem toopartner</span><span class="sxs-lookup"><span data-stu-id="52bb6-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="52bb6-136">* Błąd odszyfrowywania MDN</span><span class="sxs-lookup"><span data-stu-id="52bb6-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="52bb6-137">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-137">Error description</span></span> |  <span data-ttu-id="52bb6-138">[przetwarzane błąd: nie powiodło się odszyfrowywania]</span><span class="sxs-lookup"><span data-stu-id="52bb6-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="52bb6-139">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-139">User action</span></span> | <span data-ttu-id="52bb6-140">Dodaj @base64ToBinary tooMDN przed wysłaniem toopartner</span><span class="sxs-lookup"><span data-stu-id="52bb6-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="52bb6-141">* Brakuje certyfikatu podpisywania</span><span class="sxs-lookup"><span data-stu-id="52bb6-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="52bb6-142">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-142">Error description</span></span>| <span data-ttu-id="52bb6-143">Witaj certyfikat podpisywania nie skonfigurowano dla strony AS2.</span><span class="sxs-lookup"><span data-stu-id="52bb6-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="52bb6-144">AS2 — z: partner1 AS2 — do: partner2</span><span class="sxs-lookup"><span data-stu-id="52bb6-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="52bb6-145">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-145">User action</span></span> | <span data-ttu-id="52bb6-146">Skonfiguruj ustawienia umowy AS2 z prawidłowego certyfikatu do podpisu</span><span class="sxs-lookup"><span data-stu-id="52bb6-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="52bb6-147">X12 i EDIFACT</span><span class="sxs-lookup"><span data-stu-id="52bb6-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="52bb6-148">* Początkowe lub końcowe miejsca znaleziono</span><span class="sxs-lookup"><span data-stu-id="52bb6-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="52bb6-149">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-149">Error description</span></span> | <span data-ttu-id="52bb6-150">Napotkano błąd podczas analizowania.</span><span class="sxs-lookup"><span data-stu-id="52bb6-150">Error encountered during parsing.</span></span> <span data-ttu-id="52bb6-151">Witaj transakcji Edifact ustawić o identyfikatorze "123456"zawarte w interchange (bez grupy) o identyfikatorze "987654", identyfikatorem nadawcy "Partner1", identyfikator odbiorcy "Partner2" zostanie wstrzymane z następujących błędów: wiodące końcowe separatora, znaleziono</span><span class="sxs-lookup"><span data-stu-id="52bb6-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="52bb6-152">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-152">User action</span></span> | <span data-ttu-id="52bb6-153">toobe ustawienia umowy Hello skonfigurowane tooallow spacji wiodących i końcowych miejsca.</span><span class="sxs-lookup"><span data-stu-id="52bb6-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="52bb6-154">Edytowanie umowy ustawienia tooallow spacji wiodących i końcowych miejsca</span><span class="sxs-lookup"><span data-stu-id="52bb6-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![Zezwalaj na miejsce](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="52bb6-156">* Zduplikowane wyboru włączył hello umowy</span><span class="sxs-lookup"><span data-stu-id="52bb6-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="52bb6-157">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-157">Error description</span></span> | <span data-ttu-id="52bb6-158">Zduplikowany numer formantu</span><span class="sxs-lookup"><span data-stu-id="52bb6-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="52bb6-159">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-159">User action</span></span> | <span data-ttu-id="52bb6-160">Ten błąd wskazuje, że wiadomość hello Odebrano ma numery zduplikowane kontroli.</span><span class="sxs-lookup"><span data-stu-id="52bb6-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="52bb6-161">Popraw liczbę kontroli hello i ponownie wyślij wiadomość hello</span><span class="sxs-lookup"><span data-stu-id="52bb6-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="52bb6-162">* Brak schematu hello umowy</span><span class="sxs-lookup"><span data-stu-id="52bb6-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="52bb6-163">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-163">Error description</span></span> | <span data-ttu-id="52bb6-164">Napotkano błąd podczas analizowania.</span><span class="sxs-lookup"><span data-stu-id="52bb6-164">Error encountered during parsing.</span></span> <span data-ttu-id="52bb6-165">zestaw transakcji Hello X12 o identyfikatorze '564220001' zawarte w grupy funkcjonalnej o identyfikatorze "56422', w wymiany o identyfikatorze"000056422"o identyfikatorze nadawcy" 12345678", identyfikator odbiorcy" 87654321"zostanie wstrzymane z następujących błędów"wiadomość hello ma ty nieznany dokumentu PE i nie rozwiązało tooany hello istniejących schematów skonfigurowanych w umowie hello "</span><span class="sxs-lookup"><span data-stu-id="52bb6-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="52bb6-166">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-166">User action</span></span> | <span data-ttu-id="52bb6-167">Konfigurowanie schematu w ustawieniach umowy hello</span><span class="sxs-lookup"><span data-stu-id="52bb6-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="52bb6-168">* Niepoprawny schemat hello umowy</span><span class="sxs-lookup"><span data-stu-id="52bb6-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="52bb6-169">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-169">Error description</span></span> | <span data-ttu-id="52bb6-170">wiadomości powitania ma nieznany typ dokumentu i nie rozwiązało tooany hello istniejących schematów skonfigurowanych w hello umowy.</span><span class="sxs-lookup"><span data-stu-id="52bb6-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="52bb6-171">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-171">User action</span></span> | <span data-ttu-id="52bb6-172">Skonfiguruj poprawny schemat w ustawieniach umowy hello</span><span class="sxs-lookup"><span data-stu-id="52bb6-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="52bb6-173">Plik prosty</span><span class="sxs-lookup"><span data-stu-id="52bb6-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="52bb6-174">* Komunikat wejściowy o nie treści</span><span class="sxs-lookup"><span data-stu-id="52bb6-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="52bb6-175">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="52bb6-175">Error description</span></span> | <span data-ttu-id="52bb6-176">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="52bb6-176">InvalidTemplate.</span></span> <span data-ttu-id="52bb6-177">Nie można tooprocess wyrażeń języka szablonu w danych wejściowych "Flat_File_Decoding" akcji w wierszu "1" i kolumnie "1902": "Wymagana właściwość"content"oczekuje, ale wartość otrzymano wartość null.</span><span class="sxs-lookup"><span data-stu-id="52bb6-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="52bb6-178">Ścieżka ".".</span><span class="sxs-lookup"><span data-stu-id="52bb6-178">Path ''.'.</span></span> |
| <span data-ttu-id="52bb6-179">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="52bb6-179">User action</span></span> | <span data-ttu-id="52bb6-180">Ten błąd oznacza, że komunikat wejściowy hello nie zawiera treści</span><span class="sxs-lookup"><span data-stu-id="52bb6-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="52bb6-181">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="52bb6-181">Learn more</span></span>
[<span data-ttu-id="52bb6-182">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="52bb6-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
