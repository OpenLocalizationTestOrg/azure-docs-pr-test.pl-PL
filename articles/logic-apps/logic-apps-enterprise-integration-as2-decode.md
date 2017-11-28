---
title: "komunikaty aaaDecode AS2 — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Jak toouse hello dekodera AS2 w hello pakiet integracyjny dla przedsiębiorstw dla usługi Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="587e7-103">Dekodowanie AS2 wiadomości dla usługi Azure Logic Apps z hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="587e7-103">Decode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span> 

<span data-ttu-id="587e7-104">tooestablish bezpieczeństwa i niezawodności podczas przesyłania wiadomości, należy użyć hello AS2 zdekodować komunikatu łącznika.</span><span class="sxs-lookup"><span data-stu-id="587e7-104">tooestablish security and reliability while transmitting messages, use hello Decode AS2 message connector.</span></span> <span data-ttu-id="587e7-105">Ten łącznik umożliwia cyfrowe podpisywanie, odszyfrowywania i potwierdzeń za pośrednictwem komunikatu powiadomienia dyspozycji (MDN).</span><span class="sxs-lookup"><span data-stu-id="587e7-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="587e7-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="587e7-106">Before you start</span></span>

<span data-ttu-id="587e7-107">Oto hello elementy, które należy:</span><span class="sxs-lookup"><span data-stu-id="587e7-107">Here's hello items you need:</span></span>

