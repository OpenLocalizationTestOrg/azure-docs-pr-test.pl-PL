---
title: "Dekodowanie X12 wiadomości - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i generowanie potwierdzeń z X12 dekodera komunikat w pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 18719a8f49c74973947517161f7306c233a9323f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="22836-103">Dekodowanie X12 wiadomości dla usługi Azure Logic Apps z pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="22836-103">Decode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="22836-104">Łącznik komunikat dekodowania X12 można zweryfikować koperty przed umowy z partnerem handlowym, zweryfikować EDI i właściwości specyficzne dla partnera, podzielić wymianę w zestawy transakcji lub zachować całą wymianę i generowanie potwierdzeń dla przetworzonych transakcji.</span><span class="sxs-lookup"><span data-stu-id="22836-104">With the Decode X12 message connector, you can validate the envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="22836-105">Aby użyć tego łącznika, należy dodać łącznika do istniejącego wyzwalacza w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="22836-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="22836-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="22836-106">Before you start</span></span>

<span data-ttu-id="22836-107">Oto elementy, które są potrzebne:</span><span class="sxs-lookup"><span data-stu-id="22836-107">Here's the items you need:</span></span>

* <span data-ttu-id="22836-108">Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="22836-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="22836-109">[Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22836-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="22836-110">Musi mieć konto integracji dekodowania X12 łącznika komunikatu.</span><span class="sxs-lookup"><span data-stu-id="22836-110">You must have an integration account to use the Decode X12 message connector.</span></span>
* <span data-ttu-id="22836-111">Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="22836-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="22836-112">[X12 umowy](logic-apps-enterprise-integration-x12.md) jest już zdefiniowany w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="22836-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="22836-113">Dekodowanie X12 wiadomości</span><span class="sxs-lookup"><span data-stu-id="22836-113">Decode X12 messages</span></span>

