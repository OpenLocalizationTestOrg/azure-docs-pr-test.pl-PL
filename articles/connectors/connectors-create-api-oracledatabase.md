---
title: "Łącznik bazą danych Oracle hello aaaAdd w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj łącznika bazy danych Oracle hello w aplikacji logiki"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="9cf07-103">Rozpoczynanie pracy z hello bazą danych Oracle łącznika</span><span class="sxs-lookup"><span data-stu-id="9cf07-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="9cf07-104">Za pomocą łącznika bazy danych Oracle hello, możesz utworzyć organizacyjnej przepływów pracy korzystających z danych w istniejącej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="9cf07-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="9cf07-105">Ten łącznik można połączyć tooan instalowania lokalną bazą danych Oracle lub maszyny wirtualnej platformy Azure z bazą danych Oracle.</span><span class="sxs-lookup"><span data-stu-id="9cf07-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="9cf07-106">Ten łącznik można:</span><span class="sxs-lookup"><span data-stu-id="9cf07-106">With this connector, you can:</span></span>

* <span data-ttu-id="9cf07-107">Tworzenie przepływu pracy przez dodanie nowej bazy danych klientów tooa klientów lub aktualizowanie zamówienia w bazie danych zamówienia.</span><span class="sxs-lookup"><span data-stu-id="9cf07-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="9cf07-108">Użyj akcji tooget wiersz danych, wstawić nowy wiersz, a nawet usuwać.</span><span class="sxs-lookup"><span data-stu-id="9cf07-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="9cf07-109">Na przykład gdy zostaje utworzony rekord w Dynamics CRM Online (wyzwalacz), następnie wstawienia wiersza w bazie danych programu Oracle (działanie).</span><span class="sxs-lookup"><span data-stu-id="9cf07-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="9cf07-110">W tym temacie pokazano, jak toouse hello łącznik bazy danych Oracle w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="9cf07-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cf07-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9cf07-111">Prerequisites</span></span>

