---
title: "Łączenia komputerów z systemem Windows Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono kroki dotyczące łączenia komputerów z systemem Windows w infrastrukturze lokalnej usługi analizy dzienników przy użyciu dostosowanej wersji programu Microsoft Monitoring Agent (MMA)."
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
ms.openlocfilehash: 48a0eaeb10d406d551c9e5870edde06809bd7544
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-computers-to-the-log-analytics-service-in-azure"></a><span data-ttu-id="62a93-103">Łączenie komputerów z systemem Windows z usługą analizy dzienników na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="62a93-103">Connect Windows computers to the Log Analytics service in Azure</span></span>

<span data-ttu-id="62a93-104">W tym artykule przedstawiono kroki dotyczące łączenia komputerów z systemem Windows w infrastrukturze lokalnej OMS obszarów roboczych przy użyciu dostosowanej wersji programu Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="62a93-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="62a93-105">Należy zainstalować i nawiąż połączenie agentów dla wszystkich komputerów, które chcesz dołączyć, aby je do wysyłania danych z usługą analizy dzienników oraz do wyświetlania i korzystania z tych danych.</span><span class="sxs-lookup"><span data-stu-id="62a93-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span></span> <span data-ttu-id="62a93-106">Każdy agent może raportować do wielu obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="62a93-106">Each agent can report to multiple workspaces.</span></span>

<span data-ttu-id="62a93-107">Można zainstalować agentów przy użyciu wiersza polecenia Instalatora lub z żądanego stanu konfiguracji (DSC) w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="62a93-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="62a93-108">Dla maszyn wirtualnych działających na platformie Azure, można uprościć instalacji przy użyciu [rozszerzenie maszyny wirtualnej](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="62a93-108">For virtual machines running in Azure, you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="62a93-109">Na komputerach z połączeniem internetowym agent używa połączenia z Internetem do wysyłania danych z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="62a93-109">On computers with Internet connectivity, the agent uses the connection to the Internet to send data to OMS.</span></span> <span data-ttu-id="62a93-110">W przypadku komputerów, które nie ma łączności z Internetem, można użyć serwera proxy lub [bramy OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="62a93-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="62a93-111">Łączenie komputerów z systemem Windows z usługą OMS jest proste, przy użyciu trzech prostych kroków:</span><span class="sxs-lookup"><span data-stu-id="62a93-111">Connecting your Windows computers to OMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="62a93-112">Pobierz plik Instalatora agenta z portalu OMS</span><span class="sxs-lookup"><span data-stu-id="62a93-112">Download the agent setup file from the OMS portal</span></span>
2. <span data-ttu-id="62a93-113">Zainstaluj agenta przy użyciu wybranej metody</span><span class="sxs-lookup"><span data-stu-id="62a93-113">Install the agent using the method you choose</span></span>
3. <span data-ttu-id="62a93-114">Skonfiguruj agenta lub Dodaj dodatkowe obszary robocze, w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="62a93-114">Configure the agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="62a93-115">Na poniższym diagramie przedstawiono relację między komputerami z systemem Windows i pakietu OMS po zainstalowaniu i skonfigurować agentów.</span><span class="sxs-lookup"><span data-stu-id="62a93-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![OMS — direct — agent — diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="62a93-117">Jeśli zasady zabezpieczeń IT nie zezwalają na komputerach w sieci, aby nawiązać połączenie z Internetem, można skonfigurować komputery do łączenia się z bramą OMS.</span><span class="sxs-lookup"><span data-stu-id="62a93-117">If your IT security policies do not allow computers on your network to connect to the Internet, you can configure your computers to connect to the OMS Gateway.</span></span> <span data-ttu-id="62a93-118">Aby uzyskać więcej informacji i kroki dotyczące sposobu konfigurowania serwerów do komunikacji za pośrednictwem bramy OMS z usługą OMS, zobacz [łączenia komputerów przy użyciu bramy OMS OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="62a93-118">For more information and steps on how to configure your servers to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="62a93-119">Wymagania systemowe i wymaganej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="62a93-119">System requirements and required configuration</span></span>
<span data-ttu-id="62a93-120">Przed zainstalowaniem lub wdrożyć agentów, przejrzyj następujące informacje, aby upewnić się, że spełniają wymagania.</span><span class="sxs-lookup"><span data-stu-id="62a93-120">Before you install or deploy agents, review the following details to ensure you meet the requirements.</span></span>

