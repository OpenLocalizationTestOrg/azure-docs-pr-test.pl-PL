---
title: "aaaLearn jak toouse hello łącznik FTP w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połącz tooFTP toomanage serwera plików. Można wykonywać różne akcje, takie jak przekazywanie, aktualizacji, Pobierz i usuwania plików na serwerze FTP."
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
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a><span data-ttu-id="8b118-105">Rozpoczynanie pracy z hello łącznik FTP</span><span class="sxs-lookup"><span data-stu-id="8b118-105">Get started with hello FTP connector</span></span>
<span data-ttu-id="8b118-106">Korzystanie ze toomonitor łącznika hello FTP, zarządzanie i utworzyć pliki na serwerze FTP.</span><span class="sxs-lookup"><span data-stu-id="8b118-106">Use hello FTP connector toomonitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="8b118-107">toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="8b118-107">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="8b118-108">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8b118-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooftp"></a><span data-ttu-id="8b118-109">Połącz tooFTP</span><span class="sxs-lookup"><span data-stu-id="8b118-109">Connect tooFTP</span></span>
<span data-ttu-id="8b118-110">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="8b118-110">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="8b118-111">A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="8b118-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tooftp"></a><span data-ttu-id="8b118-112">Tworzenie tooFTP połączenia</span><span class="sxs-lookup"><span data-stu-id="8b118-112">Create a connection tooFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="8b118-113">Użyj wyzwalacz FTP</span><span class="sxs-lookup"><span data-stu-id="8b118-113">Use a FTP trigger</span></span>
<span data-ttu-id="8b118-114">Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="8b118-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="8b118-115">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="8b118-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="8b118-116">Łącznik FTP Hello wymaga się, że serwer FTP, który jest dostępny z Internetu hello i jest skonfigurowany toooperate trybu PASYWNEGO.</span><span class="sxs-lookup"><span data-stu-id="8b118-116">hello FTP connector requires an FTP server that  is accessible from hello Internet and is configured toooperate with PASSIVE mode.</span></span> <span data-ttu-id="8b118-117">Ponadto łącznik hello FTP jest **nie jest zgodne z niejawnych FTPS (FTP za pośrednictwem protokołu SSL)**.</span><span class="sxs-lookup"><span data-stu-id="8b118-117">Also, hello FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="8b118-118">Witaj łącznik FTP obsługuje tylko jawne FTPS (FTP za pośrednictwem protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="8b118-118">hello FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="8b118-119">W tym przykładzie I przedstawia sposób toouse hello **FTP - podczas dodawania lub modyfikowania pliku** wyzwolenia tooinitiate przepływu pracy aplikacji logiki, po dodaniu pliku lub zmodyfikowane na serwerze FTP.</span><span class="sxs-lookup"><span data-stu-id="8b118-119">In this example, I will show you how toouse hello **FTP - When a file is added or modified** trigger tooinitiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="8b118-120">Przykład przedsiębiorstwa można użyć tego wyzwalacza toomonitor FTP folder nowych plików, które reprezentują zamówień od klientów.</span><span class="sxs-lookup"><span data-stu-id="8b118-120">In an enterprise example, you could use this trigger toomonitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="8b118-121">Można następnie użyć akcji łącznik FTP takich jak **pobrać zawartość pliku** tooget zawartość hello hello kolejności dla dalszego przetwarzania i przechowywania w bazie danych zamówienia.</span><span class="sxs-lookup"><span data-stu-id="8b118-121">You could then use an FTP connector action such as **Get file content** tooget hello contents of hello order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="8b118-122">Wprowadź *ftp* w polu wyszukiwania hello hello logiki aplikacji designer wybierz hello **FTP - podczas dodawania lub modyfikowania pliku** wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="8b118-122">Enter *ftp* in hello search box on hello logic apps designer then select hello **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="8b118-123">![Obraz wyzwalacza FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="8b118-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="8b118-124">Witaj **podczas dodawania lub modyfikowania pliku** otwiera formantu</span><span class="sxs-lookup"><span data-stu-id="8b118-124">hello **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="8b118-125">![Wyzwalacz FTP — obraz 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="8b118-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="8b118-126">Wybierz hello **...**  znajdujący się po prawej stronie powitania hello formantu.</span><span class="sxs-lookup"><span data-stu-id="8b118-126">Select hello **...** located on hello right side of hello control.</span></span> <span data-ttu-id="8b118-127">Spowoduje to otwarcie formant wyboru hello folderu</span><span class="sxs-lookup"><span data-stu-id="8b118-127">This opens hello folder picker control</span></span>  
   <span data-ttu-id="8b118-128">![Obraz wyzwalacza FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="8b118-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="8b118-129">Wybierz hello  **>**  (Strzałka w prawo), a następnie przejdź do folderu hello toofind mają toomonitor dla nowych lub zmienionych plików.</span><span class="sxs-lookup"><span data-stu-id="8b118-129">Select hello **>** (right arrow) and browse toofind hello folder that you want toomonitor for new or modified files.</span></span> <span data-ttu-id="8b118-130">Wybierz hello folder — hello folder jest teraz wyświetlany na powitania **folderu** formantu.</span><span class="sxs-lookup"><span data-stu-id="8b118-130">Select hello folder and notice hello folder is now displayed in hello **Folder** control.</span></span>  
   <span data-ttu-id="8b118-131">![Obraz wyzwalacza FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="8b118-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="8b118-132">W tym momencie aplikację logiki została skonfigurowana z wyzwalaczy, które rozpocznie się uruchom hello innych wyzwalacze i akcje w przepływie pracy powitania po modyfikacji lub utworzone w określonym folderze FTP hello pliku.</span><span class="sxs-lookup"><span data-stu-id="8b118-132">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow when a file is either modified or created in hello specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="8b118-133">Dla logiki aplikacji toobe funkcjonalności musi ona zawierać przynajmniej jeden wyzwalacz i jedną akcję.</span><span class="sxs-lookup"><span data-stu-id="8b118-133">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="8b118-134">Wykonaj kroki hello hello następnej sekcji tooadd akcji.</span><span class="sxs-lookup"><span data-stu-id="8b118-134">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="8b118-135">Za pomocą akcji FTP</span><span class="sxs-lookup"><span data-stu-id="8b118-135">Use a FTP action</span></span>
<span data-ttu-id="8b118-136">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="8b118-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="8b118-137">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="8b118-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="8b118-138">Teraz, wyzwalacz został dodany, wykonaj te kroki tooadd akcję, która pobierze zawartość pliku nowe lub zmodyfikowane hello znalezione przez wyzwalacz hello hello.</span><span class="sxs-lookup"><span data-stu-id="8b118-138">Now that you have added a trigger, follow these steps tooadd an action that will get hello contents of hello new or modified file found by hello trigger.</span></span>    

1. <span data-ttu-id="8b118-139">Wybierz **+ nowy krok** tooadd hello hello akcji tooget hello zawartość hello pliku na serwerze hello FTP</span><span class="sxs-lookup"><span data-stu-id="8b118-139">Select **+ New step** tooadd hello hello action tooget hello contents of hello file on hello FTP server</span></span>  
2. <span data-ttu-id="8b118-140">Wybierz hello **Dodaj akcję** łącza.</span><span class="sxs-lookup"><span data-stu-id="8b118-140">Select hello **Add an action** link.</span></span>  
   <span data-ttu-id="8b118-141">![Obraz akcji FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="8b118-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="8b118-142">Wprowadź *FTP* tooFTP związane z toosearch dla wszystkich akcji.</span><span class="sxs-lookup"><span data-stu-id="8b118-142">Enter *FTP* toosearch for all actions related tooFTP.</span></span>
4. <span data-ttu-id="8b118-143">Wybierz **FTP — pobranie zawartości pliku** jako hello tootake akcji, gdy nowe lub zmodyfikowane pliku znajduje się w folderze hello FTP.</span><span class="sxs-lookup"><span data-stu-id="8b118-143">Select **FTP - Get file content**  as hello action tootake when a new or modified file is found in hello FTP folder.</span></span>      
   <span data-ttu-id="8b118-144">![Obraz akcji FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="8b118-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="8b118-145">Witaj **pobrać zawartość pliku** sterowania zostanie otwarta.</span><span class="sxs-lookup"><span data-stu-id="8b118-145">hello **Get file content** control opens.</span></span> <span data-ttu-id="8b118-146">**Uwaga**: użytkownik będzie zostanie wyświetlony monit o tooauthorize Twojego tooaccess aplikacji logiki konta serwera FTP, jeśli nie zostało zrobione to wcześniej.</span><span class="sxs-lookup"><span data-stu-id="8b118-146">**Note**: you will be prompted tooauthorize your logic app tooaccess your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="8b118-147">![Obraz akcji FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="8b118-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="8b118-148">Wybierz hello **pliku** formantu (hello biały znak znajdujący się poniżej **pliku***).</span><span class="sxs-lookup"><span data-stu-id="8b118-148">Select hello **File** control (hello white space located below **FILE***).</span></span> <span data-ttu-id="8b118-149">W tym miejscu można żadnego hello różne właściwości z pliku nowe lub zmodyfikowane hello na powitania serwera FTP.</span><span class="sxs-lookup"><span data-stu-id="8b118-149">Here, you can use any of hello various properties from hello new or modified file found on hello FTP server.</span></span>  
6. <span data-ttu-id="8b118-150">Wybierz hello **plików zawartości** opcji.</span><span class="sxs-lookup"><span data-stu-id="8b118-150">Select hello **File content** option.</span></span>  
   <span data-ttu-id="8b118-151">![Obraz akcji FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="8b118-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="8b118-152">Formant Hello jest aktualizowany, wskazującą, że hello **FTP — pobranie zawartości pliku** akcji uzyskają hello *plików zawartości* hello pliku nowe lub zmodyfikowane na serwerze hello FTP.</span><span class="sxs-lookup"><span data-stu-id="8b118-152">hello control is updated, indicating that hello **FTP - Get file content** action will get hello *file content* of hello new or modified file on hello FTP server.</span></span>      
   <span data-ttu-id="8b118-153">![Obraz akcji FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="8b118-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="8b118-154">Zapisz swoją pracę, a następnie dodaj plik toohello FTP folderu tootest przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="8b118-154">Save your work then add a file toohello FTP folder tootest your workflow.</span></span>    

<span data-ttu-id="8b118-155">W tym momencie aplikacji logiki hello został skonfigurowany z toomonitor wyzwalacza folderu na serwerze FTP i hello inicjowania przepływu pracy, gdy znajdzie się nowy plik lub zmodyfikowany plik na serwerze hello FTP.</span><span class="sxs-lookup"><span data-stu-id="8b118-155">At this point, hello logic app has been configured with a trigger toomonitor a folder on an FTP server and initiate hello workflow when it finds either a new file or a modified file on hello FTP server.</span></span> 

<span data-ttu-id="8b118-156">Aplikacja logiki Hello również została skonfigurowana z akcji hello zawartość tooget hello nowych lub zmodyfikowanych plików.</span><span class="sxs-lookup"><span data-stu-id="8b118-156">hello logic app also has been configured with an action tooget hello contents of hello new or modified file.</span></span>

<span data-ttu-id="8b118-157">Można teraz dodawać innej akcji, takich jak hello [SQL Server — Wstaw wiersz](connectors-create-api-sqlazure.md) akcji tooinsert hello zawartość hello nowych lub zmodyfikowanych plików do tabeli bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="8b118-157">You can now add another action such as hello [SQL Server - insert row](connectors-create-api-sqlazure.md) action tooinsert hello contents of hello new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="8b118-158">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="8b118-158">Connector-specific details</span></span>

<span data-ttu-id="8b118-159">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="8b118-159">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8b118-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8b118-160">Next Steps</span></span>
[<span data-ttu-id="8b118-161">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="8b118-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

