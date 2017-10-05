---
title: "Praca z wiadomości XML w przepływach pracy - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Przetworzyć, sprawdzanie poprawności, transformacji i wzbogacić wiadomości XML w aplikacji logiki i business-scenariuszy przy użyciu pakiet integracyjny dla przedsiębiorstw"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 3fec4935f5317be4bf8c9e05f1c24a7c05381b1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="92109-103">Sprawdzanie poprawności i Przekształcanie XML, kodowania i dekodowania plików prostych i wzbogacić funkcji komunikatów w aplikacjach logiki</span><span class="sxs-lookup"><span data-stu-id="92109-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="92109-104">Za pomocą aplikacji logiki, możesz mieć możliwość przetwarzania komunikatów XML, które wysyłania i odbierania.</span><span class="sxs-lookup"><span data-stu-id="92109-104">Using logic apps, you have the ability to process XML messages that you send and receive.</span></span> <span data-ttu-id="92109-105">Ta funkcja jest uwzględniona w pakiet integracyjny dla przedsiębiorstw.</span><span class="sxs-lookup"><span data-stu-id="92109-105">This feature is included with the Enterprise Integration Pack.</span></span> <span data-ttu-id="92109-106">Dla tych użytkowników z tła BizTalk Server pakiet integracyjny dla przedsiębiorstw zapewnia podobne możliwości transformacji i sprawdzania poprawności komunikatów, Praca z plików prostych i nawet umożliwia XPath wzbogacić lub wyodrębniania właściwości specyficzne dla wiadomości.</span><span class="sxs-lookup"><span data-stu-id="92109-106">For those users with a BizTalk Server background, the Enterprise Integration Pack gives you similar abilities to transform and validate messages, work with flat files, and even use XPath to enrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="92109-107">Dla tych użytkowników, którzy są nowe w tym miejscu te funkcje rozwiń sposób przetwarzania komunikatów w ramach przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="92109-107">For those users who are new to this space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="92109-108">Na przykład jeśli są w scenariuszu business-to-business i pracować z określonych schematów XML, a następnie pakiet integracyjny dla przedsiębiorstw można użyć w celu zwiększenia jak firmy przetwarza tych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="92109-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use the Enterprise Integration Pack to enhance how your company processes these messages.</span></span> 

<span data-ttu-id="92109-109">Zawiera pakiet integracyjny dla przedsiębiorstw:</span><span class="sxs-lookup"><span data-stu-id="92109-109">The Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="92109-110">[Sprawdzanie poprawności kodu XML](logic-apps-enterprise-integration-xml-validation.md "Dowiedz się więcej na temat sprawdzanie poprawności kodu XML wiadomości") -zweryfikować komunikatu przychodzącego lub wychodzącego XML względem określonego schematu.</span><span class="sxs-lookup"><span data-stu-id="92109-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="92109-111">[Przekształcanie XML](../logic-apps/logic-apps-enterprise-integration-transform.md "więcej informacji na temat przekształcenia wiadomości XML i map") — przekonwertować lub dostosować komunikat XML na podstawie wymagań lub wymagania partnera.</span><span class="sxs-lookup"><span data-stu-id="92109-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or the requirements of a partner.</span></span>
* <span data-ttu-id="92109-112">[Płaskie pliku kodowania i dekodowania pliku prostego](logic-apps-enterprise-integration-flatfile.md "informacje o pliku prostego kodowania/dekodowania") — kodowania i dekodowania plik prosty.</span><span class="sxs-lookup"><span data-stu-id="92109-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="92109-113">Na przykład SAP akceptuje i wysyła IDOC pliki w formacie pliku prostego.</span><span class="sxs-lookup"><span data-stu-id="92109-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="92109-114">Wiele platform integracji utworzyć wiadomości XML, łącznie z Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="92109-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="92109-115">Tak można utworzyć aplikację logiki, która używa kodera pliku prostego "konwersji" plików XML do plików prostych.</span><span class="sxs-lookup"><span data-stu-id="92109-115">So, you can create a logic app that uses the flat file encoder to "convert" XML files to flat files.</span></span> 
* <span data-ttu-id="92109-116">[Wyrażenie XPath](https://msdn.microsoft.com/library/mt643789.aspx) — wzbogacić komunikat i wyodrębniania właściwości specyficzne dla wiadomości.</span><span class="sxs-lookup"><span data-stu-id="92109-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from the message.</span></span> <span data-ttu-id="92109-117">Następnie można wyodrębnionego właściwości kierowania wiadomości do miejsca docelowego lub pośredniczące punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="92109-117">You can then use the extracted properties to route the message to a destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="92109-118">Wypróbuj</span><span class="sxs-lookup"><span data-stu-id="92109-118">Try it out</span></span>
<span data-ttu-id="92109-119">[Wdrażanie aplikacji logiki w pełni funkcjonalna ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (przykład GitHub) przy użyciu funkcji XML w aplikacjach logiki platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="92109-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using the XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="92109-120">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="92109-120">Learn more</span></span>
[<span data-ttu-id="92109-121">Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="92109-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")
