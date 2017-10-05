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
ms.openlocfilehash: 1865d75f1b4c2aa18d5a3130f639572d19563b3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="6ea57-103">Logiki aplikacji B2B listę błędów i rozwiązania</span><span class="sxs-lookup"><span data-stu-id="6ea57-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="6ea57-104">Ten artykuł pomaga rozwiązywania problemów, które może się tak dziać w scenariusze B2B aplikacji logiki, a także sugeruje odpowiednie działania w przypadku naprawiania te błędy.</span><span class="sxs-lookup"><span data-stu-id="6ea57-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="6ea57-105">Rozdzielczość umowy</span><span class="sxs-lookup"><span data-stu-id="6ea57-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="6ea57-106">* Nie znaleziono umowę.</span><span class="sxs-lookup"><span data-stu-id="6ea57-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="6ea57-107">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-107">Error description</span></span> | <span data-ttu-id="6ea57-108">Nie znaleziono z parametrami rozpoznawania umowy umowę.</span><span class="sxs-lookup"><span data-stu-id="6ea57-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="6ea57-109">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-109">User action</span></span> | <span data-ttu-id="6ea57-110">Umowy powinno być dodane do konta integracji z tożsamości firm uzgodnione.</span><span class="sxs-lookup"><span data-stu-id="6ea57-110">The agreement should be added to the integration account with agreed business identities.</span></span></br> <span data-ttu-id="6ea57-111">Tożsamości firm powinien być zgodny z identyfikatorami komunikatu wejściowego</span><span class="sxs-lookup"><span data-stu-id="6ea57-111">The business identities should match to the input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="6ea57-112">* Nie znaleziono z tożsamościami umowę.</span><span class="sxs-lookup"><span data-stu-id="6ea57-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="6ea57-113">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-113">Error description</span></span> | <span data-ttu-id="6ea57-114">Nie znaleziono z tożsamościami umowę: "AS2Identity":: "Partner1" i "AS2Identity":: "Partner3"</span><span class="sxs-lookup"><span data-stu-id="6ea57-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="6ea57-115">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-115">User action</span></span> | <span data-ttu-id="6ea57-116">Nieprawidłowy AS2-z lub AS2 — do skonfigurowanych dla umowy.</span><span class="sxs-lookup"><span data-stu-id="6ea57-116">Invalid AS2-From or AS2-To configured for agreement.</span></span> </br> <span data-ttu-id="6ea57-117">Komunikatów AS2 AS2-z lub AS2-nagłówków lub umowy do dopasowania identyfikatorów AS2 w AS2 komunikatu nagłówków z konfiguracjami umowy</span><span class="sxs-lookup"><span data-stu-id="6ea57-117">Correct AS2 message AS2-From or AS2-To headers or agreement to match AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="6ea57-118">AS2</span><span class="sxs-lookup"><span data-stu-id="6ea57-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="6ea57-119">* Brak AS2 nagłówki komunikatów</span><span class="sxs-lookup"><span data-stu-id="6ea57-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="6ea57-120">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-120">Error description</span></span>| <span data-ttu-id="6ea57-121">Nieprawidłowy nagłówek AS2.</span><span class="sxs-lookup"><span data-stu-id="6ea57-121">Invalid AS2 headers.</span></span> <span data-ttu-id="6ea57-122">Jedną z "AS2 — do" lub "AS2 — od" nagłówki są puste</span><span class="sxs-lookup"><span data-stu-id="6ea57-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="6ea57-123">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-123">User action</span></span> | <span data-ttu-id="6ea57-124">Odebrano komunikat AS2, która nie zawiera AS2-z lub AS2 — aby lub obu nagłówków.</span><span class="sxs-lookup"><span data-stu-id="6ea57-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span></span> </br> <span data-ttu-id="6ea57-125">Sprawdź komunikat AS2 AS2-z i AS2-nagłówków i prawidłowe je na podstawie umowy konfiguracji</span><span class="sxs-lookup"><span data-stu-id="6ea57-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="6ea57-126">* Brakuje treści komunikatu AS2 i nagłówków</span><span class="sxs-lookup"><span data-stu-id="6ea57-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="6ea57-127">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-127">Error description</span></span>| <span data-ttu-id="6ea57-128">Zawartość żądania ma wartość null lub pusty</span><span class="sxs-lookup"><span data-stu-id="6ea57-128">The request content is null or empty</span></span> | 
| <span data-ttu-id="6ea57-129">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-129">User action</span></span> | <span data-ttu-id="6ea57-130">Odebrano komunikat AS2, która nie zawiera treść komunikatu</span><span class="sxs-lookup"><span data-stu-id="6ea57-130">An AS2 message was received that did not contain the message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="6ea57-131">* Błąd odszyfrowywania wiadomości AS2</span><span class="sxs-lookup"><span data-stu-id="6ea57-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="6ea57-132">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-132">Error description</span></span> |  <span data-ttu-id="6ea57-133">[przetwarzane błąd: nie powiodło się odszyfrowywania]</span><span class="sxs-lookup"><span data-stu-id="6ea57-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="6ea57-134">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-134">User action</span></span> | <span data-ttu-id="6ea57-135">Dodaj @base64ToBinary do AS2Message przed wysłaniem do partnera</span><span class="sxs-lookup"><span data-stu-id="6ea57-135">Add @base64ToBinary to AS2Message before sending to partner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="6ea57-136">* Błąd odszyfrowywania MDN</span><span class="sxs-lookup"><span data-stu-id="6ea57-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="6ea57-137">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-137">Error description</span></span> |  <span data-ttu-id="6ea57-138">[przetwarzane błąd: nie powiodło się odszyfrowywania]</span><span class="sxs-lookup"><span data-stu-id="6ea57-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="6ea57-139">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-139">User action</span></span> | <span data-ttu-id="6ea57-140">Dodaj @base64ToBinary do MDN przed wysłaniem do partnera</span><span class="sxs-lookup"><span data-stu-id="6ea57-140">Add @base64ToBinary to MDN before sending to partner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="6ea57-141">* Brakuje certyfikatu podpisywania</span><span class="sxs-lookup"><span data-stu-id="6ea57-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="6ea57-142">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-142">Error description</span></span>| <span data-ttu-id="6ea57-143">Nie skonfigurowano certyfikatu podpisywania firmy AS2.</span><span class="sxs-lookup"><span data-stu-id="6ea57-143">The Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="6ea57-144">AS2 — z: partner1 AS2 — do: partner2</span><span class="sxs-lookup"><span data-stu-id="6ea57-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="6ea57-145">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-145">User action</span></span> | <span data-ttu-id="6ea57-146">Skonfiguruj ustawienia umowy AS2 z prawidłowego certyfikatu do podpisu</span><span class="sxs-lookup"><span data-stu-id="6ea57-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="6ea57-147">X12 i EDIFACT</span><span class="sxs-lookup"><span data-stu-id="6ea57-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="6ea57-148">* Początkowe lub końcowe miejsca znaleziono</span><span class="sxs-lookup"><span data-stu-id="6ea57-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="6ea57-149">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-149">Error description</span></span> | <span data-ttu-id="6ea57-150">Napotkano błąd podczas analizowania.</span><span class="sxs-lookup"><span data-stu-id="6ea57-150">Error encountered during parsing.</span></span> <span data-ttu-id="6ea57-151">Transakcja Edifact zestawu o identyfikatorze "123456"zawarte w interchange (bez grupy) o identyfikatorze "987654", identyfikator nadawcy "Partner1", identyfikator odbiorcy "Partner2" zostanie wstrzymane z następujących błędów: wiodące końcowe separatora, znaleziono</span><span class="sxs-lookup"><span data-stu-id="6ea57-151">The Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="6ea57-152">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-152">User action</span></span> | <span data-ttu-id="6ea57-153">Ustawienia umowy, aby umożliwiać spacji wiodących i końcowych miejsca.</span><span class="sxs-lookup"><span data-stu-id="6ea57-153">The agreement settings to be configured to allow leading and trailing space.</span></span> </br> <span data-ttu-id="6ea57-154">Edytowanie umowy ustawienia umożliwiające programowi miejsca wiodące i końcowe</span><span class="sxs-lookup"><span data-stu-id="6ea57-154">Edit agreement settings to allow leading and trailing space</span></span> |
|   |   |