- <span data-ttu-id="62a93-121">OMS MMA można zainstalować tylko na komputerach z systemem Windows Server 2008 SP 1 lub nowszym lub Windows 7 z dodatkiem SP1 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="62a93-121">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="62a93-122">Potrzebujesz subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62a93-122">You need an Azure subscription.</span></span>  <span data-ttu-id="62a93-123">Aby uzyskać więcej informacji, zobacz [wprowadzenie do analizy dzienników](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="62a93-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="62a93-124">Każdy komputer z systemem Windows musi mieć możliwość połączenia z Internetem przy użyciu protokołu HTTPS lub bramy OMS.</span><span class="sxs-lookup"><span data-stu-id="62a93-124">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span></span> <span data-ttu-id="62a93-125">To połączenie może być bezpośrednio, za pośrednictwem serwera proxy lub za pośrednictwem bramy OMS.</span><span class="sxs-lookup"><span data-stu-id="62a93-125">This connection can be direct, via a proxy, or through the OMS Gateway.</span></span>
- <span data-ttu-id="62a93-126">OMS MMA można zainstalować na komputerach autonomicznych, serwerów i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="62a93-126">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="62a93-127">Jeśli chcesz połączyć się OMS z maszynami wirtualnymi hostowanymi na platformie Azure, zobacz [łączenie maszyn wirtualnych platformy Azure do analizy dzienników](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="62a93-127">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="62a93-128">Agent musi wybrać TCP port 443 dla różnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="62a93-128">The agent needs to use TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="62a93-129">Sieć</span><span class="sxs-lookup"><span data-stu-id="62a93-129">Network</span></span>

<span data-ttu-id="62a93-130">Dla agentów systemu Windows połączyć się i zarejestruj usługę muszą mieć dostęp do zasobów sieciowych, w tym adresy URL domeny i numery portów.</span><span class="sxs-lookup"><span data-stu-id="62a93-130">For Windows agents to connect to and register with the OMS service, they must have access to network resources, including the port numbers and domain URLs.</span></span>

- <span data-ttu-id="62a93-131">W przypadku serwerów proxy konieczne jest zapewnienie, że ich odpowiednie zasoby są skonfigurowane w ustawieniach agenta.</span><span class="sxs-lookup"><span data-stu-id="62a93-131">For proxy servers, you need to ensure that the appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="62a93-132">Dla zapór, które ograniczają dostęp do Internetu należy lub Twojej sieci engineers, należy skonfigurować zaporę tak, aby zezwolić na dostęp do pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="62a93-132">For firewalls that restrict access to the Internet, you or your networking engineers need to configure your firewall to permit access to OMS.</span></span> <span data-ttu-id="62a93-133">W ustawieniach agenta nie jest wymagana żadna akcja.</span><span class="sxs-lookup"><span data-stu-id="62a93-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="62a93-134">W poniższej tabeli przedstawiono zasoby wymagane do komunikacji.</span><span class="sxs-lookup"><span data-stu-id="62a93-134">The following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="62a93-135">Niektóre z następujących zasobów wspomina Operational Insights, który został poprzednia nazwa protokołu analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="62a93-135">Some of the following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="62a93-136">Zasób agenta</span><span class="sxs-lookup"><span data-stu-id="62a93-136">Agent Resource</span></span> | <span data-ttu-id="62a93-137">Porty</span><span class="sxs-lookup"><span data-stu-id="62a93-137">Ports</span></span> | <span data-ttu-id="62a93-138">Obejście inspekcji HTTPS</span><span class="sxs-lookup"><span data-stu-id="62a93-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="62a93-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="62a93-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="62a93-140">443</span><span class="sxs-lookup"><span data-stu-id="62a93-140">443</span></span> | <span data-ttu-id="62a93-141">Tak</span><span class="sxs-lookup"><span data-stu-id="62a93-141">Yes</span></span> |
| <span data-ttu-id="62a93-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="62a93-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="62a93-143">443</span><span class="sxs-lookup"><span data-stu-id="62a93-143">443</span></span> | <span data-ttu-id="62a93-144">Tak</span><span class="sxs-lookup"><span data-stu-id="62a93-144">Yes</span></span> |
| <span data-ttu-id="62a93-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="62a93-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="62a93-146">443</span><span class="sxs-lookup"><span data-stu-id="62a93-146">443</span></span> | <span data-ttu-id="62a93-147">Tak</span><span class="sxs-lookup"><span data-stu-id="62a93-147">Yes</span></span> |
| <span data-ttu-id="62a93-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="62a93-148">*.azure-automation.net</span></span> | <span data-ttu-id="62a93-149">443</span><span class="sxs-lookup"><span data-stu-id="62a93-149">443</span></span> | <span data-ttu-id="62a93-150">Tak</span><span class="sxs-lookup"><span data-stu-id="62a93-150">Yes</span></span> |



## <a name="download-the-agent-setup-file-from-oms"></a><span data-ttu-id="62a93-151">Pobierz plik Instalatora agenta z usługą OMS</span><span class="sxs-lookup"><span data-stu-id="62a93-151">Download the agent setup file from OMS</span></span>
1. <span data-ttu-id="62a93-152">W portalu OMS na **omówienie** kliknij przycisk **ustawienia** kafelka.</span><span class="sxs-lookup"><span data-stu-id="62a93-152">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span></span>  <span data-ttu-id="62a93-153">Kliknij przycisk **połączonych źródeł** u góry.</span><span class="sxs-lookup"><span data-stu-id="62a93-153">Click the **Connected Sources** tab at the top.</span></span>  
    <span data-ttu-id="62a93-154">![Połączone kartę źródła](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="62a93-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="62a93-155">Kliknij przycisk **serwerów z systemem Windows** , a następnie kliknij przycisk **Pobierz agenta systemu Windows** zastosowania do typu procesora komputera można pobrać pliku ustawień.</span><span class="sxs-lookup"><span data-stu-id="62a93-155">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span></span>
3. <span data-ttu-id="62a93-156">Po prawej stronie **identyfikator obszaru roboczego**, kliknij ikonę kopiowania i wklejania identyfikator do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="62a93-156">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span></span>
4. <span data-ttu-id="62a93-157">Po prawej stronie **klucz podstawowy**, kliknij ikonę kopiowania i wklejania klucza do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="62a93-157">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span></span>     

## <a name="install-the-agent-using-setup"></a><span data-ttu-id="62a93-158">Zainstaluj agenta przy użyciu Instalatora</span><span class="sxs-lookup"><span data-stu-id="62a93-158">Install the agent using setup</span></span>
1. <span data-ttu-id="62a93-159">Uruchom Instalatora, aby zainstalować agenta na komputerze, na którym chcesz zarządzać.</span><span class="sxs-lookup"><span data-stu-id="62a93-159">Run Setup to install the agent on a computer that you want to manage.</span></span>
2. <span data-ttu-id="62a93-160">Na stronie powitalnej kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="62a93-160">On the Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="62a93-161">Na stronie postanowienia licencyjne przeczytaj licencji, a następnie kliknij przycisk **zgadzam się**.</span><span class="sxs-lookup"><span data-stu-id="62a93-161">On the License Terms page, read the license and then click **I Agree**.</span></span>
4. <span data-ttu-id="62a93-162">Na stronie folderu docelowego, zmienić lub zachować domyślny folder instalacji, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="62a93-162">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="62a93-163">Na stronie Opcje instalacji agenta można połączyć agenta do Analiza dzienników Azure (OMS), Operations Manager lub puste opcji, jeśli chcesz później skonfigurować agenta.</span><span class="sxs-lookup"><span data-stu-id="62a93-163">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span></span> <span data-ttu-id="62a93-164">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="62a93-164">Click **Next**.</span></span>   
    - <span data-ttu-id="62a93-165">Jeśli zdecydujesz się na łączenie się Analiza dzienników Azure (OMS), Wklej **identyfikator obszaru roboczego** i **klucz obszaru roboczego (klucz podstawowy)** , który został skopiowany do Notatnika w poprzedniej procedurze, a następnie kliknij przycisk **dalej** .</span><span class="sxs-lookup"><span data-stu-id="62a93-165">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="62a93-166">![Wklej klucz podstawowy i identyfikator obszaru roboczego](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="62a93-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="62a93-167">Jeśli chcesz nawiązać połączenie programu Operations Manager, wpisz **Nazwa grupy zarządzania**, **serwera zarządzania** nazwa, i **portu serwera zarządzania**, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="62a93-167">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="62a93-168">Na stronie konto akcji agenta, wybierz konto systemu lokalnego lub konta domeny lokalnej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="62a93-168">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="62a93-169">![Konfiguracja grupy zarządzania](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![konto akcji agenta](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="62a93-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="62a93-170">Na stronie gotowy do instalacji, przejrzyj wybrane opcje, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="62a93-170">On the Ready to Install page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="62a93-171">W konfiguracji została ukończona pomyślnie kliknij pozycję **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="62a93-171">On the Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="62a93-172">Po zakończeniu **programu Microsoft Monitoring Agent** pojawia się w **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="62a93-172">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="62a93-173">Można sprawdzić konfigurację istnieje i sprawdź, czy agent jest podłączony do Operational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="62a93-173">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span></span> <span data-ttu-id="62a93-174">Podczas połączenia z usługą OMS, agent wyświetla komunikat z informacją: **Microsoft Monitoring Agent pomyślnie połączył się z usługą Microsoft Operations Management Suite.**</span><span class="sxs-lookup"><span data-stu-id="62a93-174">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="62a93-175">Skonfiguruj ustawienia serwera proxy</span><span class="sxs-lookup"><span data-stu-id="62a93-175">Configure proxy settings</span></span>

<span data-ttu-id="62a93-176">Poniższa procedura pozwala skonfigurować ustawienia serwera proxy dla programu Microsoft Monitoring Agent za pomocą Panelu sterowania.</span><span class="sxs-lookup"><span data-stu-id="62a93-176">You can use the following procedure to configure proxy settings for the Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="62a93-177">Należy użyć tej procedury dla każdego serwera.</span><span class="sxs-lookup"><span data-stu-id="62a93-177">You need to use this procedure for each server.</span></span> <span data-ttu-id="62a93-178">Jeśli masz wiele serwerów, które trzeba skonfigurować, łatwiejszym rozwiązaniem może być użycie skryptu automatyzującego ten proces.</span><span class="sxs-lookup"><span data-stu-id="62a93-178">If you have many servers that you need to configure, you might find it easier to use a script to automate this process.</span></span> <span data-ttu-id="62a93-179">W takim przypadku zobacz następną procedurę [Aby skonfigurować ustawienia serwera proxy dla programu Microsoft Monitoring Agent za pomocą skryptu](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="62a93-179">If so, see the next procedure [To configure proxy settings for the Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="62a93-180">Aby skonfigurować ustawienia serwera proxy dla programu Microsoft Monitoring Agent za pomocą Panelu sterowania</span><span class="sxs-lookup"><span data-stu-id="62a93-180">To configure proxy settings for the Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="62a93-181">Otwórz **Panel sterowania**.</span><span class="sxs-lookup"><span data-stu-id="62a93-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="62a93-182">Otwórz program **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="62a93-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="62a93-183">Kliknij kartę **Ustawienia serwera proxy**.</span><span class="sxs-lookup"><span data-stu-id="62a93-183">Click the **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="62a93-184">![karta Ustawienia serwera proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="62a93-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="62a93-185">Zaznacz pozycję **Użyj serwera proxy**, a następnie wpisz adres URL i numer portu, jeśli jest potrzebny, podobnie jak pokazano na przykładzie.</span><span class="sxs-lookup"><span data-stu-id="62a93-185">Select **Use a proxy server** and type the URL and port number, if one is needed, similar to the example shown.</span></span> <span data-ttu-id="62a93-186">Jeśli Twój serwer proxy wymaga uwierzytelniania, wpisz nazwę użytkownika i hasło, aby uzyskać dostęp do serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="62a93-186">If your proxy server requires authentication, type the username and password to access the proxy server.</span></span>


### <a name="verify-agent-connectivity-to-oms"></a><span data-ttu-id="62a93-187">Sprawdź łączność agent pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="62a93-187">Verify agent connectivity to OMS</span></span>

<span data-ttu-id="62a93-188">Można łatwo sprawdzić, czy agentów komunikują się z OMS, korzystając z następującej procedury:</span><span class="sxs-lookup"><span data-stu-id="62a93-188">You can easily verify whether your agents are communicating with OMS using the following procedure:</span></span>

1.  <span data-ttu-id="62a93-189">Na komputerze z agentem systemu Windows otwórz Panel sterowania.</span><span class="sxs-lookup"><span data-stu-id="62a93-189">On the computer with the Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="62a93-190">Otwórz program Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="62a93-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="62a93-191">Kliknij kartę Analiza dzienników Azure (OMS).</span><span class="sxs-lookup"><span data-stu-id="62a93-191">Click the Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="62a93-192">W kolumnie Stan powinny być widoczne czy agent pomyślnie połączony z usługą Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="62a93-192">In the Status column, you should see that the agent connected successfully to the Operations Management Suite service.</span></span>

![Agent połączone](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="62a93-194">Aby skonfigurować ustawienia serwera proxy dla programu Microsoft Monitoring Agent za pomocą skryptu</span><span class="sxs-lookup"><span data-stu-id="62a93-194">To configure proxy settings for the Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="62a93-195">Skopiuj poniższy przykład, zaktualizuj go informacjami specyficznymi dla Twojego środowiska, zapisz go z rozszerzeniem nazwy pliku PS1, a następnie uruchom skrypt na każdym komputerze, który łączy się bezpośrednio z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="62a93-195">Copy the following sample, update it with information specific to your environment, save it with a PS1 file name extension, and then run the script on each computer that connects directly to the OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get the Health Service configuration object.  We need to determine if we
    #have the right update rollup with the API we need.  If not, no need to run the rest of the script.
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

    Write-Output "Setting proxy to $ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-the-agent-using-the-command-line"></a><span data-ttu-id="62a93-196">Zainstaluj agenta przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="62a93-196">Install the agent using the command line</span></span>
- <span data-ttu-id="62a93-197">Zmodyfikuj, a następnie skorzystaj z następującego przykładu, aby zainstalować agenta przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="62a93-197">Modify and then use the following example to install the agent using the command line.</span></span> <span data-ttu-id="62a93-198">W przykładzie jest wykonywane pełni dyskretnej instalacji.</span><span class="sxs-lookup"><span data-stu-id="62a93-198">The example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="62a93-199">Jeśli chcesz uaktualnić agenta, należy użyć analizy dzienników interfejs API obsługi skryptów.</span><span class="sxs-lookup"><span data-stu-id="62a93-199">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span></span> <span data-ttu-id="62a93-200">Zobacz następną sekcję, aby uaktualnić agenta.</span><span class="sxs-lookup"><span data-stu-id="62a93-200">See the next section to upgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="62a93-201">Agent używa IExpress jako jego własny ekstraktor przy użyciu `/c` polecenia.</span><span class="sxs-lookup"><span data-stu-id="62a93-201">The agent uses IExpress as its self-extractor using the `/c` command.</span></span> <span data-ttu-id="62a93-202">Widać przełączniki wiersza polecenia w [przełączniki wiersza polecenia dla IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) , a następnie zaktualizować przykładu do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="62a93-202">You can see the command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>

|<span data-ttu-id="62a93-203">Opcje MMA</span><span class="sxs-lookup"><span data-stu-id="62a93-203">MMA-specific options</span></span>                   |<span data-ttu-id="62a93-204">Uwagi</span><span class="sxs-lookup"><span data-stu-id="62a93-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="62a93-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="62a93-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="62a93-206">1 = Konfigurowanie agenta z obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="62a93-206">1 = Configure the agent to report to a workspace</span></span>                |
|<span data-ttu-id="62a93-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="62a93-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="62a93-208">Identyfikator obszaru roboczego (guid) dla obszaru roboczego do dodania</span><span class="sxs-lookup"><span data-stu-id="62a93-208">Workspace Id (guid) for the workspace to add</span></span>                    |
|<span data-ttu-id="62a93-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="62a93-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="62a93-210">Klucz obszaru roboczego używany do uwierzytelniania początkowo z obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="62a93-210">Workspace key used to initially authenticate with the workspace</span></span> |
|<span data-ttu-id="62a93-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="62a93-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="62a93-212">Określ środowiska chmury, w którym znajduje się obszar roboczy</span><span class="sxs-lookup"><span data-stu-id="62a93-212">Specify the cloud environment where the workspace is located</span></span> <br> <span data-ttu-id="62a93-213">0 = komercyjnych chmury azure (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="62a93-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="62a93-214">1 = azure dla instytucji rządowych</span><span class="sxs-lookup"><span data-stu-id="62a93-214">1 = Azure Government</span></span> |
|<span data-ttu-id="62a93-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="62a93-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="62a93-216">Identyfikator URI serwera proxy do użycia</span><span class="sxs-lookup"><span data-stu-id="62a93-216">URI for the proxy to use</span></span> |
|<span data-ttu-id="62a93-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="62a93-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="62a93-218">Nazwa użytkownika do uzyskania dostępu uwierzytelnionego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="62a93-218">Username to access an authenticated proxy</span></span> |
|<span data-ttu-id="62a93-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="62a93-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="62a93-220">Hasło dostępu uwierzytelnionego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="62a93-220">Password to access an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="62a93-221">Aby uniknąć naciśnięcie limit długości wiersza polecenia IExpress, zainstaluj agenta z obszarem roboczym, nie skonfigurowany, a następnie użyj skryptu konfiguracji dla obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="62a93-221">To avoid hitting the command-line length limit of IExpress, install the agent with no workspace configured and then use a script to set configuration for the workspace.</span></span>

>[!NOTE]
<span data-ttu-id="62a93-222">Jeśli otrzymasz `Command line option syntax error.` przy użyciu `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parametru, można użyć następującego obejścia:</span><span class="sxs-lookup"><span data-stu-id="62a93-222">If you get a `Command line option syntax error.` when using the `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use the following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="62a93-223">Dodaj obszar roboczy za pomocą skryptu</span><span class="sxs-lookup"><span data-stu-id="62a93-223">Add a workspace using a script</span></span>
<span data-ttu-id="62a93-224">Dodaj obszar roboczy za pomocą interfejsu API skryptów agent analizy dzienników z następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="62a93-224">Add a workspace using the Log Analytics agent scripting API with the following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="62a93-225">Aby dodać obszar roboczy na platformie Azure dla instytucji rządowych Stanów Zjednoczonych, skorzystaj z poniższego przykładu skryptu:</span><span class="sxs-lookup"><span data-stu-id="62a93-225">To add a workspace in Azure for US Government, use the following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="62a93-226">Jeśli używano wiersza polecenia lub skryptu wcześniej do zainstalowania i skonfigurowania agenta, `EnableAzureOperationalInsights` została zastąpiona `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="62a93-226">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-the-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="62a93-227">Zainstaluj agenta przy użyciu usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="62a93-227">Install the agent using DSC in Azure Automation</span></span>

<span data-ttu-id="62a93-228">Poniższy przykładowy skrypt służy do instalowania agenta przy użyciu usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="62a93-228">You can use the following script example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="62a93-229">W przykładzie przedstawiono instalację agenta 64-bitowe, zidentyfikowane przez `URI` wartość.</span><span class="sxs-lookup"><span data-stu-id="62a93-229">The example installs the 64-bit agent, identified by the `URI` value.</span></span> <span data-ttu-id="62a93-230">Umożliwia także 32-bitowej wersji zastępując wartość identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="62a93-230">You can also use the 32-bit version by replacing the URI value.</span></span> <span data-ttu-id="62a93-231">Identyfikatory URI dla obu wersji są:</span><span class="sxs-lookup"><span data-stu-id="62a93-231">The URIs for both versions are:</span></span>

- <span data-ttu-id="62a93-232">Agent 64-bitowego systemu Windows — https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="62a93-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="62a93-233">Agent 32-bitowego systemu Windows — https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="62a93-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="62a93-234">W tym przykładzie procedury i skrypt nie spowoduje uaktualnienie istniejącego agenta.</span><span class="sxs-lookup"><span data-stu-id="62a93-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="62a93-235">Importowanie konfiguracji DSC xPSDesiredStateConfiguration modułu na podstawie [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="62a93-235">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="62a93-236">Tworzenie zasobów zmiennej usługi Automatyzacja Azure *OPSINSIGHTS_WS_ID* i *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="62a93-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="62a93-237">Ustaw *OPSINSIGHTS_WS_ID* do zestawu i identyfikator obszaru roboczego analizy dzienników OMS *OPSINSIGHTS_WS_KEY* w kluczu podstawowym obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="62a93-237">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span></span>
3.  <span data-ttu-id="62a93-238">Użyj następującego skryptu i zapisać go jako MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="62a93-238">Use the following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="62a93-239">Zmodyfikuj, a następnie skorzystaj z następującego przykładu, aby zainstalować agenta przy użyciu usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="62a93-239">Modify and then use the following example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="62a93-240">Zaimportuj MMAgent.ps1 do automatyzacji Azure za pomocą usługi Automatyzacja Azure, interfejsu lub apletu polecenia.</span><span class="sxs-lookup"><span data-stu-id="62a93-240">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="62a93-241">Przypisać konfiguracji węzła.</span><span class="sxs-lookup"><span data-stu-id="62a93-241">Assign a node to the configuration.</span></span> <span data-ttu-id="62a93-242">W ciągu 15 minut węzeł sprawdza konfigurację i MMA zostanie przypisany do węzła.</span><span class="sxs-lookup"><span data-stu-id="62a93-242">Within 15 minutes, the node checks its configuration and the MMA is pushed to the node.</span></span>

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

### <a name="get-the-latest-productid-value"></a><span data-ttu-id="62a93-243">Pobierz najnowszą wartość ProductId</span><span class="sxs-lookup"><span data-stu-id="62a93-243">Get the latest ProductId value</span></span>

<span data-ttu-id="62a93-244">`ProductId value` W MMAgent.ps1 skrypt jest unikatowa dla każdej wersji agenta.</span><span class="sxs-lookup"><span data-stu-id="62a93-244">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span></span> <span data-ttu-id="62a93-245">Po opublikowaniu zaktualizowaną wersję każdego agenta, wartość ProductId zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="62a93-245">When an updated version of each agent is published, the ProductId value changes.</span></span> <span data-ttu-id="62a93-246">Tak gdy ProductId zmieni się w przyszłości, można znaleźć wersji agenta za pomocą prostego skryptu.</span><span class="sxs-lookup"><span data-stu-id="62a93-246">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span></span> <span data-ttu-id="62a93-247">Po umieszczeniu najnowszą wersję agenta zainstalowana na serwerze testowym, służy poniższy skrypt można uzyskać wartość ProductId zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="62a93-247">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span></span> <span data-ttu-id="62a93-248">Ostatnia wartość ProductId można aktualizować wartość w skrypcie MMAgent.ps1.</span><span class="sxs-lookup"><span data-stu-id="62a93-248">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span></span>

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

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="62a93-249">Ręcznie skonfigurować agenta, lub Dodaj dodatkowe obszary robocze</span><span class="sxs-lookup"><span data-stu-id="62a93-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="62a93-250">Jeśli po zainstalowaniu agentów, ale ich nie skonfigurowano lub jeśli Agent ma raportować do wielu obszarów roboczych, można użyć następujące informacje, aby włączyć agenta lub ponownie go skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="62a93-250">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span></span> <span data-ttu-id="62a93-251">Po skonfigurowaniu agent, będą rejestrować się w usłudze agenta i niezbędnych informacji konfiguracyjnych oraz pakietów administracyjnych, które zawierają informacje o rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="62a93-251">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="62a93-252">Po zainstalowaniu programu Microsoft Monitoring Agent, otwórz **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="62a93-252">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="62a93-253">Otwórz **programu Microsoft Monitoring Agent** , a następnie kliknij przycisk **Analiza dzienników Azure (OMS)** kartę.</span><span class="sxs-lookup"><span data-stu-id="62a93-253">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="62a93-254">Kliknij przycisk **Dodaj** otworzyć **Dodaj obszar roboczy analizy dzienników** pole.</span><span class="sxs-lookup"><span data-stu-id="62a93-254">Click **Add** to open the **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="62a93-255">Wklej **identyfikator obszaru roboczego** i **klucz obszaru roboczego (klucz podstawowy)** skopiowanego do Notatnika w poprzedniej procedurze dla obszaru roboczego, który chcesz dodać, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="62a93-255">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span></span>  
    <span data-ttu-id="62a93-256">![Konfigurowanie usługi Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="62a93-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="62a93-257">Po zebraniu danych z komputerów monitorowanych przez agenta, liczbę komputerów monitorowanych przez OMS będą wyświetlane w portalu OMS na **połączonych źródeł** karcie **ustawienia** jako **serwerów Połączone**.</span><span class="sxs-lookup"><span data-stu-id="62a93-257">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="to-disable-an-agent"></a><span data-ttu-id="62a93-258">Aby wyłączyć agenta</span><span class="sxs-lookup"><span data-stu-id="62a93-258">To disable an agent</span></span>
1. <span data-ttu-id="62a93-259">Po zainstalowaniu agenta, należy otworzyć **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="62a93-259">After installing the agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="62a93-260">Otwórz program Microsoft Monitoring Agent, a następnie kliknij przycisk **Analiza dzienników Azure (OMS)** kartę.</span><span class="sxs-lookup"><span data-stu-id="62a93-260">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="62a93-261">Wybierz obszar roboczy, a następnie kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="62a93-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="62a93-262">Powtórz ten krok dla wszystkich innych obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="62a93-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="62a93-263">Opcjonalnie możesz skonfigurować agentów do raportu do grupy zarządzania programu Operations Manager</span><span class="sxs-lookup"><span data-stu-id="62a93-263">Optionally, configure agents to report to an Operations Manager management group</span></span>

<span data-ttu-id="62a93-264">Jeśli używasz programu Operations Manager w infrastrukturze IT, umożliwia także MMA agent jako agent programu Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="62a93-264">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span></span>

### <a name="to-configure-mma-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="62a93-265">Aby skonfigurować agentów MMA zgłoszenia do grupy zarządzania programu Operations Manager</span><span class="sxs-lookup"><span data-stu-id="62a93-265">To configure MMA agents to report to an Operations Manager management group</span></span>
1.  <span data-ttu-id="62a93-266">Na komputerze, na których jest zainstalowany agent, otwórz **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="62a93-266">On the computer where the agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="62a93-267">Otwórz **programu Microsoft Monitoring Agent** , a następnie kliknij przycisk **programu Operations Manager** kartę.</span><span class="sxs-lookup"><span data-stu-id="62a93-267">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>  
    <span data-ttu-id="62a93-268">![Karta Microsoft Monitoring Agent programu Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="62a93-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="62a93-269">Jeśli serwery programu Operations Manager są zintegrowane z usługą Active Directory, kliknij przycisk **automatycznie Aktualizuj przypisania grupy zarządzania z usług AD DS**.</span><span class="sxs-lookup"><span data-stu-id="62a93-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="62a93-270">Kliknij przycisk **Dodaj** otworzyć **Dodaj grupę zarządzania** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="62a93-270">Click **Add** to open the **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="62a93-271">![Program Microsoft Monitoring Agent Dodaj grupę zarządzania](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="62a93-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="62a93-272">W **Nazwa grupy zarządzania** wpisz nazwę grupy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="62a93-272">In **Management group name** box, type the name of your management group.</span></span>
6.  <span data-ttu-id="62a93-273">W **podstawowego serwera zarządzania** wpisz nazwę komputera w podstawowy serwer zarządzania.</span><span class="sxs-lookup"><span data-stu-id="62a93-273">In the **Primary management server** box, type the computer name of the primary management server.</span></span>
7.  <span data-ttu-id="62a93-274">W **port serwera zarządzania** wpisz numer portu TCP.</span><span class="sxs-lookup"><span data-stu-id="62a93-274">In the **Management server port** box, type the TCP port number.</span></span>
8.  <span data-ttu-id="62a93-275">W obszarze **konto akcji agenta**, wybierz konto systemu lokalnego lub konta domeny lokalnej.</span><span class="sxs-lookup"><span data-stu-id="62a93-275">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="62a93-276">Kliknij przycisk **OK** zamknąć **Dodaj grupę zarządzania** okno dialogowe, a następnie kliknij przycisk **OK** zamknąć **właściwości agenta monitorowania firmy Microsoft** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="62a93-276">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="62a93-277">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62a93-277">Next steps</span></span>

- <span data-ttu-id="62a93-278">[Dodaj rozwiązania Log Analytics z galerii rozwiązań](log-analytics-add-solutions.md), aby dodać funkcje i zebrać dane.</span><span class="sxs-lookup"><span data-stu-id="62a93-278">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
