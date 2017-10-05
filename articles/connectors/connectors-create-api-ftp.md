---
title: "Informacje o sposobie korzystania z łącznika FTP w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Nawiązać połączenia z serwerem FTP można zarządzać plikami. Można wykonywać różne akcje, takie jak przekazywanie, aktualizacji, Pobierz i usuwania plików na serwerze FTP."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 61bfbedfd4f1e84b6976099323a32f3a720634c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="3a2c6-105">Rozpoczynanie pracy z łącznik FTP</span><span class="sxs-lookup"><span data-stu-id="3a2c6-105">Get started with the FTP connector</span></span>
<span data-ttu-id="3a2c6-106">Użyj konektora serwera FTP do monitorowania, zarządzania i utworzyć pliki na serwerze FTP.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="3a2c6-107">Aby użyć [każdy łącznik](apis-list.md), należy najpierw utworzyć aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="3a2c6-108">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3a2c6-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="3a2c6-109">Nawiązać połączenie FTP</span><span class="sxs-lookup"><span data-stu-id="3a2c6-109">Connect to FTP</span></span>
<span data-ttu-id="3a2c6-110">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* do usługi.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="3a2c6-111">A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="3a2c6-112">Utwórz połączenie FTP</span><span class="sxs-lookup"><span data-stu-id="3a2c6-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="3a2c6-113">Użyj wyzwalacz FTP</span><span class="sxs-lookup"><span data-stu-id="3a2c6-113">Use a FTP trigger</span></span>
<span data-ttu-id="3a2c6-114">Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy zdefiniowanych w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="3a2c6-115">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3a2c6-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="3a2c6-116">Łącznik FTP wymaga, aby serwer FTP jest dostępny z Internetu, który jest skonfigurowany do pracy w trybie PASYWNYM.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="3a2c6-117">Ponadto łącznik FTP jest **nie jest zgodne z niejawnych FTPS (FTP za pośrednictwem protokołu SSL)**.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="3a2c6-118">Łącznik FTP obsługuje tylko jawne FTPS (FTP za pośrednictwem protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="3a2c6-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="3a2c6-119">W tym przykładzie, I opisano sposób użycia **FTP - podczas dodawania lub modyfikowania pliku** wyzwalacz tak, aby inicjować przepływ pracy aplikacji logiki, po dodaniu pliku lub zmodyfikowane na serwerze FTP.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="3a2c6-120">W przykładzie przedsiębiorstwa można użyć tego wyzwalacza do monitorowania folderu FTP dla nowych plików, które reprezentują zamówień od klientów.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="3a2c6-121">Można następnie użyć akcji łącznik FTP takich jak **pobrać zawartość pliku** do uzyskania zawartości zlecenia dla dalszego przetwarzania i przechowywania w bazie danych zamówienia.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="3a2c6-122">Wprowadź *ftp* w polu wyszukiwania w Projektancie aplikacji logiki wybiorą **FTP - podczas dodawania lub modyfikowania pliku** wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="3a2c6-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="3a2c6-123">![Obraz wyzwalacza FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="3a2c6-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="3a2c6-124">**Podczas dodawania lub modyfikowania pliku** otwiera formantu</span><span class="sxs-lookup"><span data-stu-id="3a2c6-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="3a2c6-125">![Wyzwalacz FTP — obraz 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="3a2c6-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="3a2c6-126">Wybierz **...**  znajdujący się po prawej stronie formantu.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="3a2c6-127">Spowoduje to otwarcie formant wyboru folderu</span><span class="sxs-lookup"><span data-stu-id="3a2c6-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="3a2c6-128">![Obraz wyzwalacza FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="3a2c6-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="3a2c6-129">Wybierz  **>**  (Strzałka w prawo) i przejdź do folderu, który chcesz monitorować nowe lub zmodyfikowane pliki.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="3a2c6-130">Wybierz folder i zwróć uwagę, folder zostanie wyświetlona w **folderu** formantu.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="3a2c6-131">![Obraz wyzwalacza FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="3a2c6-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="3a2c6-132">W tym momencie aplikację logiki została skonfigurowana z wyzwalaczy, które rozpocznie wykonywania innych wyzwalacze i akcje w przepływie pracy zmodyfikowanie lub utworzony w folderze FTP określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="3a2c6-133">Dla aplikacji logiki działała musi ona zawierać przynajmniej jeden wyzwalacz i jedną akcję.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="3a2c6-134">Wykonaj kroki opisane w następnej sekcji, aby dodać akcję.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="3a2c6-135">Za pomocą akcji FTP</span><span class="sxs-lookup"><span data-stu-id="3a2c6-135">Use a FTP action</span></span>
<span data-ttu-id="3a2c6-136">Akcja jest przeprowadzane przez przepływ pracy zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="3a2c6-137">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3a2c6-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="3a2c6-138">Teraz, wyzwalacz został dodany, wykonaj następujące kroki, aby dodać akcję, która pobierze zawartość pliku nowe lub zmodyfikowane, znalezione przez wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="3a2c6-139">Wybierz **+ nowy krok** Aby dodać akcję do uzyskania zawartości pliku na serwerze FTP</span><span class="sxs-lookup"><span data-stu-id="3a2c6-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="3a2c6-140">Wybierz **Dodaj akcję** łącza.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="3a2c6-141">![Obraz akcji FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="3a2c6-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="3a2c6-142">Wprowadź *FTP* aby wyszukać wszystkie operacje dotyczące FTP.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="3a2c6-143">Wybierz **FTP — pobranie zawartości pliku** jako akcję wykonywaną, gdy nowe lub zmodyfikowane pliku znajduje się w folderze FTP.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="3a2c6-144">![Obraz akcji FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="3a2c6-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="3a2c6-145">**Pobrać zawartość pliku** sterowania zostanie otwarta.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-145">The **Get file content** control opens.</span></span> <span data-ttu-id="3a2c6-146">**Uwaga**: pojawi się monit o autoryzowanie aplikację logiki, aby uzyskać dostęp do konta serwera FTP, jeśli nie zostało zrobione to wcześniej.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="3a2c6-147">![Obraz akcji FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="3a2c6-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="3a2c6-148">Wybierz **pliku** formantu (biały znak znajdujący się poniżej **pliku***).</span><span class="sxs-lookup"><span data-stu-id="3a2c6-148">Select the **File** control (the white space located below **FILE***).</span></span> <span data-ttu-id="3a2c6-149">W tym miejscu służy różnych właściwości z pliku nowe lub zmodyfikowane na serwerze FTP.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="3a2c6-150">Wybierz **plików zawartości** opcji.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="3a2c6-151">![Obraz akcji FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="3a2c6-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="3a2c6-152">Formant jest aktualizowany, co oznacza, że **FTP — pobranie zawartości pliku** akcji uzyskają *plików zawartości* pliku nowe lub zmodyfikowane na serwerze FTP.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="3a2c6-153">![Obraz akcji FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="3a2c6-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="3a2c6-154">Zapisz swoją pracę, a następnie dodaj plik do folderu FTP, aby przetestować przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="3a2c6-155">W tym momencie aplikacji logiki została skonfigurowana z wyzwalaczem monitorowania folderu na serwerze FTP i inicjowania przepływu pracy, gdy znajdzie się nowy plik lub zmodyfikowany plik na serwerze FTP.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="3a2c6-156">Aplikacja logiki również została skonfigurowana z akcją do uzyskania zawartości pliku nowe lub zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="3a2c6-157">Można teraz dodawać innej akcji takich jak [SQL Server — Wstaw wiersz](connectors-create-api-sqlazure.md) akcji, aby wstawić zawartość pliku nowe lub zmodyfikowane do tabeli bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="3a2c6-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="3a2c6-158">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="3a2c6-158">Connector-specific details</span></span>

<span data-ttu-id="3a2c6-159">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="3a2c6-159">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3a2c6-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3a2c6-160">Next Steps</span></span>
[<span data-ttu-id="3a2c6-161">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="3a2c6-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

