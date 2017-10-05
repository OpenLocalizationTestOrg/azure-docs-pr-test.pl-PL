---
title: "Dekodowanie edifact B2B aplikacje logiki rozwiązać UNH2.5 - Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 62ad8183cc6e9f56255b2729a04ee7710d00a21a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-handle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="c9864-103">Sposób obsługi EDIFACT dokumentów, w których UNH2.5 segment</span><span class="sxs-lookup"><span data-stu-id="c9864-103">How to handle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="c9864-104">Gdy UNH2.5 znajduje się w dokumencie EDIFACT, jest używany do wyszukiwania schematu.</span><span class="sxs-lookup"><span data-stu-id="c9864-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="c9864-105">Przykład: Pole UNH jest **EAN008** w komunikacie EDIFACT</span><span class="sxs-lookup"><span data-stu-id="c9864-105">Example: The UNH field is **EAN008** in the EDIFACT message</span></span>  
<span data-ttu-id="c9864-106">UNH + SSDD1 + ZAMÓWIEŃ: D: 03B: UN:**EAN008**"</span><span class="sxs-lookup"><span data-stu-id="c9864-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="c9864-107">Kroki do wykonania w celu obsługi wiadomości</span><span class="sxs-lookup"><span data-stu-id="c9864-107">Steps to follow to handle the message</span></span> 
1. <span data-ttu-id="c9864-108">Aktualizacja schematu</span><span class="sxs-lookup"><span data-stu-id="c9864-108">Update the schema</span></span>
2. <span data-ttu-id="c9864-109">Sprawdź ustawienia umowy</span><span class="sxs-lookup"><span data-stu-id="c9864-109">Check the agreement settings</span></span>  

## <a name="update-the-schema"></a><span data-ttu-id="c9864-110">Aktualizacja schematu</span><span class="sxs-lookup"><span data-stu-id="c9864-110">Update the schema</span></span>
<span data-ttu-id="c9864-111">Przetworzyć komunikatu, należy wdrożyć schematu z UNH2.5 Nazwa węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="c9864-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span></span>  <span data-ttu-id="c9864-112">Dla danego przykładem, nazwa głównego schematu jest **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="c9864-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="c9864-113">Dla każdego D03B_ORDERS inny segment UNH2.5 trzeba wdrażania poszczególnych schematu.</span><span class="sxs-lookup"><span data-stu-id="c9864-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span></span>  

## <a name="add-schema-to-the-edifact-agreement"></a><span data-ttu-id="c9864-114">Dodaj umowy EDIFACT schematu</span><span class="sxs-lookup"><span data-stu-id="c9864-114">Add schema to the EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="c9864-115">Dekodowanie EDIFACT</span><span class="sxs-lookup"><span data-stu-id="c9864-115">EDIFACT Decode</span></span>
<span data-ttu-id="c9864-116">Zdekodować komunikatu przychodzącego, należy skonfigurować schematu w EDIFACT umowy odbierają ustawienia</span><span class="sxs-lookup"><span data-stu-id="c9864-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="c9864-117">Dodać schematu do konta integracji</span><span class="sxs-lookup"><span data-stu-id="c9864-117">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="c9864-118">Konfigurowanie schematu w EDIFACT umowy odbierają ustawienia.</span><span class="sxs-lookup"><span data-stu-id="c9864-118">Configure the schema in the EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="c9864-119">Wybierz umowy EDIFACT i kliknij przycisk **edycji w formacie JSON**.</span><span class="sxs-lookup"><span data-stu-id="c9864-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="c9864-120">Dodaj wartość UNH2.5 Umowy odbierania **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c9864-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="c9864-121">Kodowanie EDIFACT</span><span class="sxs-lookup"><span data-stu-id="c9864-121">EDIFACT Encode</span></span>
<span data-ttu-id="c9864-122">Kodowanie komunikatu przychodzącego, należy skonfigurować schematu w ustawieniach wysyłania umowy EDIFACT</span><span class="sxs-lookup"><span data-stu-id="c9864-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="c9864-123">Dodać schematu do konta integracji</span><span class="sxs-lookup"><span data-stu-id="c9864-123">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="c9864-124">Konfigurowanie schematu w ustawieniach wysyłania umowy EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="c9864-124">Configure the schema in the EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="c9864-125">Wybierz umowy EDIFACT i kliknij przycisk **edycji w formacie JSON**.</span><span class="sxs-lookup"><span data-stu-id="c9864-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="c9864-126">Dodaj wartość UNH2.5 Umowy wysyłania **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="c9864-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9864-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c9864-127">Next Steps</span></span>
* [<span data-ttu-id="c9864-128">Dowiedz się więcej o integracji konta umów</span><span class="sxs-lookup"><span data-stu-id="c9864-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  