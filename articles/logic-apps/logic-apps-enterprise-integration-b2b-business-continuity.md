---
title: "Odzyskiwanie po awarii dla konta integracji B2B — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4896d9da456bcc17b1a4d92259ef3d57f8575d8b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="7ff87-103">Odzyskiwanie po awarii między region B2B aplikacje logiki</span><span class="sxs-lookup"><span data-stu-id="7ff87-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="7ff87-104">Obciążeń B2B obejmują transakcje pieniężne jak zamówienia i faktury.</span><span class="sxs-lookup"><span data-stu-id="7ff87-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="7ff87-105">Podczas zdarzenia po awarii jest krytyczne dla działalności Szybkie odzyskiwanie, aby spełnić SLA biznesowej uzgodnione z ich partnerów.</span><span class="sxs-lookup"><span data-stu-id="7ff87-105">During a disaster event, it's critical for a business to quickly recover to meet the business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="7ff87-106">W tym artykule przedstawiono sposób tworzenia planu ciągłości biznesowej B2B obciążeń.</span><span class="sxs-lookup"><span data-stu-id="7ff87-106">This article demonstrates how to build a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="7ff87-107">Gotowość odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="7ff87-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="7ff87-108">Przełączyć region pomocniczy podczas zdarzenia po awarii</span><span class="sxs-lookup"><span data-stu-id="7ff87-108">Fail over to secondary region during a disaster event</span></span> 
* <span data-ttu-id="7ff87-109">Wrócić do regionu podstawowego po zdarzeniu po awarii</span><span class="sxs-lookup"><span data-stu-id="7ff87-109">Fall back to primary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="7ff87-110">Gotowość odzyskiwania po awarii</span><span class="sxs-lookup"><span data-stu-id="7ff87-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="7ff87-111">Określić region pomocniczy i utworzyć [konta integracji](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in the secondary region.</span></span>

2. <span data-ttu-id="7ff87-112">Dodaj partnerów, schematów i umów dotyczących przepływów wymagane wiadomości, którym stan uruchomienia musi zostać zreplikowane do regionu pomocniczego konta integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-112">Add partners, schemas, and agreements for the required message flows where the run status needs to be replicated to secondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="7ff87-113">Upewnij się, że istnieje spójności w konwencji nazewnictwa artefaktu konta integracji w regionach.</span><span class="sxs-lookup"><span data-stu-id="7ff87-113">Make sure there's consistency in the integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="7ff87-114">Aby stan uruchomienia ściąganie danych z regionu podstawowego, należy utworzyć aplikację logiki w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-114">To pull the run status from the primary region, create a logic app in the secondary region.</span></span> 

   <span data-ttu-id="7ff87-115">Ta aplikacja logiki powinny mieć *wyzwalacza* i *akcji*.</span><span class="sxs-lookup"><span data-stu-id="7ff87-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="7ff87-116">Wyzwalacz ma nawiązać regionie podstawowym konta integracji i akcji należy łączyć do regionu pomocniczego konta integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-116">The trigger should connect to primary region integration account, and the action should connect to secondary region integration account.</span></span> 
   <span data-ttu-id="7ff87-117">Oparte na przedział czasu, wyzwalacz sonduje regionu podstawowego, uruchom tabeli stanu i pobiera nowe rekordy, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="7ff87-117">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span></span> <span data-ttu-id="7ff87-118">Aktualizuje je do regionu pomocniczego konta integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-118">The action updates them to secondary region integration account.</span></span> 
   <span data-ttu-id="7ff87-119">Dzięki temu można uzyskać stanu działania przyrostowe od regionu podstawowego do regionu pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="7ff87-119">This helps to get incremental runtime status from primary region to secondary region.</span></span>

4. <span data-ttu-id="7ff87-120">Ciągłość prowadzenia działalności biznesowej na koncie integracji usługa Logic Apps jest przeznaczona do obsługi oparte na protokołach B2B - X12, AS2 i EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="7ff87-120">Business continuity in Logic Apps integration account is designed to support based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="7ff87-121">Aby uzyskać szczegółowy opis kroków, wybierz odpowiednie łącza.</span><span class="sxs-lookup"><span data-stu-id="7ff87-121">To find detailed steps, select the respective links.</span></span>

