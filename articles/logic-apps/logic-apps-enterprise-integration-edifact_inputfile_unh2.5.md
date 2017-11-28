---
title: "aaaLogic B2B aplikacje dekodowania edifact rozwiązać UNH2.5 - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Azure B2B aplikacje logiki dekodowania edifact rozwiązać UNH2.5"
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
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="9ea97-103">Jak toohandle EDIFACT dokumentów o UNH2.5 segmentu</span><span class="sxs-lookup"><span data-stu-id="9ea97-103">How toohandle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="9ea97-104">Gdy UNH2.5 znajduje się w dokumencie EDIFACT hello, jest używany do wyszukiwania schematu.</span><span class="sxs-lookup"><span data-stu-id="9ea97-104">When UNH2.5 is present in hello EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="9ea97-105">Przykład: pole UNH hello jest **EAN008** w wiadomości powitania EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9ea97-105">Example: hello UNH field is **EAN008** in hello EDIFACT message</span></span>  
<span data-ttu-id="9ea97-106">UNH + SSDD1 + ZAMÓWIEŃ: D: 03B: UN:**EAN008**"</span><span class="sxs-lookup"><span data-stu-id="9ea97-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="9ea97-107">Wiadomości powitania toohandle toofollow kroki</span><span class="sxs-lookup"><span data-stu-id="9ea97-107">Steps toofollow toohandle hello message</span></span> 
1. <span data-ttu-id="9ea97-108">Aktualizacja schematu hello</span><span class="sxs-lookup"><span data-stu-id="9ea97-108">Update hello schema</span></span>
2. <span data-ttu-id="9ea97-109">Sprawdź ustawienia umowy hello</span><span class="sxs-lookup"><span data-stu-id="9ea97-109">Check hello agreement settings</span></span>  

## <a name="update-hello-schema"></a><span data-ttu-id="9ea97-110">Aktualizacja schematu hello</span><span class="sxs-lookup"><span data-stu-id="9ea97-110">Update hello schema</span></span>
<span data-ttu-id="9ea97-111">wiadomości powitania tooprocess, należy toodeploy schematu z nazwa węzła głównego UNH2.5 hello.</span><span class="sxs-lookup"><span data-stu-id="9ea97-111">tooprocess hello message, you need toodeploy a schema with hello UNH2.5 root node name.</span></span>  <span data-ttu-id="9ea97-112">Dla danego przykładem, nazwa głównego schematu hello jest **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="9ea97-112">For given an example, hello schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="9ea97-113">Dla każdego D03B_ORDERS inny segment UNH2.5 trzeba toodeploy poszczególnych schematu.</span><span class="sxs-lookup"><span data-stu-id="9ea97-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have toodeploy an individual schema.</span></span>  

## <a name="add-schema-toohello-edifact-agreement"></a><span data-ttu-id="9ea97-114">Dodawanie umowy EDIFACT toohello schematu</span><span class="sxs-lookup"><span data-stu-id="9ea97-114">Add schema toohello EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="9ea97-115">Dekodowanie EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9ea97-115">EDIFACT Decode</span></span>
<span data-ttu-id="9ea97-116">tooDecode przychodząca wiadomość hello, skonfiguruj hello schematu w hello EDIFACT umowy odbierają ustawienia</span><span class="sxs-lookup"><span data-stu-id="9ea97-116">tooDecode hello incoming message, configure hello schema in hello EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="9ea97-117">Dodaj konto integracji toohello schematu hello</span><span class="sxs-lookup"><span data-stu-id="9ea97-117">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="9ea97-118">Konfigurowanie schematu hello w hello EDIFACT umowy odbierają ustawienia.</span><span class="sxs-lookup"><span data-stu-id="9ea97-118">Configure hello schema in hello EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="9ea97-119">Wybierz umowy EDIFACT i kliknij przycisk **edycji w formacie JSON**.</span><span class="sxs-lookup"><span data-stu-id="9ea97-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="9ea97-120">Dodaj wartość UNH2.5 w hello umowy Receive **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9ea97-120">Add UNH2.5 value in hello Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="9ea97-121">Kodowanie EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9ea97-121">EDIFACT Encode</span></span>
<span data-ttu-id="9ea97-122">tooEncode przychodząca wiadomość hello, skonfiguruj hello schematu w ustawieniach wysyłania umowy EDIFACT hello</span><span class="sxs-lookup"><span data-stu-id="9ea97-122">tooEncode hello incoming message, configure hello schema in hello EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="9ea97-123">Dodaj konto integracji toohello schematu hello</span><span class="sxs-lookup"><span data-stu-id="9ea97-123">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="9ea97-124">Skonfiguruj hello schematu w ustawieniach wysyłania umowy EDIFACT hello.</span><span class="sxs-lookup"><span data-stu-id="9ea97-124">Configure hello schema in hello EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="9ea97-125">Wybierz umowy EDIFACT i kliknij przycisk **edycji w formacie JSON**.</span><span class="sxs-lookup"><span data-stu-id="9ea97-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="9ea97-126">Dodaj wartość UNH2.5 w hello wysyłania umowy **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="9ea97-126">Add UNH2.5 value in hello Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ea97-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ea97-127">Next Steps</span></span>
* [<span data-ttu-id="9ea97-128">Dowiedz się więcej o integracji konta umów</span><span class="sxs-lookup"><span data-stu-id="9ea97-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  