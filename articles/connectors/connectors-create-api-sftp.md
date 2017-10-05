---
title: "Informacje o sposobie korzystania z łącznika SFTP w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połączyć z interfejsem API SFTP do wysyłania i odbierania plików. Można wykonywać różne operacje, takie jak tworzenie, aktualizowanie, Pobierz i usuwania plików."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 31253d8daee1581167a96a20ba8ad529a04b3e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sftp-connector"></a><span data-ttu-id="2f558-105">Rozpoczynanie pracy z łącznikiem SFTP</span><span class="sxs-lookup"><span data-stu-id="2f558-105">Get started with the SFTP connector</span></span>
<span data-ttu-id="2f558-106">Użyj konektora SFTP dostępu do konta SFTP do wysyłania i odbierania plików.</span><span class="sxs-lookup"><span data-stu-id="2f558-106">Use the SFTP connector to access an SFTP account to send and receive files.</span></span> <span data-ttu-id="2f558-107">Można wykonywać różne operacje, takie jak tworzenie, aktualizowanie, Pobierz i usuwania plików.</span><span class="sxs-lookup"><span data-stu-id="2f558-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="2f558-108">Aby użyć [każdy łącznik](apis-list.md), należy najpierw utworzyć aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="2f558-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="2f558-109">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2f558-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="2f558-110">Nawiązać połączenia z użyciem protokołu SFTP</span><span class="sxs-lookup"><span data-stu-id="2f558-110">Connect to SFTP</span></span>
<span data-ttu-id="2f558-111">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* do usługi.</span><span class="sxs-lookup"><span data-stu-id="2f558-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="2f558-112">A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="2f558-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sftp"></a><span data-ttu-id="2f558-113">Utwórz połączenie z użyciem protokołu SFTP</span><span class="sxs-lookup"><span data-stu-id="2f558-113">Create a connection to SFTP</span></span>
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="2f558-114">Użyj wyzwalacz SFTP</span><span class="sxs-lookup"><span data-stu-id="2f558-114">Use an SFTP trigger</span></span>
<span data-ttu-id="2f558-115">Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy zdefiniowanych w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="2f558-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="2f558-116">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="2f558-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="2f558-117">W tym przykładzie **SFTP - podczas dodawania lub modyfikowania pliku** wyzwalacza jest używane do inicjowania przepływu pracy aplikacji logiki, gdy plik zostanie dodany do lub zmodyfikowane na serwerze SFTP.</span><span class="sxs-lookup"><span data-stu-id="2f558-117">In this example, the **SFTP - When a file is added or modified** trigger is used to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="2f558-118">Możesz również dodać warunek, który sprawdza zawartość pliku nowe lub zmodyfikowane i podejmuje decyzję, aby wyodrębnić plik, jeśli jego zawartość wskazują, że należy wyodrębnić przed rozpoczęciem korzystania z zawartości.</span><span class="sxs-lookup"><span data-stu-id="2f558-118">You also add a condition that checks the contents of the new or modified file, and makes a decision to extract the file if its contents indicate that it should be extracted before using the contents.</span></span> <span data-ttu-id="2f558-119">Na koniec Dodaj akcję w celu wyodrębnienia zawartości pliku i umieścić w folderze na serwerze SFTP wyodrębniona zawartość.</span><span class="sxs-lookup"><span data-stu-id="2f558-119">Finally, add an action to extract the contents of a file, and place the extracted contents in a folder on the SFTP server.</span></span> 

<span data-ttu-id="2f558-120">W przykładzie przedsiębiorstwa może użyć tego wyzwalacza do monitorowania folderu SFTP dla nowych plików, które reprezentują zamówień klienta.</span><span class="sxs-lookup"><span data-stu-id="2f558-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="2f558-121">Następnie można użyć akcji łącznika SFTP, takich jak **pobrać zawartość pliku**, aby pobrać zawartość kolejność dla dalszego przetwarzania i przechowywania w bazie danych zamówienia.</span><span class="sxs-lookup"><span data-stu-id="2f558-121">You could then use an SFTP connector action, such as **Get file content**, to get the contents of the order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="2f558-122">Dodaj warunek</span><span class="sxs-lookup"><span data-stu-id="2f558-122">Add a condition</span></span>
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="2f558-123">Za pomocą akcji SFTP</span><span class="sxs-lookup"><span data-stu-id="2f558-123">Use an SFTP action</span></span>
<span data-ttu-id="2f558-124">Akcja jest przeprowadzane przez przepływ pracy zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="2f558-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="2f558-125">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="2f558-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="2f558-126">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="2f558-126">Connector-specific details</span></span>

<span data-ttu-id="2f558-127">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="2f558-127">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="2f558-128">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="2f558-128">More connectors</span></span>
<span data-ttu-id="2f558-129">Wróć do [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="2f558-129">Go back to the [APIs list](apis-list.md).</span></span>