1. <span data-ttu-id="22836-114">[Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="22836-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="22836-115">Dekoduj X12 łącznika komunikatu nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="22836-115">The Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="22836-116">W Projektancie aplikacji logiki dodać wyzwalacza, a następnie dodać do aplikacji logiki akcję.</span><span class="sxs-lookup"><span data-stu-id="22836-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="22836-117">W polu wyszukiwania wprowadź "x12" filtru.</span><span class="sxs-lookup"><span data-stu-id="22836-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="22836-118">Wybierz **X12-dekodowania X12 komunikat**.</span><span class="sxs-lookup"><span data-stu-id="22836-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Wyszukaj "x12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="22836-120">Jeśli wcześniej nie utworzono wszystkie połączenia z kontem integracji, zostanie wyświetlony monit o utworzyć teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="22836-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="22836-121">Nazwa połączenia, a następnie wybierz konta integracji, na którym chcesz się połączyć.</span><span class="sxs-lookup"><span data-stu-id="22836-121">Name your connection, and select the integration account that you want to connect.</span></span> 

    ![Podaj szczegóły połączenia konta integracji](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="22836-123">Właściwości oznaczone gwiazdką są wymagane.</span><span class="sxs-lookup"><span data-stu-id="22836-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="22836-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="22836-124">Property</span></span> | <span data-ttu-id="22836-125">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="22836-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="22836-126">Nazwa połączenia *</span><span class="sxs-lookup"><span data-stu-id="22836-126">Connection Name *</span></span> |<span data-ttu-id="22836-127">Wprowadź dowolną nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="22836-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="22836-128">Konta integracji *</span><span class="sxs-lookup"><span data-stu-id="22836-128">Integration Account *</span></span> |<span data-ttu-id="22836-129">Wprowadź nazwę konta integracji.</span><span class="sxs-lookup"><span data-stu-id="22836-129">Enter a name for your integration account.</span></span> <span data-ttu-id="22836-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22836-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="22836-131">Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie do tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="22836-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="22836-132">Aby zakończyć tworzenie połączenia, wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="22836-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![Szczegóły połączenia konta integracji](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="22836-134">Po połączeniu z utworzenie, jak pokazano w tym przykładzie wybierz X12 pliku prostego komunikatu zdekodować.</span><span class="sxs-lookup"><span data-stu-id="22836-134">After your connection is created, as shown in this example, select the X12 flat file message to decode.</span></span>

    ![utworzone połączenie konta integracji](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="22836-136">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="22836-136">For example:</span></span>

    ![Wybierz X12 płaskim komunikat pliku dekodowania](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="22836-138">X12 dekodowania szczegóły</span><span class="sxs-lookup"><span data-stu-id="22836-138">X12 Decode details</span></span>

<span data-ttu-id="22836-139">X12 łącznik dekodowania wykonuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="22836-139">The X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="22836-140">Weryfikuje koperty przed handlowymi umowy z partnerem</span><span class="sxs-lookup"><span data-stu-id="22836-140">Validates the envelope against trading partner agreement</span></span>
* <span data-ttu-id="22836-141">Sprawdza poprawność właściwości specyficzne dla partnerów i EDI</span><span class="sxs-lookup"><span data-stu-id="22836-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="22836-142">Sprawdzanie poprawności strukturalnych EDI i rozszerzony schemat sprawdzania poprawności</span><span class="sxs-lookup"><span data-stu-id="22836-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="22836-143">Sprawdzanie poprawności struktury koperty wymiany.</span><span class="sxs-lookup"><span data-stu-id="22836-143">Validation of the structure of the interchange envelope.</span></span>
  * <span data-ttu-id="22836-144">Sprawdzanie poprawności schematu envelope względem schematu kontroli.</span><span class="sxs-lookup"><span data-stu-id="22836-144">Schema validation of the envelope against the control schema.</span></span>
  * <span data-ttu-id="22836-145">Sprawdzanie poprawności schematu elementów dane zestawu transakcji względem schematu wiadomości.</span><span class="sxs-lookup"><span data-stu-id="22836-145">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="22836-146">EDI weryfikacji w przypadku elementów dane zestawu transakcji</span><span class="sxs-lookup"><span data-stu-id="22836-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="22836-147">Sprawdza, czy numery kontroli zestawu wymiany, grupy i transakcji nie są duplikatami</span><span class="sxs-lookup"><span data-stu-id="22836-147">Verifies that the interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="22836-148">Sprawdza numer kontroli wymiany przed wymianę wcześniej odebrane.</span><span class="sxs-lookup"><span data-stu-id="22836-148">Checks the interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="22836-149">Sprawdza, czy numer grupy kontroli względem innych numery kontroli grupy w wymiany.</span><span class="sxs-lookup"><span data-stu-id="22836-149">Checks the group control number against other group control numbers in the interchange.</span></span>
  * <span data-ttu-id="22836-150">Sprawdza, czy transakcja Ustaw numer kontroli względem innych numery kontroli zestawu transakcji w tej grupie.</span><span class="sxs-lookup"><span data-stu-id="22836-150">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="22836-151">Dzieli wymiany w zestawy transakcji lub zachowuje całego wymiany:</span><span class="sxs-lookup"><span data-stu-id="22836-151">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="22836-152">Wymiany podziału jako zestawy transakcji - zawiesić zestawy transakcji o błędzie: wymiany podziałów do transakcji ustawia i analizuje każdego zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="22836-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="22836-153">X12 akcji dekodowania danych wyjściowych zestawów tylko tych transakcji niepowodzenie sprawdzania poprawności do `badMessages`i ustawia transakcji pozostałe dane wyjściowe `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="22836-153">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="22836-154">Podziel wymiany jako zestawy transakcji - zawiesić wymiany na błąd: wymiany podziałów do transakcji ustawia i analizuje każdego zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="22836-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="22836-155">Jeśli jeden lub więcej transakcji ustawia w wymiany wystąpi niepowodzenie weryfikacji, X12 akcji dekodowania danych wyjściowych ustawia wszystkich transakcji w tym wymiany do `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="22836-155">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="22836-156">Zachowaj wymiany — zawiesza zestawy transakcji na błąd: Zachowaj wymiany i przetwarzanie całego wsadowej operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="22836-156">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="22836-157">X12 akcji dekodowania danych wyjściowych zestawów tylko tych transakcji niepowodzenie sprawdzania poprawności do `badMessages`i ustawia transakcji pozostałe dane wyjściowe `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="22836-157">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="22836-158">Zachowaj wymiany — zawiesza wymiany na błąd: Zachowaj wymiany i przetwarzanie całego wsadowej operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="22836-158">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="22836-159">Jeśli jeden lub więcej transakcji ustawia w wymiany wystąpi niepowodzenie weryfikacji, X12 akcji dekodowania danych wyjściowych ustawia wszystkich transakcji w tym wymiany do `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="22836-159">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span> 
* <span data-ttu-id="22836-160">Generuje potwierdzenia techniczne i/lub funkcjonalne (jeśli jest skonfigurowane).</span><span class="sxs-lookup"><span data-stu-id="22836-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="22836-161">Generuje techniczne potwierdzenia wyniku weryfikacji nagłówka.</span><span class="sxs-lookup"><span data-stu-id="22836-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="22836-162">Potwierdzenie techniczne informuje o stanie przetwarzania nagłówka wymiany i przyczepy przez odbiornik. adres.</span><span class="sxs-lookup"><span data-stu-id="22836-162">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver.</span></span>
  * <span data-ttu-id="22836-163">Generuje funkcjonalności potwierdzenia wyniku weryfikacji treści.</span><span class="sxs-lookup"><span data-stu-id="22836-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="22836-164">Potwierdzenie funkcjonalności raporty każdego wystąpił błąd podczas przetwarzania odebranego dokumentu</span><span class="sxs-lookup"><span data-stu-id="22836-164">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="22836-165">Wyświetlanie struktury swagger</span><span class="sxs-lookup"><span data-stu-id="22836-165">View the swagger</span></span>
<span data-ttu-id="22836-166">Zobacz [swagger szczegóły](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="22836-166">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="22836-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22836-167">Next steps</span></span>
[<span data-ttu-id="22836-168">Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="22836-168">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

