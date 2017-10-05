---
title: "Kodowanie wiadomości EDIFACT - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i generowanie kodu XML za pomocą kodera wiadomości EDIFACT w pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
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
ms.openlocfilehash: b8d577326d23ec45cb4a9ec0e450ebf7afd945f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="3d88d-103">Kodowanie wiadomości EDIFACT dla usługi Azure Logic Apps z pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="3d88d-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="3d88d-104">Łącznik EDIFACT kodowania komunikatu weryfikacji EDI i właściwości specyficzne dla partnera, generowanie dokumentu XML dla każdego zestawu transakcji, a żądania potwierdzenia technicznych i funkcjonalności potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="3d88d-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="3d88d-105">Aby użyć tego łącznika, należy dodać łącznika do istniejącego wyzwalacza w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="3d88d-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3d88d-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="3d88d-106">Before you start</span></span>

<span data-ttu-id="3d88d-107">Oto elementy, które są potrzebne:</span><span class="sxs-lookup"><span data-stu-id="3d88d-107">Here's the items you need:</span></span>

* <span data-ttu-id="3d88d-108">Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="3d88d-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="3d88d-109">[Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3d88d-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="3d88d-110">Musi mieć konto integracji do używania łącznika EDIFACT kodowania komunikatu.</span><span class="sxs-lookup"><span data-stu-id="3d88d-110">You must have an integration account to use the Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="3d88d-111">Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="3d88d-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="3d88d-112">[Umowy EDIFACT](logic-apps-enterprise-integration-edifact.md) jest już zdefiniowany w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="3d88d-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="3d88d-113">Kodowanie EDIFACT wiadomości</span><span class="sxs-lookup"><span data-stu-id="3d88d-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="3d88d-114">[Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3d88d-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="3d88d-115">Kodowanie EDIFACT łącznika komunikatu nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="3d88d-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="3d88d-116">W Projektancie aplikacji logiki dodać wyzwalacza, a następnie dodać do aplikacji logiki akcję.</span><span class="sxs-lookup"><span data-stu-id="3d88d-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="3d88d-117">W polu wyszukiwania wprowadź "EDIFACT" jako filtr.</span><span class="sxs-lookup"><span data-stu-id="3d88d-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="3d88d-118">Wybierz opcję **kodowania komunikatu EDIFACT przez Nazwa umowy** lub **Koduj EDIFACT komunikat przez tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="3d88d-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span></span>
   
    ![Wyszukiwanie EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="3d88d-120">Jeśli wcześniej nie utworzono wszystkie połączenia z kontem integracji, zostanie wyświetlony monit o utworzyć teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="3d88d-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="3d88d-121">Nazwa połączenia, a następnie wybierz konta integracji, na którym chcesz się połączyć.</span><span class="sxs-lookup"><span data-stu-id="3d88d-121">Name your connection, and select the integration account that you want to connect.</span></span>

    ![Tworzenie połączenia konta integracji](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="3d88d-123">Właściwości oznaczone gwiazdką są wymagane.</span><span class="sxs-lookup"><span data-stu-id="3d88d-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="3d88d-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3d88d-124">Property</span></span> | <span data-ttu-id="3d88d-125">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="3d88d-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="3d88d-126">Nazwa połączenia *</span><span class="sxs-lookup"><span data-stu-id="3d88d-126">Connection Name *</span></span> |<span data-ttu-id="3d88d-127">Wprowadź dowolną nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="3d88d-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="3d88d-128">Konta integracji *</span><span class="sxs-lookup"><span data-stu-id="3d88d-128">Integration Account *</span></span> |<span data-ttu-id="3d88d-129">Wprowadź nazwę konta integracji.</span><span class="sxs-lookup"><span data-stu-id="3d88d-129">Enter a name for your integration account.</span></span> <span data-ttu-id="3d88d-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3d88d-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="3d88d-131">Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie do tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="3d88d-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="3d88d-132">Aby zakończyć tworzenie połączenia, wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3d88d-132">To finish creating your connection, choose **Create**.</span></span>

    ![Szczegóły połączenia konta integracji](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="3d88d-134">Utworzono połączenie.</span><span class="sxs-lookup"><span data-stu-id="3d88d-134">Your connection is now created.</span></span>

    ![utworzone połączenie konta integracji](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="3d88d-136">Kodowanie komunikatu EDIFACT przez Nazwa umowy</span><span class="sxs-lookup"><span data-stu-id="3d88d-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="3d88d-137">Jeśli wybrano opcję kodowanie wiadomości EDIFACT według nazwy umowy, otwórz **umowy nazwa EDIFACT** listy, wprowadź lub wybierz nazwę umowy EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="3d88d-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="3d88d-138">Wprowadź komunikat XML do kodowania.</span><span class="sxs-lookup"><span data-stu-id="3d88d-138">Enter the XML message to encode.</span></span>

![Wprowadź nazwę umowy EDIFACT i wiadomości XML do kodowania](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="3d88d-140">Kodowanie komunikatu EDIFACT przez tożsamości</span><span class="sxs-lookup"><span data-stu-id="3d88d-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="3d88d-141">Jeśli wybierzesz kodowanie wiadomości EDIFACT przez tożsamości, wprowadź identyfikator nadawcy, Kwalifikator nadawcy, odbiorcy identyfikator i kwalifikator odbiornika zgodnie z konfiguracją umowy EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="3d88d-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="3d88d-142">Wybierz wiadomości XML do kodowania.</span><span class="sxs-lookup"><span data-stu-id="3d88d-142">Select the XML message to encode.</span></span>

![Podaj tożsamości dla nadawcy i odbiorcy, wybierz wiadomości XML do kodowania](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="3d88d-144">Szczegóły EDIFACT kodowania</span><span class="sxs-lookup"><span data-stu-id="3d88d-144">EDIFACT Encode details</span></span>

<span data-ttu-id="3d88d-145">Łącznik kodowania EDIFACT wykonuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="3d88d-145">The Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="3d88d-146">Rozwiązać przez dopasowanie kwalifikator nadawcy & identyfikator i odbiornika kwalifikator identyfikator umowy</span><span class="sxs-lookup"><span data-stu-id="3d88d-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="3d88d-147">Serializuje wymiany EDI, konwertowanie wiadomości w formacie XML w EDI zestawy transakcji w wymiany.</span><span class="sxs-lookup"><span data-stu-id="3d88d-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="3d88d-148">Stosuje zestaw transakcji nagłówka i przyczepy segmentów</span><span class="sxs-lookup"><span data-stu-id="3d88d-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="3d88d-149">Generuje numer formantu wymiany, numer kontroli grupy i numer kontroli zestawu transakcji, każdy wychodzący wymiany</span><span class="sxs-lookup"><span data-stu-id="3d88d-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="3d88d-150">Zastępuje separatorów w danych ładunku</span><span class="sxs-lookup"><span data-stu-id="3d88d-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="3d88d-151">Sprawdza poprawność właściwości specyficzne dla partnerów i EDI</span><span class="sxs-lookup"><span data-stu-id="3d88d-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="3d88d-152">Sprawdzanie poprawności schematu elementów dane zestawu transakcji względem schematu wiadomości.</span><span class="sxs-lookup"><span data-stu-id="3d88d-152">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="3d88d-153">EDI Weryfikacja w przypadku elementów dane zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="3d88d-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="3d88d-154">Rozszerzonej weryfikacji w przypadku elementów dane zestawu transakcji</span><span class="sxs-lookup"><span data-stu-id="3d88d-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="3d88d-155">Generuje dokument XML dla każdego zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="3d88d-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="3d88d-156">Żądania potwierdzenia techniczne i/lub funkcjonalne (jeśli jest skonfigurowane).</span><span class="sxs-lookup"><span data-stu-id="3d88d-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="3d88d-157">Jako potwierdzenie technicznych komunikat CONTRL oznacza otrzymania wymiany.</span><span class="sxs-lookup"><span data-stu-id="3d88d-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="3d88d-158">Jako potwierdzenie funkcjonalności komunikat CONTRL oznacza akceptacji lub odrzucenia wymiany stwierdzono, grupy lub wiadomości z listą błędów lub nieobsługiwanych funkcji</span><span class="sxs-lookup"><span data-stu-id="3d88d-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="3d88d-159">Plik struktury Swagger widoku</span><span class="sxs-lookup"><span data-stu-id="3d88d-159">View Swagger file</span></span>
<span data-ttu-id="3d88d-160">Aby wyświetlić szczegóły Swagger EDIFACT łącznika, zobacz [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="3d88d-160">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d88d-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d88d-161">Next steps</span></span>
[<span data-ttu-id="3d88d-162">Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="3d88d-162">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

