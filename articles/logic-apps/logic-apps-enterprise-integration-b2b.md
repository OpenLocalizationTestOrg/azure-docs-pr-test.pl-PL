---
title: "rozwiązania aaaCreate B2B - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Odbieranie danych w aplikacjach logiki za pomocą funkcji hello B2B w hello pakiet integracyjny dla przedsiębiorstw"
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
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a><span data-ttu-id="3a01b-103">Odbieranie danych w aplikacjach logiki z funkcjami B2B hello w hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="3a01b-103">Receive data in logic apps with hello B2B features in hello Enterprise Integration Pack</span></span>

<span data-ttu-id="3a01b-104">Po utworzeniu konta integracji z partnerami i umów są gotowe toocreate biznesowego przepływu pracy toobusiness (B2B) dla aplikacji logiki z hello [pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3a01b-104">After you create an integration account that has partners and agreements, you are ready toocreate a business toobusiness (B2B) workflow for your logic app with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a01b-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3a01b-105">Prerequisites</span></span>

<span data-ttu-id="3a01b-106">Witaj toouse AS2 i X12 akcje, muszą mieć konta integracji przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="3a01b-106">toouse hello AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="3a01b-107">Dowiedz się [jak toocreate integracji przedsiębiorstwa konta](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="3a01b-107">Learn [how toocreate an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="3a01b-108">Tworzenie aplikacji logiki z łączniki B2B</span><span class="sxs-lookup"><span data-stu-id="3a01b-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="3a01b-109">Wykonaj te kroki toocreate B2B logikę aplikacji, która używa hello AS2 i X12 akcje tooreceive danych z partnerem handlowym:</span><span class="sxs-lookup"><span data-stu-id="3a01b-109">Follow these steps toocreate a B2B logic app that uses hello AS2 and X12 actions tooreceive data from a trading partner:</span></span>

1. <span data-ttu-id="3a01b-110">Tworzenie aplikacji logiki, następnie [połączone konto integracji aplikacji tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="3a01b-110">Create a logic app, then [link your app tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="3a01b-111">Dodaj **żądania - zostanie odebrane żądanie HTTP podczas** aplikacji logiki tooyour wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="3a01b-111">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="3a01b-112">Witaj tooadd **dekodowania AS2** akcji, wybierz opcję **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="3a01b-112">tooadd hello **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="3a01b-113">toofilter wszystkie toohello akcje ma, wprowadź wyraz hello **as2** hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="3a01b-113">toofilter all actions toohello one that you want, enter hello word **as2** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="3a01b-114">Wybierz hello **AS2 - AS2 zdekodować komunikatu** akcji.</span><span class="sxs-lookup"><span data-stu-id="3a01b-114">Select hello **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="3a01b-115">Dodaj hello **treści** , które mają toouse jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="3a01b-115">Add hello **Body** that you want toouse as input.</span></span> <span data-ttu-id="3a01b-116">W tym przykładzie wybierz hello treści żądania HTTP hello czy wyzwalaczy hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="3a01b-116">In this example, select hello body of hello HTTP request that triggers hello logic app.</span></span> <span data-ttu-id="3a01b-117">Lub wprowadź wyrażenie danych wejściowych hello nagłówków hello **nagłówki** pola:</span><span class="sxs-lookup"><span data-stu-id="3a01b-117">Or enter an expression that inputs hello headers in hello **HEADERS** field:</span></span>

    <span data-ttu-id="3a01b-118">@triggerOutputs() [nagłówki]</span><span class="sxs-lookup"><span data-stu-id="3a01b-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="3a01b-119">Dodaj wymagane hello **nagłówki** dla AS2, który można znaleźć w nagłówkach żądania hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="3a01b-119">Add hello required **Headers** for AS2, which you can find in hello HTTP request headers.</span></span> <span data-ttu-id="3a01b-120">W tym przykładzie wybierz hello nagłówków żądania HTTP hello aplikacji logiki hello tego wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="3a01b-120">In this example, select hello headers of hello HTTP request that trigger hello logic app.</span></span>

8. <span data-ttu-id="3a01b-121">Teraz Dodaj hello dekodowania X12 komunikat akcji.</span><span class="sxs-lookup"><span data-stu-id="3a01b-121">Now add hello Decode X12 message action.</span></span> <span data-ttu-id="3a01b-122">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="3a01b-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="3a01b-123">toofilter wszystkie toohello akcje ma, wprowadź wyraz hello **x12** hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="3a01b-123">toofilter all actions toohello one that you want, enter hello word **x12** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="3a01b-124">Wybierz hello **X12-dekodowania X12 komunikat** akcji.</span><span class="sxs-lookup"><span data-stu-id="3a01b-124">Select hello **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="3a01b-125">Teraz należy określić hello wejściowych toothis akcji.</span><span class="sxs-lookup"><span data-stu-id="3a01b-125">Now you must specify hello input toothis action.</span></span> <span data-ttu-id="3a01b-126">Tych danych wejściowych jest hello hello poprzedniej akcji AS2 dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3a01b-126">This input is hello output from hello previous AS2 action.</span></span>

    <span data-ttu-id="3a01b-127">zawartości rzeczywiste wiadomość Hello jest w obiekcie JSON i kodowanie base64, dlatego należy określić wyrażenie jako dane wejściowe hello.</span><span class="sxs-lookup"><span data-stu-id="3a01b-127">hello actual message content is in a JSON object and is base64 encoded, so you must specify an expression as hello input.</span></span> 
    <span data-ttu-id="3a01b-128">Wprowadź powitania po wyrażeniu w hello **X12 PŁASKIM tooDECODE komunikat pliku** pola wejściowego:</span><span class="sxs-lookup"><span data-stu-id="3a01b-128">Enter hello following expression in hello **X12 FLAT FILE MESSAGE tooDECODE** input field:</span></span>
    
    <span data-ttu-id="3a01b-129">@base64ToString(body('Decode_AS2_message')? ["AS2Message"]? ["Content"])</span><span class="sxs-lookup"><span data-stu-id="3a01b-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="3a01b-130">Teraz dodać kroki toodecode hello X12 danych otrzymanych od partnera handlowego hello i dane wyjściowe elementów w obiekcie JSON.</span><span class="sxs-lookup"><span data-stu-id="3a01b-130">Now add steps toodecode hello X12 data received from hello trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="3a01b-131">Odebrano toonotify hello partnerów, którzy hello danych, możesz wysłać ponownie odpowiedzi zawierające hello AS2 komunikat dyspozycji powiadomienia (MDN) w celu wykonania akcji odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="3a01b-131">toonotify hello partner that hello data was received, you can send back a response containing hello AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="3a01b-132">Witaj tooadd **odpowiedzi** akcji, wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="3a01b-132">tooadd hello **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="3a01b-133">toofilter wszystkie toohello akcje ma, wprowadź wyraz hello **odpowiedzi** hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="3a01b-133">toofilter all actions toohello one that you want, enter hello word **response** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="3a01b-134">Wybierz hello **odpowiedzi** akcji.</span><span class="sxs-lookup"><span data-stu-id="3a01b-134">Select hello **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="3a01b-135">tooaccess hello MDN z danych wyjściowych hello hello **komunikat dekodowania X12** akcji, odpowiedź hello zestaw **treści** wartością tego wyrażenia:</span><span class="sxs-lookup"><span data-stu-id="3a01b-135">tooaccess hello MDN from hello output of hello **Decode X12 message** action, set hello response **BODY** field with this expression:</span></span>

    <span data-ttu-id="3a01b-136">@base64ToString(body('Decode_AS2_message')? ["OutgoingMdn"]? ["Content"])</span><span class="sxs-lookup"><span data-stu-id="3a01b-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="3a01b-137">Zapisz swoją pracę.</span><span class="sxs-lookup"><span data-stu-id="3a01b-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="3a01b-138">Teraz po zakończeniu konfigurowania aplikacji logiki B2B.</span><span class="sxs-lookup"><span data-stu-id="3a01b-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="3a01b-139">W przypadku aplikacji rzeczywistych można toostore hello zdekodować X12 danych w magazynie — biznesowych (LOB) aplikacji lub danych.</span><span class="sxs-lookup"><span data-stu-id="3a01b-139">In a real world application, you might want toostore hello decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="3a01b-140">tooconnect aplikacji biznesowych i użyć tych interfejsów API w aplikacji logiki, można dodać dodatkowe akcje lub zapisać niestandardowych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="3a01b-140">tooconnect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="3a01b-141">Funkcje i przypadki użycia</span><span class="sxs-lookup"><span data-stu-id="3a01b-141">Features and use cases</span></span>

* <span data-ttu-id="3a01b-142">Hello AS2 i X12 dekodowania i kodowania akcje let wymiany danych między partnerami handlowymi przy użyciu standardowych protokołach branżowych w aplikacjach logiki.</span><span class="sxs-lookup"><span data-stu-id="3a01b-142">hello AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="3a01b-143">tooexchange danych z partnerami handlowymi, używając AS2 i X12 z lub bez siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="3a01b-143">tooexchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="3a01b-144">Akcje B2B Hello pomóc łatwe tworzenie partnerów i umów w ramach konta integracji i używać ich w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="3a01b-144">hello B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="3a01b-145">Podczas rozszerzania aplikacji logiki z innymi działaniami umożliwia wysyłanie oraz odbieranie danych między innych aplikacji i usług, takich jak SalesForce.</span><span class="sxs-lookup"><span data-stu-id="3a01b-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="3a01b-146">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="3a01b-146">Learn more</span></span>
[<span data-ttu-id="3a01b-147">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="3a01b-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
