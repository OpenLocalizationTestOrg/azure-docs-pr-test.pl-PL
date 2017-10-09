---
title: 'Synchronizacja programu Azure AD Connect: zagadnienia i zadania operacyjne | Dokumentacja firmy Microsoft'
description: "W tym temacie opisano zadania operacyjne synchronizacji usługi Azure AD Connect i w jaki sposób tooprepare pracy tego składnika."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="9d426-103">Synchronizacja programu Azure AD Connect: brany pod uwagę i zadania operacyjne</span><span class="sxs-lookup"><span data-stu-id="9d426-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="9d426-104">Celem Hello tego tematu jest toodescribe zadań operacyjnych synchronizacji usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9d426-104">hello objective of this topic is toodescribe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="9d426-105">Tryb przejściowy</span><span class="sxs-lookup"><span data-stu-id="9d426-105">Staging mode</span></span>
<span data-ttu-id="9d426-106">Tryb przejściowy może służyć do kilka scenariuszy, w tym:</span><span class="sxs-lookup"><span data-stu-id="9d426-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="9d426-107">Wysoka dostępność.</span><span class="sxs-lookup"><span data-stu-id="9d426-107">High availability.</span></span>
* <span data-ttu-id="9d426-108">Testowania i wdrażania nowych zmian konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9d426-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="9d426-109">Wprowadzenie nowego serwera i zlikwidować stary hello.</span><span class="sxs-lookup"><span data-stu-id="9d426-109">Introduce a new server and decommission hello old.</span></span>

<span data-ttu-id="9d426-110">Z serwerem w trybie przejściowym można zmieniać toohello zmian konfiguracji i Podgląd hello przed wprowadzeniem powitania serwera active.</span><span class="sxs-lookup"><span data-stu-id="9d426-110">With a server in staging mode, you can make changes toohello configuration and preview hello changes before you make hello server active.</span></span> <span data-ttu-id="9d426-111">Można też toorun pełny import i pełną synchronizację tooverify oczekuje wszystkie zmiany przed wprowadzeniem tych zmian w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="9d426-111">It also allows you toorun full import and full synchronization tooverify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="9d426-112">Podczas instalacji można wybrać powitania serwera toobe w **Tryb przejściowy**.</span><span class="sxs-lookup"><span data-stu-id="9d426-112">During installation, you can select hello server toobe in **staging mode**.</span></span> <span data-ttu-id="9d426-113">Ta akcja powoduje powitania serwera active importowania i synchronizacji, ale nie działa on żadnych eksportów.</span><span class="sxs-lookup"><span data-stu-id="9d426-113">This action makes hello server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="9d426-114">Serwer w trybie przejściowym nie jest uruchomiona, synchronizacja haseł lub zapisywania zwrotnego haseł, nawet jeśli te funkcje są wybrane podczas instalacji.</span><span class="sxs-lookup"><span data-stu-id="9d426-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="9d426-115">Po wyłączeniu trybu przejściowego powitania serwera rozpoczyna eksportowanie umożliwia synchronizację haseł i włącza funkcję zapisywania zwrotnego haseł.</span><span class="sxs-lookup"><span data-stu-id="9d426-115">When you disable staging mode, hello server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="9d426-116">Nadal można wymusić eksportu przy użyciu Menedżera usługi synchronizacji hello.</span><span class="sxs-lookup"><span data-stu-id="9d426-116">You can still force an export by using hello synchronization service manager.</span></span>

<span data-ttu-id="9d426-117">Serwer w trybie przejściowym nadal tooreceive zmiany z usługi Active Directory i Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d426-117">A server in staging mode continues tooreceive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="9d426-118">Zawsze ma kopię hello najnowsze zmiany i podejmij bardzo szybko mogą za pośrednictwem obowiązki hello innego serwera.</span><span class="sxs-lookup"><span data-stu-id="9d426-118">It always has a copy of hello latest changes and can very fast take over hello responsibilities of another server.</span></span> <span data-ttu-id="9d426-119">Jeśli serwer podstawowy tooyour zmian konfiguracji, jest toomake Twojego odpowiedzialność hello tego samego serwera toohello zmiany w trybie przejściowym.</span><span class="sxs-lookup"><span data-stu-id="9d426-119">If you make configuration changes tooyour primary server, it is your responsibility toomake hello same changes toohello server in staging mode.</span></span>