![Zezwalaj na miejsce](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-the-agreement"></a><span data-ttu-id="6ea57-156">* Zduplikowane wyboru włączył umowy</span><span class="sxs-lookup"><span data-stu-id="6ea57-156">* Duplicate check has enabled in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="6ea57-157">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-157">Error description</span></span> | <span data-ttu-id="6ea57-158">Zduplikowany numer formantu</span><span class="sxs-lookup"><span data-stu-id="6ea57-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="6ea57-159">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-159">User action</span></span> | <span data-ttu-id="6ea57-160">Ten błąd wskazuje, że odebranego komunikatu ma numery zduplikowane kontroli.</span><span class="sxs-lookup"><span data-stu-id="6ea57-160">This error indicates the received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="6ea57-161">Popraw liczbę kontroli i ponownie wysłać wiadomość</span><span class="sxs-lookup"><span data-stu-id="6ea57-161">Correct the control number and resend the message</span></span> |
|   |   |

### <a name="-missing-schema-in-the-agreement"></a><span data-ttu-id="6ea57-162">* Brak schematu umowy</span><span class="sxs-lookup"><span data-stu-id="6ea57-162">* Missing schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="6ea57-163">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-163">Error description</span></span> | <span data-ttu-id="6ea57-164">Napotkano błąd podczas analizowania.</span><span class="sxs-lookup"><span data-stu-id="6ea57-164">Error encountered during parsing.</span></span> <span data-ttu-id="6ea57-165">X12 zestawu transakcji o identyfikatorze '564220001' zawarte w grupy funkcjonalnej o identyfikatorze "56422', w wymiany o identyfikatorze"000056422"o identyfikatorze nadawcy" 12345678", identyfikator odbiorcy" 87654321"zostanie wstrzymane z następujących błędów" wiadomość ma nieznany typ dokumentu ND nie zostało rozwiązane do żadnego z istniejących schematów skonfigurowanych w umowie"</span><span class="sxs-lookup"><span data-stu-id="6ea57-165">The X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span></span> |
| <span data-ttu-id="6ea57-166">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-166">User action</span></span> | <span data-ttu-id="6ea57-167">Konfigurowanie schematu w ustawieniach umowy</span><span class="sxs-lookup"><span data-stu-id="6ea57-167">Configure schema in the agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-the-agreement"></a><span data-ttu-id="6ea57-168">* Niepoprawny schemat umowy</span><span class="sxs-lookup"><span data-stu-id="6ea57-168">* Incorrect schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="6ea57-169">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-169">Error description</span></span> | <span data-ttu-id="6ea57-170">Wiadomość ma nieznany typ dokumentu i nie zostało rozwiązane do żadnego z istniejących schematów skonfigurowanych w umowie.</span><span class="sxs-lookup"><span data-stu-id="6ea57-170">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span></span> |
| <span data-ttu-id="6ea57-171">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-171">User action</span></span> | <span data-ttu-id="6ea57-172">Skonfiguruj poprawny schemat w ustawieniach umowy</span><span class="sxs-lookup"><span data-stu-id="6ea57-172">Configure correct schema in the agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="6ea57-173">Plik prosty</span><span class="sxs-lookup"><span data-stu-id="6ea57-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="6ea57-174">* Komunikat wejściowy o nie treści</span><span class="sxs-lookup"><span data-stu-id="6ea57-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="6ea57-175">Opis błędu</span><span class="sxs-lookup"><span data-stu-id="6ea57-175">Error description</span></span> | <span data-ttu-id="6ea57-176">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="6ea57-176">InvalidTemplate.</span></span> <span data-ttu-id="6ea57-177">Nie można wyrażeń języka szablonu procesu w danych wejściowych "Flat_File_Decoding" akcji w wierszu "1" i kolumnie "1902": "Wymagana właściwość"content"oczekuje, ale wartość otrzymano wartość null.</span><span class="sxs-lookup"><span data-stu-id="6ea57-177">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="6ea57-178">Ścieżka ".".</span><span class="sxs-lookup"><span data-stu-id="6ea57-178">Path ''.'.</span></span> |
| <span data-ttu-id="6ea57-179">Akcja użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ea57-179">User action</span></span> | <span data-ttu-id="6ea57-180">Ten błąd oznacza, że komunikat wejściowy nie zawiera jednostkę</span><span class="sxs-lookup"><span data-stu-id="6ea57-180">This error indicates the input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="6ea57-181">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="6ea57-181">Learn more</span></span>
[<span data-ttu-id="6ea57-182">Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="6ea57-182">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)