---
title: "Dekodowanie EDIFACT wiadomości - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i generowanie potwierdzeń z dekodera komunikat EDIFACT w pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e3787b48037360bf6066ddce2bacba6842213b2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="f0bdc-103">Dekodowanie EDIFACT wiadomości dla usługi Azure Logic Apps z pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="f0bdc-103">Decode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="f0bdc-104">Łącznik EDIFACT dekodowanie komunikatu można zweryfikować właściwości specyficzne dla partnerów i EDI, podzielić wymianę w zestawy transakcji lub zachować całą wymianę i generowanie potwierdzeń przetworzonych transakcji.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-104">With the Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="f0bdc-105">Aby użyć tego łącznika, należy dodać łącznika do istniejącego wyzwalacza w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f0bdc-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="f0bdc-106">Before you start</span></span>

<span data-ttu-id="f0bdc-107">Oto elementy, które są potrzebne:</span><span class="sxs-lookup"><span data-stu-id="f0bdc-107">Here's the items you need:</span></span>

* <span data-ttu-id="f0bdc-108">Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="f0bdc-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="f0bdc-109">[Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="f0bdc-110">Musi mieć konto integracji do używania łącznika EDIFACT dekodowanie komunikatu.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-110">You must have an integration account to use the Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="f0bdc-111">Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="f0bdc-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="f0bdc-112">[Umowy EDIFACT](logic-apps-enterprise-integration-edifact.md) jest już zdefiniowany w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="f0bdc-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="f0bdc-113">Dekodowanie EDIFACT wiadomości</span><span class="sxs-lookup"><span data-stu-id="f0bdc-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="f0bdc-114">[Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f0bdc-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="f0bdc-115">Dekodowanie EDIFACT łącznika komunikatu nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-115">The Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="f0bdc-116">W Projektancie aplikacji logiki dodać wyzwalacza, a następnie dodać do aplikacji logiki akcję.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3. <span data-ttu-id="f0bdc-117">W polu wyszukiwania wprowadź "EDIFACT" jako filtr.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="f0bdc-118">Wybierz **zdekodować komunikatu EDIFACT**.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![Wyszukiwanie EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="f0bdc-120">Jeśli wcześniej nie utworzono wszystkie połączenia z kontem integracji, zostanie wyświetlony monit o utworzyć teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="f0bdc-121">Nazwa połączenia, a następnie wybierz konta integracji, na którym chcesz się połączyć.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![Tworzenie konta integracji](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="f0bdc-123">Właściwości oznaczone gwiazdką są wymagane.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="f0bdc-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="f0bdc-124">Property</span></span> | <span data-ttu-id="f0bdc-125">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="f0bdc-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="f0bdc-126">Nazwa połączenia *</span><span class="sxs-lookup"><span data-stu-id="f0bdc-126">Connection Name *</span></span> |<span data-ttu-id="f0bdc-127">Wprowadź dowolną nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="f0bdc-128">Konta integracji *</span><span class="sxs-lookup"><span data-stu-id="f0bdc-128">Integration Account *</span></span> |<span data-ttu-id="f0bdc-129">Wprowadź nazwę konta integracji.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-129">Enter a name for your integration account.</span></span> <span data-ttu-id="f0bdc-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

4. <span data-ttu-id="f0bdc-131">Gdy wszystko będzie gotowe, aby zakończyć tworzenie połączenia, wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-131">When you're done to finish creating your connection, choose **Create**.</span></span> <span data-ttu-id="f0bdc-132">Szczegóły połączenia powinien wyglądać podobnie jak w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="f0bdc-132">Your connection details should look similar to this example:</span></span>

    ![Szczegóły konta integracji](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="f0bdc-134">Po utworzeniu połączenia, jak pokazano w poniższym przykładzie, wybierz komunikat pliku prostego EDIFACT zdekodować.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-134">After your connection is created, as shown in this example, select the EDIFACT flat file message to decode.</span></span>

    ![utworzone połączenie konta integracji](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="f0bdc-136">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f0bdc-136">For example:</span></span>

    ![Wybierz EDIFACT pliku prostego komunikatu dekodowania](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="f0bdc-138">Szczegóły dekodera EDIFACT</span><span class="sxs-lookup"><span data-stu-id="f0bdc-138">EDIFACT decoder details</span></span>

<span data-ttu-id="f0bdc-139">Łącznik dekodowania EDIFACT wykonuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="f0bdc-139">The Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="f0bdc-140">Weryfikuje koperty przed handlowymi umowy z partnerem.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-140">Validates the envelope against trading partner agreement.</span></span>
* <span data-ttu-id="f0bdc-141">Rozpoznaje umowy przez dopasowanie kwalifikator nadawcy i identyfikator oraz kwalifikator odbiornik i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-141">Resolves the agreement by matching the sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="f0bdc-142">Dzieli wymiany na wiele transakcji, gdy wymiany ma więcej niż jednej transakcji na podstawie umowy odbierać konfigurację ustawień.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-142">Splits an interchange into multiple transactions when the interchange has more than one transaction based on the agreement's receive settings configuration.</span></span>
* <span data-ttu-id="f0bdc-143">Rozkłada wymiany.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-143">Disassembles the interchange.</span></span>
* <span data-ttu-id="f0bdc-144">Weryfikuje EDI i właściwości specyficzne dla partnera, w tym:</span><span class="sxs-lookup"><span data-stu-id="f0bdc-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="f0bdc-145">Sprawdzanie poprawności struktury koperty wymiany</span><span class="sxs-lookup"><span data-stu-id="f0bdc-145">Validation of the interchange envelope structure</span></span>
  * <span data-ttu-id="f0bdc-146">Sprawdzanie poprawności schematu envelope względem schematu kontroli</span><span class="sxs-lookup"><span data-stu-id="f0bdc-146">Schema validation of the envelope against the control schema</span></span>
  * <span data-ttu-id="f0bdc-147">Sprawdzanie poprawności schematu elementów danych transakcji zestawu względem schematu komunikatów</span><span class="sxs-lookup"><span data-stu-id="f0bdc-147">Schema validation of the transaction-set data elements against the message schema</span></span>
  * <span data-ttu-id="f0bdc-148">EDI weryfikacji w przypadku elementów dane zestawu transakcji</span><span class="sxs-lookup"><span data-stu-id="f0bdc-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="f0bdc-149">Sprawdza, czy numery kontroli zestawu wymiany, grupy i transakcji nie są duplikatami (jeśli jest skonfigurowane)</span><span class="sxs-lookup"><span data-stu-id="f0bdc-149">Verifies that the interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="f0bdc-150">Sprawdza numer kontroli wymiany przed wymianę wcześniej odebrane.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-150">Checks the interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="f0bdc-151">Sprawdza, czy numer grupy kontroli względem innych numery kontroli grupy w wymiany.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-151">Checks the group control number against other group control numbers in the interchange.</span></span> 
  * <span data-ttu-id="f0bdc-152">Sprawdza, czy transakcja Ustaw numer kontroli względem innych numery kontroli zestawu transakcji w tej grupie.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-152">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="f0bdc-153">Dzieli wymiany w zestawy transakcji lub zachowuje całego wymiany:</span><span class="sxs-lookup"><span data-stu-id="f0bdc-153">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="f0bdc-154">Wymiany podziału jako zestawy transakcji - zawiesić zestawy transakcji o błędzie: wymiany podziałów do transakcji ustawia i analizuje każdego zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="f0bdc-155">X12 akcji dekodowania danych wyjściowych zestawów tylko tych transakcji niepowodzenie sprawdzania poprawności do `badMessages`i ustawia transakcji pozostałe dane wyjściowe `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-155">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="f0bdc-156">Podziel wymiany jako zestawy transakcji - zawiesić wymiany na błąd: wymiany podziałów do transakcji ustawia i analizuje każdego zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="f0bdc-157">Jeśli jeden lub więcej transakcji ustawia w wymiany wystąpi niepowodzenie weryfikacji, X12 akcji dekodowania danych wyjściowych ustawia wszystkich transakcji w tym wymiany do `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-157">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="f0bdc-158">Zachowaj wymiany — zawiesza zestawy transakcji na błąd: Zachowaj wymiany i przetwarzanie całego wsadowej operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-158">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="f0bdc-159">X12 akcji dekodowania danych wyjściowych zestawów tylko tych transakcji niepowodzenie sprawdzania poprawności do `badMessages`i ustawia transakcji pozostałe dane wyjściowe `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-159">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="f0bdc-160">Zachowaj wymiany — zawiesza wymiany na błąd: Zachowaj wymiany i przetwarzanie całego wsadowej operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-160">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="f0bdc-161">Jeśli jeden lub więcej transakcji ustawia w wymiany wystąpi niepowodzenie weryfikacji, X12 akcji dekodowania danych wyjściowych ustawia wszystkich transakcji w tym wymiany do `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-161">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
* <span data-ttu-id="f0bdc-162">Generuje Technical (kontrola) i/lub funkcjonalności potwierdzenia (jeśli jest skonfigurowane).</span><span class="sxs-lookup"><span data-stu-id="f0bdc-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="f0bdc-163">Potwierdzenia techniczne lub potwierdzenia CONTRL zgłasza wyniki syntaktycznych wyboru zakończenie Odebrano wymiany.</span><span class="sxs-lookup"><span data-stu-id="f0bdc-163">A Technical Acknowledgment or the CONTRL ACK reports the results of a syntactical check of the complete received interchange.</span></span>
  * <span data-ttu-id="f0bdc-164">Potwierdzenie funkcjonalności potwierdza zaakceptować lub odrzucić odebrane wymiany lub grupy</span><span class="sxs-lookup"><span data-stu-id="f0bdc-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="f0bdc-165">Plik struktury Swagger widoku</span><span class="sxs-lookup"><span data-stu-id="f0bdc-165">View Swagger file</span></span>
<span data-ttu-id="f0bdc-166">Aby wyświetlić szczegóły Swagger EDIFACT łącznika, zobacz [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="f0bdc-166">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0bdc-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0bdc-167">Next steps</span></span>
[<span data-ttu-id="f0bdc-168">Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="f0bdc-168">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

