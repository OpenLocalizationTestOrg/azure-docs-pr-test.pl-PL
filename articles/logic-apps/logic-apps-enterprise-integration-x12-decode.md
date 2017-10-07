---
title: "komunikaty aaaDecode X12 — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i generowanie potwierdzeń z dekodera wiadomość hello X12 w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
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
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="86383-103">Dekodowanie X12 komunikatów dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="86383-103">Decode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="86383-104">Łącznik wiadomość hello dekodowania X12 można zweryfikować koperty hello przed umowy z partnerem handlowym, sprawdzanie poprawności EDI i właściwości specyficzne dla partnera, podzielić wymianę w zestawy transakcji lub zachować całą wymianę i generowanie potwierdzenia dla przetworzonych transakcji.</span><span class="sxs-lookup"><span data-stu-id="86383-104">With hello Decode X12 message connector, you can validate hello envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="86383-105">toouse tego łącznika, należy dodać tooan łącznika hello istniejących wyzwalacza w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="86383-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="86383-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="86383-106">Before you start</span></span>

<span data-ttu-id="86383-107">Oto hello elementy, które należy:</span><span class="sxs-lookup"><span data-stu-id="86383-107">Here's hello items you need:</span></span>

* <span data-ttu-id="86383-108">Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="86383-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="86383-109">[Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="86383-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="86383-110">Musi mieć łącznik wiadomość hello dekodowania X12 integracji konta toouse.</span><span class="sxs-lookup"><span data-stu-id="86383-110">You must have an integration account toouse hello Decode X12 message connector.</span></span>
* <span data-ttu-id="86383-111">Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="86383-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="86383-112">[X12 umowy](logic-apps-enterprise-integration-x12.md) jest już zdefiniowany w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="86383-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="86383-113">Dekodowanie X12 wiadomości</span><span class="sxs-lookup"><span data-stu-id="86383-113">Decode X12 messages</span></span>

