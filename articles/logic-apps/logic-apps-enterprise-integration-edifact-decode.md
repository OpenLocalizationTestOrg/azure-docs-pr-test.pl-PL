---
title: "komunikaty EDIFACT aaaDecode — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i generowanie potwierdzeń z dekodera komunikat EDIFACT hello w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
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
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="f247d-103">Dekodowanie EDIFACT wiadomości dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="f247d-103">Decode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="f247d-104">Łącznik wiadomość hello dekodowania EDIFACT można zweryfikować właściwości specyficzne dla partnerów i EDI, podzielić wymianę w zestawy transakcji lub zachować całą wymianę i generowanie potwierdzeń przetworzonych transakcji.</span><span class="sxs-lookup"><span data-stu-id="f247d-104">With hello Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="f247d-105">toouse tego łącznika, należy dodać tooan łącznika hello istniejących wyzwalacza w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="f247d-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f247d-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="f247d-106">Before you start</span></span>

<span data-ttu-id="f247d-107">Oto hello elementy, które należy:</span><span class="sxs-lookup"><span data-stu-id="f247d-107">Here's hello items you need:</span></span>

* <span data-ttu-id="f247d-108">Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="f247d-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="f247d-109">[Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f247d-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="f247d-110">Musi mieć łącznika integracji konta toouse hello EDIFACT dekodowanie komunikatu.</span><span class="sxs-lookup"><span data-stu-id="f247d-110">You must have an integration account toouse hello Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="f247d-111">Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="f247d-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="f247d-112">[Umowy EDIFACT](logic-apps-enterprise-integration-edifact.md) jest już zdefiniowany w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="f247d-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="f247d-113">Dekodowanie EDIFACT wiadomości</span><span class="sxs-lookup"><span data-stu-id="f247d-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="f247d-114">[Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f247d-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="f247d-115">Hello EDIFACT zdekodować komunikatu łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="f247d-115">hello Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="f247d-116">W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.</span><span class="sxs-lookup"><span data-stu-id="f247d-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3. <span data-ttu-id="f247d-117">W polu wyszukiwania hello wprowadź "EDIFACT" jako filtr.</span><span class="sxs-lookup"><span data-stu-id="f247d-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="f247d-118">Wybierz **zdekodować komunikatu EDIFACT**.</span><span class="sxs-lookup"><span data-stu-id="f247d-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![Wyszukiwanie EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="f247d-120">Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="f247d-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="f247d-121">Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect.</span><span class="sxs-lookup"><span data-stu-id="f247d-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Tworzenie konta integracji](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="f247d-123">Właściwości oznaczone gwiazdką są wymagane.</span><span class="sxs-lookup"><span data-stu-id="f247d-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="f247d-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="f247d-124">Property</span></span> | <span data-ttu-id="f247d-125">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="f247d-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="f247d-126">Nazwa połączenia *</span><span class="sxs-lookup"><span data-stu-id="f247d-126">Connection Name *</span></span> |<span data-ttu-id="f247d-127">Wprowadź dowolną nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="f247d-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="f247d-128">Konta integracji *</span><span class="sxs-lookup"><span data-stu-id="f247d-128">Integration Account *</span></span> |<span data-ttu-id="f247d-129">Wprowadź nazwę konta integracji.</span><span class="sxs-lookup"><span data-stu-id="f247d-129">Enter a name for your integration account.</span></span> <span data-ttu-id="f247d-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f247d-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

4. <span data-ttu-id="f247d-131">Po zakończeniu tworzenia połączenia toofinish wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f247d-131">When you're done toofinish creating your connection, choose **Create**.</span></span> <span data-ttu-id="f247d-132">Szczegóły połączenia powinien wyglądać podobnie przykład toothis:</span><span class="sxs-lookup"><span data-stu-id="f247d-132">Your connection details should look similar toothis example:</span></span>

    ![Szczegóły konta integracji](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="f247d-134">Po utworzeniu połączenia, jak pokazano w poniższym przykładzie, wybierz hello EDIFACT pliku prostego komunikatu toodecode.</span><span class="sxs-lookup"><span data-stu-id="f247d-134">After your connection is created, as shown in this example, select hello EDIFACT flat file message toodecode.</span></span>

    ![utworzone połączenie konta integracji](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="f247d-136">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f247d-136">For example:</span></span>

    ![Wybierz EDIFACT pliku prostego komunikatu dekodowania](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="f247d-138">Szczegóły dekodera EDIFACT</span><span class="sxs-lookup"><span data-stu-id="f247d-138">EDIFACT decoder details</span></span>

<span data-ttu-id="f247d-139">Łącznik dekodowania EDIFACT Hello wykonuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="f247d-139">hello Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="f247d-140">Weryfikuje koperty hello przed handlowymi umowy z partnerem.</span><span class="sxs-lookup"><span data-stu-id="f247d-140">Validates hello envelope against trading partner agreement.</span></span>
* <span data-ttu-id="f247d-141">Rozpoznaje umowy hello przez dopasowanie hello kwalifikator nadawcy i identyfikator oraz kwalifikator odbiornik i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="f247d-141">Resolves hello agreement by matching hello sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="f247d-142">Dzieli wymiany na wiele transakcji, gdy wymiany hello ma więcej niż jednej transakcji na podstawie umowy hello odbierać konfigurację ustawień.</span><span class="sxs-lookup"><span data-stu-id="f247d-142">Splits an interchange into multiple transactions when hello interchange has more than one transaction based on hello agreement's receive settings configuration.</span></span>
* <span data-ttu-id="f247d-143">Rozkłada hello wymiany.</span><span class="sxs-lookup"><span data-stu-id="f247d-143">Disassembles hello interchange.</span></span>
* <span data-ttu-id="f247d-144">Weryfikuje EDI i właściwości specyficzne dla partnera, w tym:</span><span class="sxs-lookup"><span data-stu-id="f247d-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="f247d-145">Sprawdzanie poprawności hello wymiany koperty struktury</span><span class="sxs-lookup"><span data-stu-id="f247d-145">Validation of hello interchange envelope structure</span></span>
  * <span data-ttu-id="f247d-146">Sprawdzanie poprawności schematu koperty hello schematem kontroli hello</span><span class="sxs-lookup"><span data-stu-id="f247d-146">Schema validation of hello envelope against hello control schema</span></span>
  * <span data-ttu-id="f247d-147">Sprawdzanie poprawności schematu elementów dane zestawu transakcji hello schematem wiadomość hello</span><span class="sxs-lookup"><span data-stu-id="f247d-147">Schema validation of hello transaction-set data elements against hello message schema</span></span>
  * <span data-ttu-id="f247d-148">EDI weryfikacji w przypadku elementów dane zestawu transakcji</span><span class="sxs-lookup"><span data-stu-id="f247d-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="f247d-149">Sprawdza, czy hello wymiany, grupy i transakcji zestaw numerów kontroli nie są duplikatami (jeśli jest skonfigurowane)</span><span class="sxs-lookup"><span data-stu-id="f247d-149">Verifies that hello interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="f247d-150">Sprawdza hello wymiany kontroli numer przed wymianę wcześniej odebrane.</span><span class="sxs-lookup"><span data-stu-id="f247d-150">Checks hello interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="f247d-151">Sprawdza hello grupy kontroli numer względem innych numery kontroli grupy w hello wymiany.</span><span class="sxs-lookup"><span data-stu-id="f247d-151">Checks hello group control number against other group control numbers in hello interchange.</span></span> 
  * <span data-ttu-id="f247d-152">Sprawdza, czy transakcja hello Ustaw numer kontroli względem innych numery kontroli zestawu transakcji w tej grupie.</span><span class="sxs-lookup"><span data-stu-id="f247d-152">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="f247d-153">Dzieli wymiany hello w zestawy transakcji lub zachowuje hello całego wymiany:</span><span class="sxs-lookup"><span data-stu-id="f247d-153">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="f247d-154">Wymiany podziału jako zestawy transakcji - zawiesić zestawy transakcji o błędzie: wymiany podziałów do transakcji ustawia i analizuje każdego zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="f247d-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="f247d-155">Akcja dekodowania Hello X12 wyświetla tylko te zestawy transakcji, Niepowodzenie weryfikacji za`badMessages`i wyświetla hello pozostałych transakcji ustawia zbyt`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="f247d-155">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="f247d-156">Podziel wymiany jako zestawy transakcji - zawiesić wymiany na błąd: wymiany podziałów do transakcji ustawia i analizuje każdego zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="f247d-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="f247d-157">Jeśli jeden lub więcej transakcji ustawia w hello wymiany Niepowodzenie weryfikacji, hello X12 dekodowania akcji generuje wszystkich transakcji hello ustawia w tym wymiany zbyt`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="f247d-157">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="f247d-158">Zachowaj wymiany — zawiesza zestawy transakcji na błąd: proces i Zachowaj hello wymiany hello całego wsadowej operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="f247d-158">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="f247d-159">Akcja dekodowania Hello X12 wyświetla tylko te zestawy transakcji, Niepowodzenie weryfikacji za`badMessages`i wyświetla hello pozostałych transakcji ustawia zbyt`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="f247d-159">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="f247d-160">Zachowaj wymiany — zawiesza wymiany na błąd: proces i Zachowaj hello wymiany hello całego wsadowej operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="f247d-160">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="f247d-161">Jeśli jeden lub więcej transakcji ustawia w hello wymiany Niepowodzenie weryfikacji, hello X12 dekodowania akcji generuje wszystkich transakcji hello ustawia w tym wymiany zbyt`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="f247d-161">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
* <span data-ttu-id="f247d-162">Generuje Technical (kontrola) i/lub funkcjonalności potwierdzenia (jeśli jest skonfigurowane).</span><span class="sxs-lookup"><span data-stu-id="f247d-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="f247d-163">Techniczne potwierdzeń lub hello potwierdzenia CONTRL wyświetla wyniki hello syntaktycznych sprawdzenia hello zakończenie Odebrano wymiany.</span><span class="sxs-lookup"><span data-stu-id="f247d-163">A Technical Acknowledgment or hello CONTRL ACK reports hello results of a syntactical check of hello complete received interchange.</span></span>
  * <span data-ttu-id="f247d-164">Potwierdzenie funkcjonalności potwierdza zaakceptować lub odrzucić odebrane wymiany lub grupy</span><span class="sxs-lookup"><span data-stu-id="f247d-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="f247d-165">Plik struktury Swagger widoku</span><span class="sxs-lookup"><span data-stu-id="f247d-165">View Swagger file</span></span>
<span data-ttu-id="f247d-166">Szczegóły programu Swagger hello tooview hello EDIFACT łącznika, zobacz [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="f247d-166">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f247d-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f247d-167">Next steps</span></span>
[<span data-ttu-id="f247d-168">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="f247d-168">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