<span data-ttu-id="9d426-120">Dla osób, które znajomości starszych technologii synchronizacji hello Tryb przejściowy różni się od hello serwer ma własną bazę danych SQL.</span><span class="sxs-lookup"><span data-stu-id="9d426-120">For those of you with knowledge of older sync technologies, hello staging mode is different since hello server has its own SQL database.</span></span> <span data-ttu-id="9d426-121">Taka architektura umożliwia hello przemieszczania tryb serwera toobe znajdujących się w różnych centrach danych.</span><span class="sxs-lookup"><span data-stu-id="9d426-121">This architecture allows hello staging mode server toobe located in a different datacenter.</span></span>

### <a name="verify-hello-configuration-of-a-server"></a><span data-ttu-id="9d426-122">Sprawdź konfigurację powitania serwera</span><span class="sxs-lookup"><span data-stu-id="9d426-122">Verify hello configuration of a server</span></span>
<span data-ttu-id="9d426-123">tooapply tej metody, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9d426-123">tooapply this method, follow these steps:</span></span>

1. [<span data-ttu-id="9d426-124">Przygotowanie</span><span class="sxs-lookup"><span data-stu-id="9d426-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="9d426-125">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="9d426-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="9d426-126">Importuje i synchronizuje</span><span class="sxs-lookup"><span data-stu-id="9d426-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="9d426-127">Sprawdź</span><span class="sxs-lookup"><span data-stu-id="9d426-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="9d426-128">Serwer active przełącznika</span><span class="sxs-lookup"><span data-stu-id="9d426-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="9d426-129">Przygotowanie</span><span class="sxs-lookup"><span data-stu-id="9d426-129">Prepare</span></span>
1. <span data-ttu-id="9d426-130">Zainstalować program Azure AD Connect, wybierz **Tryb przejściowy**i usuń zaznaczenie pozycji **rozpoczęcia synchronizacji** na ostatniej stronie powitania w Kreatorze instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="9d426-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on hello last page in hello installation wizard.</span></span> <span data-ttu-id="9d426-131">W tym trybie można aparatu synchronizacji hello toorun ręcznie.</span><span class="sxs-lookup"><span data-stu-id="9d426-131">This mode allows you toorun hello sync engine manually.</span></span>
   <span data-ttu-id="9d426-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="9d426-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="9d426-133">Znak poza/logowania i z hello start menu wybierz opcję **usługi synchronizacji**.</span><span class="sxs-lookup"><span data-stu-id="9d426-133">Sign off/sign in and from hello start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="9d426-134">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="9d426-134">Configuration</span></span>
<span data-ttu-id="9d426-135">Jeśli wprowadzono zmiany niestandardowe toohello podstawowego serwera i chcesz toocompare hello konfiguracji z hello przemieszczania serwera, użyj [Dokumentatora konfiguracji usługi Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="9d426-135">If you have made custom changes toohello primary server and want toocompare hello configuration with hello staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="9d426-136">Importuje i synchronizuje</span><span class="sxs-lookup"><span data-stu-id="9d426-136">Import and Synchronize</span></span>
1. <span data-ttu-id="9d426-137">Wybierz **łączniki**, i wybierz hello pierwszego łącznika z typem hello **usług domenowych w usłudze Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d426-137">Select **Connectors**, and select hello first Connector with hello type **Active Directory Domain Services**.</span></span> <span data-ttu-id="9d426-138">Kliknij przycisk **Uruchom**, wybierz pozycję **pełny import**, i **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d426-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="9d426-139">Wykonaj te kroki dla wszystkich łączników tego typu.</span><span class="sxs-lookup"><span data-stu-id="9d426-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="9d426-140">Wybierz hello łącznika z typem **usługi Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="9d426-140">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="9d426-141">Kliknij przycisk **Uruchom**, wybierz pozycję **pełny import**, i **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d426-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="9d426-142">Upewnij się, że karta hello łączniki nadal jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="9d426-142">Make sure hello tab Connectors is still selected.</span></span> <span data-ttu-id="9d426-143">Dla poszczególnych łączników o typie **usług domenowych w usłudze Active Directory**, kliknij przycisk **Uruchom**, wybierz pozycję **synchronizacja przyrostowa**, i **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d426-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="9d426-144">Wybierz hello łącznika z typem **usługi Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="9d426-144">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="9d426-145">Kliknij przycisk **Uruchom**, wybierz pozycję **synchronizacja przyrostowa**, i **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d426-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="9d426-146">Masz teraz przemieszczanego eksportu zmiany tooAzure AD i lokalnej usłudze AD (Jeśli używasz wdrożenia hybrydowego programu Exchange).</span><span class="sxs-lookup"><span data-stu-id="9d426-146">You have now staged export changes tooAzure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="9d426-147">Następne kroki Hello pozwalają tooinspect nowości dotyczących toochange przed rozpoczęciem faktycznie hello eksportu toohello katalogów.</span><span class="sxs-lookup"><span data-stu-id="9d426-147">hello next steps allow you tooinspect what is about toochange before you actually start hello export toohello directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="9d426-148">Weryfikuj</span><span class="sxs-lookup"><span data-stu-id="9d426-148">Verify</span></span>
1. <span data-ttu-id="9d426-149">Uruchom wiersz polecenia i przejdź zbyt`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="9d426-149">Start a cmd prompt and go too`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="9d426-150">Instalacja: `csexport "Name of Connector" %temp%\export.xml /f:x` nazwę hello hello łącznika można znaleźć w usługi synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="9d426-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` hello name of hello Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="9d426-151">Ma ona nazwę too"contoso.com podobne — AAD" dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d426-151">It has a name similar too"contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="9d426-152">Skopiuj skrypt programu PowerShell hello z sekcji hello [CSAnalyzer](#appendix-csanalyzer) tooa plik o nazwie `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="9d426-152">Copy hello PowerShell script from hello section [CSAnalyzer](#appendix-csanalyzer) tooa file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="9d426-153">Otwórz okno programu PowerShell i Przeglądaj toohello folder, w którym utworzono hello skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d426-153">Open a PowerShell window and browse toohello folder where you created hello PowerShell script.</span></span>
5. <span data-ttu-id="9d426-154">Instalacja: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="9d426-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="9d426-155">Istnieje już plik o nazwie **processedusers1.csv** które można zbadać w programie Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="9d426-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="9d426-156">Wszystkie zmiany przemieszczane tooAzure toobe wyeksportowane AD znajdują się w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="9d426-156">All changes staged toobe exported tooAzure AD are found in this file.</span></span>
7. <span data-ttu-id="9d426-157">Wprowadź niezbędne zmiany danych toohello lub konfiguracji i uruchom następujące kroki ponownie (importowania i synchronizowania i sprawdź, czy) do momentu hello zmiany, które są o toobe wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="9d426-157">Make necessary changes toohello data or configuration and run these steps again (Import and Synchronize and Verify) until hello changes that are about toobe exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="9d426-158">Serwer active przełącznika</span><span class="sxs-lookup"><span data-stu-id="9d426-158">Switch active server</span></span>
1. <span data-ttu-id="9d426-159">Na powitania aktualnie aktywnego serwera wyłącz powitania serwera (DirSync/FIM/usługi Azure AD Sync), więc nie jest eksportowany tooAzure AD lub ustaw go w trybie (Azure AD Connect) przejściowym.</span><span class="sxs-lookup"><span data-stu-id="9d426-159">On hello currently active server, either turn off hello server (DirSync/FIM/Azure AD Sync) so it is not exporting tooAzure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="9d426-160">Uruchom Kreatora instalacji hello na powitania serwera w **Tryb przejściowy** i Wyłącz **Tryb przejściowy**.</span><span class="sxs-lookup"><span data-stu-id="9d426-160">Run hello installation wizard on hello server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="9d426-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="9d426-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="9d426-162">Odzyskiwanie po awarii</span><span class="sxs-lookup"><span data-stu-id="9d426-162">Disaster recovery</span></span>
<span data-ttu-id="9d426-163">Część projektu implementacji hello jest tooplan, dla jakiego toodo w przypadku braku awarii, w którym utratę powitania serwera synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="9d426-163">Part of hello implementation design is tooplan for what toodo in case there is a disaster where you lose hello sync server.</span></span> <span data-ttu-id="9d426-164">Istnieją różne modele toouse i które jeden toouse zależy od wielu czynników, takich jak:</span><span class="sxs-lookup"><span data-stu-id="9d426-164">There are different models toouse and which one toouse depends on several factors including:</span></span>

* <span data-ttu-id="9d426-165">Co to jest ustawiona tolerancja, nie będą mogli upewnij zmian tooobjects w programie Azure AD podczas hello Przestój?</span><span class="sxs-lookup"><span data-stu-id="9d426-165">What is your tolerance for not being able make changes tooobjects in Azure AD during hello downtime?</span></span>
* <span data-ttu-id="9d426-166">Jeśli używasz synchronizacji haseł, czy użytkownicy hello zaakceptować mają toouse hello stare hasło w usłudze Azure AD w przypadku ich zmiany lokalne?</span><span class="sxs-lookup"><span data-stu-id="9d426-166">If you use password synchronization, do hello users accept that they have toouse hello old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="9d426-167">Czy użytkownik ma zależności w czasie rzeczywistym operacje, takie jak zapisywanie zwrotne haseł?</span><span class="sxs-lookup"><span data-stu-id="9d426-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="9d426-168">W zależności od toothese hello odpowiedzi na pytania i zasady organizacji można zaimplementować jedną z następujących strategii hello:</span><span class="sxs-lookup"><span data-stu-id="9d426-168">Depending on hello answers toothese questions and your organization’s policy, one of hello following strategies can be implemented:</span></span>

* <span data-ttu-id="9d426-169">Ponownie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9d426-169">Rebuild when needed.</span></span>
* <span data-ttu-id="9d426-170">Zapasowe serwer zapasowy nie powinien, znany jako **Tryb przejściowy**.</span><span class="sxs-lookup"><span data-stu-id="9d426-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="9d426-171">Użyj maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9d426-171">Use virtual machines.</span></span>

<span data-ttu-id="9d426-172">Jeśli nie używasz hello wbudowanych baza danych SQL Express, a następnie należy także przejrzeć hello [wysokiej dostępności SQL](#sql-high-availability) sekcji.</span><span class="sxs-lookup"><span data-stu-id="9d426-172">If you do not use hello built-in SQL Express database, then you should also review hello [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="9d426-173">Skompiluj ponownie w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="9d426-173">Rebuild when needed</span></span>
<span data-ttu-id="9d426-174">Strategia działało jest tooplan do odbudowywania serwera, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9d426-174">A viable strategy is tooplan for a server rebuild when needed.</span></span> <span data-ttu-id="9d426-175">Zazwyczaj instalowanie hello aparatu synchronizacji i hello początkowej importowania i synchronizacji można wykonać w kilka godzin.</span><span class="sxs-lookup"><span data-stu-id="9d426-175">Usually, installing hello sync engine and do hello initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="9d426-176">Jeśli serwer zapasowe jest niedostępna, jest możliwe tootemporarily Użyj aparatu synchronizacji hello toohost kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="9d426-176">If there isn’t a spare server available, it is possible tootemporarily use a domain controller toohost hello sync engine.</span></span>

<span data-ttu-id="9d426-177">Serwer aparatu synchronizacji Hello nie przechowuje jakikolwiek stan informacje o obiektach hello tak hello bazy danych może zostać ponownie skompilowany od hello danych w usłudze Active Directory i Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d426-177">hello sync engine server does not store any state about hello objects so hello database can be rebuilt from hello data in Active Directory and Azure AD.</span></span> <span data-ttu-id="9d426-178">Witaj **sourceAnchor** atrybutów jest używane toojoin hello obiektów z lokalnymi i hello chmury.</span><span class="sxs-lookup"><span data-stu-id="9d426-178">hello **sourceAnchor** attribute is used toojoin hello objects from on-premises and hello cloud.</span></span> <span data-ttu-id="9d426-179">Po odbudowaniu lokalne powitania serwera z istniejących obiektów i hello chmury, a następnie hello synchronizacji dopasowań aparat tych obiektów jednocześnie ponownie na ponowną instalację.</span><span class="sxs-lookup"><span data-stu-id="9d426-179">If you rebuild hello server with existing objects on-premises and hello cloud, then hello sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="9d426-180">Witaj należy toodocument i Zapisz kwestie hello zmian konfiguracji serwera toohello, takie jak reguły filtrowania i synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="9d426-180">hello things you need toodocument and save are hello configuration changes made toohello server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="9d426-181">Przed rozpoczęciem tej synchronizacji, należy ponownie zastosować te konfiguracje niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="9d426-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="9d426-182">Zapasowe serwer zapasowy nie powinien — Tryb przejściowy</span><span class="sxs-lookup"><span data-stu-id="9d426-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="9d426-183">Jeśli masz środowisku bardziej złożonym, następnie o jeden lub więcej serwerów rezerwy jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="9d426-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="9d426-184">Podczas instalacji, możesz włączyć toobe serwera, w **Tryb przejściowy**.</span><span class="sxs-lookup"><span data-stu-id="9d426-184">During installation, you can enable a server toobe in **staging mode**.</span></span>

<span data-ttu-id="9d426-185">Aby uzyskać więcej informacji, zobacz [Tryb przejściowy](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="9d426-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="9d426-186">Użyj maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="9d426-186">Use virtual machines</span></span>
<span data-ttu-id="9d426-187">Typowe i obsługiwane metody to aparat synchronizacji hello toorun na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d426-187">A common and supported method is toorun hello sync engine in a virtual machine.</span></span> <span data-ttu-id="9d426-188">W przypadku, gdy hello host ma problemu, obraz hello z serwerem aparatu synchronizacji hello może być tooanother migrowanego serwera.</span><span class="sxs-lookup"><span data-stu-id="9d426-188">In case hello host has an issue, hello image with hello sync engine server can be migrated tooanother server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="9d426-189">SQL wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="9d426-189">SQL High Availability</span></span>
<span data-ttu-id="9d426-190">Jeśli nie używasz programu SQL Server Express dostarczonego z programem Azure AD Connect hello, następnie wysoką dostępność dla programu SQL Server należy również rozważyć.</span><span class="sxs-lookup"><span data-stu-id="9d426-190">If you are not using hello SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="9d426-191">rozwiązania wysokiej dostępności Hello obsługiwane obejmują klastrowania SQL i AOA (zawsze włączone grupy dostępności).</span><span class="sxs-lookup"><span data-stu-id="9d426-191">hello high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="9d426-192">Nieobsługiwany rozwiązania obejmują dublowania.</span><span class="sxs-lookup"><span data-stu-id="9d426-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="9d426-193">Dodano obsługę dla SQL AOA tooAzure AD Connect w wersji 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="9d426-193">Support for SQL AOA was added tooAzure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="9d426-194">Przed zainstalowaniem usługi Azure AD Connect, należy włączyć SQL AOA.</span><span class="sxs-lookup"><span data-stu-id="9d426-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="9d426-195">Podczas instalacji Azure AD Connect wykrywa, czy podane wystąpienie programu SQL hello jest włączone dla SQL AOA.</span><span class="sxs-lookup"><span data-stu-id="9d426-195">During installation, Azure AD Connect detects whether hello SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="9d426-196">Po włączeniu SQL AOA Azure dalsze AD Connect danych liczbowych czy SQL AOA jest skonfigurowany toouse synchronicznego lub asynchronicznego replikacji.</span><span class="sxs-lookup"><span data-stu-id="9d426-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured toouse synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="9d426-197">Podczas konfigurowania hello odbiornika grupy dostępności, zaleca się ustawienie hello RegisterAllProvidersIP właściwości too0.</span><span class="sxs-lookup"><span data-stu-id="9d426-197">When setting up hello Availability Group Listener, it is recommended that you set hello RegisterAllProvidersIP property too0.</span></span> <span data-ttu-id="9d426-198">Jest to spowodowane Azure AD Connect aktualnie używa programu SQL Native Client tooconnect tooSQL i SQL Native Client nie obsługuje użycia hello właściwości MultiSubNetFailover.</span><span class="sxs-lookup"><span data-stu-id="9d426-198">This is because Azure AD Connect currently uses SQL Native Client tooconnect tooSQL and SQL Native Client does not support hello use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="9d426-199">Dodatek CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="9d426-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="9d426-200">Zobacz sekcję hello [Sprawdź](#verify) na temat toouse ten skrypt.</span><span class="sxs-lookup"><span data-stu-id="9d426-200">See hello section [verify](#verify) on how toouse this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="9d426-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d426-201">Next steps</span></span>
<span data-ttu-id="9d426-202">**Tematy poglądowe**</span><span class="sxs-lookup"><span data-stu-id="9d426-202">**Overview topics**</span></span>  

* [<span data-ttu-id="9d426-203">Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji</span><span class="sxs-lookup"><span data-stu-id="9d426-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="9d426-204">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d426-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