1. <span data-ttu-id="86383-114">[Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="86383-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="86383-115">Hello dekodowania X12 komunikat łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="86383-115">hello Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="86383-116">W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.</span><span class="sxs-lookup"><span data-stu-id="86383-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="86383-117">W polu wyszukiwania hello wprowadź "x12" filtru.</span><span class="sxs-lookup"><span data-stu-id="86383-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="86383-118">Wybierz **X12-dekodowania X12 komunikat**.</span><span class="sxs-lookup"><span data-stu-id="86383-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Wyszukaj "x12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="86383-120">Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="86383-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="86383-121">Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect.</span><span class="sxs-lookup"><span data-stu-id="86383-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 

    ![Podaj szczegóły połączenia konta integracji](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="86383-123">Właściwości oznaczone gwiazdką są wymagane.</span><span class="sxs-lookup"><span data-stu-id="86383-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="86383-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="86383-124">Property</span></span> | <span data-ttu-id="86383-125">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="86383-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="86383-126">Nazwa połączenia *</span><span class="sxs-lookup"><span data-stu-id="86383-126">Connection Name *</span></span> |<span data-ttu-id="86383-127">Wprowadź dowolną nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="86383-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="86383-128">Konta integracji *</span><span class="sxs-lookup"><span data-stu-id="86383-128">Integration Account *</span></span> |<span data-ttu-id="86383-129">Wprowadź nazwę konta integracji.</span><span class="sxs-lookup"><span data-stu-id="86383-129">Enter a name for your integration account.</span></span> <span data-ttu-id="86383-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="86383-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="86383-131">Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie przykład toothis.</span><span class="sxs-lookup"><span data-stu-id="86383-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="86383-132">Wybierz toofinish Tworzenie połączenia **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="86383-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![Szczegóły połączenia konta integracji](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="86383-134">Po utworzeniu połączenia, jak pokazano w poniższym przykładzie, wybierz toodecode komunikat pliku prostego powitania X12.</span><span class="sxs-lookup"><span data-stu-id="86383-134">After your connection is created, as shown in this example, select hello X12 flat file message toodecode.</span></span>

    ![utworzone połączenie konta integracji](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="86383-136">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="86383-136">For example:</span></span>

    ![Wybierz X12 płaskim komunikat pliku dekodowania](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="86383-138">X12 dekodowania szczegóły</span><span class="sxs-lookup"><span data-stu-id="86383-138">X12 Decode details</span></span>

<span data-ttu-id="86383-139">Łącznik dekodowania Hello X12 wykonuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="86383-139">hello X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="86383-140">Weryfikuje koperty hello przed handlowymi umowy z partnerem</span><span class="sxs-lookup"><span data-stu-id="86383-140">Validates hello envelope against trading partner agreement</span></span>
* <span data-ttu-id="86383-141">Sprawdza poprawność właściwości specyficzne dla partnerów i EDI</span><span class="sxs-lookup"><span data-stu-id="86383-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="86383-142">Sprawdzanie poprawności strukturalnych EDI i rozszerzony schemat sprawdzania poprawności</span><span class="sxs-lookup"><span data-stu-id="86383-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="86383-143">Sprawdzanie poprawności hello struktury hello koperty wymiany.</span><span class="sxs-lookup"><span data-stu-id="86383-143">Validation of hello structure of hello interchange envelope.</span></span>
  * <span data-ttu-id="86383-144">Sprawdzanie poprawności schematu koperty hello schematem hello kontroli.</span><span class="sxs-lookup"><span data-stu-id="86383-144">Schema validation of hello envelope against hello control schema.</span></span>
  * <span data-ttu-id="86383-145">Sprawdzanie poprawności schematu elementów dane zestawu transakcji hello schematem wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="86383-145">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="86383-146">EDI weryfikacji w przypadku elementów dane zestawu transakcji</span><span class="sxs-lookup"><span data-stu-id="86383-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="86383-147">Sprawdza, czy hello wymiany, grupy i transakcji zestaw numerów kontroli nie są duplikatami</span><span class="sxs-lookup"><span data-stu-id="86383-147">Verifies that hello interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="86383-148">Sprawdza hello wymiany kontroli numer przed wymianę wcześniej odebrane.</span><span class="sxs-lookup"><span data-stu-id="86383-148">Checks hello interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="86383-149">Sprawdza hello grupy kontroli numer względem innych numery kontroli grupy w hello wymiany.</span><span class="sxs-lookup"><span data-stu-id="86383-149">Checks hello group control number against other group control numbers in hello interchange.</span></span>
  * <span data-ttu-id="86383-150">Sprawdza, czy transakcja hello Ustaw numer kontroli względem innych numery kontroli zestawu transakcji w tej grupie.</span><span class="sxs-lookup"><span data-stu-id="86383-150">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="86383-151">Dzieli wymiany hello w zestawy transakcji lub zachowuje hello całego wymiany:</span><span class="sxs-lookup"><span data-stu-id="86383-151">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="86383-152">Wymiany podziału jako zestawy transakcji - zawiesić zestawy transakcji o błędzie: wymiany podziałów do transakcji ustawia i analizuje każdego zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="86383-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="86383-153">Akcja dekodowania Hello X12 wyświetla tylko te zestawy transakcji, Niepowodzenie weryfikacji za`badMessages`i wyświetla hello pozostałych transakcji ustawia zbyt`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="86383-153">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="86383-154">Podziel wymiany jako zestawy transakcji - zawiesić wymiany na błąd: wymiany podziałów do transakcji ustawia i analizuje każdego zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="86383-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="86383-155">Jeśli jeden lub więcej transakcji ustawia w hello wymiany Niepowodzenie weryfikacji, hello X12 dekodowania akcji generuje wszystkich transakcji hello ustawia w tym wymiany zbyt`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="86383-155">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="86383-156">Zachowaj wymiany — zawiesza zestawy transakcji na błąd: proces i Zachowaj hello wymiany hello całego wsadowej operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="86383-156">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="86383-157">Akcja dekodowania Hello X12 wyświetla tylko te zestawy transakcji, Niepowodzenie weryfikacji za`badMessages`i wyświetla hello pozostałych transakcji ustawia zbyt`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="86383-157">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="86383-158">Zachowaj wymiany — zawiesza wymiany na błąd: proces i Zachowaj hello wymiany hello całego wsadowej operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="86383-158">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="86383-159">Jeśli jeden lub więcej transakcji ustawia w hello wymiany Niepowodzenie weryfikacji, hello X12 dekodowania akcji generuje wszystkich transakcji hello ustawia w tym wymiany zbyt`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="86383-159">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span> 
* <span data-ttu-id="86383-160">Generuje potwierdzenia techniczne i/lub funkcjonalne (jeśli jest skonfigurowane).</span><span class="sxs-lookup"><span data-stu-id="86383-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="86383-161">Generuje techniczne potwierdzenia wyniku weryfikacji nagłówka.</span><span class="sxs-lookup"><span data-stu-id="86383-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="86383-162">Hello techniczne potwierdzenia raporty hello stan przetwarzania hello wymiany nagłówka i przyczepy przez hello adres odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="86383-162">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver.</span></span>
  * <span data-ttu-id="86383-163">Generuje funkcjonalności potwierdzenia wyniku weryfikacji treści.</span><span class="sxs-lookup"><span data-stu-id="86383-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="86383-164">Witaj potwierdzenia funkcjonalności raporty każdy błąd podczas przetwarzania hello otrzymał dokument</span><span class="sxs-lookup"><span data-stu-id="86383-164">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="86383-165">Widok hello swagger</span><span class="sxs-lookup"><span data-stu-id="86383-165">View hello swagger</span></span>
<span data-ttu-id="86383-166">Zobacz hello [swagger szczegóły](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="86383-166">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="86383-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86383-167">Next steps</span></span>
[<span data-ttu-id="86383-168">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="86383-168">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

