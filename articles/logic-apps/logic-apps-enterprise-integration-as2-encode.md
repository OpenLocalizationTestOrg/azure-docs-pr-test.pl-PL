---
title: "komunikaty aaaEncode AS2 — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Jak toouse hello kodera AS2 w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="dedb2-103">Kodowanie wiadomości AS2 dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="dedb2-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="dedb2-104">tooestablish bezpieczeństwa i niezawodności podczas przesyłania wiadomości, należy użyć hello AS2 kodowania komunikatu łącznika.</span><span class="sxs-lookup"><span data-stu-id="dedb2-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="dedb2-105">Ten łącznik umożliwia cyfrowe podpisywanie, szyfrowanie i potwierdzeń za pośrednictwem wiadomości dyspozycji powiadomienia (MDN), które również prowadzi toosupport dla Niemożność wyparcia się.</span><span class="sxs-lookup"><span data-stu-id="dedb2-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="dedb2-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="dedb2-106">Before you start</span></span>

<span data-ttu-id="dedb2-107">Oto hello elementy, które należy:</span><span class="sxs-lookup"><span data-stu-id="dedb2-107">Here's hello items you need:</span></span>

* <span data-ttu-id="dedb2-108">Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="dedb2-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="dedb2-109">[Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dedb2-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="dedb2-110">Musi mieć łącznika integracji konta toouse hello AS2 kodowania komunikatu.</span><span class="sxs-lookup"><span data-stu-id="dedb2-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="dedb2-111">Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="dedb2-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="dedb2-112">[Umowy AS2](logic-apps-enterprise-integration-as2.md) jest już zdefiniowany w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="dedb2-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="dedb2-113">Kodowanie wiadomości AS2</span><span class="sxs-lookup"><span data-stu-id="dedb2-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="dedb2-114">[Tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="dedb2-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="dedb2-115">Hello AS2 kodowania komunikatu łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="dedb2-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="dedb2-116">W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.</span><span class="sxs-lookup"><span data-stu-id="dedb2-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="dedb2-117">W polu wyszukiwania hello wprowadź "AS2" filtru.</span><span class="sxs-lookup"><span data-stu-id="dedb2-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="dedb2-118">Wybierz **AS2 - AS2 kodowania komunikatu**.</span><span class="sxs-lookup"><span data-stu-id="dedb2-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Wyszukaj "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="dedb2-120">Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="dedb2-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="dedb2-121">Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect.</span><span class="sxs-lookup"><span data-stu-id="dedb2-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![Utwórz konto toointegration połączeń](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="dedb2-123">Właściwości oznaczone gwiazdką są wymagane.</span><span class="sxs-lookup"><span data-stu-id="dedb2-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="dedb2-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="dedb2-124">Property</span></span> | <span data-ttu-id="dedb2-125">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="dedb2-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="dedb2-126">Nazwa połączenia *</span><span class="sxs-lookup"><span data-stu-id="dedb2-126">Connection Name *</span></span> |<span data-ttu-id="dedb2-127">Wprowadź dowolną nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="dedb2-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="dedb2-128">Konta integracji *</span><span class="sxs-lookup"><span data-stu-id="dedb2-128">Integration Account *</span></span> |<span data-ttu-id="dedb2-129">Wprowadź nazwę konta integracji.</span><span class="sxs-lookup"><span data-stu-id="dedb2-129">Enter a name for your integration account.</span></span> <span data-ttu-id="dedb2-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dedb2-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="dedb2-131">Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie przykład toothis.</span><span class="sxs-lookup"><span data-stu-id="dedb2-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="dedb2-132">Wybierz toofinish Tworzenie połączenia **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="dedb2-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![Szczegóły połączenia integracji](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="dedb2-134">Po utworzeniu połączenia, jak pokazano w poniższym przykładzie, podaj szczegóły **AS2 — od**, **AS2 tooidentifiers** zgodnie z konfiguracją w umowie, i **treści**, który jest Witaj ładunek komunikatu.</span><span class="sxs-lookup"><span data-stu-id="dedb2-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![Podaj wymagane pola](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="dedb2-136">Szczegóły kodera AS2</span><span class="sxs-lookup"><span data-stu-id="dedb2-136">AS2 encoder details</span></span>

<span data-ttu-id="dedb2-137">Łącznik AS2 kodowania Hello wykonuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="dedb2-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="dedb2-138">Stosuje nagłówków AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="dedb2-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="dedb2-139">Znaki wychodzących wiadomości (jeśli jest skonfigurowane)</span><span class="sxs-lookup"><span data-stu-id="dedb2-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="dedb2-140">Szyfruje komunikaty wychodzące (jeśli jest skonfigurowane)</span><span class="sxs-lookup"><span data-stu-id="dedb2-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="dedb2-141">Kompresuje wiadomość hello (jeśli jest skonfigurowane)</span><span class="sxs-lookup"><span data-stu-id="dedb2-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="dedb2-142">Spróbuj w tym przykładzie</span><span class="sxs-lookup"><span data-stu-id="dedb2-142">Try this sample</span></span>

<span data-ttu-id="dedb2-143">tootry wdrażanie logiki pełnej funkcjonalności aplikacji oraz przykładowy AS2 scenariusza, zobacz hello [AS2 szablon aplikacji logiki oraz scenariusz](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="dedb2-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="dedb2-144">Widok hello swagger</span><span class="sxs-lookup"><span data-stu-id="dedb2-144">View hello swagger</span></span>
<span data-ttu-id="dedb2-145">Zobacz hello [swagger szczegóły](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="dedb2-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dedb2-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dedb2-146">Next steps</span></span>
[<span data-ttu-id="dedb2-147">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="dedb2-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") 