* <span data-ttu-id="587e7-108">Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="587e7-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="587e7-109">[Konta integracji](logic-apps-enterprise-integration-create-integration-account.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="587e7-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="587e7-110">Musi mieć łącznika integracji konta toouse hello AS2 dekodowanie komunikatu.</span><span class="sxs-lookup"><span data-stu-id="587e7-110">You must have an integration account toouse hello Decode AS2 message connector.</span></span>
* <span data-ttu-id="587e7-111">Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="587e7-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="587e7-112">[Umowy AS2](logic-apps-enterprise-integration-as2.md) jest już zdefiniowany w ramach konta integracji</span><span class="sxs-lookup"><span data-stu-id="587e7-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="587e7-113">Dekodowanie AS2 wiadomości</span><span class="sxs-lookup"><span data-stu-id="587e7-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="587e7-114">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="587e7-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="587e7-115">Hello AS2 zdekodować komunikatu łącznika nie ma wyzwalaczy, dlatego należy dodać wyzwalacza do uruchamiania aplikacji logiki, takich jak wyzwalacz żądania.</span><span class="sxs-lookup"><span data-stu-id="587e7-115">hello Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="587e7-116">W hello projektanta aplikacji logiki dodać wyzwalacz, a następnie dodaj aplikację logiki tooyour akcji.</span><span class="sxs-lookup"><span data-stu-id="587e7-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="587e7-117">W polu wyszukiwania hello wprowadź "AS2" filtru.</span><span class="sxs-lookup"><span data-stu-id="587e7-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="587e7-118">Wybierz **AS2 - AS2 zdekodować komunikatu**.</span><span class="sxs-lookup"><span data-stu-id="587e7-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![Wyszukaj "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="587e7-120">Jeśli wszystkie połączenia nie został wcześniej utworzyć konta integracji tooyour, zostanie wyświetlony monit toocreate teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="587e7-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="587e7-121">Nazwa połączenia, a następnie wybierz hello integracji konta, które ma tooconnect.</span><span class="sxs-lookup"><span data-stu-id="587e7-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Utwórz połączenie integracji](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="587e7-123">Właściwości oznaczone gwiazdką są wymagane.</span><span class="sxs-lookup"><span data-stu-id="587e7-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="587e7-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="587e7-124">Property</span></span> | <span data-ttu-id="587e7-125">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="587e7-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="587e7-126">Nazwa połączenia *</span><span class="sxs-lookup"><span data-stu-id="587e7-126">Connection Name *</span></span> |<span data-ttu-id="587e7-127">Wprowadź dowolną nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="587e7-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="587e7-128">Konta integracji *</span><span class="sxs-lookup"><span data-stu-id="587e7-128">Integration Account *</span></span> |<span data-ttu-id="587e7-129">Wprowadź nazwę konta integracji.</span><span class="sxs-lookup"><span data-stu-id="587e7-129">Enter a name for your integration account.</span></span> <span data-ttu-id="587e7-130">Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="587e7-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="587e7-131">Gdy wszystko będzie gotowe, szczegóły połączenia powinien wyglądać podobnie przykład toothis.</span><span class="sxs-lookup"><span data-stu-id="587e7-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="587e7-132">Wybierz toofinish Tworzenie połączenia **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="587e7-132">toofinish creating your connection, choose **Create**.</span></span>

    ![Szczegóły połączenia integracji](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="587e7-134">Po utworzeniu połączenia, jak pokazano w poniższym przykładzie, wybierz **treści** i **nagłówki** z hello żądania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="587e7-134">After your connection is created, as shown in this example, select **Body** and **Headers** from hello Request outputs.</span></span>
   
    ![utworzone połączenie integracji](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="587e7-136">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="587e7-136">For example:</span></span>

    ![Wybierz treści i nagłówków z danych wyjściowych żądań](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="587e7-138">Szczegóły dekodera AS2</span><span class="sxs-lookup"><span data-stu-id="587e7-138">AS2 decoder details</span></span>

<span data-ttu-id="587e7-139">Łącznik AS2 dekodowania Hello wykonuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="587e7-139">hello Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="587e7-140">Przetwarza nagłówków AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="587e7-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="587e7-141">Sprawdza, czy podpis hello (jeśli jest skonfigurowane)</span><span class="sxs-lookup"><span data-stu-id="587e7-141">Verifies hello signature (if configured)</span></span>
* <span data-ttu-id="587e7-142">Odszyfrowuje wiadomości powitania (jeśli jest skonfigurowane)</span><span class="sxs-lookup"><span data-stu-id="587e7-142">Decrypts hello messages (if configured)</span></span>
* <span data-ttu-id="587e7-143">Dekompresuje wiadomość hello (jeśli jest skonfigurowane)</span><span class="sxs-lookup"><span data-stu-id="587e7-143">Decompresses hello message (if configured)</span></span>
* <span data-ttu-id="587e7-144">Uzgadnia odebrane MDN z oryginalnej wiadomości wychodzących hello</span><span class="sxs-lookup"><span data-stu-id="587e7-144">Reconciles a received MDN with hello original outbound message</span></span>
* <span data-ttu-id="587e7-145">Aktualizacje i są powiązane rekordy w bazie danych bez odrzucania hello</span><span class="sxs-lookup"><span data-stu-id="587e7-145">Updates and correlates records in hello non-repudiation database</span></span>
* <span data-ttu-id="587e7-146">Zapisuje rekordy AS2 raportowania stanu</span><span class="sxs-lookup"><span data-stu-id="587e7-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="587e7-147">zawartość ładunek danych wyjściowych Hello jest kodowany w standardzie base64</span><span class="sxs-lookup"><span data-stu-id="587e7-147">hello output payload contents are base64 encoded</span></span>
* <span data-ttu-id="587e7-148">Określa, czy MDN jest wymagana i czy hello MDN powinna być synchroniczne czy asynchroniczne na podstawie konfiguracji umowy AS2</span><span class="sxs-lookup"><span data-stu-id="587e7-148">Determines whether an MDN is required, and whether hello MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="587e7-149">Generuje MDN synchroniczna lub asynchroniczna, (na podstawie konfiguracji umów)</span><span class="sxs-lookup"><span data-stu-id="587e7-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="587e7-150">Ustawia właściwości i tokenów korelacji hello na powitania MDN</span><span class="sxs-lookup"><span data-stu-id="587e7-150">Sets hello correlation tokens and properties on hello MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="587e7-151">Spróbuj w tym przykładzie</span><span class="sxs-lookup"><span data-stu-id="587e7-151">Try this sample</span></span>

<span data-ttu-id="587e7-152">tootry wdrażanie logiki pełnej funkcjonalności aplikacji oraz przykładowy AS2 scenariusza, zobacz hello [AS2 szablon aplikacji logiki oraz scenariusz](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="587e7-152">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="587e7-153">Widok hello swagger</span><span class="sxs-lookup"><span data-stu-id="587e7-153">View hello swagger</span></span>
<span data-ttu-id="587e7-154">Zobacz hello [swagger szczegóły](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="587e7-154">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="587e7-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="587e7-155">Next steps</span></span>
[<span data-ttu-id="587e7-156">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="587e7-156">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

