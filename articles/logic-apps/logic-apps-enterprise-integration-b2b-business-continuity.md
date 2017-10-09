---
title: "odzyskiwanie aaaDisaster dla konta integracji B2B — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: Odzyskiwanie po awarii B2B aplikacje logiki
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="f7e8b-103">Odzyskiwanie po awarii między region B2B aplikacje logiki</span><span class="sxs-lookup"><span data-stu-id="f7e8b-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="f7e8b-104">Obciążeń B2B obejmują transakcje pieniężne jak zamówienia i faktury.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="f7e8b-105">Podczas zdarzenia po awarii jest krytyczne w hello toomeet Odzyskaj tooquickly biznesowych, które SLA biznesowej uzgodnione z ich partnerów.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="f7e8b-106">W tym artykule przedstawiono, jak zaplanować obciążeń B2B toobuild ciągłość prowadzenia działalności biznesowej.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="f7e8b-107">Gotowość odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="f7e8b-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="f7e8b-108">Tryb failover toosecondary region podczas zdarzenia po awarii</span><span class="sxs-lookup"><span data-stu-id="f7e8b-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="f7e8b-109">Rezerwowe tooprimary region po zdarzeniu po awarii</span><span class="sxs-lookup"><span data-stu-id="f7e8b-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="f7e8b-110">Gotowość odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="f7e8b-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="f7e8b-111">Określić region pomocniczy i utworzyć [konta integracji](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) w regionie pomocniczym hello.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="f7e8b-112">Dodaj partnerów, schematów i umów dotyczących przepływów wiadomość hello wymagane gdy hello stan uruchomienia musi toobe replikowane toosecondary region integracji konta.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="f7e8b-113">Upewnij się, że istnieje spójności w konwencji nazewnictwa artefaktu hello integracji konta w regionach.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="f7e8b-114">Witaj toopull stan uruchomienia z hello regionu podstawowego, tworzenie aplikacji logiki w regionie pomocniczym hello.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="f7e8b-115">Ta aplikacja logiki powinny mieć *wyzwalacza* i *akcji*.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="f7e8b-116">Hello wyzwalacza należy łączyć konta integracji regionu tooprimary i hello akcji powinna łączyć toosecondary region integracji konta.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="f7e8b-117">W oparciu o czas hello, wyzwalacz hello sonduje tabeli stanie hello regionu podstawowego, uruchom i pobiera nowe rekordy hello, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="f7e8b-118">Witaj aktualizuje je toosecondary region integracji konta.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="f7e8b-119">Dzięki temu stanu działania przyrostowe tooget z regionu toosecondary regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="f7e8b-120">Ciągłość prowadzenia działalności biznesowej w aplikacjach logiki integracji konto jest zaprojektowana toosupport oparte na protokołach B2B - X12, AS2 i EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="f7e8b-121">kroki szczegółowe toofind, wybierz hello odpowiednich łącza.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="f7e8b-122">Witaj zalecenie jest toodeploy za wszystkie zasoby w regionie podstawowym w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="f7e8b-123">Zasoby regionu podstawowego obejmują bazy danych SQL Azure lub bazy danych rozwiązania Cosmos platformy Azure, Azure Service Bus i usługi Azure Event Hubs, używany do obsługi wiadomości, Azure API Management i hello funkcji usługi Azure Logic Apps w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="f7e8b-124">Nawiąż połączenie z regionu pomocniczego tooa regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="f7e8b-125">Witaj toopull stan uruchomienia z regionu podstawowego, tworzenie aplikacji logiki w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="f7e8b-126">Aplikacja logiki Hello powinien mieć wyzwalacza i akcji.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="f7e8b-127">wyzwalacz Hello powinien łączyć tooa regionu podstawowego integracji konta.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="f7e8b-128">Akcja Hello powinien łączyć tooa region pomocniczy integracji konta.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="f7e8b-129">W oparciu o czas hello, wyzwalacz hello sonduje tabeli stanie hello regionu podstawowego, uruchom i pobiera nowe rekordy hello, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="f7e8b-130">Witaj aktualizuje je tooa region pomocniczy integracji konta.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="f7e8b-131">Ten proces pomaga stanu działania przyrostowe tooget hello region pomocniczy toohello regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="f7e8b-132">Ciągłość prowadzenia działalności biznesowej w ramach konta integracji usługa Logic Apps zapewnia obsługę oparte na AS2, EDIFACT i protokoły B2B hello X12.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="f7e8b-133">Aby uzyskać szczegółowe instrukcje na temat używania X12 i AS2, zobacz [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) i [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="f7e8b-134">Tryb failover region pomocniczy tooa podczas zdarzenia po awarii</span><span class="sxs-lookup"><span data-stu-id="f7e8b-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="f7e8b-135">Podczas zdarzenie po awarii, gdy hello regionu podstawowego nie jest dostępna dla ciągłość prowadzenia działalności biznesowej, region pomocniczy toohello bezpośredniego ruchu.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="f7e8b-136">Pomaga region pomocniczy, toorecover biznesowych działa szybko toomeet powitalne uzgodnione RPO/czasu odzyskania przez ich partnerów.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="f7e8b-137">Zmniejsza on również toofail działań za pośrednictwem z jednego regionu tooanother.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="f7e8b-138">Brak oczekiwanego opóźnienia podczas kopiowania numery kontroli z regionu pomocniczego tooa regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="f7e8b-139">tooavoid wysyłania zduplikowane kontroli wygenerowanego numery toopartners podczas zdarzenia po awarii, hello zaleca numery kontroli hello tooincrement w umowach region pomocniczy hello przy użyciu [poleceń cmdlet programu PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="f7e8b-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="f7e8b-140">Zdarzenia po awarii regionu podstawowego tooa rezerwowe</span><span class="sxs-lookup"><span data-stu-id="f7e8b-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="f7e8b-141">regionu podstawowego wstecz tooa toofall gdy jest ona dostępna, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f7e8b-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="f7e8b-142">Akceptować komunikatów z partnerami w regionie pomocniczym hello.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="f7e8b-143">Zwiększenie liczby kontroli hello wygenerowany dla wszystkich umów regionu podstawowego hello przy użyciu [poleceń cmdlet programu PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="f7e8b-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="f7e8b-144">Bezpośrednie ruch z regionu podstawowego toohello hello regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="f7e8b-145">Sprawdź, czy jest włączone, aplikacja logiki hello utworzona w dodatkowej regionie hello ściąganie stan uruchomienia z hello regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="f7e8b-146">X12</span><span class="sxs-lookup"><span data-stu-id="f7e8b-146">X12</span></span> 

<span data-ttu-id="f7e8b-147">Ciągłość prowadzenia działalności biznesowej dla EDI X 12 dokumenty są oparte na numery kontroli:</span><span class="sxs-lookup"><span data-stu-id="f7e8b-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="f7e8b-148">Można również użyć hello [X12 szybki start szablonu](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="f7e8b-149">Tworzenie konta integracji podstawowe i pomocnicze są wymagania wstępne toouse hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="f7e8b-150">Witaj szablonu pomaga toocreate dwie aplikacje logiki, jeden dla kontroli odebranej liczby i drugi dla numery wygenerowanego kontroli.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="f7e8b-151">Odpowiednich wyzwalacze i akcje są tworzone w aplikacjach logiki hello, łączenie hello wyzwalacza toohello integracji podstawowego konta i hello akcji toohello dodatkowej integracji.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="f7e8b-152">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="f7e8b-152">**Prerequisites**</span></span>

<span data-ttu-id="f7e8b-153">odzyskiwanie po awarii tooenable dla wiadomości przychodzących, wybierz hello zduplikowane Sprawdź ustawienia w ustawieniach odbierania hello X12 umowy.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![Wybierz ustawienia sprawdzania duplikatów](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="f7e8b-155">Utwórz [aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="f7e8b-156">Wyszukaj **X12**i wybierz **X12-modyfikacji numer formantu**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Wyszukaj X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="f7e8b-158">wyzwalacz Hello monituje tooestablish konto połączenia tooan integracji.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="f7e8b-159">wyzwalacz Hello powinny być połączone konta integracji regionu podstawowego tooa.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="f7e8b-160">Wpisz nazwę połączenia, wybierz użytkownika *regionie podstawowym konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![Nazwa konta integracji regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="f7e8b-162">Witaj **DateTime toostart kontroli numer synchronizacji** ustawienie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="f7e8b-163">Witaj **częstotliwość** można ustawić za**dzień**, **godzina**, **minutę**, lub **drugi** interwał.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Daty i godziny i częstotliwość](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="f7e8b-165">Wybierz **nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-165">Select **New step** > **Add an action**.</span></span>

   ![Nowy krok, Dodaj Action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="f7e8b-167">Wyszukaj **X12**i wybierz **X12-dodania lub zaktualizowania numery kontroli**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Dodaj lub zaktualizuj numery kontroli](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="f7e8b-169">Wybierz tooconnect konto akcji tooa region pomocniczy integracji **zmienić połączenie** > **Dodaj nowe połączenie** listę hello integracji dostępnych kont.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="f7e8b-170">Wpisz nazwę połączenia, wybierz użytkownika *regionu pomocniczego konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![Nazwa konta integracji regionu pomocniczego](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="f7e8b-172">Przełącz tooraw wejść, klikając ikonę hello w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Dane wejściowe tooraw przełącznika](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="f7e8b-174">Wybierz treść z selektora zawartości dynamicznej hello, a następnie zapisz hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![Pola zawartości dynamicznej](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="f7e8b-176">W oparciu o czas hello, wyzwalacz hello sonduje hello regionu podstawowego Odebrano kontroli numer tabeli i ściąga hello nowych rekordów.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="f7e8b-177">Witaj aktualizuje rekordów hello hello region pomocniczy integracji konta.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="f7e8b-178">Jeśli nie ma żadnych aktualizacji, stan wyzwalacza hello jest wyświetlany jako **pomijane**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![Kontrola numeru tabeli](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="f7e8b-180">W oparciu o czas hello, stan czasu wykonywania przyrostowych hello są replikowane z regionu pomocniczego tooa regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="f7e8b-181">Podczas zdarzenie po awarii, gdy hello regionu podstawowego nie jest dostępna, bezpośrednie ruchu toohello region pomocniczy dla ciągłość prowadzenia działalności biznesowej.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="f7e8b-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="f7e8b-182">EDIFACT</span></span> 

<span data-ttu-id="f7e8b-183">Ciągłość prowadzenia działalności biznesowej dla dokumentów EDI EDIFACT opiera się na numery kontroli.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="f7e8b-184">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="f7e8b-184">**Prerequisites**</span></span>

<span data-ttu-id="f7e8b-185">odzyskiwanie po awarii tooenable dla wiadomości przychodzących, wybierz hello zduplikowane Sprawdź ustawienia w ustawieniach odbierania umowy EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Wybierz ustawienia sprawdzania duplikatów](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="f7e8b-187">Utwórz [aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="f7e8b-188">Wyszukaj **EDIFACT**i wybierz **EDIFACT - modyfikacji numer formantu**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Wyszukaj EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="f7e8b-190">wyzwalacz Hello monituje tooestablish konto połączenia tooan integracji.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="f7e8b-191">wyzwalacz Hello powinny być połączone konta integracji regionu podstawowego tooa.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="f7e8b-192">Wpisz nazwę połączenia, wybierz użytkownika *regionie podstawowym konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![Nazwa konta integracji regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="f7e8b-194">Witaj **DateTime toostart kontroli numer synchronizacji** ustawienie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="f7e8b-195">Witaj **częstotliwość** można ustawić za**dzień**, **godzina**, **minutę**, lub **drugi** interwał.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![Daty i godziny i częstotliwość](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="f7e8b-197">Wybierz **nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-197">Select **New step** > **Add an action**.</span></span>    

   ![Nowy krok, Dodaj Action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="f7e8b-199">Wyszukaj **EDIFACT**i wybierz **EDIFACT - dodania lub zaktualizowania numery kontroli**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Dodaj lub zaktualizuj numery kontroli](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="f7e8b-201">Wybierz tooconnect konto akcji tooa region pomocniczy integracji **zmienić połączenie** > **Dodaj nowe połączenie** listę hello integracji dostępnych kont.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="f7e8b-202">Wpisz nazwę połączenia, wybierz użytkownika *regionu pomocniczego konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nazwa konta integracji regionu pomocniczego](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="f7e8b-204">Przełącz tooraw wejść, klikając ikonę hello w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Dane wejściowe tooraw przełącznika](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="f7e8b-206">Wybierz treść z selektora zawartości dynamicznej hello, a następnie zapisz hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Pola zawartości dynamicznej](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="f7e8b-208">W oparciu o czas hello, wyzwalacz hello sonduje hello regionu podstawowego Odebrano kontroli numer tabeli i ściąga hello nowych rekordów.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="f7e8b-209">Witaj aktualizuje hello rekordów toohello region pomocniczy integracji konta.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="f7e8b-210">Jeśli nie ma żadnych aktualizacji, stan wyzwalacza hello jest wyświetlany jako **pomijane**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![Kontrola numeru tabeli](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="f7e8b-212">W oparciu o czas hello, stan czasu wykonywania przyrostowych hello są replikowane z regionu pomocniczego tooa regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="f7e8b-213">Podczas zdarzenie po awarii, gdy hello regionu podstawowego nie jest dostępna, bezpośrednie ruchu toohello region pomocniczy dla ciągłość prowadzenia działalności biznesowej.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="f7e8b-214">AS2</span><span class="sxs-lookup"><span data-stu-id="f7e8b-214">AS2</span></span> 

<span data-ttu-id="f7e8b-215">Ciągłość prowadzenia działalności biznesowej dla dokumentów, które używają protokołu AS2 hello jest na podstawie Identyfikatora wiadomości powitania i hello Micznych wartości.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="f7e8b-216">Można również użyć hello [szablonów szybki start AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="f7e8b-217">Tworzenie konta integracji podstawowe i pomocnicze są wymagania wstępne toouse hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="f7e8b-218">Szablon Hello ułatwia tworzenie aplikacji logiki wyzwalacza i akcji.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="f7e8b-219">Aplikacja logiki Hello tworzy połączenie z kontem podstawowym integracji tooa wyzwalacza i konto akcji tooa dodatkowej integracji.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="f7e8b-220">Utwórz [aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) w regionie pomocniczym hello.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="f7e8b-221">Wyszukaj **AS2**i wybierz **AS2 — wartość Micznych po utworzeniu**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Wyszukaj AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="f7e8b-223">Wyzwalacz monituje tooestablish konto połączenia tooan integracji.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="f7e8b-224">wyzwalacz Hello powinny być połączone konta integracji regionu podstawowego tooa.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="f7e8b-225">Wpisz nazwę połączenia, wybierz użytkownika *regionie podstawowym konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nazwa konta integracji regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="f7e8b-227">Witaj **DateTime toostart Micznych wartość synchronizacji** ustawienie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="f7e8b-228">Witaj **częstotliwość** można ustawić za**dzień**, **godzina**, **minutę**, lub **drugi** interwał.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Daty i godziny i częstotliwość](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="f7e8b-230">Wybierz **nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-230">Select **New step** > **Add an action**.</span></span>  

   ![Nowy krok, Dodaj Action](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="f7e8b-232">Wyszukaj **AS2**i wybierz **AS2 - dodania lub zaktualizowania zawartości Micznych**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Dodawanie Mikrofon lub aktualizacji](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="f7e8b-234">Wybierz tooconnect konto akcji tooa dodatkowej integracji **zmienić połączenie** > **Dodaj nowe połączenie** listę hello integracji dostępnych kont.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="f7e8b-235">Wpisz nazwę połączenia, wybierz użytkownika *regionu pomocniczego konta integracji* z hello listy, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nazwa konta integracji regionu pomocniczego](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="f7e8b-237">Przełącz tooraw wejść, klikając ikonę hello w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Dane wejściowe tooraw przełącznika](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="f7e8b-239">Wybierz treść z selektora zawartości dynamicznej hello, a następnie zapisz hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Zawartość dynamiczna](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="f7e8b-241">W oparciu o czas hello, wyzwalacz hello sonduje hello regionu podstawowego tabeli i ściąga hello nowych rekordów.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="f7e8b-242">Witaj aktualizuje je toohello region pomocniczy integracji konta.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="f7e8b-243">Jeśli nie ma żadnych aktualizacji, stan wyzwalacza hello jest wyświetlany jako **pomijane**.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![Tabela regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="f7e8b-245">W oparciu o czas hello, stan czasu wykonywania przyrostowych hello są replikowane z regionu pomocniczego toohello hello regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="f7e8b-246">Podczas zdarzenie po awarii, gdy hello regionu podstawowego nie jest dostępna, bezpośrednie ruchu toohello region pomocniczy dla ciągłość prowadzenia działalności biznesowej.</span><span class="sxs-lookup"><span data-stu-id="f7e8b-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f7e8b-247">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7e8b-247">Next steps</span></span>

[<span data-ttu-id="f7e8b-248">Monitorowanie komunikatów B2B</span><span class="sxs-lookup"><span data-stu-id="f7e8b-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

