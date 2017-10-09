---
title: "komunikaty aaaEncode X12 — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdź poprawność EDI i przekonwertować kodowany w formacie XML komunikaty z X12 komunikatu kodera w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
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
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="b3c86-103">Kodowanie X12 komunikatów dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="b3c86-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="b3c86-104">Łącznik wiadomość hello Koduj X12 zweryfikować EDI i właściwości specyficzne dla partnera, przekonwertować wiadomości w formacie XML na EDI zestawów transakcji w hello wymiany, a żądania potwierdzenia technicznych i funkcjonalności potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="b3c86-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="b3c86-105">toouse tego łącznika, należy dodać tooan łącznika hello istniejących wyzwalacza w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b3c86-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="b3c86-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b3c86-106">Before you start</span></span>

<span data-ttu-id="b3c86-107">Oto hello elementy, które należy:</span><span class="sxs-lookup"><span data-stu-id="b3c86-107">Here's hello items you need:</span></span>

* <span data-ttu-id="b3c86-108">Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="b3c86-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="b3c86-109">[Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b3c86-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="b3c86-110">Musi mieć łącznik wiadomość hello Koduj X12 integracji konta toouse.</span><span class="sxs-lookup"><span data-stu-id="b3c86-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="b3c86-111">Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="b3c86-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="b3c86-112">[X12 umowy](logic-apps-enterprise-integration-x12.md) jest już zdefiniowany w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="b3c86-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="b3c86-113">Kodowanie X12 wiadomości</span><span class="sxs-lookup"><span data-stu-id="b3c86-113">Encode X12 messages</span></span>

