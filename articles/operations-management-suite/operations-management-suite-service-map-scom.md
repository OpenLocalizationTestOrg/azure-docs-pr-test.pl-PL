---
title: Mapa integracji programu System Center Operations Manager aaaService | Dokumentacja firmy Microsoft
description: "Mapa usługi jest rozwiązaniem Operations Management Suite, który automatycznie odnajduje składniki aplikacji w systemie Windows i systemów Linux i map hello komunikacji między usługami. W tym artykule omówiono przy użyciu mapy usługi tooautomatically tworzenie diagramów aplikacji rozproszonej w programie Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="d8b9b-104">Mapa usług integracji z programem System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="d8b9b-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="d8b9b-105">Ta funkcja jest dostępna w publicznej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="d8b9b-106">Mapa usług pakiet zarządzania Operations automatycznie wykrywa składniki aplikacji w systemach Windows i Linux i mapuje hello komunikacji między usługami.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="d8b9b-107">Mapy usługi umożliwia tooview swojemu hello serwerów traktować ich jako połączonych systemy, które dostarczają usług krytycznych.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-107">Service Map allows you tooview your servers hello way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="d8b9b-108">Mapa usługi pokazuje połączeń między serwerami, procesów i portów w dowolnej architekturze połączenia TCP, bez konieczności wykonywania konfiguracyjnych wymaganych oprócz hello instalację agenta.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides hello installation of an agent.</span></span> <span data-ttu-id="d8b9b-109">Aby uzyskać więcej informacji, zobacz hello [mapy usługi dokumentacji](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="d8b9b-109">For more information, see hello [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="d8b9b-110">Dzięki tej integracji między mapy usługi i System Center Operations Manager może automatycznie tworzyć diagramy aplikacji rozproszonej w programie Operations Manager, które są oparte na powitania dynamiczne zależności mapy w mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on hello dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8b9b-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d8b9b-111">Prerequisites</span></span>
* <span data-ttu-id="d8b9b-112">Grupy zarządzania programu Operations Manager, który jest zarządzany z zestawu serwerów.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="d8b9b-113">Obszar roboczy usługi Operations Management Suite z hello włączonej funkcji mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-113">An Operations Management Suite workspace with hello Service Map solution enabled.</span></span>
* <span data-ttu-id="d8b9b-114">Zestaw serwerów (co najmniej jeden), które są zarządzane przez programu Operations Manager i wysyłania danych tooService mapy.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-114">A set of servers (at least one) that are being managed by Operations Manager and sending data tooService Map.</span></span> <span data-ttu-id="d8b9b-115">Serwery z systemem Windows i Linux są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="d8b9b-116">Nazwy głównej usługi z toohello dostępu subskrypcji Azure, która jest skojarzona z obszarem roboczym usługi Operations Management Suite hello.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-116">A service principal with access toohello Azure subscription that is associated with hello Operations Management Suite workspace.</span></span> <span data-ttu-id="d8b9b-117">Aby uzyskać więcej informacji, przejdź zbyt[Tworzenie nazwy głównej usługi](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="d8b9b-117">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-hello-service-map-management-pack"></a><span data-ttu-id="d8b9b-118">Zainstaluj pakiet administracyjny hello mapy usług</span><span class="sxs-lookup"><span data-stu-id="d8b9b-118">Install hello Service Map management pack</span></span>
<span data-ttu-id="d8b9b-119">Należy włączyć hello integrację programu Operations Manager a Service Map importując hello Microsoft.SystemCenter.ServiceMap pakietu administracyjnego (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="d8b9b-119">You enable hello integration between Operations Manager and Service Map by importing hello Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="d8b9b-120">Witaj pakietu zawiera hello następujące pakiety administracyjne:</span><span class="sxs-lookup"><span data-stu-id="d8b9b-120">hello bundle contains hello following management packs:</span></span>
* <span data-ttu-id="d8b9b-121">Widoki aplikacji mapy usługi firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="d8b9b-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="d8b9b-122">Wewnętrzny mapy usługi programu Microsoft System Center</span><span class="sxs-lookup"><span data-stu-id="d8b9b-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="d8b9b-123">Zastąpienia mapy usługi programu Microsoft System Center</span><span class="sxs-lookup"><span data-stu-id="d8b9b-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="d8b9b-124">Mapa usług programu Microsoft System Center</span><span class="sxs-lookup"><span data-stu-id="d8b9b-124">Microsoft System Center Service Map</span></span>

## <a name="configure-hello-service-map-integration"></a><span data-ttu-id="d8b9b-125">Konfigurowanie hello mapy usługi integracji</span><span class="sxs-lookup"><span data-stu-id="d8b9b-125">Configure hello Service Map integration</span></span>
<span data-ttu-id="d8b9b-126">Po zainstalowaniu pakietu administracyjnego hello mapy usługi nowy węzeł **mapy usługi**, jest wyświetlana w obszarze **Operations Management Suite** w hello **administracji** okienka.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-126">After you install hello Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in hello **Administration** pane.</span></span> 

<span data-ttu-id="d8b9b-127">tooconfigure mapy usług integracji, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="d8b9b-127">tooconfigure Service Map integration, do hello following:</span></span>

1. <span data-ttu-id="d8b9b-128">tooopen hello Kreatora konfiguracji w hello **omówienie mapy usługi** okienku, kliknij przycisk **Dodawanie obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-128">tooopen hello configuration wizard, in hello **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![W okienku omówienie mapy usług](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="d8b9b-130">W hello **konfiguracji połączenia** okna, wprowadź nazwę dzierżawcy hello lub identyfikator, Identyfikatora aplikacji (znanej także jako nazwa użytkownika hello lub clientID) i hasło hello nazwy głównej usługi, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-130">In hello **Connection Configuration** window, enter hello tenant name or ID, application ID (also known as hello username or clientID), and password of hello service principal, and then click **Next**.</span></span> <span data-ttu-id="d8b9b-131">Aby uzyskać więcej informacji, przejdź zbyt[Tworzenie nazwy głównej usługi](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="d8b9b-131">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

    ![Witaj konfiguracji połączenia okna](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="d8b9b-133">W hello **wyboru subskrypcji** okna, wybierz hello subskrypcji platformy Azure, grupy zasobów platformy Azure (hello, który zawiera obszar roboczy usługi Operations Management Suite hello) i obszar roboczy usługi Operations Management Suite, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-133">In hello **Subscription Selection** window, select hello Azure subscription, Azure resource group (hello one that contains hello Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Witaj obszar roboczy konfiguracji menedżera operacji](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="d8b9b-135">W hello **wybranej grupy maszyny** okna, możesz wybrać grupy maszyny mapy usługi ma toosync tooOperations Manager.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-135">In hello **Machine Group Selection** window, you choose which Service Map Machine Groups you want toosync tooOperations Manager.</span></span> <span data-ttu-id="d8b9b-136">Kliknij przycisk **grupami maszyn Dodaj lub usuń**, wybierz grupy z listy hello **dostępnych grup maszyny**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-136">Click **Add/Remove Machine Groups**, choose groups from hello list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="d8b9b-137">Po wybraniu grup kliknij przycisk **Ok** toofinish.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-137">When you are finished selecting groups, click **Ok** toofinish.</span></span>
    
    ![Witaj grup maszyny konfiguracji programu Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="d8b9b-139">W hello **wybór serwera** okna, konfigurowania hello grupy serwerów mapy usługi z serwerami hello, które mają toosync między programem Operations Manager i mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-139">In hello **Server Selection** window, you configure hello Service Map Servers Group with hello servers that you want toosync between Operations Manager and Service Map.</span></span> <span data-ttu-id="d8b9b-140">Kliknij przycisk **Dodaj lub Usuń serwery**.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="d8b9b-141">Aby toobuild integracji hello diagramu aplikacji rozproszonej dla serwera serwer hello musi mieć:</span><span class="sxs-lookup"><span data-stu-id="d8b9b-141">For hello integration toobuild a distributed application diagram for a server, hello server must be:</span></span>

    * <span data-ttu-id="d8b9b-142">Zarządzane przez program Operations Manager</span><span class="sxs-lookup"><span data-stu-id="d8b9b-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="d8b9b-143">Zarządzane przez usługę mapy</span><span class="sxs-lookup"><span data-stu-id="d8b9b-143">Managed by Service Map</span></span>
    * <span data-ttu-id="d8b9b-144">Na liście hello grupy serwerów mapy usługi</span><span class="sxs-lookup"><span data-stu-id="d8b9b-144">Listed in hello Service Map Servers Group</span></span>

    ![Witaj Grupa konfiguracji programu Operations Manager](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="d8b9b-146">Opcjonalnie: Wybierz powitania serwera zarządzania zasobów puli toocommunicate usłudze Operations Management Suite, a następnie kliknij przycisk **Dodaj obszar roboczy**.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-146">Optional: Select hello Management Server resource pool toocommunicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Witaj puli zasobów konfiguracji menedżera operacji](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="d8b9b-148">Może on potrwać minutę tooconfigure i zarejestruj obszar roboczy usługi Operations Management Suite hello.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-148">It might take a minute tooconfigure and register hello Operations Management Suite workspace.</span></span> <span data-ttu-id="d8b9b-149">Po skonfigurowaniu programu Operations Manager inicjuje hello pierwszej synchronizacji mapy usługi Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-149">After it is configured, Operations Manager initiates hello first Service Map sync from Operations Management Suite.</span></span>

    ![Witaj puli zasobów konfiguracji menedżera operacji](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="d8b9b-151">Monitor mapy usług</span><span class="sxs-lookup"><span data-stu-id="d8b9b-151">Monitor Service Map</span></span>
<span data-ttu-id="d8b9b-152">Po podłączeniu obszar roboczy usługi Operations Management Suite hello nowego folderu, mapy usług jest wyświetlana w hello **monitorowanie** okienku hello konsoli programu Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-152">After hello Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in hello **Monitoring** pane of hello Operations Manager console.</span></span>

![Witaj okienku Monitoring programu Operations Manager](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="d8b9b-154">Witaj mapy usługi znajduje się w nim czterech węzłów:</span><span class="sxs-lookup"><span data-stu-id="d8b9b-154">hello Service Map folder has four nodes:</span></span>
* <span data-ttu-id="d8b9b-155">**Aktywne alerty**: Wyświetla listę wszystkich aktywnych alertów hello o hello komunikacji między programem Operations Manager i mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-155">**Active Alerts**: Lists all hello active alerts about hello communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="d8b9b-156">Należy pamiętać, że te alerty nie są alerty Operations Management Suite jest zsynchronizowany tooOperations menedżera.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-156">Note that these alerts are not Operations Management Suite alerts being synced tooOperations Manager.</span></span> 

* <span data-ttu-id="d8b9b-157">**Serwery**: Wyświetla hello monitorowane serwery, które są skonfigurowane toosync z mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-157">**Servers**: Lists hello monitored servers that are configured toosync from Service Map.</span></span>

    ![Witaj w okienku monitorowanie serwerów programu Operations Manager](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="d8b9b-159">**Maszyny widoków zależności grup**: Wyświetla listę wszystkich grup maszyny, które są synchronizowane z mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="d8b9b-160">Możesz kliknąć tooview wszystkie grupy diagram swojej aplikacji rozproszonej.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-160">You can click any group tooview its distributed application diagram.</span></span>

    ![diagram aplikacji rozproszonej menedżera operacji Hello](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="d8b9b-162">**Widoki zależności serwera**: Wyświetla listę wszystkich serwerów, które są synchronizowane z mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="d8b9b-163">Możesz kliknąć tooview dowolnego serwera diagram swojej aplikacji rozproszonej.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-163">You can click any server tooview its distributed application diagram.</span></span>

    ![diagram aplikacji rozproszonej menedżera operacji Hello](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a><span data-ttu-id="d8b9b-165">Edytowanie lub usuwanie obszaru roboczego hello</span><span class="sxs-lookup"><span data-stu-id="d8b9b-165">Edit or delete hello workspace</span></span>
<span data-ttu-id="d8b9b-166">Możesz edytować lub usunąć obszar roboczy hello skonfigurowane za pomocą hello **omówienie mapy usługi** okienka (**administracji** okienko > **Operations Management Suite**  >  **Usługi mapy**).</span><span class="sxs-lookup"><span data-stu-id="d8b9b-166">You can edit or delete hello configured workspace through hello **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="d8b9b-167">Teraz można skonfigurować tylko jeden obszar roboczy usługi Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![w okienku Menedżera Edytuj obszar roboczy usługi Operations Hello](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="d8b9b-169">Konfigurowanie reguł i zastąpień</span><span class="sxs-lookup"><span data-stu-id="d8b9b-169">Configure rules and overrides</span></span>
<span data-ttu-id="d8b9b-170">Reguła, _Microsoft.SystemCenter.ServiceMapImport.Rule_, jest tworzona tooperiodically pobierania informacji z mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created tooperiodically fetch information from Service Map.</span></span> <span data-ttu-id="d8b9b-171">toochange chronometrażu synchronizacji, można skonfigurować zastąpienia reguły hello (**tworzenie** okienko > **reguły** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="d8b9b-171">toochange sync timings, you can configure overrides of hello rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![Okno właściwości zastępuje programu Operations Manager Hello](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="d8b9b-173">**Włączone**: Włącz lub Wyłącz Aktualizacje automatyczne.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="d8b9b-174">**IntervalMinutes**: zresetować hello między aktualizacjami.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-174">**IntervalMinutes**: Reset hello time between updates.</span></span> <span data-ttu-id="d8b9b-175">Witaj domyślny interwał to jedna godzina.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-175">hello default interval is one hour.</span></span> <span data-ttu-id="d8b9b-176">Chcąc mapy serwera toosync częściej, można zmienić wartości hello.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-176">If you want toosync server maps more frequently, you can change hello value.</span></span>
* <span data-ttu-id="d8b9b-177">**TimeoutSeconds**: hello długość czasu, zanim upłynie limit czasu żądania hello resetowania.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-177">**TimeoutSeconds**: Reset hello length of time before hello request times out.</span></span> 
* <span data-ttu-id="d8b9b-178">**TimeWindowMinutes**: resetowanie przedział czasu hello na potrzeby zapytań o dane.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-178">**TimeWindowMinutes**: Reset hello time window for querying data.</span></span> <span data-ttu-id="d8b9b-179">Domyślna to 60-minutowe okna.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-179">Default is a 60-minute window.</span></span> <span data-ttu-id="d8b9b-180">Hello maksymalna wartość dozwolona przez usługę mapy wynosi 60 min.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-180">hello maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="d8b9b-181">Znane problemy i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="d8b9b-181">Known issues and limitations</span></span>

<span data-ttu-id="d8b9b-182">Hello bieżący projekt przedstawia hello następujące problemy i ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="d8b9b-182">hello current design presents hello following issues and limitations:</span></span>
* <span data-ttu-id="d8b9b-183">Obszar roboczy usługi Operations Management Suite pojedynczego tooa można łączyć.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-183">You can only connect tooa single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="d8b9b-184">Mimo że można dodawać serwery toohello grupy serwerów mapy usługi ręcznie za pośrednictwem hello **tworzenie** okienku hello mapy dla tych serwerów nie zostały zsynchronizowane natychmiast.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-184">Although you can add servers toohello Service Map Servers Group manually through hello **Authoring** pane, hello maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="d8b9b-185">Podczas następnego cyklu synchronizacji hello one będą synchronizowane z mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-185">They will be synced from Service Map during hello next sync cycle.</span></span>
* <span data-ttu-id="d8b9b-186">Jeśli wprowadzisz zmiany toohello rozproszonych aplikacji diagramy utworzone przez pakiet administracyjny hello te zmiany zostaną zastąpione prawdopodobnie na powitania następnej synchronizacji z mapy usługi.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-186">If you make any changes toohello Distributed Application Diagrams created by hello management pack, those changes will likely be overwritten on hello next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="d8b9b-187">Tworzenie nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="d8b9b-187">Create a service principal</span></span>
<span data-ttu-id="d8b9b-188">Oficjalnej dokumentacji platformy Azure o tworzeniu usługę podmiotu zabezpieczeń zobacz:</span><span class="sxs-lookup"><span data-stu-id="d8b9b-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="d8b9b-189">Tworzenie nazwy głównej usługi za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8b9b-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="d8b9b-190">Tworzenie nazwy głównej usługi przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d8b9b-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="d8b9b-191">Tworzenie nazwy głównej usługi przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d8b9b-191">Create a service principal by using hello Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="d8b9b-192">Opinia</span><span class="sxs-lookup"><span data-stu-id="d8b9b-192">Feedback</span></span>
<span data-ttu-id="d8b9b-193">Masz opinię, abyśmy o mapy usługi lub tej dokumentacji?</span><span class="sxs-lookup"><span data-stu-id="d8b9b-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="d8b9b-194">Można znaleźć w naszych [strony User Voice](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), gdzie można sugeruje funkcje lub oddawać głosy na istniejące sugestie.</span><span class="sxs-lookup"><span data-stu-id="d8b9b-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
