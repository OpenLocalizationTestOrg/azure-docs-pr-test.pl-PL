---
title: "Kodowanie X12 wiadomości - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i przekonwertować kodowany w formacie XML komunikaty z X12 komunikatu kodera w pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 29d19364b9a98e351c95f13e68a2e63b9f6439f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="6a4d6-103">Kodowanie X12 wiadomości dla usługi Azure Logic Apps z pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="6a4d6-103">Encode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="6a4d6-104">Łącznik komunikat Koduj X12 zweryfikować EDI i właściwości specyficzne dla partnera, przekonwertować wiadomości w formacie XML na EDI zestawów transakcji w wymiany, a żądania potwierdzenia technicznych i funkcjonalności potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="6a4d6-105">Aby użyć tego łącznika, należy dodać łącznika do istniejącego wyzwalacza w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="6a4d6-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6a4d6-106">Before you start</span></span>

<span data-ttu-id="6a4d6-107">Oto elementy, które są potrzebne:</span><span class="sxs-lookup"><span data-stu-id="6a4d6-107">Here's the items you need:</span></span>

* <span data-ttu-id="6a4d6-108">Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="6a4d6-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="6a4d6-109">[Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="6a4d6-110">Musi mieć konto integracji Koduj X12 łącznika komunikatu.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-110">You must have an integration account to use the Encode X12 message connector.</span></span>
* <span data-ttu-id="6a4d6-111">Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="6a4d6-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="6a4d6-112">[X12 umowy](logic-apps-enterprise-integration-x12.md) jest już zdefiniowany w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="6a4d6-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="6a4d6-113">Kodowanie X12 wiadomości</span><span class="sxs-lookup"><span data-stu-id="6a4d6-113">Encode X12 messages</span></span>

