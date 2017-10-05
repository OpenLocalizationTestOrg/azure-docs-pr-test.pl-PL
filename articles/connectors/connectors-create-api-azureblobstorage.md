---
title: "Dodawanie magazynu obiektów blob platformy Azure łącznika w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Rozpoczęcie pracy i skonfigurować łącznik magazynu obiektów blob platformy Azure w aplikacji logiki"
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
ms.openlocfilehash: bc7908868828bd1628633cf9e57f8c44f8000827
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="05431-103">Korzystania z łącznika magazynu obiektów blob platformy Azure w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="05431-103">Use the Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="05431-104">Łącznik magazynu obiektów Blob platformy Azure umożliwia przekazywanie, zaktualizować, Pobierz i usuwanie obiektów blob na koncie magazynu, w całości mieści się w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="05431-104">Use the Azure Blob storage connector to upload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="05431-105">Z magazynu obiektów blob platformy Azure możesz:</span><span class="sxs-lookup"><span data-stu-id="05431-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="05431-106">Tworzenie przepływu pracy przez przekazanie nowych projektów lub pobieranie plików, które zostały niedawno zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="05431-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="05431-107">Akcje służy do pobierania metadanych pliku, usuń plik, kopiowania plików i inne.</span><span class="sxs-lookup"><span data-stu-id="05431-107">Use actions to get file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="05431-108">Na przykład po zaktualizowaniu narzędzie Azure witryny sieci web (wyzwalacz) zaktualizować pliku w magazynie obiektów blob (działanie).</span><span class="sxs-lookup"><span data-stu-id="05431-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="05431-109">W tym temacie przedstawiono sposób korzystania z łącznika magazynu obiektów blob w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="05431-109">This topic shows you how to use the blob storage connector in a logic app.</span></span>

<span data-ttu-id="05431-110">Aby dowiedzieć się więcej na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="05431-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="05431-111">Aby dowiedzieć się więcej na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="05431-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-blob-storage"></a><span data-ttu-id="05431-112">Łączenie się z magazynem obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="05431-112">Connect to Azure blob storage</span></span>
<span data-ttu-id="05431-113">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* do usługi.</span><span class="sxs-lookup"><span data-stu-id="05431-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="05431-114">Połączenie stanowi połączenie między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="05431-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="05431-115">Na przykład, aby połączyć konto magazynu, należy najpierw utworzyć magazynu obiektów blob *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="05431-115">For example, to connect to a storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="05431-116">Aby utworzyć połączenie, wprowadź poświadczenia, zwykle używanego do uzyskania dostępu do usługi, którą jest nawiązywane.</span><span class="sxs-lookup"><span data-stu-id="05431-116">To create a connection, enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="05431-117">Dlatego z usługą Azure storage, wprowadź poświadczenia konta magazynu do utworzenia połączenia.</span><span class="sxs-lookup"><span data-stu-id="05431-117">So with Azure storage, enter the credentials to your storage account to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="05431-118">Tworzenie połączenia</span><span class="sxs-lookup"><span data-stu-id="05431-118">Create the connection</span></span>
> [!INCLUDE [Create a connection to Azure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="05431-119">Użyć wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="05431-119">Use a trigger</span></span>
<span data-ttu-id="05431-120">Ten łącznik nie ma żadnych wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="05431-120">This connector does not have any triggers.</span></span> <span data-ttu-id="05431-121">Użyj innych wyzwalaczy, aby uruchomić aplikację logiki, takie jak wyzwalacz cyklu wyzwalacza HTTP elementu Webhook, wyzwalaczy dostępny z innych łączników i inne.</span><span class="sxs-lookup"><span data-stu-id="05431-121">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="05431-122">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) przykładowego.</span><span class="sxs-lookup"><span data-stu-id="05431-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="05431-123">Za pomocą akcji</span><span class="sxs-lookup"><span data-stu-id="05431-123">Use an action</span></span>
<span data-ttu-id="05431-124">Akcja jest przeprowadzane przez przepływ pracy zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="05431-124">An action is an operation carried out by the workflow defined in a logic app.</span></span>

1. <span data-ttu-id="05431-125">Wybierz znak plus.</span><span class="sxs-lookup"><span data-stu-id="05431-125">Select the plus sign.</span></span> <span data-ttu-id="05431-126">Zobacz kilka opcji: **Dodaj akcję**, **Dodaj warunek**, lub jeden z **więcej** opcje.</span><span class="sxs-lookup"><span data-stu-id="05431-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="05431-127">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="05431-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="05431-128">W polu tekstowym wpisz "blob", aby uzyskać listę dostępnych akcji.</span><span class="sxs-lookup"><span data-stu-id="05431-128">In the text box, type “blob” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="05431-129">W tym przykładzie wybierz **AzureBlob - Get metadanych pliku przy użyciu ścieżki**.</span><span class="sxs-lookup"><span data-stu-id="05431-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="05431-130">Jeśli połączenie już istnieje, następnie wybierz **...** (Pokaż selektora), aby wybrać plik.</span><span class="sxs-lookup"><span data-stu-id="05431-130">If a connection already exists, then select the **...** (Show Picker) button to select a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="05431-131">Jeśli zostanie wyświetlony monit o informacje dotyczące połączenia, wprowadź szczegóły, aby utworzyć połączenie.</span><span class="sxs-lookup"><span data-stu-id="05431-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="05431-132">[Utwórz połączenie](connectors-create-api-azureblobstorage.md#create-the-connection) w tym temacie opisano te właściwości.</span><span class="sxs-lookup"><span data-stu-id="05431-132">[Create the connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="05431-133">W tym przykładzie uzyskujemy metadane pliku.</span><span class="sxs-lookup"><span data-stu-id="05431-133">In this example, we get the metadata of a file.</span></span> <span data-ttu-id="05431-134">Aby wyświetlić metadane, Dodaj inną akcję, która tworzy nowy plik przy użyciu innego łącznika.</span><span class="sxs-lookup"><span data-stu-id="05431-134">To see the metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="05431-135">Na przykład dodać akcję OneDrive, która tworzy nowy plik "test" na podstawie metadanych.</span><span class="sxs-lookup"><span data-stu-id="05431-135">For example, add a OneDrive action that creates a new "test" file based on the metadata.</span></span> 


5. <span data-ttu-id="05431-136">**Zapisz** zmiany (lewym górnym rogu paska narzędzi).</span><span class="sxs-lookup"><span data-stu-id="05431-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="05431-137">Aplikację logiki jest zapisywana i automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="05431-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="05431-138">[Eksplorator usługi Storage](http://storageexplorer.com/) to doskonałe narzędzie do zarządzania wieloma kontami magazynu.</span><span class="sxs-lookup"><span data-stu-id="05431-138">[Storage Explorer](http://storageexplorer.com/) is a great tool to  manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="05431-139">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="05431-139">Connector-specific details</span></span>

<span data-ttu-id="05431-140">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="05431-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="05431-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05431-141">Next steps</span></span>
<span data-ttu-id="05431-142">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="05431-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="05431-143">Eksploruj dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="05431-143">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

