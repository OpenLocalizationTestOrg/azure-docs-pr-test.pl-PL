---
title: "Łącznik usługi Azure SQL Database hello aaaAdd w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie łącznika usługi Azure SQL Database z parametrami interfejsu API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a><span data-ttu-id="e1e6b-103">Rozpoczynanie pracy z łącznika usługi Azure SQL Database hello</span><span class="sxs-lookup"><span data-stu-id="e1e6b-103">Get started with hello Azure SQL Database connector</span></span>
<span data-ttu-id="e1e6b-104">Za pomocą łącznika usługi Azure SQL Database hello, tworzyć przepływy pracy dla organizacji zarządzających danych w tabelach.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-104">Using hello Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="e1e6b-105">Z bazy danych SQL można:</span><span class="sxs-lookup"><span data-stu-id="e1e6b-105">With SQL Database, you:</span></span>

* <span data-ttu-id="e1e6b-106">Tworzenie przepływu pracy przez dodanie nowej bazy danych klientów tooa klientów lub aktualizowanie zamówienia w bazie danych zamówienia.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-106">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="e1e6b-107">Użyj akcji tooget wiersz danych, wstawić nowy wiersz, a nawet usuwać.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-107">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="e1e6b-108">Na przykład gdy zostaje utworzony rekord w Dynamics CRM Online (wyzwalacz), następnie wstawienia wiersza w bazie danych SQL Azure (działanie).</span><span class="sxs-lookup"><span data-stu-id="e1e6b-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="e1e6b-109">W tym temacie pokazano, jak toouse hello łącznika bazy danych SQL w aplikacji logiki, a także list hello akcje.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-109">This topic shows you how toouse hello SQL Database connector in a logic app, and also lists hello actions.</span></span>

<span data-ttu-id="e1e6b-110">toolearn więcej informacji na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e1e6b-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-sql-database"></a><span data-ttu-id="e1e6b-111">Połącz tooAzure bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="e1e6b-111">Connect tooAzure SQL Database</span></span>
<span data-ttu-id="e1e6b-112">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-112">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="e1e6b-113">Połączenie stanowi połączenie między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="e1e6b-114">Na przykład tooSQL tooconnect bazy danych, należy najpierw utworzyć bazę danych SQL *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-114">For example, tooconnect tooSQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="e1e6b-115">toocreate połączenie, wprowadź poświadczenia hello tooaccess hello usługi, którą jest nawiązywane zwykle jest używana.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-115">toocreate a connection, you enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="e1e6b-116">Tak w bazie danych SQL, wprowadź połączenie hello toocreate poświadczenia bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-116">So, in SQL Database, enter your SQL Database credentials toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="e1e6b-117">Utwórz połączenie hello</span><span class="sxs-lookup"><span data-stu-id="e1e6b-117">Create hello connection</span></span>
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="e1e6b-118">Użyć wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="e1e6b-118">Use a trigger</span></span>
<span data-ttu-id="e1e6b-119">Ten łącznik nie ma żadnych wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-119">This connector does not have any triggers.</span></span> <span data-ttu-id="e1e6b-120">Użyj innych wyzwalaczy toostart hello aplikacji logiki, takie jak wyzwalacz cyklu wyzwalacza HTTP elementu Webhook, wyzwalaczy dostępny z innych łączników i inne.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-120">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="e1e6b-121">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) przykładowego.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="e1e6b-122">Za pomocą akcji</span><span class="sxs-lookup"><span data-stu-id="e1e6b-122">Use an action</span></span>
<span data-ttu-id="e1e6b-123">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-123">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="e1e6b-124">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e1e6b-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="e1e6b-125">Wybierz znak plus hello.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-125">Select hello plus sign.</span></span> <span data-ttu-id="e1e6b-126">Zobacz kilka opcji: **Dodaj akcję**, **Dodaj warunek**, lub jeden z hello **więcej** opcje.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="e1e6b-127">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="e1e6b-128">W polu tekstowym hello wpisz "sql" tooget listę wszystkich hello dostępne akcje.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-128">In hello text box, type “sql” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="e1e6b-129">W tym przykładzie wybierz **SQL Server — wiersz Get**.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="e1e6b-130">Jeśli połączenie już istnieje, a następnie wybierz hello **nazwy tabeli** z listy rozwijanej hello listy, a następnie wprowadź hello **identyfikator wiersza** ma tooreturn.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-130">If a connection already exists, then select hello **Table name** from hello drop-down list, and enter hello **Row ID** you want tooreturn.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="e1e6b-131">Jeśli zostanie wyświetlony monit o informacje o połączeniu hello, wprowadź hello szczegóły toocreate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="e1e6b-132">[Utwórz połączenie hello](connectors-create-api-sqlazure.md#create-the-connection) w tym temacie opisano te właściwości.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-132">[Create hello connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e1e6b-133">W tym przykładzie zostanie zwrócona wiersz z tabeli.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="e1e6b-134">toosee hello dane w tym wierszu, Dodaj inną akcję, która tworzy plik za pomocą hello pola z tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-134">toosee hello data in this row, add another action that creates a file using hello fields from hello table.</span></span> <span data-ttu-id="e1e6b-135">Na przykład dodać akcję OneDrive, która używa hello imię i nazwisko pola toocreate nowy plik w hello konta magazynu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-135">For example, add a OneDrive action that uses hello FirstName and LastName fields toocreate a new file in hello cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="e1e6b-136">**Zapisz** zmiany (lewym górnym rogu paska narzędzi hello).</span><span class="sxs-lookup"><span data-stu-id="e1e6b-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="e1e6b-137">Aplikację logiki jest zapisywana i automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="e1e6b-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="e1e6b-138">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="e1e6b-138">Connector-specific details</span></span>

<span data-ttu-id="e1e6b-139">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="e1e6b-139">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e1e6b-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e1e6b-140">Next steps</span></span>
<span data-ttu-id="e1e6b-141">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e1e6b-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e1e6b-142">Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e1e6b-142">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

