---
title: "aaaLearn jak toouse hello SFTP łącznika w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połącz toosend tooSFTP interfejsu API i odbierania plików. Można wykonywać różne operacje, takie jak tworzenie, aktualizowanie, Pobierz i usuwania plików."
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
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="ca26a-105">Rozpoczynanie pracy z hello SFTP łącznika</span><span class="sxs-lookup"><span data-stu-id="ca26a-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="ca26a-106">Użyj hello SFTP łącznika tooaccess toosend konta SFTP uprawnia do plików.</span><span class="sxs-lookup"><span data-stu-id="ca26a-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="ca26a-107">Można wykonywać różne operacje, takie jak tworzenie, aktualizowanie, Pobierz i usuwania plików.</span><span class="sxs-lookup"><span data-stu-id="ca26a-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="ca26a-108">toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="ca26a-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="ca26a-109">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ca26a-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="ca26a-110">Połącz tooSFTP</span><span class="sxs-lookup"><span data-stu-id="ca26a-110">Connect tooSFTP</span></span>
<span data-ttu-id="ca26a-111">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="ca26a-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="ca26a-112">A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="ca26a-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="ca26a-113">Tworzenie tooSFTP połączenia</span><span class="sxs-lookup"><span data-stu-id="ca26a-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="ca26a-114">Użyj wyzwalacz SFTP</span><span class="sxs-lookup"><span data-stu-id="ca26a-114">Use an SFTP trigger</span></span>
<span data-ttu-id="ca26a-115">Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="ca26a-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="ca26a-116">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ca26a-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="ca26a-117">W tym przykładzie hello **SFTP - podczas dodawania lub modyfikowania pliku** wyzwalacza jest używane tooinitiate przepływu pracy aplikacji logiki, po dodaniu pliku lub zmodyfikowane na serwerze SFTP.</span><span class="sxs-lookup"><span data-stu-id="ca26a-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="ca26a-118">Możesz również dodać warunek, który sprawdza hello zawartość pliku nowe lub zmodyfikowane hello i tworzy plik hello tooextract decyzji, jeśli jego zawartość wskazują, że należy wyodrębnić przed użyciem hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="ca26a-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="ca26a-119">Na koniec Dodaj akcję tooextract hello zawartość pliku i umieścić w folderze na serwerze SFTP hello hello wyodrębnić zawartość.</span><span class="sxs-lookup"><span data-stu-id="ca26a-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="ca26a-120">Przykład przedsiębiorstwa można użyć tego wyzwalacza toomonitor folderu SFTP nowych plików, które reprezentują zamówień klienta.</span><span class="sxs-lookup"><span data-stu-id="ca26a-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="ca26a-121">Następnie można użyć akcji łącznika SFTP, takich jak **pobrać zawartość pliku**, zawartość hello tooget hello kolejności dla dalszego przetwarzania i przechowywania w bazie danych zamówienia.</span><span class="sxs-lookup"><span data-stu-id="ca26a-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="ca26a-122">Dodaj warunek</span><span class="sxs-lookup"><span data-stu-id="ca26a-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="ca26a-123">Za pomocą akcji SFTP</span><span class="sxs-lookup"><span data-stu-id="ca26a-123">Use an SFTP action</span></span>
<span data-ttu-id="ca26a-124">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="ca26a-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="ca26a-125">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ca26a-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="ca26a-126">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="ca26a-126">Connector-specific details</span></span>

<span data-ttu-id="ca26a-127">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="ca26a-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="ca26a-128">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="ca26a-128">More connectors</span></span>
<span data-ttu-id="ca26a-129">Przejdź wstecz toohello [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ca26a-129">Go back toohello [APIs list](apis-list.md).</span></span>
