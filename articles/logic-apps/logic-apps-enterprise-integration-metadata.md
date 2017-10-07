---
title: Integracja aaaManage konta artefaktu metadanych - Azure Logic Apps | Dokumentacja firmy Microsoft
description: "Dodawanie lub pobrać artefaktu metadanych z konta integracji dla usługi Azure Logic Apps"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="001a3-103">Zarządzanie artefaktu metadanych w konta integracji dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="001a3-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="001a3-104">Można zdefiniować niestandardowych metadanych dla artefaktów na kontach integracji i pobrać metadane w czasie wykonywania dla aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="001a3-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="001a3-105">Na przykład można określić metadanych artefaktów, takich jak partnerów, umów, schematów i map — wszystkie sklepu metadanych za pomocą pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="001a3-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="001a3-106">Obecnie usługa artefaktów nie można utworzyć metadanych za pośrednictwem interfejsu użytkownika, ale za pomocą interfejsów API REST toocreate metadanych.</span><span class="sxs-lookup"><span data-stu-id="001a3-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs toocreate metadata.</span></span> <span data-ttu-id="001a3-107">metadane tooadd podczas tworzenia lub wybierz partnera, umowy lub schematu w hello portalu Azure, wybierz **edycji w formacie JSON**.</span><span class="sxs-lookup"><span data-stu-id="001a3-107">tooadd metadata when you create or select a partner, agreement, or schema in hello Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="001a3-108">tooretrieve artefaktu metadanych w aplikacjach logiki, można użyć funkcji wyszukiwania artefaktu kont integracji hello.</span><span class="sxs-lookup"><span data-stu-id="001a3-108">tooretrieve artifact metadata in logic apps, you can use hello Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a><span data-ttu-id="001a3-109">Dodatek tooartifacts metadanych konta integracji</span><span class="sxs-lookup"><span data-stu-id="001a3-109">Add metadata tooartifacts in integration accounts</span></span>

1. <span data-ttu-id="001a3-110">Utwórz [konta integracji](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="001a3-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="001a3-111">Na przykład dodać konto artefaktu tooyour integracji, [partnera](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [umowy](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), lub [schematu](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="001a3-111">Add an artifact tooyour integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="001a3-112">Wybierz artefakt hello, wybierz **edycji w formacie JSON**i wprowadź szczegóły metadanych.</span><span class="sxs-lookup"><span data-stu-id="001a3-112">Select hello artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Wprowadź metadanych](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="001a3-114">Pobieranie metadanych z artefaktów dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="001a3-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="001a3-115">Utwórz [aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="001a3-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="001a3-116">Utwórz [łącza z Twojego konta integracji tooyour aplikacji logiki](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="001a3-116">Create a [link from your logic app tooyour integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="001a3-117">W Projektancie aplikacji logiki, dodać wyzwalacza, takich jak *żądania* lub *HTTP* tooyour aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="001a3-117">In Logic App Designer, add a trigger like *Request* or *HTTP* tooyour logic app.</span></span>

4.  <span data-ttu-id="001a3-118">Wybierz **następnego kroku** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="001a3-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="001a3-119">Wyszukaj *integracji* , można znaleźć, a następnie wybierz **konta integracji — wyszukiwanie artefaktu konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="001a3-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Wybierz wyszukiwanie artefaktu konta integracji](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="001a3-121">Wybierz hello **typu artefaktu**i podaj hello **nazwa artefaktu**.</span><span class="sxs-lookup"><span data-stu-id="001a3-121">Select hello **Artifact Type**, and provide hello **Artifact Name**.</span></span>

    ![Wybierz typ artefaktu i określ nazwę artefaktów](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="001a3-123">Przykład: Pobrać partnera metadanych</span><span class="sxs-lookup"><span data-stu-id="001a3-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="001a3-124">Metadane partnera ma `routingUrl` szczegóły:</span><span class="sxs-lookup"><span data-stu-id="001a3-124">Partner metadata has these `routingUrl` details:</span></span>

![Znajdź partnera z metadanych "routingURL"](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="001a3-126">W aplikacji logiki, Dodaj Twój wyzwalacz **konta integracji — wyszukiwanie artefaktu konta integracji** akcji dla swojego partnera i **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="001a3-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Dodawanie wyzwalacza, artefaktu wyszukiwania i aplikacji logiki tooyour "HTTP"](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="001a3-128">Witaj tooretrieve identyfikatora URI, przejdź tooCode widoku aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="001a3-128">tooretrieve hello URI, go tooCode View for your logic app.</span></span> <span data-ttu-id="001a3-129">Definicję aplikacji logiki powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="001a3-129">Your logic app definition should look like this example:</span></span>

    ![Wyszukiwanie wyszukiwania](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="001a3-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="001a3-131">Next steps</span></span>
* [<span data-ttu-id="001a3-132">Dowiedz się więcej na temat umów</span><span class="sxs-lookup"><span data-stu-id="001a3-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  
