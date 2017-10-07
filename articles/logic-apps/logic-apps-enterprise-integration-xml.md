---
title: "aaaWorking XML wiadomości w przepływach pracy - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Przetworzyć, sprawdzanie poprawności, przekształcania i wzbogacić XML wiadomości w aplikacji logiki i tooscenarios firm za pomocą hello pakiet integracyjny dla przedsiębiorstw"
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
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="070a2-103">Sprawdzanie poprawności i Przekształcanie XML, kodowania i dekodowania plików prostych i wzbogacić funkcji komunikatów w aplikacjach logiki</span><span class="sxs-lookup"><span data-stu-id="070a2-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="070a2-104">Za pomocą aplikacji logiki, masz hello możliwości tooprocess XML wiadomości, które wysyłania i odbierania.</span><span class="sxs-lookup"><span data-stu-id="070a2-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="070a2-105">Ta funkcja jest uwzględniona w hello pakiet integracyjny dla przedsiębiorstw.</span><span class="sxs-lookup"><span data-stu-id="070a2-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="070a2-106">Dla tych użytkowników z tła BizTalk Server hello pakiet integracyjny dla przedsiębiorstw zapewnia podobne możliwości tootransform i sprawdzania poprawności komunikatów, pracy z plików prostych i nawet Użyj XPath tooenrich lub wyodrębniania właściwości specyficzne dla wiadomości.</span><span class="sxs-lookup"><span data-stu-id="070a2-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="070a2-107">Dla tych użytkowników, którzy są nowe miejsce toothis te funkcje rozwiń sposób przetwarzania komunikatów w ramach przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="070a2-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="070a2-108">Na przykład jeśli są w scenariuszu business-to-business i pracować z określonych schematów XML, możesz użyć tooenhance pakiet integracyjny dla przedsiębiorstw hello jak firmy przetwarza tych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="070a2-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="070a2-109">Witaj pakiet integracyjny dla przedsiębiorstw obejmuje:</span><span class="sxs-lookup"><span data-stu-id="070a2-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="070a2-110">[Sprawdzanie poprawności kodu XML](logic-apps-enterprise-integration-xml-validation.md "Dowiedz się więcej na temat sprawdzanie poprawności kodu XML wiadomości") -zweryfikować komunikatu przychodzącego lub wychodzącego XML względem określonego schematu.</span><span class="sxs-lookup"><span data-stu-id="070a2-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="070a2-111">[Przekształcanie XML](../logic-apps/logic-apps-enterprise-integration-transform.md "więcej informacji na temat przekształcenia wiadomości XML i map") — przekonwertować lub dostosować komunikat XML na podstawie wymagań lub wymagania hello partnera.</span><span class="sxs-lookup"><span data-stu-id="070a2-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="070a2-112">[Płaskie pliku kodowania i dekodowania pliku prostego](logic-apps-enterprise-integration-flatfile.md "informacje o pliku prostego kodowania/dekodowania") — kodowania i dekodowania plik prosty.</span><span class="sxs-lookup"><span data-stu-id="070a2-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="070a2-113">Na przykład SAP akceptuje i wysyła IDOC pliki w formacie pliku prostego.</span><span class="sxs-lookup"><span data-stu-id="070a2-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="070a2-114">Wiele platform integracji utworzyć wiadomości XML, łącznie z Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="070a2-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="070a2-115">Tak można utworzyć aplikację logiki, że koder pliku prostego powitania używa zbyt "Konwertuj" pliki tooflat plików XML.</span><span class="sxs-lookup"><span data-stu-id="070a2-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="070a2-116">[Wyrażenie XPath](https://msdn.microsoft.com/library/mt643789.aspx) — wzbogacić komunikat i wyodrębniania właściwości specyficzne dla wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="070a2-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="070a2-117">Mogą być następnie wyodrębnić hello Użyj właściwości tooroute hello komunikat tooa docelowego lub pośredniczące punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="070a2-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="070a2-118">Wypróbuj</span><span class="sxs-lookup"><span data-stu-id="070a2-118">Try it out</span></span>
<span data-ttu-id="070a2-119">[Wdrażanie aplikacji logiki w pełni funkcjonalna ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (przykład GitHub) przy użyciu funkcji XML hello w aplikacjach logiki platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="070a2-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="070a2-120">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="070a2-120">Learn more</span></span>
[<span data-ttu-id="070a2-121">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="070a2-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")
