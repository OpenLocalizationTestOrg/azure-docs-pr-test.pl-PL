---
title: "komunikaty EDIFACT aaaEncode — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i generowanie kodu XML za pomocą kodera wiadomości EDIFACT w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="5d234-103">Kodowanie wiadomości EDIFACT dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="5d234-103">Encode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="5d234-104">Łącznik wiadomość hello kodowania EDIFACT zweryfikować EDI i właściwości specyficzne dla partnera, generowanie dokumentu XML dla każdego zestawu transakcji, a żądania potwierdzenia technicznych i funkcjonalności potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="5d234-104">With hello Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="5d234-105">toouse tego łącznika, należy dodać tooan łącznika hello istniejących wyzwalacza w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="5d234-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5d234-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="5d234-106">Before you start</span></span>

<span data-ttu-id="5d234-107">Oto hello elementy, które należy:</span><span class="sxs-lookup"><span data-stu-id="5d234-107">Here's hello items you need:</span></span>

* <span data-ttu-id="5d234-108">Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="5d234-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="5d234-109">[Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5d234-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="5d234-110">Musi mieć łącznika integracji konta toouse hello EDIFACT kodowania komunikatu.</span><span class="sxs-lookup"><span data-stu-id="5d234-110">You must have an integration account toouse hello Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="5d234-111">Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="5d234-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="5d234-112">[Umowy EDIFACT](logic-apps-enterprise-integration-edifact.md) jest już zdefiniowany w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="5d234-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="5d234-113">Kodowanie EDIFACT wiadomości</span><span class="sxs-lookup"><span data-stu-id="5d234-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="5d234-114">[Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5d234-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="5d234-115">Hello EDIFACT kodowania komunikatu łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="5d234-115">hello Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="5d234-116">W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.</span><span class="sxs-lookup"><span data-stu-id="5d234-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="5d234-117">W polu wyszukiwania hello wprowadź "EDIFACT" jako filtr.</span><span class="sxs-lookup"><span data-stu-id="5d234-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="5d234-118">Wybierz opcję **kodowania komunikatu EDIFACT przez Nazwa umowy** lub **Koduj tooEDIFACT komunikatu przez tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="5d234-118">Select either **Encode EDIFACT Message by agreement name** or **Encode tooEDIFACT message by identities**.</span></span>
   
    ![Wyszukiwanie EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="5d234-120">Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="5d234-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="5d234-121">Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect.</span><span class="sxs-lookup"><span data-stu-id="5d234-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>

    ![Tworzenie połączenia konta integracji](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="5d234-123">Właściwości oznaczone gwiazdką są wymagane.</span><span class="sxs-lookup"><span data-stu-id="5d234-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="5d234-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5d234-124">Property</span></span> | <span data-ttu-id="5d234-125">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="5d234-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="5d234-126">Nazwa połączenia *</span><span class="sxs-lookup"><span data-stu-id="5d234-126">Connection Name *</span></span> |<span data-ttu-id="5d234-127">Wprowadź dowolną nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="5d234-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="5d234-128">Konta integracji *</span><span class="sxs-lookup"><span data-stu-id="5d234-128">Integration Account *</span></span> |<span data-ttu-id="5d234-129">Wprowadź nazwę konta integracji.</span><span class="sxs-lookup"><span data-stu-id="5d234-129">Enter a name for your integration account.</span></span> <span data-ttu-id="5d234-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5d234-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="5d234-131">Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie przykład toothis.</span><span class="sxs-lookup"><span data-stu-id="5d234-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="5d234-132">Wybierz toofinish Tworzenie połączenia **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5d234-132">toofinish creating your connection, choose **Create**.</span></span>

    ![Szczegóły połączenia konta integracji](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="5d234-134">Utworzono połączenie.</span><span class="sxs-lookup"><span data-stu-id="5d234-134">Your connection is now created.</span></span>

    ![utworzone połączenie konta integracji](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="5d234-136">Kodowanie komunikatu EDIFACT przez Nazwa umowy</span><span class="sxs-lookup"><span data-stu-id="5d234-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="5d234-137">Jeśli wybrano opcję tooencode EDIFACT wiadomości przez nazwę umowy, otwórz hello **umowy nazwa EDIFACT** listy, wprowadź lub wybierz nazwę umowy EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="5d234-137">If you chose tooencode EDIFACT messages by agreement name, open hello **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="5d234-138">Wprowadź tooencode wiadomości XML hello.</span><span class="sxs-lookup"><span data-stu-id="5d234-138">Enter hello XML message tooencode.</span></span>

![Wprowadź nazwę umowy EDIFACT i tooencode wiadomości XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="5d234-140">Kodowanie komunikatu EDIFACT przez tożsamości</span><span class="sxs-lookup"><span data-stu-id="5d234-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="5d234-141">Jeśli wybierzesz tooencode EDIFACT wiadomości przez tożsamości, wprowadź identyfikator nadawcy hello, Kwalifikator nadawcy identyfikator odbiornika i odbiornika kwalifikator zgodnie z konfiguracją umowy EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="5d234-141">If you choose tooencode EDIFACT messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="5d234-142">Wybierz hello tooencode wiadomości XML.</span><span class="sxs-lookup"><span data-stu-id="5d234-142">Select hello XML message tooencode.</span></span>

![Podaj tożsamości dla nadawcy i odbiorcy, wybierz tooencode wiadomości XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="5d234-144">Szczegóły EDIFACT kodowania</span><span class="sxs-lookup"><span data-stu-id="5d234-144">EDIFACT Encode details</span></span>

<span data-ttu-id="5d234-145">Łącznik kodowania EDIFACT Hello wykonuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="5d234-145">hello Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="5d234-146">Rozwiąż umowy hello przez dopasowanie kwalifikator nadawcy hello & Identyfikator kwalifikator odbiornik i identyfikator</span><span class="sxs-lookup"><span data-stu-id="5d234-146">Resolve hello agreement by matching hello sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="5d234-147">Serializuje hello EDI wymiany danych, konwertowanie wiadomości w formacie XML w EDI zestawy transakcji w hello wymiany.</span><span class="sxs-lookup"><span data-stu-id="5d234-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="5d234-148">Stosuje zestaw transakcji nagłówka i przyczepy segmentów</span><span class="sxs-lookup"><span data-stu-id="5d234-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="5d234-149">Generuje numer formantu wymiany, numer kontroli grupy i numer kontroli zestawu transakcji, każdy wychodzący wymiany</span><span class="sxs-lookup"><span data-stu-id="5d234-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="5d234-150">Zastępuje separatorów hello ładunek danych</span><span class="sxs-lookup"><span data-stu-id="5d234-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="5d234-151">Sprawdza poprawność właściwości specyficzne dla partnerów i EDI</span><span class="sxs-lookup"><span data-stu-id="5d234-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="5d234-152">Sprawdzanie poprawności schematu elementów dane zestawu transakcji hello schematem wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="5d234-152">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="5d234-153">EDI Weryfikacja w przypadku elementów dane zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="5d234-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="5d234-154">Rozszerzonej weryfikacji w przypadku elementów dane zestawu transakcji</span><span class="sxs-lookup"><span data-stu-id="5d234-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="5d234-155">Generuje dokument XML dla każdego zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="5d234-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="5d234-156">Żądania potwierdzenia techniczne i/lub funkcjonalne (jeśli jest skonfigurowane).</span><span class="sxs-lookup"><span data-stu-id="5d234-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="5d234-157">Jako potwierdzenie technicznych wiadomości powitania CONTRL wskazuje otrzymania wymiany.</span><span class="sxs-lookup"><span data-stu-id="5d234-157">As a technical acknowledgment, hello CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="5d234-158">Jako funkcjonalności potwierdzenie wiadomości powitania CONTRL wskazuje akceptacji lub odrzucenia wymiany hello odebrane, grupy lub wiadomości z listą błędów lub nieobsługiwanych funkcji</span><span class="sxs-lookup"><span data-stu-id="5d234-158">As a functional acknowledgment, hello CONTRL message indicates acceptance or rejection of hello received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="5d234-159">Plik struktury Swagger widoku</span><span class="sxs-lookup"><span data-stu-id="5d234-159">View Swagger file</span></span>
<span data-ttu-id="5d234-160">Szczegóły programu Swagger hello tooview hello EDIFACT łącznika, zobacz [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="5d234-160">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d234-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d234-161">Next steps</span></span>
[<span data-ttu-id="5d234-162">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="5d234-162">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