5. <span data-ttu-id="7ff87-122">Zaleca się za wdrażanie wszystkie zasoby w regionie podstawowym w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-122">The recommendation is to deploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="7ff87-123">Zasoby regionu podstawowego obejmują bazy danych SQL Azure lub bazy danych rozwiązania Cosmos platformy Azure, Azure Service Bus i usługi Azure Event Hubs, używany do obsługi wiadomości, Azure API Management i funkcji usługi Azure Logic Apps w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="7ff87-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and the Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="7ff87-124">Nawiąż połączenie z regionu podstawowego w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-124">Establish a connection from a primary region to a secondary region.</span></span> <span data-ttu-id="7ff87-125">Aby stan uruchomienia ściąganie danych z regionu podstawowego, należy utworzyć aplikację logiki w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-125">To pull the run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="7ff87-126">Aplikację logiki ma wyzwalacz i akcji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-126">The logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="7ff87-127">Wyzwalacz ma nawiązać konta integracji regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="7ff87-127">The trigger should connect to a primary region integration account.</span></span> 
   <span data-ttu-id="7ff87-128">Akcja powinni połączyć się z regionu pomocniczego konta integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-128">The action should connect to a secondary region integration account.</span></span> 
   <span data-ttu-id="7ff87-129">Oparte na przedział czasu, wyzwalacz sonduje regionu podstawowego, uruchom tabeli stanu i pobiera nowe rekordy, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="7ff87-129">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span></span> 
   <span data-ttu-id="7ff87-130">Aktualizuje je do regionu pomocniczego konta integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-130">The action updates them to a secondary region integration account.</span></span> 
   <span data-ttu-id="7ff87-131">Ten proces pozwala uzyskać stanu działania przyrostowe w regionie podstawowym w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-131">This process helps to get incremental runtime status from the primary region to the secondary region.</span></span>

