---
title: "Dodaj dysk Google łącznika w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie łącznika dysk Google z parametrami interfejsu API REST"
services: 
suite: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2bcebc5-02d2-435b-b0da-ef53bc51c4b6
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c066a10b33e172eb5f16eede43ec407794000c90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-google-drive-connector"></a><span data-ttu-id="4401b-103">Rozpoczynanie pracy z łącznikiem dysk Google</span><span class="sxs-lookup"><span data-stu-id="4401b-103">Get started with the Google Drive connector</span></span>
<span data-ttu-id="4401b-104">Nawiązać dysk Google, aby utworzyć pliki, Pobierz wiersze i inne.</span><span class="sxs-lookup"><span data-stu-id="4401b-104">Connect to Google Drive to create files, get rows, and more.</span></span> <span data-ttu-id="4401b-105">Dysk Google można:</span><span class="sxs-lookup"><span data-stu-id="4401b-105">With Google Drive, you can:</span></span> 

* <span data-ttu-id="4401b-106">Tworzenie sieci przepływu biznesowe na podstawie danych otrzymywanych z wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="4401b-106">Build your business flow based on the data you get from your search.</span></span> 
* <span data-ttu-id="4401b-107">Użyj działania do wyszukania obrazów, wiadomości i inne.</span><span class="sxs-lookup"><span data-stu-id="4401b-107">Use actions to search images, search the news, and more.</span></span> <span data-ttu-id="4401b-108">Te akcje uzyskać odpowiedzi, a następnie udostępnić dane wyjściowe do innych działań.</span><span class="sxs-lookup"><span data-stu-id="4401b-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="4401b-109">Na przykład można wyszukać wideo, a następnie za pomocą usługi Twitter zaksięgowania wideo do serwisu Twitter.</span><span class="sxs-lookup"><span data-stu-id="4401b-109">For example, you can search for a video, and then use Twitter to post that video to a Twitter feed.</span></span>

<span data-ttu-id="4401b-110">Rozpoczynanie pracy przez teraz tworzenie aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4401b-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-the-connection-to-google-drive"></a><span data-ttu-id="4401b-111">Utwórz połączenie z dysk Google</span><span class="sxs-lookup"><span data-stu-id="4401b-111">Create the connection to Google Drive</span></span>
<span data-ttu-id="4401b-112">Po dodaniu tego łącznika do aplikacji logiki, należy zezwolić aplikacji logiki, aby połączyć się z dyskiem Google.</span><span class="sxs-lookup"><span data-stu-id="4401b-112">When you add this connector to your logic apps, you must authorize logic apps to connect to your Google Drive.</span></span>

> [!INCLUDE [Steps to create a connection to googledrive](../../includes/connectors-create-api-googledrive.md)]
> 
> 

<span data-ttu-id="4401b-113">Po utworzeniu połączenia, należy wprowadzić dysk Google właściwości, takie jak nazwa pliku lub ścieżka folderu.</span><span class="sxs-lookup"><span data-stu-id="4401b-113">After you create the connection, you enter the Google Drive properties, like the folder path or file name.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="4401b-114">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="4401b-114">Connector-specific details</span></span>

<span data-ttu-id="4401b-115">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/googledrive/).</span><span class="sxs-lookup"><span data-stu-id="4401b-115">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/googledrive/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="4401b-116">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="4401b-116">More connectors</span></span>
<span data-ttu-id="4401b-117">Wróć do [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4401b-117">Go back to the [APIs list](apis-list.md).</span></span>