1. <span data-ttu-id="b3c86-114">[Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b3c86-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="b3c86-115">Hello Koduj X12 komunikat łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="b3c86-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="b3c86-116">W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.</span><span class="sxs-lookup"><span data-stu-id="b3c86-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="b3c86-117">W polu wyszukiwania hello wprowadź "x12" filtru.</span><span class="sxs-lookup"><span data-stu-id="b3c86-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="b3c86-118">Wybierz opcję **X12-kodowania komunikatu tooX12 według nazwy umowy** lub **X12-kodowania komunikatu tooX12 przez tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="b3c86-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    ![Wyszukaj "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="b3c86-120">Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="b3c86-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="b3c86-121">Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b3c86-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![Integracja połączenia konta](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="b3c86-123">Właściwości oznaczone gwiazdką są wymagane.</span><span class="sxs-lookup"><span data-stu-id="b3c86-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="b3c86-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b3c86-124">Property</span></span> | <span data-ttu-id="b3c86-125">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="b3c86-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="b3c86-126">Nazwa połączenia *</span><span class="sxs-lookup"><span data-stu-id="b3c86-126">Connection Name *</span></span> |<span data-ttu-id="b3c86-127">Wprowadź dowolną nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="b3c86-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="b3c86-128">Konta integracji *</span><span class="sxs-lookup"><span data-stu-id="b3c86-128">Integration Account *</span></span> |<span data-ttu-id="b3c86-129">Wprowadź nazwę konta integracji.</span><span class="sxs-lookup"><span data-stu-id="b3c86-129">Enter a name for your integration account.</span></span> <span data-ttu-id="b3c86-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b3c86-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="b3c86-131">Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie przykład toothis.</span><span class="sxs-lookup"><span data-stu-id="b3c86-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="b3c86-132">Wybierz toofinish Tworzenie połączenia **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b3c86-132">toofinish creating your connection, choose **Create**.</span></span>

    ![utworzone połączenie konta integracji](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="b3c86-134">Utworzono połączenie.</span><span class="sxs-lookup"><span data-stu-id="b3c86-134">Your connection is now created.</span></span>

    ![Szczegóły połączenia konta integracji](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="b3c86-136">Kodowanie X12 wiadomości przez Nazwa umowy</span><span class="sxs-lookup"><span data-stu-id="b3c86-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="b3c86-137">Jeśli została wybrana opcja tooencode X12 wiadomości przez nazwę umowy, otwórz hello **nazwa X12 umowy** listy, wpisz lub wybierz Twoje istniejące X12 umowy.</span><span class="sxs-lookup"><span data-stu-id="b3c86-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="b3c86-138">Wprowadź tooencode wiadomości XML hello.</span><span class="sxs-lookup"><span data-stu-id="b3c86-138">Enter hello XML message tooencode.</span></span>

![Wprowadź X12 umowy, nazwę i XML komunikatu tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="b3c86-140">Kodowanie X12 wiadomości przez tożsamości</span><span class="sxs-lookup"><span data-stu-id="b3c86-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="b3c86-141">Wybranie tooencode X12 wiadomości przez tożsamości, wprowadź identyfikator nadawcy hello, Kwalifikator nadawcy, odbiorcy identyfikator i kwalifikator odbiornika zgodnie z konfiguracją sieci X12 umowy.</span><span class="sxs-lookup"><span data-stu-id="b3c86-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="b3c86-142">Wybierz hello tooencode wiadomości XML.</span><span class="sxs-lookup"><span data-stu-id="b3c86-142">Select hello XML message tooencode.</span></span>
   
![Podaj tożsamości dla nadawcy i odbiorcy, wybierz tooencode wiadomości XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="b3c86-144">X12 kodowania szczegóły</span><span class="sxs-lookup"><span data-stu-id="b3c86-144">X12 Encode details</span></span>

<span data-ttu-id="b3c86-145">Łącznik Koduj Hello X12 wykonuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="b3c86-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="b3c86-146">Rozwiązanie umowy przez nadawcę i odbiorcę właściwości kontekstu dopasowywania.</span><span class="sxs-lookup"><span data-stu-id="b3c86-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="b3c86-147">Serializuje hello EDI wymiany danych, konwertowanie wiadomości w formacie XML w EDI zestawy transakcji w hello wymiany.</span><span class="sxs-lookup"><span data-stu-id="b3c86-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="b3c86-148">Stosuje zestaw transakcji nagłówka i przyczepy segmentów</span><span class="sxs-lookup"><span data-stu-id="b3c86-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="b3c86-149">Generuje numer formantu wymiany, numer kontroli grupy i numer kontroli zestawu transakcji, każdy wychodzący wymiany</span><span class="sxs-lookup"><span data-stu-id="b3c86-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="b3c86-150">Zastępuje separatorów hello ładunek danych</span><span class="sxs-lookup"><span data-stu-id="b3c86-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="b3c86-151">Sprawdza poprawność właściwości specyficzne dla partnerów i EDI</span><span class="sxs-lookup"><span data-stu-id="b3c86-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="b3c86-152">Sprawdzanie poprawności schematu elementów dane zestawu transakcji hello przed wiadomość hello schematu</span><span class="sxs-lookup"><span data-stu-id="b3c86-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="b3c86-153">EDI Weryfikacja w przypadku elementów dane zestawu transakcji.</span><span class="sxs-lookup"><span data-stu-id="b3c86-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="b3c86-154">Rozszerzonej weryfikacji w przypadku elementów dane zestawu transakcji</span><span class="sxs-lookup"><span data-stu-id="b3c86-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="b3c86-155">Żądania potwierdzenia techniczne i/lub funkcjonalne (jeśli jest skonfigurowane).</span><span class="sxs-lookup"><span data-stu-id="b3c86-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="b3c86-156">Generuje techniczne potwierdzenia wyniku weryfikacji nagłówka.</span><span class="sxs-lookup"><span data-stu-id="b3c86-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="b3c86-157">Stan hello raportów technicznych potwierdzenia Hello hello przetwarzania nagłówka wymiany i przyczepy przez hello adres odbiorcy</span><span class="sxs-lookup"><span data-stu-id="b3c86-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="b3c86-158">Generuje funkcjonalności potwierdzenia wyniku weryfikacji treści.</span><span class="sxs-lookup"><span data-stu-id="b3c86-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="b3c86-159">Witaj potwierdzenia funkcjonalności raporty każdy błąd podczas przetwarzania hello otrzymał dokument</span><span class="sxs-lookup"><span data-stu-id="b3c86-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="b3c86-160">Widok hello swagger</span><span class="sxs-lookup"><span data-stu-id="b3c86-160">View hello swagger</span></span>
<span data-ttu-id="b3c86-161">Zobacz hello [swagger szczegóły](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="b3c86-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b3c86-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3c86-162">Next steps</span></span>
[<span data-ttu-id="b3c86-163">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="b3c86-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

