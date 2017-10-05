---
title: "Tworzenie rozwiązań B2B - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Odbieranie danych w aplikacjach logiki za pomocą funkcji B2B w pakiet integracyjny dla przedsiębiorstw"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 0625787ddcbc0091e70b111f687e25929720ad15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="receive-data-in-logic-apps-with-the-b2b-features-in-the-enterprise-integration-pack"></a><span data-ttu-id="46044-103">Odbieranie danych w aplikacjach logiki z funkcjami B2B w pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="46044-103">Receive data in logic apps with the B2B features in the Enterprise Integration Pack</span></span>

<span data-ttu-id="46044-104">Po utworzeniu konta integracji z partnerami i umowy, można przystąpić do tworzenia przepływu pracy (B2B) firma do firma aplikację logiki z [pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46044-104">After you create an integration account that has partners and agreements, you are ready to create a business to business (B2B) workflow for your logic app with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46044-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="46044-105">Prerequisites</span></span>

<span data-ttu-id="46044-106">Aby użyć AS2 i X12 akcje, muszą mieć konta integracji przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="46044-106">To use the AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="46044-107">Dowiedz się [sposobu tworzenia konta integracji przedsiębiorstwa](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="46044-107">Learn [how to create an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="46044-108">Tworzenie aplikacji logiki z łączniki B2B</span><span class="sxs-lookup"><span data-stu-id="46044-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="46044-109">Wykonaj następujące kroki, aby utworzyć aplikację logiki B2B, który używa AS2 i X12 akcje na odbieranie danych z partnerem handlowym:</span><span class="sxs-lookup"><span data-stu-id="46044-109">Follow these steps to create a B2B logic app that uses the AS2 and X12 actions to receive data from a trading partner:</span></span>

1. <span data-ttu-id="46044-110">Tworzenie aplikacji logiki, następnie [połączyć aplikację z kontem integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="46044-110">Create a logic app, then [link your app to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="46044-111">Dodaj **żądania - zostanie odebrane żądanie HTTP podczas** do aplikacji logiki wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="46044-111">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="46044-112">Aby dodać **dekodowania AS2** akcji wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="46044-112">To add the **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="46044-113">Aby filtrować wszystkie akcje do tego, który ma, wprowadź słowo **as2** w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="46044-113">To filter all actions to the one that you want, enter the word **as2** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="46044-114">Wybierz **AS2 - AS2 zdekodować komunikatu** akcji.</span><span class="sxs-lookup"><span data-stu-id="46044-114">Select the **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="46044-115">Dodaj **treści** , który ma być używany jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="46044-115">Add the **Body** that you want to use as input.</span></span> <span data-ttu-id="46044-116">W tym przykładzie wybierz treści żądania HTTP, które wyzwala aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="46044-116">In this example, select the body of the HTTP request that triggers the logic app.</span></span> <span data-ttu-id="46044-117">Lub wprowadź wyrażenie danych wejściowych nagłówków **nagłówki** pola:</span><span class="sxs-lookup"><span data-stu-id="46044-117">Or enter an expression that inputs the headers in the **HEADERS** field:</span></span>

    <span data-ttu-id="46044-118">@triggerOutputs() [nagłówki]</span><span class="sxs-lookup"><span data-stu-id="46044-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="46044-119">Dodaj wymagane **nagłówki** dla AS2, który można znaleźć w nagłówkach żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="46044-119">Add the required **Headers** for AS2, which you can find in the HTTP request headers.</span></span> <span data-ttu-id="46044-120">W tym przykładzie wybierz nagłówki żądania HTTP, wyzwalających aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="46044-120">In this example, select the headers of the HTTP request that trigger the logic app.</span></span>

8. <span data-ttu-id="46044-121">Teraz Dodaj dekodowania X12 Akcja komunikatu.</span><span class="sxs-lookup"><span data-stu-id="46044-121">Now add the Decode X12 message action.</span></span> <span data-ttu-id="46044-122">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="46044-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="46044-123">Aby filtrować wszystkie akcje do tego, który ma, wprowadź słowo **x12** w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="46044-123">To filter all actions to the one that you want, enter the word **x12** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="46044-124">Wybierz **X12-dekodowania X12 komunikat** akcji.</span><span class="sxs-lookup"><span data-stu-id="46044-124">Select the **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="46044-125">Teraz należy określić w danych wejściowych tej akcji.</span><span class="sxs-lookup"><span data-stu-id="46044-125">Now you must specify the input to this action.</span></span> <span data-ttu-id="46044-126">Tych danych wejściowych jest dane wyjściowe z poprzedniej akcji AS2.</span><span class="sxs-lookup"><span data-stu-id="46044-126">This input is the output from the previous AS2 action.</span></span>

    <span data-ttu-id="46044-127">Zawartość komunikatu rzeczywiste w obiekcie JSON i jest kodowanie base64, dlatego należy określić wyrażenie jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="46044-127">The actual message content is in a JSON object and is base64 encoded, so you must specify an expression as the input.</span></span> 
    <span data-ttu-id="46044-128">Wprowadź poniższe wyrażenie w **X12 PŁASKIM pliku wiadomości do dekodowania** pola wejściowego:</span><span class="sxs-lookup"><span data-stu-id="46044-128">Enter the following expression in the **X12 FLAT FILE MESSAGE TO DECODE** input field:</span></span>
    
    <span data-ttu-id="46044-129">@base64ToString(body('Decode_AS2_message')? ["AS2Message"]? ["Content"])</span><span class="sxs-lookup"><span data-stu-id="46044-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="46044-130">Teraz dodać kroki w celu zdekodowania X12 dane odebrane z partnerem handlowym i dane wyjściowe elementów w obiekcie JSON.</span><span class="sxs-lookup"><span data-stu-id="46044-130">Now add steps to decode the X12 data received from the trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="46044-131">Powiadomiono partnera otrzymanie danych, możesz wysłać ponownie odpowiedzi zawierające powiadomienia dyspozycji wiadomości (MDN) AS2, w akcji odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="46044-131">To notify the partner that the data was received, you can send back a response containing the AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="46044-132">Aby dodać **odpowiedzi** akcji, wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="46044-132">To add the **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="46044-133">Aby filtrować wszystkie akcje do tego, który ma, wprowadź słowo **odpowiedzi** w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="46044-133">To filter all actions to the one that you want, enter the word **response** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="46044-134">Wybierz **odpowiedzi** akcji.</span><span class="sxs-lookup"><span data-stu-id="46044-134">Select the **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="46044-135">Dostęp MDN z danych wyjściowych do **komunikat dekodowania X12** akcji, ustaw odpowiedzi **treści** wartością tego wyrażenia:</span><span class="sxs-lookup"><span data-stu-id="46044-135">To access the MDN from the output of the **Decode X12 message** action, set the response **BODY** field with this expression:</span></span>

    <span data-ttu-id="46044-136">@base64ToString(body('Decode_AS2_message')? ["OutgoingMdn"]? ["Content"])</span><span class="sxs-lookup"><span data-stu-id="46044-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="46044-137">Zapisz swoją pracę.</span><span class="sxs-lookup"><span data-stu-id="46044-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="46044-138">Teraz po zakończeniu konfigurowania aplikacji logiki B2B.</span><span class="sxs-lookup"><span data-stu-id="46044-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="46044-139">W przypadku aplikacji rzeczywistych można przechowywać X12 dekodowane dane w magazynie — biznesowych (LOB) aplikacji lub danych.</span><span class="sxs-lookup"><span data-stu-id="46044-139">In a real world application, you might want to store the decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="46044-140">Aby połączyć aplikacje LOB i użycia tych interfejsów API w aplikacji logiki, można dodać dodatkowe akcje lub zapisać niestandardowych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="46044-140">To connect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="46044-141">Funkcje i przypadki użycia</span><span class="sxs-lookup"><span data-stu-id="46044-141">Features and use cases</span></span>

* <span data-ttu-id="46044-142">AS2 i X12 dekodowania i kodowania akcje let wymiany danych między partnerami handlowymi przy użyciu standardowych protokołach branżowych w aplikacjach logiki.</span><span class="sxs-lookup"><span data-stu-id="46044-142">The AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="46044-143">Wymiana danych z partnerami handlowymi, umożliwia AS2 i X12 z lub bez siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="46044-143">To exchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="46044-144">Akcje B2B pomóc łatwe tworzenie partnerów i umów w ramach konta integracji i używać ich w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="46044-144">The B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="46044-145">Podczas rozszerzania aplikacji logiki z innymi działaniami umożliwia wysyłanie oraz odbieranie danych między innych aplikacji i usług, takich jak SalesForce.</span><span class="sxs-lookup"><span data-stu-id="46044-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="46044-146">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="46044-146">Learn more</span></span>
[<span data-ttu-id="46044-147">Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="46044-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