1. <span data-ttu-id="6a4d6-114">[Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6a4d6-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="6a4d6-115">Koduj X12 łącznika komunikatu nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="6a4d6-116">W Projektancie aplikacji logiki dodać wyzwalacza, a następnie dodać do aplikacji logiki akcję.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="6a4d6-117">W polu wyszukiwania wprowadź "x12" filtru.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="6a4d6-118">Wybierz opcję **X12 —, zakodować w X12 komunikatu przez Nazwa umowy** lub **X12 —, zakodować w X12 komunikatu przez tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span></span>
   
    ![Wyszukaj "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="6a4d6-120">Jeśli wcześniej nie utworzono wszystkie połączenia z kontem integracji, zostanie wyświetlony monit o utworzyć teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="6a4d6-121">Nazwa połączenia, a następnie wybierz konta integracji, na którym chcesz się połączyć.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![Integracja połączenia konta](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="6a4d6-123">Właściwości oznaczone gwiazdką są wymagane.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="6a4d6-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6a4d6-124">Property</span></span> | <span data-ttu-id="6a4d6-125">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="6a4d6-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="6a4d6-126">Nazwa połączenia *</span><span class="sxs-lookup"><span data-stu-id="6a4d6-126">Connection Name *</span></span> |<span data-ttu-id="6a4d6-127">Wprowadź dowolną nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="6a4d6-128">Konta integracji *</span><span class="sxs-lookup"><span data-stu-id="6a4d6-128">Integration Account *</span></span> |<span data-ttu-id="6a4d6-129">Wprowadź nazwę konta integracji.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-129">Enter a name for your integration account.</span></span> <span data-ttu-id="6a4d6-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="6a4d6-131">Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie do tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="6a4d6-132">Aby zakończyć tworzenie połączenia, wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-132">To finish creating your connection, choose **Create**.</span></span>

    ![utworzone połączenie konta integracji](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="6a4d6-134">Utworzono połączenie.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-134">Your connection is now created.</span></span>

    ![Szczegóły połączenia konta integracji](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="6a4d6-136">Kodowanie X12 wiadomości przez Nazwa umowy</span><span class="sxs-lookup"><span data-stu-id="6a4d6-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="6a4d6-137">Jeśli zdecydujesz się na kodowania X12 otworzyć wiadomości przez Nazwa umowy **nazwa X12 umowy** listy, wpisz lub wybierz Twoje istniejące X12 umowy.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="6a4d6-138">Wprowadź komunikat XML do kodowania.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-138">Enter the XML message to encode.</span></span>

![Wprowadź X12 Nazwa umowy i wiadomości XML do kodowania](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="6a4d6-140">Kodowanie X12 wiadomości przez tożsamości</span><span class="sxs-lookup"><span data-stu-id="6a4d6-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="6a4d6-141">Jeśli wybierzesz do kodowania X12 wiadomości przez tożsamości, wprowadź identyfikator nadawcy, Kwalifikator nadawcy, odbiorcy identyfikator i kwalifikator odbiornik, zgodnie z konfiguracją sieci X12 umowy.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="6a4d6-142">Wybierz wiadomości XML do kodowania.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-142">Select the XML message to encode.</span></span>
   
![Podaj tożsamości dla nadawcy i odbiorcy, wybierz wiadomości XML do kodowania](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="6a4d6-144">X12 kodowania szczegóły</span><span class="sxs-lookup"><span data-stu-id="6a4d6-144">X12 Encode details</span></span>

<span data-ttu-id="6a4d6-145">X12 łącznik Koduj wykonuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="6a4d6-145">The X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="6a4d6-146">Rozwiązanie umowy przez nadawcę i odbiorcę właściwości kontekstu dopasowywania.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="6a4d6-147">Serializuje wymiany EDI, konwertowanie wiadomości w formacie XML w EDI zestawy transakcji w wymiany.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="6a4d6-148">Stosuje zestaw transakcji nagłówka i przyczepy segmentów</span><span class="sxs-lookup"><span data-stu-id="6a4d6-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="6a4d6-149">Generuje numer formantu wymiany, numer kontroli grupy i numer kontroli zestawu transakcji, każdy wychodzący wymiany</span><span class="sxs-lookup"><span data-stu-id="6a4d6-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="6a4d6-150">Zastępuje separatorów w danych ładunku</span><span class="sxs-lookup"><span data-stu-id="6a4d6-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="6a4d6-151">Sprawdza poprawność właściwości specyficzne dla partnerów i EDI</span><span class="sxs-lookup"><span data-stu-id="6a4d6-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="6a4d6-152">Sprawdzanie poprawności schematu elementów dane zestawu transakcji dla komunikatu schematu</span><span class="sxs-lookup"><span data-stu-id="6a4d6-152">Schema validation of the transaction-set data elements against the message Schema</span></span>
  * <span data-ttu-id="6a4d6-153">EDI Weryfikacja w przypadku elementów dane zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="6a4d6-154">Rozszerzonej weryfikacji w przypadku elementów dane zestawu transakcji</span><span class="sxs-lookup"><span data-stu-id="6a4d6-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="6a4d6-155">Żądania potwierdzenia techniczne i/lub funkcjonalne (jeśli jest skonfigurowane).</span><span class="sxs-lookup"><span data-stu-id="6a4d6-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="6a4d6-156">Generuje techniczne potwierdzenia wyniku weryfikacji nagłówka.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="6a4d6-157">Potwierdzenie techniczne informuje o stanie przetwarzanie nagłówka wymiany i przyczepy przez odbiornik adresu</span><span class="sxs-lookup"><span data-stu-id="6a4d6-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span></span>
  * <span data-ttu-id="6a4d6-158">Generuje funkcjonalności potwierdzenia wyniku weryfikacji treści.</span><span class="sxs-lookup"><span data-stu-id="6a4d6-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="6a4d6-159">Potwierdzenie funkcjonalności raporty każdego wystąpił błąd podczas przetwarzania odebranego dokumentu</span><span class="sxs-lookup"><span data-stu-id="6a4d6-159">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="6a4d6-160">Wyświetlanie struktury swagger</span><span class="sxs-lookup"><span data-stu-id="6a4d6-160">View the swagger</span></span>
<span data-ttu-id="6a4d6-161">Zobacz [swagger szczegóły](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="6a4d6-161">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6a4d6-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a4d6-162">Next steps</span></span>
[<span data-ttu-id="6a4d6-163">Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="6a4d6-163">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