<span data-ttu-id="7ff87-132">Ciągłość prowadzenia działalności biznesowej w ramach konta integracji usługa Logic Apps zapewnia obsługę oparte na i protokoły B2B X12, AS2, EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="7ff87-132">Business continuity in a Logic Apps integration account provides support based on the B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="7ff87-133">Aby uzyskać szczegółowe instrukcje na temat używania X12 i AS2, zobacz [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) i [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="7ff87-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-to-a-secondary-region-during-a-disaster-event"></a><span data-ttu-id="7ff87-134">Awaryjnie w regionie pomocniczym podczas zdarzenia po awarii</span><span class="sxs-lookup"><span data-stu-id="7ff87-134">Fail over to a secondary region during a disaster event</span></span>

<span data-ttu-id="7ff87-135">Podczas zdarzenie po awarii, gdy regionu podstawowego nie jest dostępna dla ciągłość prowadzenia działalności biznesowej, bezpośrednie ruchu w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-135">During a disaster event, when the primary region is not available for business continuity, direct traffic to the secondary region.</span></span> <span data-ttu-id="7ff87-136">Pomaga regionu pomocniczego, a biznesowych do odzyskania funkcji szybko, aby spełnić RPO/RTO uzgodnione przez ich partnerów.</span><span class="sxs-lookup"><span data-stu-id="7ff87-136">A secondary region helps a business to recover functions quickly to meet the RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="7ff87-137">Zmniejsza on również starań, aby przełączyć się z jednego regionu w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="7ff87-137">It also minimizes efforts to fail over from one region to another region.</span></span> 

<span data-ttu-id="7ff87-138">Brak oczekiwanego opóźnienia podczas kopiowania numery kontroli z regionu podstawowego w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-138">There is an expected latency while copying control numbers from a primary region to a secondary region.</span></span> <span data-ttu-id="7ff87-139">Aby uniknąć wysyłania numery zduplikowane kontroli wygenerowanego partnerom podczas zdarzenia po awarii, zaleca się zwiększenie liczby kontroli w regionie pomocniczym umowy przy użyciu [poleceń cmdlet programu PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="7ff87-139">To avoid sending duplicate generated control numbers to partners during a disaster event, the recommendation is to increment the control numbers in the secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-to-a-primary-region-post-disaster-event"></a><span data-ttu-id="7ff87-140">Wrócić do regionu podstawowego zdarzenia po awarii</span><span class="sxs-lookup"><span data-stu-id="7ff87-140">Fall back to a primary region post-disaster event</span></span>

<span data-ttu-id="7ff87-141">Aby wrócić do regionu podstawowego, gdy jest ona dostępna, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7ff87-141">To fall back to a primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="7ff87-142">Akceptować komunikatów z partnerami w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-142">Stop accepting messages from partners in the secondary region.</span></span>  

2. <span data-ttu-id="7ff87-143">Zwiększenie liczby wygenerowanego sterowania dla wszystkich umów regionu podstawowego przy użyciu [poleceń cmdlet programu PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="7ff87-143">Increment the generated control numbers for all the primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="7ff87-144">Bezpośrednie ruch z regionu pomocniczego do regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="7ff87-144">Direct traffic from the secondary region to the primary region.</span></span>

4. <span data-ttu-id="7ff87-145">Sprawdź, czy włączono aplikacji logiki utworzona w regionie pomocniczym dla ściąganie stan uruchomienia z regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="7ff87-145">Check that the logic app created in the secondary region for pulling run status from the primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="7ff87-146">X12</span><span class="sxs-lookup"><span data-stu-id="7ff87-146">X12</span></span> 

<span data-ttu-id="7ff87-147">Ciągłość prowadzenia działalności biznesowej dla EDI X 12 dokumenty są oparte na numery kontroli:</span><span class="sxs-lookup"><span data-stu-id="7ff87-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="7ff87-148">Można również użyć [X12 szybki start szablonu](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) do tworzenia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="7ff87-148">You can also use the [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) to create logic apps.</span></span> <span data-ttu-id="7ff87-149">Tworzenie konta integracji podstawowe i pomocnicze są wymagania wstępne, aby użyć szablonu.</span><span class="sxs-lookup"><span data-stu-id="7ff87-149">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span> <span data-ttu-id="7ff87-150">Szablon ułatwia tworzenie aplikacji logiki dwóch dla kontroli odebranej liczby i osobne numery wygenerowanego kontroli.</span><span class="sxs-lookup"><span data-stu-id="7ff87-150">The template helps to create two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="7ff87-151">Odpowiednich wyzwalacze i akcje są tworzone w aplikacjach logiki, wyzwalacz łączenia się z podstawowej integracji konta i akcji na koncie dodatkowej integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-151">Respective triggers and actions are created in the logic apps, connecting the trigger to the primary integration account and the action to the secondary integration account.</span></span>

<span data-ttu-id="7ff87-152">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="7ff87-152">**Prerequisites**</span></span>

<span data-ttu-id="7ff87-153">Aby włączyć odzyskiwanie po awarii dla wiadomości przychodzących, wybierz ustawienia sprawdzania duplikatów w X12 ustawienia odbierania umowy.</span><span class="sxs-lookup"><span data-stu-id="7ff87-153">To enable disaster recovery for inbound messages, select the duplicate check settings in the X12 agreement's Receive Settings.</span></span>

![Wybierz ustawienia sprawdzania duplikatów](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="7ff87-155">Utwórz [aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="7ff87-156">Wyszukaj **X12**i wybierz **X12-modyfikacji numer formantu**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Wyszukaj X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="7ff87-158">Wyzwalacz monituje o nawiązać połączenie z kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-158">The trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="7ff87-159">Wyzwalacz powinny być połączone z kontem integracji regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="7ff87-159">The trigger should be connected to a primary region integration account.</span></span>

3. <span data-ttu-id="7ff87-160">Wpisz nazwę połączenia, wybierz użytkownika *regionie podstawowym konta integracji* na liście i wybierz polecenie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-160">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>   

   ![Nazwa konta integracji regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="7ff87-162">**DateTime można uruchomić synchronizacji numer kontroli** ustawienie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="7ff87-162">The **DateTime to start control number sync** setting is optional.</span></span> <span data-ttu-id="7ff87-163">**Częstotliwość** może być ustawiony na **dzień**, **godzina**, **minutę**, lub **drugi** interwał.</span><span class="sxs-lookup"><span data-stu-id="7ff87-163">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Daty i godziny i częstotliwość](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="7ff87-165">Wybierz **nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-165">Select **New step** > **Add an action**.</span></span>

   ![Nowy krok, Dodaj Action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="7ff87-167">Wyszukaj **X12**i wybierz **X12-dodania lub zaktualizowania numery kontroli**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Dodaj lub zaktualizuj numery kontroli](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="7ff87-169">Aby połączyć się z regionu pomocniczego konta integracji z akcji, wybierz **zmienić połączenie** > **Dodaj nowe połączenie** listę kont dostępnych integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-169">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="7ff87-170">Wpisz nazwę połączenia, wybierz użytkownika *regionu pomocniczego konta integracji* na liście i wybierz polecenie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-170">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span> 

   ![Nazwa konta integracji regionu pomocniczego](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="7ff87-172">Przejdź do nieprzetworzone dane wejściowe, klikając ikonę w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="7ff87-172">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Przełącz się do nieprzetworzone dane wejściowe](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="7ff87-174">Wybierz treść z selektor zawartości dynamicznej, a następnie zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="7ff87-174">Select Body from the dynamic content picker, and save the logic app.</span></span>

   ![Pola zawartości dynamicznej](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="7ff87-176">Oparte na przedział czasu, wyzwalacz sonduje tabeli numerów kontroli regionu podstawowego odebranych i pobiera nowe rekordy.</span><span class="sxs-lookup"><span data-stu-id="7ff87-176">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span></span> 
   <span data-ttu-id="7ff87-177">Aktualizuje rekordy w regionie pomocniczym konta integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-177">The action updates the records in the secondary region integration account.</span></span> 
   <span data-ttu-id="7ff87-178">Jeśli nie ma żadnych aktualizacji, stan wyzwalacza jest wyświetlany jako **pomijane**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-178">If there are no updates, the trigger status appears as **Skipped**.</span></span>   

   ![Kontrola numeru tabeli](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="7ff87-180">Oparte na przedział czasu, stanu działania przyrostowe replikuje z regionu podstawowego w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-180">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span></span> <span data-ttu-id="7ff87-181">Podczas zdarzenie po awarii, gdy regionu podstawowego nie jest dostępna, bezpośrednie ruch do regionu pomocniczego dla ciągłość prowadzenia działalności biznesowej.</span><span class="sxs-lookup"><span data-stu-id="7ff87-181">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="7ff87-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="7ff87-182">EDIFACT</span></span> 

<span data-ttu-id="7ff87-183">Ciągłość prowadzenia działalności biznesowej dla dokumentów EDI EDIFACT opiera się na numery kontroli.</span><span class="sxs-lookup"><span data-stu-id="7ff87-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="7ff87-184">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="7ff87-184">**Prerequisites**</span></span>

<span data-ttu-id="7ff87-185">Aby włączyć odzyskiwanie po awarii dla wiadomości przychodzących, wybierz ustawienia sprawdzania duplikatów w umowie EDIFACT odbierania ustawień.</span><span class="sxs-lookup"><span data-stu-id="7ff87-185">To enable disaster recovery for inbound messages, select the duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Wybierz ustawienia sprawdzania duplikatów](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="7ff87-187">Utwórz [aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="7ff87-188">Wyszukaj **EDIFACT**i wybierz **EDIFACT - modyfikacji numer formantu**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Wyszukaj EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="7ff87-190">Wyzwalacz monituje o nawiązać połączenie z kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-190">The trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="7ff87-191">Wyzwalacz powinny być połączone z kontem integracji regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="7ff87-191">The trigger should be connected to a primary region integration account.</span></span> 

3. <span data-ttu-id="7ff87-192">Wpisz nazwę połączenia, wybierz użytkownika *regionie podstawowym konta integracji* na liście i wybierz polecenie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-192">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>    

   ![Nazwa konta integracji regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="7ff87-194">**DateTime można uruchomić synchronizacji numer kontroli** ustawienie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="7ff87-194">The **DateTime to start control number sync** setting is optional.</span></span> <span data-ttu-id="7ff87-195">**Częstotliwość** może być ustawiony na **dzień**, **godzina**, **minutę**, lub **drugi** interwał.</span><span class="sxs-lookup"><span data-stu-id="7ff87-195">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![Daty i godziny i częstotliwość](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="7ff87-197">Wybierz **nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-197">Select **New step** > **Add an action**.</span></span>    

   ![Nowy krok, Dodaj Action](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="7ff87-199">Wyszukaj **EDIFACT**i wybierz **EDIFACT - dodania lub zaktualizowania numery kontroli**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Dodaj lub zaktualizuj numery kontroli](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="7ff87-201">Aby połączyć się z regionu pomocniczego konta integracji z akcji, wybierz **zmienić połączenie** > **Dodaj nowe połączenie** listę kont dostępnych integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-201">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="7ff87-202">Wpisz nazwę połączenia, wybierz użytkownika *regionu pomocniczego konta integracji* na liście i wybierz polecenie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-202">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span>

   ![Nazwa konta integracji regionu pomocniczego](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="7ff87-204">Przejdź do nieprzetworzone dane wejściowe, klikając ikonę w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="7ff87-204">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Przełącz się do nieprzetworzone dane wejściowe](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="7ff87-206">Wybierz treść z selektor zawartości dynamicznej, a następnie zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="7ff87-206">Select Body from the dynamic content picker, and save the logic app.</span></span>   

   ![Pola zawartości dynamicznej](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="7ff87-208">Oparte na przedział czasu, wyzwalacz sonduje tabeli numerów kontroli regionu podstawowego odebranych i pobiera nowe rekordy.</span><span class="sxs-lookup"><span data-stu-id="7ff87-208">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span></span>
   <span data-ttu-id="7ff87-209">Aktualizuje rekordy do regionu pomocniczego konta integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-209">The action updates the records to the secondary region integration account.</span></span> 
   <span data-ttu-id="7ff87-210">Jeśli nie ma żadnych aktualizacji, stan wyzwalacza jest wyświetlany jako **pomijane**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-210">If there are no updates, the trigger status appears as **Skipped**.</span></span>

   ![Kontrola numeru tabeli](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="7ff87-212">Oparte na przedział czasu, stanu działania przyrostowe replikuje z regionu podstawowego w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-212">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span></span> <span data-ttu-id="7ff87-213">Podczas zdarzenie po awarii, gdy regionu podstawowego nie jest dostępna, bezpośrednie ruch do regionu pomocniczego dla ciągłość prowadzenia działalności biznesowej.</span><span class="sxs-lookup"><span data-stu-id="7ff87-213">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="7ff87-214">AS2</span><span class="sxs-lookup"><span data-stu-id="7ff87-214">AS2</span></span> 

<span data-ttu-id="7ff87-215">Ciągłość prowadzenia działalności biznesowej dla dokumentów, które używają protokołu AS2 opiera się na identyfikator komunikatu i wartość Mikrofon.</span><span class="sxs-lookup"><span data-stu-id="7ff87-215">Business continuity for documents that use the AS2 protocol is based on the message ID and the MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="7ff87-216">Można również użyć [szablonów szybki start AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) do tworzenia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="7ff87-216">You can also use the [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) to create logic apps.</span></span> <span data-ttu-id="7ff87-217">Tworzenie konta integracji podstawowe i pomocnicze są wymagania wstępne, aby użyć szablonu.</span><span class="sxs-lookup"><span data-stu-id="7ff87-217">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span> <span data-ttu-id="7ff87-218">Szablon ułatwia tworzenie aplikacji logiki wyzwalacza i akcji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-218">The template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="7ff87-219">Aplikację logiki tworzy połączenie z wyzwalacza konta podstawowej integracji i akcji na koncie dodatkowej integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-219">The logic app creates a connection from a trigger to a primary integration account and an action to a secondary integration account.</span></span>

1. <span data-ttu-id="7ff87-220">Utwórz [aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region.</span></span>  

2. <span data-ttu-id="7ff87-221">Wyszukaj **AS2**i wybierz **AS2 — wartość Micznych po utworzeniu**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Wyszukaj AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="7ff87-223">Wyzwalacz monituje o nawiązać połączenie z kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-223">A trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="7ff87-224">Wyzwalacz powinny być połączone z kontem integracji regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="7ff87-224">The trigger should be connected to a primary region integration account.</span></span> 
   
3. <span data-ttu-id="7ff87-225">Wpisz nazwę połączenia, wybierz użytkownika *regionie podstawowym konta integracji* na liście i wybierz polecenie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-225">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>

   ![Nazwa konta integracji regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="7ff87-227">**DateTime można uruchomić synchronizacji wartość Micznych** ustawienie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="7ff87-227">The **DateTime to start MIC value sync** setting is optional.</span></span> <span data-ttu-id="7ff87-228">**Częstotliwość** może być ustawiony na **dzień**, **godzina**, **minutę**, lub **drugi** interwał.</span><span class="sxs-lookup"><span data-stu-id="7ff87-228">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Daty i godziny i częstotliwość](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="7ff87-230">Wybierz **nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-230">Select **New step** > **Add an action**.</span></span>  

   ![Nowy krok, Dodaj Action](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="7ff87-232">Wyszukaj **AS2**i wybierz **AS2 - dodania lub zaktualizowania zawartości Micznych**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Dodawanie Mikrofon lub aktualizacji](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="7ff87-234">Połącz się kontem dodatkowej integracji z akcji, wybierz **zmienić połączenie** > **Dodaj nowe połączenie** listę kont dostępnych integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-234">To connect an action to a secondary integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="7ff87-235">Wpisz nazwę połączenia, wybierz użytkownika *regionu pomocniczego konta integracji* na liście i wybierz polecenie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-235">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span>

   ![Nazwa konta integracji regionu pomocniczego](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="7ff87-237">Przejdź do nieprzetworzone dane wejściowe, klikając ikonę w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="7ff87-237">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Przełącz się do nieprzetworzone dane wejściowe](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="7ff87-239">Wybierz treść z selektor zawartości dynamicznej, a następnie zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="7ff87-239">Select Body from the dynamic content picker, and save the logic app.</span></span>   

   ![Zawartość dynamiczna](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="7ff87-241">Oparte na przedział czasu, wyzwalacz sonduje tabeli regionu podstawowego i pobiera nowe rekordy.</span><span class="sxs-lookup"><span data-stu-id="7ff87-241">Based on the time interval, the trigger polls the primary region table and pulls the new records.</span></span> <span data-ttu-id="7ff87-242">Aktualizuje je do regionu pomocniczego konta integracji.</span><span class="sxs-lookup"><span data-stu-id="7ff87-242">The action updates them to the secondary region integration account.</span></span> 
   <span data-ttu-id="7ff87-243">Jeśli nie ma żadnych aktualizacji, stan wyzwalacza jest wyświetlany jako **pomijane**.</span><span class="sxs-lookup"><span data-stu-id="7ff87-243">If there are no updates, the trigger status appears as **Skipped**.</span></span>  

   ![Tabela regionu podstawowego](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="7ff87-245">Oparte na przedział czasu, stanu działania przyrostowe replikuje z regionu podstawowego w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="7ff87-245">Based on the time interval, the incremental runtime status replicates from the primary region to the secondary region.</span></span> <span data-ttu-id="7ff87-246">Podczas zdarzenie po awarii, gdy regionu podstawowego nie jest dostępna, bezpośrednie ruch do regionu pomocniczego dla ciągłość prowadzenia działalności biznesowej.</span><span class="sxs-lookup"><span data-stu-id="7ff87-246">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7ff87-247">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ff87-247">Next steps</span></span>

[<span data-ttu-id="7ff87-248">Monitorowanie komunikatów B2B</span><span class="sxs-lookup"><span data-stu-id="7ff87-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

