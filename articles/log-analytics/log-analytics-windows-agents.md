---
title: "tooAzure komputerów z systemem Windows aaaConnect Log Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule zawiera komputery Windows hello tooconnect kroki hello w Twojej toohello infrastruktury lokalnej usługi analizy dzienników przy użyciu dostosowanej wersji hello Microsoft Monitoring Agent (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="77c1d-103">Połączenie usługi analizy dzienników toohello komputerach systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="77c1d-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="77c1d-104">Tym artykule przedstawiono kroki hello tooconnect komputerów z systemem Windows w lokalnych obszarach roboczych tooOMS infrastruktury przy użyciu dostosowanej wersji hello Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="77c1d-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="77c1d-105">Należy tooinstall i połączyć agentów dla wszystkich komputerów hello, które mają tooonboard w kolejności ich toosend danych toohello analizy dzienników usługi i tooview oraz działanie tych danych.</span><span class="sxs-lookup"><span data-stu-id="77c1d-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="77c1d-106">Każdy agent może raportować toomultiple obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="77c1d-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="77c1d-107">Można zainstalować agentów przy użyciu wiersza polecenia Instalatora lub z żądanego stanu konfiguracji (DSC) w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="77c1d-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="77c1d-108">Dla maszyn wirtualnych działających na platformie Azure, można uprościć instalacji przy użyciu hello [rozszerzenie maszyny wirtualnej](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="77c1d-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="77c1d-109">Na komputerach z połączeniem internetowym hello agent używa hello połączenia toohello Internet toosend danych tooOMS.</span><span class="sxs-lookup"><span data-stu-id="77c1d-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="77c1d-110">Dla komputerów, które nie ma łączności z Internetem, można użyć serwera proxy lub hello [bramy OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="77c1d-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="77c1d-111">Łączenie tooOMS komputerów z systemem Windows jest proste, przy użyciu trzech prostych kroków:</span><span class="sxs-lookup"><span data-stu-id="77c1d-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="77c1d-112">Pobierz plik Instalatora agenta hello z hello portalu OMS</span><span class="sxs-lookup"><span data-stu-id="77c1d-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="77c1d-113">Zainstaluj agenta hello przy użyciu wybranej metody hello</span><span class="sxs-lookup"><span data-stu-id="77c1d-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="77c1d-114">Skonfiguruj agenta hello lub Dodaj dodatkowe obszary robocze, w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="77c1d-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="77c1d-115">Witaj Poniższy diagram przedstawia hello relacji między komputerami z systemem Windows i pakietu OMS po zainstalowaniu i skonfigurować agentów.</span><span class="sxs-lookup"><span data-stu-id="77c1d-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![OMS — direct — agent — diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="77c1d-117">Jeśli zasady zabezpieczeń IT nie zezwalają na toohello tooconnect Twojego sieci Internet komputerów, można skonfigurować Twoje komputery tooconnect toohello OMS bramy.</span><span class="sxs-lookup"><span data-stu-id="77c1d-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="77c1d-118">Aby uzyskać więcej informacji i kroki na tooconfigure Twojego toocommunicate serwerami za pośrednictwem bramy OMS toohello usługę, zobacz temat [połączyć tooOMS komputerów przy użyciu hello bramy OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="77c1d-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="77c1d-119">Wymagania systemowe i wymaganej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="77c1d-119">System requirements and required configuration</span></span>
<span data-ttu-id="77c1d-120">Przed zainstalowaniem lub wdrożyć agentów, przejrzyj następujące szczegóły tooensure wymagań hello hello.</span><span class="sxs-lookup"><span data-stu-id="77c1d-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="77c1d-121">Witaj OMS MMA można zainstalować tylko na komputerach z systemem Windows Server 2008 z dodatkiem SP 1 lub nowszym lub Windows 7 z dodatkiem SP1 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="77c1d-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="77c1d-122">Potrzebujesz subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77c1d-122">You need an Azure subscription.</span></span>  <span data-ttu-id="77c1d-123">Aby uzyskać więcej informacji, zobacz [wprowadzenie do analizy dzienników](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="77c1d-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="77c1d-124">Każdy komputer z systemem Windows musi być w stanie tooconnect toohello Internet przy użyciu protokołu HTTPS lub toohello OMS bramy.</span><span class="sxs-lookup"><span data-stu-id="77c1d-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="77c1d-125">To połączenie może być bezpośrednio, za pośrednictwem serwera proxy lub za pośrednictwem hello OMS bramy.</span><span class="sxs-lookup"><span data-stu-id="77c1d-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="77c1d-126">Witaj OMS MMA można zainstalować na komputerach autonomicznych, serwerów i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="77c1d-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="77c1d-127">Jeśli tooconnect tooOMS maszynami wirtualnymi hostowanymi na platformie Azure, zobacz [tooLog maszyny wirtualne Azure połączyć Analytics](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="77c1d-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="77c1d-128">Hello agent wymaga toouse TCP port 443 dla różnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="77c1d-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="77c1d-129">Sieć</span><span class="sxs-lookup"><span data-stu-id="77c1d-129">Network</span></span>

<span data-ttu-id="77c1d-130">Tooand tooconnect rejestru systemu Windows agentów z usługą OMS hello muszą mieć dostęp do zasobów toonetwork, w tym adresy URL domeny i numery portów hello.</span><span class="sxs-lookup"><span data-stu-id="77c1d-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="77c1d-131">W przypadku serwerów proxy należy tooensure, który hello serwera proxy odpowiednie, zasoby są konfigurowane w ustawieniach agenta.</span><span class="sxs-lookup"><span data-stu-id="77c1d-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="77c1d-132">Dla zapór, które ograniczają dostęp toohello Internet Twojej sieci inżynierów potrzebować tooconfigure Twojego tooOMS dostępu toopermit zapory.</span><span class="sxs-lookup"><span data-stu-id="77c1d-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="77c1d-133">W ustawieniach agenta nie jest wymagana żadna akcja.</span><span class="sxs-lookup"><span data-stu-id="77c1d-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="77c1d-134">Witaj w poniższej tabeli przedstawiono zasoby wymagane do komunikacji.</span><span class="sxs-lookup"><span data-stu-id="77c1d-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="77c1d-135">Niektóre hello następujące zasoby wspomina Operational Insights, który został poprzednia nazwa protokołu analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="77c1d-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="77c1d-136">Zasób agenta</span><span class="sxs-lookup"><span data-stu-id="77c1d-136">Agent Resource</span></span> | <span data-ttu-id="77c1d-137">Porty</span><span class="sxs-lookup"><span data-stu-id="77c1d-137">Ports</span></span> | <span data-ttu-id="77c1d-138">Obejście inspekcji HTTPS</span><span class="sxs-lookup"><span data-stu-id="77c1d-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="77c1d-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="77c1d-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="77c1d-140">443</span><span class="sxs-lookup"><span data-stu-id="77c1d-140">443</span></span> | <span data-ttu-id="77c1d-141">Tak</span><span class="sxs-lookup"><span data-stu-id="77c1d-141">Yes</span></span> |
| <span data-ttu-id="77c1d-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="77c1d-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="77c1d-143">443</span><span class="sxs-lookup"><span data-stu-id="77c1d-143">443</span></span> | <span data-ttu-id="77c1d-144">Tak</span><span class="sxs-lookup"><span data-stu-id="77c1d-144">Yes</span></span> |
| <span data-ttu-id="77c1d-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="77c1d-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="77c1d-146">443</span><span class="sxs-lookup"><span data-stu-id="77c1d-146">443</span></span> | <span data-ttu-id="77c1d-147">Tak</span><span class="sxs-lookup"><span data-stu-id="77c1d-147">Yes</span></span> |
| <span data-ttu-id="77c1d-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="77c1d-148">*.azure-automation.net</span></span> | <span data-ttu-id="77c1d-149">443</span><span class="sxs-lookup"><span data-stu-id="77c1d-149">443</span></span> | <span data-ttu-id="77c1d-150">Tak</span><span class="sxs-lookup"><span data-stu-id="77c1d-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="77c1d-151">Pobierz plik Instalatora agenta hello z usługą OMS</span><span class="sxs-lookup"><span data-stu-id="77c1d-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="77c1d-152">W portalu OMS hello na powitania **omówienie** kliknij przycisk hello **ustawienia** kafelka.</span><span class="sxs-lookup"><span data-stu-id="77c1d-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="77c1d-153">Kliknij przycisk hello **połączonych źródeł** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="77c1d-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="77c1d-154">![Połączone kartę źródła](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="77c1d-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="77c1d-155">Kliknij przycisk **serwerów z systemem Windows** , a następnie kliknij przycisk **Pobierz agenta systemu Windows** procesora komputera dotyczy tooyour typ pliku Instalatora hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="77c1d-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="77c1d-156">Na powitania po prawej **identyfikator obszaru roboczego**, kliknij ikonę kopiowania hello i wklej identyfikator hello do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="77c1d-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="77c1d-157">Na powitania po prawej **klucz podstawowy**, kliknij ikonę kopiowania hello i Wklej klucz hello do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="77c1d-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="77c1d-158">Instalowanie agenta hello za pomocą Instalatora</span><span class="sxs-lookup"><span data-stu-id="77c1d-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="77c1d-159">Należy uruchomić Instalator tooinstall hello agenta na komputerze, które mają toomanage.</span><span class="sxs-lookup"><span data-stu-id="77c1d-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="77c1d-160">Na stronie powitalnej powitania kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="77c1d-161">Na stronie powitania postanowienia licencyjne przeczytaj hello licencji, a następnie kliknij przycisk **zgadzam się**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="77c1d-162">Na stronie powitania, Folder docelowy, zmienić lub zachować hello domyślny folder instalacji, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="77c1d-163">Na stronie Opcje instalacji agenta hello można wybrać tooconnect hello agenta tooAzure analizy dzienników (OMS) programu Operations Manager lub puste opcje hello jeśli agenci mają przechodzić tooconfigure hello później.</span><span class="sxs-lookup"><span data-stu-id="77c1d-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="77c1d-164">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-164">Click **Next**.</span></span>   
    - <span data-ttu-id="77c1d-165">W przypadku wybrania tooAzure tooconnect analizy dzienników (OMS) Wklej hello **identyfikator obszaru roboczego** i **klucz obszaru roboczego (klucz podstawowy)** , który został skopiowany do Notatnika w poprzedniej procedurze hello, a następnie kliknij przycisk  **Następny**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="77c1d-166">![Wklej klucz podstawowy i identyfikator obszaru roboczego](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="77c1d-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="77c1d-167">W przypadku wybrania tooconnect tooOperations Manager wpisz hello **Nazwa grupy zarządzania**, **serwera zarządzania** nazwa, i **Port serwera zarządzania**, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="77c1d-168">Na stronie konto akcji agenta hello wybierz hello lokalne konto systemowe lub konto domeny lokalnych, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="77c1d-169">![Konfiguracja grupy zarządzania](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![konto akcji agenta](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="77c1d-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="77c1d-170">Na stronie gotowe tooInstall hello, przejrzyj wybrane opcje, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="77c1d-171">Na powitania konfiguracji została ukończona pomyślnie kliknij pozycję **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="77c1d-172">Po zakończeniu hello **programu Microsoft Monitoring Agent** pojawia się w **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="77c1d-173">Można sprawdzić konfigurację istnieje i sprawdź, czy hello agent jest połączonych tooOperational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="77c1d-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="77c1d-174">Gdy hello połączonych tooOMS agenta wyświetla komunikat z informacją: **hello Microsoft Monitoring Agent pomyślnie nawiązało połączenie toohello usługi programu Microsoft Operations Management Suite.**</span><span class="sxs-lookup"><span data-stu-id="77c1d-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="77c1d-175">Skonfiguruj ustawienia serwera proxy</span><span class="sxs-lookup"><span data-stu-id="77c1d-175">Configure proxy settings</span></span>

<span data-ttu-id="77c1d-176">Możesz użyć hello następujące ustawienia serwera proxy tooconfigure procedury dla hello za pomocą Panelu sterowania agenta monitorowania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="77c1d-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="77c1d-177">Należy toouse tę procedurę dla każdego serwera.</span><span class="sxs-lookup"><span data-stu-id="77c1d-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="77c1d-178">Jeśli masz wiele serwerów należy tooconfigure, może być łatwiejsze toouse tooautomate skrypt tego procesu.</span><span class="sxs-lookup"><span data-stu-id="77c1d-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="77c1d-179">Jeśli tak, zobacz następną procedurę hello [tooconfigure ustawienia serwera proxy dla hello Microsoft Monitoring Agent za pomocą skryptu](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="77c1d-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="77c1d-180">ustawienia serwera proxy tooconfigure hello za pomocą Panelu sterowania agenta monitorowania firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="77c1d-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="77c1d-181">Otwórz **Panel sterowania**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="77c1d-182">Otwórz program **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="77c1d-183">Kliknij przycisk hello **ustawienia serwera Proxy** kartę.</span><span class="sxs-lookup"><span data-stu-id="77c1d-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="77c1d-184">![karta Ustawienia serwera proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="77c1d-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="77c1d-185">Wybierz **Użyj serwera proxy** i wpisz hello adres URL i numer portu, jeśli jest wymagane, podobne toohello przykładzie.</span><span class="sxs-lookup"><span data-stu-id="77c1d-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="77c1d-186">Jeśli serwer proxy wymaga uwierzytelniania, wpisz hello nazwy użytkownika i hasła tooaccess powitania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="77c1d-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="77c1d-187">Sprawdź tooOMS łączności agenta</span><span class="sxs-lookup"><span data-stu-id="77c1d-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="77c1d-188">Można łatwo sprawdzić, czy agentów komunikują się z OMS przy użyciu hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="77c1d-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="77c1d-189">Na komputerze hello z agentem systemu Windows hello Otwórz Panel sterowania.</span><span class="sxs-lookup"><span data-stu-id="77c1d-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="77c1d-190">Otwórz program Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="77c1d-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="77c1d-191">Kliknij kartę Analiza dzienników Azure (OMS) hello.</span><span class="sxs-lookup"><span data-stu-id="77c1d-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="77c1d-192">W kolumnie Stan hello powinny pojawić się, że hello agent Połączono pomyślnie toohello usługi Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="77c1d-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![Agent połączone](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="77c1d-194">ustawienia serwera proxy tooconfigure hello Microsoft Monitoring Agent za pomocą skryptu</span><span class="sxs-lookup"><span data-stu-id="77c1d-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="77c1d-195">Skopiuj hello następujące przykładowe, zaktualizowania go ze środowiska tooyour określonych informacji, Zapisz plik z rozszerzeniem nazwy pliku PS1, a następnie uruchom skrypt hello na każdym komputerze, który łączy się bezpośrednio toohello usługę.</span><span class="sxs-lookup"><span data-stu-id="77c1d-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="77c1d-196">Instalowanie agenta hello za pomocą wiersza polecenia hello</span><span class="sxs-lookup"><span data-stu-id="77c1d-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="77c1d-197">Modyfikowanie, a następnie użyj następującego agenta hello tooinstall przykład przy użyciu wiersza polecenia hello hello.</span><span class="sxs-lookup"><span data-stu-id="77c1d-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="77c1d-198">przykład Witaj wykonanie pełni dyskretnej instalacji.</span><span class="sxs-lookup"><span data-stu-id="77c1d-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="77c1d-199">Jeśli chcesz tooupgrade agenta należy hello toouse analizy dzienników interfejs API obsługi skryptów.</span><span class="sxs-lookup"><span data-stu-id="77c1d-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="77c1d-200">Zobacz hello następnej sekcji tooupgrade agenta.</span><span class="sxs-lookup"><span data-stu-id="77c1d-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="77c1d-201">Hello agent używa IExpress jako jego samorozpakowujący się plik typu przy użyciu hello `/c` polecenia.</span><span class="sxs-lookup"><span data-stu-id="77c1d-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="77c1d-202">Widać hello przełączniki wiersza polecenia w [przełączniki wiersza polecenia dla IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) , a następnie aktualizację hello toosuit przykład potrzeb.</span><span class="sxs-lookup"><span data-stu-id="77c1d-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="77c1d-203">Opcje MMA</span><span class="sxs-lookup"><span data-stu-id="77c1d-203">MMA-specific options</span></span>                   |<span data-ttu-id="77c1d-204">Uwagi</span><span class="sxs-lookup"><span data-stu-id="77c1d-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="77c1d-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="77c1d-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="77c1d-206">1 = obszar roboczy tooa tooreport Konfiguruj hello agenta</span><span class="sxs-lookup"><span data-stu-id="77c1d-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="77c1d-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="77c1d-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="77c1d-208">Identyfikator obszaru roboczego (guid) dla hello tooadd obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="77c1d-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="77c1d-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="77c1d-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="77c1d-210">Obszar roboczy klucza tooinitially używane uwierzytelniania za pomocą obszaru roboczego hello</span><span class="sxs-lookup"><span data-stu-id="77c1d-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="77c1d-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="77c1d-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="77c1d-212">Określ hello środowiska chmury, gdzie znajduje się obszar roboczy hello</span><span class="sxs-lookup"><span data-stu-id="77c1d-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="77c1d-213">0 = komercyjnych chmury azure (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="77c1d-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="77c1d-214">1 = azure dla instytucji rządowych</span><span class="sxs-lookup"><span data-stu-id="77c1d-214">1 = Azure Government</span></span> |
|<span data-ttu-id="77c1d-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="77c1d-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="77c1d-216">Identyfikator URI dla hello toouse serwera proxy</span><span class="sxs-lookup"><span data-stu-id="77c1d-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="77c1d-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="77c1d-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="77c1d-218">Nazwa użytkownika tooaccess uwierzytelnionego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="77c1d-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="77c1d-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="77c1d-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="77c1d-220">Hasło tooaccess uwierzytelnionego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="77c1d-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="77c1d-221">tooavoid naciśnięcie hello wiersza polecenia limit długości IExpress, zainstaluj hello agenta z obszarem roboczym, nie skonfigurowany, a następnie użyj konfigurację tooset skryptu hello obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="77c1d-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="77c1d-222">Jeśli otrzymasz `Command line option syntax error.` przy użyciu hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parametru, można użyć hello następujące rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="77c1d-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="77c1d-223">Dodaj obszar roboczy za pomocą skryptu</span><span class="sxs-lookup"><span data-stu-id="77c1d-223">Add a workspace using a script</span></span>
<span data-ttu-id="77c1d-224">Dodaj obszar roboczy przy użyciu interfejsu API hello analizy dzienników agenta skryptów z hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="77c1d-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="77c1d-225">tooadd obszaru roboczego platformy Azure dla instytucji rządowych Stanów Zjednoczonych, użyj powitania po przykładowym skrypcie:</span><span class="sxs-lookup"><span data-stu-id="77c1d-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="77c1d-226">Jeśli używano hello wiersza polecenia lub skryptu wcześniej tooinstall lub skonfigurować agenta hello `EnableAzureOperationalInsights` została zastąpiona `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="77c1d-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="77c1d-227">Zainstaluj agenta hello przy użyciu usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="77c1d-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="77c1d-228">Możesz użyć hello następującego skryptu przykład tooinstall hello agenta przy użyciu usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="77c1d-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="77c1d-229">przykład Witaj instaluje hello agent 64-bitowe, zidentyfikowane przez hello `URI` wartość.</span><span class="sxs-lookup"><span data-stu-id="77c1d-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="77c1d-230">Umożliwia także hello 32-bitowej wersji zastępując hello wartość identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="77c1d-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="77c1d-231">Witaj identyfikatorów URI dla obu wersji są:</span><span class="sxs-lookup"><span data-stu-id="77c1d-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="77c1d-232">Agent 64-bitowego systemu Windows — https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="77c1d-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="77c1d-233">Agent 32-bitowego systemu Windows — https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="77c1d-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="77c1d-234">W tym przykładzie procedury i skrypt nie spowoduje uaktualnienie istniejącego agenta.</span><span class="sxs-lookup"><span data-stu-id="77c1d-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="77c1d-235">Importuj xPSDesiredStateConfiguration hello DSC modułu z [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="77c1d-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="77c1d-236">Tworzenie zasobów zmiennej usługi Automatyzacja Azure *OPSINSIGHTS_WS_ID* i *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="77c1d-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="77c1d-237">Ustaw *OPSINSIGHTS_WS_ID* identyfikator obszaru roboczego analizy dzienników OMS tooyour i ustaw *OPSINSIGHTS_WS_KEY* toohello klucza podstawowego obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="77c1d-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="77c1d-238">Użyj hello następujący skrypt i zapisać go jako MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="77c1d-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="77c1d-239">Modyfikuj, a następnie użyj powitania po agenta hello tooinstall przykład przy użyciu usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="77c1d-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="77c1d-240">Zaimportuj MMAgent.ps1 do automatyzacji Azure przy użyciu interfejsu usługi Automatyzacja Azure hello lub polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="77c1d-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="77c1d-241">Przypisywanie konfiguracji toohello węzła.</span><span class="sxs-lookup"><span data-stu-id="77c1d-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="77c1d-242">W ciągu 15 minut węzeł hello sprawdza konfigurację i hello MMA spoczywa toohello węzła.</span><span class="sxs-lookup"><span data-stu-id="77c1d-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="77c1d-243">Pobierz najnowszą wartość ProductId hello</span><span class="sxs-lookup"><span data-stu-id="77c1d-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="77c1d-244">Witaj `ProductId value` w hello MMAgent.ps1 skryptów jest unikatowy tooeach wersja agenta.</span><span class="sxs-lookup"><span data-stu-id="77c1d-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="77c1d-245">Po opublikowaniu zaktualizowaną wersję każdego agenta hello wartość ProductId zmiany.</span><span class="sxs-lookup"><span data-stu-id="77c1d-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="77c1d-246">Tak po zmianie w przyszłych hello hello ProductId można znaleźć wersji agenta hello za pomocą prostego skryptu.</span><span class="sxs-lookup"><span data-stu-id="77c1d-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="77c1d-247">Po umieszczeniu hello najnowszą wersję agenta zainstalowana na serwerze testowym, można użyć hello następującego skryptu tooget hello zainstalowany ProductId wartość.</span><span class="sxs-lookup"><span data-stu-id="77c1d-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="77c1d-248">Za pomocą najnowszej wartości ProductId hello, można zaktualizować wartości hello hello MMAgent.ps1 skryptu.</span><span class="sxs-lookup"><span data-stu-id="77c1d-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="77c1d-249">Ręcznie skonfigurować agenta, lub Dodaj dodatkowe obszary robocze</span><span class="sxs-lookup"><span data-stu-id="77c1d-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="77c1d-250">Jeśli po zainstalowaniu agentów, ale ich nie skonfigurowano lub jeśli użytkownik chce hello agenta tooreport toomultiple w obszary robocze, możesz użyć hello następujące informacje tooenable agenta lub ponownej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="77c1d-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="77c1d-251">Po skonfigurowaniu hello agent, będą rejestrować się z usługą agenta hello i niezbędnych informacji konfiguracyjnych oraz pakietów administracyjnych, które zawierają informacje o rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="77c1d-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="77c1d-252">Po zainstalowaniu programu Microsoft Monitoring Agent hello Otwórz **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="77c1d-253">Otwórz **programu Microsoft Monitoring Agent** , a następnie kliknij przycisk hello **Analiza dzienników Azure (OMS)** kartę.</span><span class="sxs-lookup"><span data-stu-id="77c1d-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="77c1d-254">Kliknij przycisk **Dodaj** tooopen hello **Dodaj obszar roboczy analizy dzienników** pole.</span><span class="sxs-lookup"><span data-stu-id="77c1d-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="77c1d-255">Wklej hello **identyfikator obszaru roboczego** i **klucz obszaru roboczego (klucz podstawowy)** skopiowane do Notatnika w poprzedniej procedurze hello obszaru roboczego, mają tooadd, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="77c1d-256">![Konfigurowanie usługi Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="77c1d-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="77c1d-257">Po zebraniu danych z komputerów monitorowanych przez agenta hello, hello liczbę komputerów monitorowanych przez OMS będą wyświetlane w portalu OMS hello na powitania **połączonych źródeł** karcie **ustawienia** jako  **Serwery połączone**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="77c1d-258">toodisable agenta</span><span class="sxs-lookup"><span data-stu-id="77c1d-258">toodisable an agent</span></span>
1. <span data-ttu-id="77c1d-259">Po zainstalowaniu agenta hello, otwórz **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="77c1d-260">Otwórz program Microsoft Monitoring Agent, a następnie kliknij przycisk hello **Analiza dzienników Azure (OMS)** kartę.</span><span class="sxs-lookup"><span data-stu-id="77c1d-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="77c1d-261">Wybierz obszar roboczy, a następnie kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="77c1d-262">Powtórz ten krok dla wszystkich innych obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="77c1d-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="77c1d-263">Opcjonalnie możesz skonfigurować grupy zarządzania programu Operations Manager tooan tooreport agentów</span><span class="sxs-lookup"><span data-stu-id="77c1d-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="77c1d-264">Jeśli używasz programu Operations Manager w infrastrukturze IT, umożliwia także hello MMA agent jako agent programu Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="77c1d-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="77c1d-265">Grupa zarządzania programu Operations Manager tooan tooreport tooconfigure MMA agentów</span><span class="sxs-lookup"><span data-stu-id="77c1d-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="77c1d-266">Witaj gdzie hello agent jest zainstalowany, Otwórz na komputerze **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="77c1d-267">Otwórz **programu Microsoft Monitoring Agent** , a następnie kliknij przycisk hello **programu Operations Manager** kartę.</span><span class="sxs-lookup"><span data-stu-id="77c1d-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="77c1d-268">![Karta Microsoft Monitoring Agent programu Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="77c1d-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="77c1d-269">Jeśli serwery programu Operations Manager są zintegrowane z usługą Active Directory, kliknij przycisk **automatycznie Aktualizuj przypisania grupy zarządzania z usług AD DS**.</span><span class="sxs-lookup"><span data-stu-id="77c1d-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="77c1d-270">Kliknij przycisk **Dodaj** tooopen hello **Dodaj grupę zarządzania** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="77c1d-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="77c1d-271">![Program Microsoft Monitoring Agent Dodaj grupę zarządzania](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="77c1d-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="77c1d-272">W **Nazwa grupy zarządzania** okno, nazwa typu hello grupy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="77c1d-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="77c1d-273">W hello **podstawowego serwera zarządzania** okno, wpisz nazwę komputera hello z hello podstawowego serwera zarządzania.</span><span class="sxs-lookup"><span data-stu-id="77c1d-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="77c1d-274">W hello **port serwera zarządzania** wpisz numer portu TCP hello typu.</span><span class="sxs-lookup"><span data-stu-id="77c1d-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="77c1d-275">W obszarze **konto akcji agenta**, wybierz hello lokalne konto systemowe lub konto domeny lokalnych.</span><span class="sxs-lookup"><span data-stu-id="77c1d-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="77c1d-276">Kliknij przycisk **OK** tooclose hello **Dodaj grupę zarządzania** okno dialogowe, a następnie kliknij przycisk **OK** tooclose hello **właściwości agenta monitorowania firmy Microsoft**okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="77c1d-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="77c1d-277">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77c1d-277">Next steps</span></span>

- <span data-ttu-id="77c1d-278">[Dodawanie rozwiązania analizy dzienników z galerii rozwiązań hello](log-analytics-add-solutions.md) tooadd funkcjonalność i zbieranie danych.</span><span class="sxs-lookup"><span data-stu-id="77c1d-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
