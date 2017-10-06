---
title: "Witaj aaaAdd magazynu obiektów blob Azure łącznika w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Rozpoczęcie pracy i skonfigurować łącznik magazynu obiektów blob platformy Azure hello w aplikacji logiki"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="11057-103">Użyj łącznika magazynu obiektów blob platformy Azure hello w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="11057-103">Use hello Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="11057-104">Użyj hello Azure Blob magazynu łącznika tooupload aktualizacji, Pobierz i usuwanie obiektów blob na koncie magazynu, w całości mieści się w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="11057-104">Use hello Azure Blob storage connector tooupload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="11057-105">Z magazynu obiektów blob platformy Azure możesz:</span><span class="sxs-lookup"><span data-stu-id="11057-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="11057-106">Tworzenie przepływu pracy przez przekazanie nowych projektów lub pobieranie plików, które zostały niedawno zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="11057-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="11057-107">Użyj akcji tooget pliku metadanych, usuń plik, kopiowania plików i inne.</span><span class="sxs-lookup"><span data-stu-id="11057-107">Use actions tooget file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="11057-108">Na przykład po zaktualizowaniu narzędzie Azure witryny sieci web (wyzwalacz) zaktualizować pliku w magazynie obiektów blob (działanie).</span><span class="sxs-lookup"><span data-stu-id="11057-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="11057-109">W tym temacie pokazano, jak toouse hello obiektu blob magazynu łącznika w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="11057-109">This topic shows you how toouse hello blob storage connector in a logic app.</span></span>

<span data-ttu-id="11057-110">toolearn więcej informacji na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="11057-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="11057-111">toolearn więcej informacji na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="11057-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-blob-storage"></a><span data-ttu-id="11057-112">Połącz tooAzure magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="11057-112">Connect tooAzure blob storage</span></span>
<span data-ttu-id="11057-113">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="11057-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="11057-114">Połączenie stanowi połączenie między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="11057-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="11057-115">Na przykład tooconnect tooa konta magazynu, należy najpierw utworzyć magazynu obiektów blob *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="11057-115">For example, tooconnect tooa storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="11057-116">toocreate połączenie, wprowadź poświadczenia hello tooaccess hello usługi, którą jest nawiązywane zwykle jest używana.</span><span class="sxs-lookup"><span data-stu-id="11057-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="11057-117">Dlatego z usługą Azure storage, należy wprowadzić hello poświadczenia tooyour konta toocreate hello połączenia z magazynem.</span><span class="sxs-lookup"><span data-stu-id="11057-117">So with Azure storage, enter hello credentials tooyour storage account toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="11057-118">Utwórz połączenie hello</span><span class="sxs-lookup"><span data-stu-id="11057-118">Create hello connection</span></span>
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="11057-119">Użyć wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="11057-119">Use a trigger</span></span>
<span data-ttu-id="11057-120">Ten łącznik nie ma żadnych wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="11057-120">This connector does not have any triggers.</span></span> <span data-ttu-id="11057-121">Użyj innych wyzwalaczy toostart hello aplikacji logiki, takie jak wyzwalacz cyklu wyzwalacza HTTP elementu Webhook, wyzwalaczy dostępny z innych łączników i inne.</span><span class="sxs-lookup"><span data-stu-id="11057-121">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="11057-122">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) przykładowego.</span><span class="sxs-lookup"><span data-stu-id="11057-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="11057-123">Za pomocą akcji</span><span class="sxs-lookup"><span data-stu-id="11057-123">Use an action</span></span>
<span data-ttu-id="11057-124">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="11057-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span>

1. <span data-ttu-id="11057-125">Wybierz znak plus hello.</span><span class="sxs-lookup"><span data-stu-id="11057-125">Select hello plus sign.</span></span> <span data-ttu-id="11057-126">Zobacz kilka opcji: **Dodaj akcję**, **Dodaj warunek**, lub jeden z hello **więcej** opcje.</span><span class="sxs-lookup"><span data-stu-id="11057-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="11057-127">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="11057-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="11057-128">W polu tekstowym hello wpisz "blob" tooget listę wszystkich hello dostępne akcje.</span><span class="sxs-lookup"><span data-stu-id="11057-128">In hello text box, type “blob” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="11057-129">W tym przykładzie wybierz **AzureBlob - Get metadanych pliku przy użyciu ścieżki**.</span><span class="sxs-lookup"><span data-stu-id="11057-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="11057-130">Jeśli połączenie już istnieje, a następnie wybierz hello **...** (Pokaż selektora) przycisk tooselect pliku.</span><span class="sxs-lookup"><span data-stu-id="11057-130">If a connection already exists, then select hello **...** (Show Picker) button tooselect a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="11057-131">Jeśli zostanie wyświetlony monit o informacje o połączeniu hello, wprowadź hello szczegóły toocreate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="11057-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="11057-132">[Utwórz połączenie hello](connectors-create-api-azureblobstorage.md#create-the-connection) w tym temacie opisano te właściwości.</span><span class="sxs-lookup"><span data-stu-id="11057-132">[Create hello connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="11057-133">W tym przykładzie uzyskujemy hello metadane pliku.</span><span class="sxs-lookup"><span data-stu-id="11057-133">In this example, we get hello metadata of a file.</span></span> <span data-ttu-id="11057-134">toosee hello metadanych, Dodaj inną akcję, która tworzy nowy plik przy użyciu innego łącznika.</span><span class="sxs-lookup"><span data-stu-id="11057-134">toosee hello metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="11057-135">Na przykład dodać akcję OneDrive, która tworzy nowy plik "test" na podstawie hello metadanych.</span><span class="sxs-lookup"><span data-stu-id="11057-135">For example, add a OneDrive action that creates a new "test" file based on hello metadata.</span></span> 


5. <span data-ttu-id="11057-136">**Zapisz** zmiany (lewym górnym rogu paska narzędzi hello).</span><span class="sxs-lookup"><span data-stu-id="11057-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="11057-137">Aplikację logiki jest zapisywana i automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="11057-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="11057-138">[Eksplorator usługi Storage](http://storageexplorer.com/) to doskonałe narzędzie Zarządzanie zbyt wiele kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="11057-138">[Storage Explorer](http://storageexplorer.com/) is a great tool too manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="11057-139">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="11057-139">Connector-specific details</span></span>

<span data-ttu-id="11057-140">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="11057-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="11057-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="11057-141">Next steps</span></span>
<span data-ttu-id="11057-142">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="11057-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="11057-143">Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="11057-143">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