* <span data-ttu-id="9cf07-112">Obsługiwane wersje programu Oracle:</span><span class="sxs-lookup"><span data-stu-id="9cf07-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="9cf07-113">Oracle 9 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="9cf07-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="9cf07-114">Oprogramowania klienta Oracle 8.1.7 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="9cf07-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="9cf07-115">Instalowanie bramy danych lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="9cf07-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="9cf07-116">[Połączenie lokalne tooon dane z aplikacji logiki](../logic-apps/logic-apps-gateway-connection.md) list hello kroki.</span><span class="sxs-lookup"><span data-stu-id="9cf07-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="9cf07-117">Brama Hello jest wymagane tooconnect tooan lokalną bazą danych Oracle lub maszynie Wirtualnej platformy Azure z bazy danych Oracle zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="9cf07-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="9cf07-118">Brama danych lokalne powitania działa jako mostka i udostępnia bezpiecznego transferu danych między lokalnymi danych (który nie znajduje się w chmurze hello) i aplikacje logiki.</span><span class="sxs-lookup"><span data-stu-id="9cf07-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="9cf07-119">Witaj, tej samej bramy może być używane z wieloma usługami i wiele źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="9cf07-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="9cf07-120">Tak konieczne może być bramy hello tooinstall raz.</span><span class="sxs-lookup"><span data-stu-id="9cf07-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="9cf07-121">Na komputerze hello, w którym zainstalowano bramę danych lokalne powitania, należy zainstalować powitania klienta Oracle.</span><span class="sxs-lookup"><span data-stu-id="9cf07-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="9cf07-122">Należy upewnić się, tooinstall hello dostawca danych programu Oracle 64-bitowego dla platformy .NET z bazy danych Oracle:</span><span class="sxs-lookup"><span data-stu-id="9cf07-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="9cf07-123">64-bitowych ODAC 12c w wersji 4 (12.1.0.2.4) dla systemu Windows x64</span><span class="sxs-lookup"><span data-stu-id="9cf07-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="9cf07-124">Jeśli nie zainstalowano klienta Oracle hello, wystąpił błąd występuje, gdy spróbuj toocreate lub użyj hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="9cf07-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="9cf07-125">Zobacz hello typowych błędów w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="9cf07-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="9cf07-126">Dodaj hello łącznika</span><span class="sxs-lookup"><span data-stu-id="9cf07-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cf07-127">Ten łącznik nie ma żadnych wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="9cf07-127">This connector does not have any triggers.</span></span> <span data-ttu-id="9cf07-128">Ma ona tylko akcje.</span><span class="sxs-lookup"><span data-stu-id="9cf07-128">It has only actions.</span></span> <span data-ttu-id="9cf07-129">Tak podczas tworzenia aplikacji logiki, Dodaj inny toostart wyzwalacza aplikacji logiki, takie jak **harmonogram - cyklu**, lub **żądania / odpowiedzi - odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="9cf07-130">W hello [portalu Azure](https://portal.azure.com), tworzenie aplikacji logiki puste.</span><span class="sxs-lookup"><span data-stu-id="9cf07-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="9cf07-131">Na początku hello aplikację logiki, wybierz hello **żądanie / odpowiedź — żądanie** wyzwalacz:</span><span class="sxs-lookup"><span data-stu-id="9cf07-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="9cf07-132">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-132">Select **Save**.</span></span> <span data-ttu-id="9cf07-133">Po zapisaniu, adres URL żądania jest generowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="9cf07-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="9cf07-134">Wybierz **nowy krok**i wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="9cf07-135">Wpisz `oracle` toosee hello dostępne akcje:</span><span class="sxs-lookup"><span data-stu-id="9cf07-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="9cf07-136">Dotyczy to również hello najszybszy sposób toosee hello wyzwalacze i Akcje dostępne dla wszystkich łączników.</span><span class="sxs-lookup"><span data-stu-id="9cf07-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="9cf07-137">Wpisz część nazwy łącznika hello, takich jak `oracle`.</span><span class="sxs-lookup"><span data-stu-id="9cf07-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="9cf07-138">Projektant Hello wymieniono żadne wyzwalacze i wszystkie akcje.</span><span class="sxs-lookup"><span data-stu-id="9cf07-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="9cf07-139">Wybierz jedno z hello działań, takich jak **bazą danych Oracle — wiersz Get**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="9cf07-140">Wybierz **Połącz za pośrednictwem bramy danych lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="9cf07-141">Wprowadź nazwę serwera Oracle hello, metody uwierzytelniania, nazwy użytkownika, hasło i wybierz hello bramy:</span><span class="sxs-lookup"><span data-stu-id="9cf07-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="9cf07-142">Po nawiązaniu połączenia, wybierz tabelę z listy hello, a następnie wprowadź hello wiersza identyfikator tooyour tabeli.</span><span class="sxs-lookup"><span data-stu-id="9cf07-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="9cf07-143">Należy tooknow hello identyfikator toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="9cf07-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="9cf07-144">Jeśli nie znasz, skontaktuj się z administratorem bazy danych Oracle i pobrać dane wyjściowe hello `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="9cf07-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="9cf07-145">Dzięki temu hello informacje umożliwiające identyfikację potrzebne tooproceed.</span><span class="sxs-lookup"><span data-stu-id="9cf07-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="9cf07-146">W hello poniższy przykład zadanie dane zostały zwrócone z bazy danych zasobów ludzkich:</span><span class="sxs-lookup"><span data-stu-id="9cf07-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="9cf07-147">W następnym kroku należy można użyć dowolnego z hello toobuild innych łączników przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="9cf07-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="9cf07-148">Jeśli tootest pobieranie danych z bazy danych Oracle, a następnie wyślij do siebie wiadomość e-mail z hello danych Oracle przy użyciu jednej z hello wysłać wiadomości e-mail łączników, takie usługi Office 365 lub Gmail.</span><span class="sxs-lookup"><span data-stu-id="9cf07-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="9cf07-149">Używaj tokenów dynamiczne hello z hello Oracle tabeli toobuild hello `Subject` i `Body` Twojego adresu e-mail:</span><span class="sxs-lookup"><span data-stu-id="9cf07-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="9cf07-150">**Zapisz** aplikacji logiki, a następnie wybierz **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="9cf07-151">Zamknij projektanta hello i przyjrzyj się Historia uruchomień hello hello stanu.</span><span class="sxs-lookup"><span data-stu-id="9cf07-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="9cf07-152">W przypadku niepowodzenia zaznacz wiersz nie powiodło się wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="9cf07-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="9cf07-153">Otwiera Hello projektanta i programy, które użytkownik, który krok nie powiodło się, a także przedstawiono hello informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="9cf07-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="9cf07-154">Zakończy się pomyślnie, powinien otrzymywać wiadomość e-mail z informacjami o hello, dodane.</span><span class="sxs-lookup"><span data-stu-id="9cf07-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="9cf07-155">Koncepcje przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="9cf07-155">Workflow ideas</span></span>

* <span data-ttu-id="9cf07-156">Mają hasztagiem hello #oracle toomonitor i put tweetów hello w bazie danych, dzięki czemu może być zbadać i używane w innych aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="9cf07-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="9cf07-157">W aplikacji logiki, Dodaj hello `Twitter - When a new tweet is posted` wyzwalania, a następnie wprowadź hello **#oracle** hasztagiem.</span><span class="sxs-lookup"><span data-stu-id="9cf07-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="9cf07-158">Następnie należy dodać hello `Oracle Database - Insert row` akcji i wybierz tabelę:</span><span class="sxs-lookup"><span data-stu-id="9cf07-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="9cf07-159">Komunikaty są wysyłane tooa kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9cf07-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="9cf07-160">Mają tooget te komunikaty i umieść je w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="9cf07-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="9cf07-161">W aplikacji logiki, Dodaj hello `Service Bus - when a message is received in a queue` wyzwalacza i wybierz hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="9cf07-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="9cf07-162">Następnie należy dodać hello `Oracle Database - Insert row` akcji i wybierz tabelę:</span><span class="sxs-lookup"><span data-stu-id="9cf07-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="9cf07-163">Typowe błędy</span><span class="sxs-lookup"><span data-stu-id="9cf07-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="9cf07-164">**Błąd**: nie można osiągnąć hello bramy</span><span class="sxs-lookup"><span data-stu-id="9cf07-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="9cf07-165">**Przyczyna**: hello lokalnych danych brama nie jest w stanie tooconnect toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="9cf07-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="9cf07-166">**Środki zaradcze**: Upewnij się, że brama jest uruchomiona na hello na lokalnym komputerze, na którym został zainstalowany i że mogą się łączyć toohello internet.</span><span class="sxs-lookup"><span data-stu-id="9cf07-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="9cf07-167">Zalecamy nie zainstalowanie bramy hello na komputerze, który może zostać wyłączone lub uśpienia.</span><span class="sxs-lookup"><span data-stu-id="9cf07-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="9cf07-168">Można również uruchomić ponownie usługi bramy danych lokalne powitania (PBIEgwService).</span><span class="sxs-lookup"><span data-stu-id="9cf07-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="9cf07-169">**Błąd**: Dostawca hello jest używany jest przestarzały: "element System.Data.OracleClient wymaga oprogramowania klienta w wersji version 8.1.7 Oracle lub większą.".</span><span class="sxs-lookup"><span data-stu-id="9cf07-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="9cf07-170">Odwiedź stronę [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello oficjalnego dostawcę.</span><span class="sxs-lookup"><span data-stu-id="9cf07-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="9cf07-171">**Przyczyna**: powitania klienta Oracle zestawu SDK nie jest zainstalowany na komputerze hello, gdzie hello lokalnymi brama danych jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="9cf07-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="9cf07-172">**Rozdzielczość**: Pobierz i zainstaluj klienta Oracle hello SDK hello tym samym komputerze co brama danych lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="9cf07-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="9cf07-173">**Błąd**: Tabela "[Nazwa_tabeli]" nie definiuje żadnych kolumn klucza</span><span class="sxs-lookup"><span data-stu-id="9cf07-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="9cf07-174">**Przyczyna**: hello tabela nie ma żadnego klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="9cf07-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="9cf07-175">**Rozdzielczość**: hello łącznika bazy danych programu Oracle wymaga użycia tabelę z kolumną klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="9cf07-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="9cf07-176">Obecnie nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="9cf07-176">Currently not supported</span></span>

* <span data-ttu-id="9cf07-177">Widoki i procedury składowane</span><span class="sxs-lookup"><span data-stu-id="9cf07-177">Views and stored procedures</span></span> 
* <span data-ttu-id="9cf07-178">Tabeli za pomocą kluczy złożonych</span><span class="sxs-lookup"><span data-stu-id="9cf07-178">Any table with composite keys</span></span>
* <span data-ttu-id="9cf07-179">Zagnieżdżone typy obiektów w tabelach</span><span class="sxs-lookup"><span data-stu-id="9cf07-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="9cf07-180">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="9cf07-180">Connector-specific details</span></span>

<span data-ttu-id="9cf07-181">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="9cf07-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="9cf07-182">Uzyskaj pomoc</span><span class="sxs-lookup"><span data-stu-id="9cf07-182">Get some help</span></span>

<span data-ttu-id="9cf07-183">Witaj [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) jest doskonałym umieścić tooask pytania, odpowiedzi na pytania i zobacz, co robią użytkownicy innych Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="9cf07-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="9cf07-184">Można zwiększyć Logic Apps i łącznikami głosu i przesyłanie pomysłów na [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="9cf07-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="9cf07-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9cf07-185">Next steps</span></span>
<span data-ttu-id="9cf07-186">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)i przejrzyj dostępne łączniki hello w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="9cf07-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
