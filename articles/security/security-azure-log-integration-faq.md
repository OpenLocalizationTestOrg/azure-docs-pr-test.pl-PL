---
title: "Integracja dzienników Azure — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "W tym artykule odpowiedzi na pytania dotyczące integracji dziennika Azure."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: bfdc7154160bb6bb7dc9c46eb2352ce74310c4de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="337e7-103">Integracja dzienników Azure — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="337e7-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="337e7-104">Ten artykuł zawiera odpowiedzi na często zadawane pytania (FAQ) dotyczące integracji dziennika Azure.</span><span class="sxs-lookup"><span data-stu-id="337e7-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="337e7-105">Integracja dziennika Azure to usługa systemu operacyjnego Windows używanej do integracji nowych dzienników z zasobów platformy Azure w sieci lokalnej zabezpieczeń informacji i zdarzenia (SIEM) systemów zarządzania.</span><span class="sxs-lookup"><span data-stu-id="337e7-105">Azure Log Integration is a Windows operating system service that you can use to integrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="337e7-106">Integracja ta zapewnia jednolity pulpit nawigacyjny dla wszystkich zasobów, lokalnie lub w chmurze.</span><span class="sxs-lookup"><span data-stu-id="337e7-106">This integration provides a unified dashboard for all your assets, on-premises or in the cloud.</span></span> <span data-ttu-id="337e7-107">Możesz agregować, skorelowania, analizowanie i alertów zdarzeń zabezpieczeń skojarzonych z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="337e7-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-the-azure-log-integration-software-free"></a><span data-ttu-id="337e7-108">Zwolnieniu oprogramowania integracji dziennika Azure?</span><span class="sxs-lookup"><span data-stu-id="337e7-108">Is the Azure Log Integration software free?</span></span>
<span data-ttu-id="337e7-109">Tak.</span><span class="sxs-lookup"><span data-stu-id="337e7-109">Yes.</span></span> <span data-ttu-id="337e7-110">Brak bezpłatne oprogramowanie Integration dziennika Azure.</span><span class="sxs-lookup"><span data-stu-id="337e7-110">There is no charge for the Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="337e7-111">Gdzie jest integracja dziennika Azure?</span><span class="sxs-lookup"><span data-stu-id="337e7-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="337e7-112">Jest obecnie dostępna w Azure handlowych i Azure dla instytucji rządowych i nie jest dostępny w Chinach lub Niemczech.</span><span class="sxs-lookup"><span data-stu-id="337e7-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-the-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="337e7-113">Jak można wyświetlić kont magazynu, z których integracji dziennika Azure jest ściąganie dzienniki maszyny Wirtualnej platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="337e7-113">How can I see the storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="337e7-114">Uruchom polecenie **listy źródeł azlog**.</span><span class="sxs-lookup"><span data-stu-id="337e7-114">Run the command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-the-azure-log-integration-logs-are-from"></a><span data-ttu-id="337e7-115">Jak sprawdzić, subskrypcji, w której są dzienniki Azure dziennika integracji z?</span><span class="sxs-lookup"><span data-stu-id="337e7-115">How can I tell which subscription the Azure Log Integration logs are from?</span></span>

<span data-ttu-id="337e7-116">W przypadku dzienników inspekcji, które są umieszczone w **AzureResourcemanagerJson** katalogów, subskrypcji identyfikator jest nazwa pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="337e7-116">In the case of audit logs that are placed in the **AzureResourcemanagerJson** directories, the subscription ID is in the log file name.</span></span> <span data-ttu-id="337e7-117">Dotyczy to również dzienniki w **AzureSecurityCenterJson** folderu.</span><span class="sxs-lookup"><span data-stu-id="337e7-117">This is also true for logs in the **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="337e7-118">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="337e7-118">For example:</span></span>

<span data-ttu-id="337e7-119">20170407T070805_2768037.0000000023. **1111e5ee-1111-111b-a11e-1e111e1111dc**JSON</span><span class="sxs-lookup"><span data-stu-id="337e7-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="337e7-120">Dzienniki inspekcji w usłudze Azure Active Directory zawierają identyfikator dzierżawy jako część nazwy.</span><span class="sxs-lookup"><span data-stu-id="337e7-120">Azure Active Directory audit logs include the tenant ID as part of the name.</span></span>

<span data-ttu-id="337e7-121">Dzienniki diagnostyczne, które są odczytywane z Centrum zdarzeń nie ma identyfikator subskrypcji jako część nazwy.</span><span class="sxs-lookup"><span data-stu-id="337e7-121">Diagnostic logs that are read from an event hub do not include the subscription ID as part of the name.</span></span> <span data-ttu-id="337e7-122">Zamiast tego zawierają przyjazną nazwę określony jako część tworzenie źródło zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="337e7-122">Instead, they include the friendly name specified as part of the creation of the event hub source.</span></span> 

## <a name="how-can-i-update-the-proxy-configuration"></a><span data-ttu-id="337e7-123">Jak można zaktualizować konfiguracji serwera proxy?</span><span class="sxs-lookup"><span data-stu-id="337e7-123">How can I update the proxy configuration?</span></span>
<span data-ttu-id="337e7-124">Jeśli ustawienie serwera proxy nie zezwalają na dostęp do magazynu Azure bezpośrednio, otwórz **AZLOG. WYWOŁANIE PLIKU EXE. CONFIG** w pliku **c:\Program Files\Microsoft Azure dziennika integracji**.</span><span class="sxs-lookup"><span data-stu-id="337e7-124">If your proxy setting does not allow Azure storage access directly, open the **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="337e7-125">Aktualizowanie pliku, aby uwzględnić **defaultProxy —** sekcji o adresie serwera proxy w swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="337e7-125">Update the file to include the **defaultProxy** section with the proxy address of your organization.</span></span> <span data-ttu-id="337e7-126">Po ukończeniu aktualizacji, Zatrzymaj i uruchom usługę za pomocą poleceń **azlog net stop** i **net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="337e7-126">After the update is done, stop and start the service by using the commands **net stop azlog** and **net start azlog**.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-the-subscription-information-in-windows-events"></a><span data-ttu-id="337e7-127">Jak wyświetlić informacje dotyczące subskrypcji w zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="337e7-127">How can I see the subscription information in Windows events?</span></span>
<span data-ttu-id="337e7-128">Dołącz identyfikator subskrypcji do przyjaznej nazwy podczas dodawania źródła:</span><span class="sxs-lookup"><span data-stu-id="337e7-128">Append the subscription ID to the friendly name while adding the source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="337e7-129">Zdarzenie XML ma następujące metadane, identyfikator subskrypcji w tym:</span><span class="sxs-lookup"><span data-stu-id="337e7-129">The event XML has the following metadata, including the subscription ID:</span></span>

![Zdarzenie XML][1]

## <a name="error-messages"></a><span data-ttu-id="337e7-131">Komunikaty o błędach</span><span class="sxs-lookup"><span data-stu-id="337e7-131">Error messages</span></span>
### <a name="when-i-run-the-command-azlog-createazureid-why-do-i-get-the-following-error"></a><span data-ttu-id="337e7-132">Po uruchomieniu polecenia **azlog createazureid**, dlaczego uzyskać następujący błąd?</span><span class="sxs-lookup"><span data-stu-id="337e7-132">When I run the command **azlog createazureid**, why do I get the following error?</span></span>
<span data-ttu-id="337e7-133">Błąd:</span><span class="sxs-lookup"><span data-stu-id="337e7-133">Error:</span></span>

  <span data-ttu-id="337e7-134">*Nie można utworzyć aplikację AAD - dzierżawy 72f988bf-86f1-41af-91ab-2d7cd011db37-Przyczyna = "Zabronione" - komunikat = "Wystarczających uprawnień do ukończenia tej operacji."*</span><span class="sxs-lookup"><span data-stu-id="337e7-134">*Failed to create AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges to complete the operation.'*</span></span>

<span data-ttu-id="337e7-135">**Azlog createazureid** polecenie podejmuje próbę utworzenia nazwy głównej usługi w wszystkich dzierżaw usługi Azure AD dla subskrypcji, w których Azure logowania ma dostęp.</span><span class="sxs-lookup"><span data-stu-id="337e7-135">The **azlog createazureid** command attempts to create a service principal in all the Azure AD tenants for the subscriptions that the Azure login has access to.</span></span> <span data-ttu-id="337e7-136">Jeśli logowanie w usłudze Azure jest tylko użytkownik-Gość w tej dzierżawie usługi Azure AD, polecenie kończy się niepowodzeniem "Wystarczających uprawnień do ukończenia tej operacji."</span><span class="sxs-lookup"><span data-stu-id="337e7-136">If your Azure login is only a guest user in that Azure AD tenant, the command fails with "Insufficient privileges to complete the operation."</span></span> <span data-ttu-id="337e7-137">Poproś administratora dzierżawy. Aby dodać konto użytkownika w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="337e7-137">Ask the tenant admin to add your account as a user in the tenant.</span></span>

### <a name="when-i-run-the-command-azlog-authorize-why-do-i-get-the-following-error"></a><span data-ttu-id="337e7-138">Po uruchomieniu polecenia **azlog autoryzować**, dlaczego uzyskać następujący błąd?</span><span class="sxs-lookup"><span data-stu-id="337e7-138">When I run the command **azlog authorize**, why do I get the following error?</span></span>
<span data-ttu-id="337e7-139">Błąd:</span><span class="sxs-lookup"><span data-stu-id="337e7-139">Error:</span></span>

  <span data-ttu-id="337e7-140">*Ostrzeżenie tworzenia przypisania roli - AuthorizationFailed: klient janedo@microsoft.com"z obiektem id"fe9e03e4-4dad-4328-910f-fd24a9660bd2"nie ma autoryzacji do wykonania akcji"Microsoft.Authorization/roleAssignments/write"w zakresie" / Subskrypcje / 70d 95299-d689-4c 97-b971-0d8ff0000000 ".*</span><span class="sxs-lookup"><span data-stu-id="337e7-140">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="337e7-141">**Autoryzować azlog** polecenia przypisuje rolę czytelnika do nazwy głównej usługi Azure AD (utworzone za pomocą **azlog createazureid**) do podanego subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="337e7-141">The **azlog authorize** command assigns the role of reader to the Azure AD service principal (created with **azlog createazureid**) to the provided subscriptions.</span></span> <span data-ttu-id="337e7-142">Jeśli logowanie w usłudze Azure nie jest administratora współpracującego lub właściciela subskrypcji, nie jest on z komunikatem o błędzie "Autoryzacja nie powiodła się.".</span><span class="sxs-lookup"><span data-stu-id="337e7-142">If the Azure login is not a co-administrator or an owner of the subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="337e7-143">Azure opartej na rolach kontroli dostępu (RBAC) administratora współpracującego lub właściciela wymaganego do ukończenia tej akcji.</span><span class="sxs-lookup"><span data-stu-id="337e7-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed to complete this action.</span></span>

## <a name="where-can-i-find-the-definition-of-the-properties-in-the-audit-log"></a><span data-ttu-id="337e7-144">Gdzie można znaleźć definicji właściwości w dzienniku inspekcji?</span><span class="sxs-lookup"><span data-stu-id="337e7-144">Where can I find the definition of the properties in the audit log?</span></span>
<span data-ttu-id="337e7-145">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="337e7-145">See:</span></span>

* [<span data-ttu-id="337e7-146">Operacje inspekcji z usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="337e7-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="337e7-147">Wyświetl listę zdarzeń zarządzania w ramach subskrypcji w interfejsie API REST Azure monitora</span><span class="sxs-lookup"><span data-stu-id="337e7-147">List the management events in a subscription in the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="337e7-148">Gdzie znaleźć szczegółowe informacje o alertach Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="337e7-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="337e7-149">Zobacz [reagowanie na alerty zabezpieczeń w Centrum zabezpieczeń Azure i zarządzanie nimi](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="337e7-149">See [Managing and responding to security alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="337e7-150">Jak zmodyfikować, jakie informacje są zbierane z diagnostyki maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="337e7-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="337e7-151">Aby uzyskać szczegółowe informacje dotyczące sposobu uzyskania, modyfikowania i ustawiania konfiguracji diagnostyki Azure zobacz [Użyj programu PowerShell, aby włączyć na maszynie wirtualnej z systemem Windows Azure Diagnostics](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="337e7-151">For details on how to get, modify, and set the Azure Diagnostics configuration, see [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="337e7-152">Poniższy przykład pobiera konfigurację diagnostyki Azure:</span><span class="sxs-lookup"><span data-stu-id="337e7-152">The following example gets the Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="337e7-153">Poniższy przykład modyfikuje konfigurację diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="337e7-153">The following example modifies the Azure Diagnostics configuration.</span></span> <span data-ttu-id="337e7-154">W tej konfiguracji tylko zdarzeń 4624 identyfikator i identyfikator 4625 są zbierane z dziennika zdarzeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="337e7-154">In this configuration, only event ID 4624 and event ID 4625 are collected from the security event log.</span></span> <span data-ttu-id="337e7-155">Antimalware Microsoft Azure zdarzenia są zbierane z dziennika zdarzeń systemu.</span><span class="sxs-lookup"><span data-stu-id="337e7-155">Microsoft Antimalware for Azure events are collected from the system event log.</span></span> <span data-ttu-id="337e7-156">Aby uzyskać więcej informacji dotyczących korzystania z wyrażenia XPath, zobacz [wykorzystywanie zdarzenia](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="337e7-156">For details on the use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="337e7-157">Poniższy przykład przedstawia konfigurację diagnostyki Azure:</span><span class="sxs-lookup"><span data-stu-id="337e7-157">The following example sets the Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="337e7-158">Po wprowadzeniu zmian sprawdź konto magazynu, aby upewnić się, że poprawne zdarzenia są zbierane.</span><span class="sxs-lookup"><span data-stu-id="337e7-158">After you make changes, check the storage account to ensure that the correct events are collected.</span></span>

<span data-ttu-id="337e7-159">Jeśli masz problemy podczas instalacji i konfiguracji, otwórz [żądania obsługi](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="337e7-159">If you have any issues during the installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="337e7-160">Wybierz **integracji dziennika** jako usługa żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="337e7-160">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-to-integrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="337e7-161">Azure dziennika integracji można używać do integracji dzienniki obserwatora sieciowego Mój SIEM?</span><span class="sxs-lookup"><span data-stu-id="337e7-161">Can I use Azure Log Integration to integrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="337e7-162">Azure obserwatora sieciowego generuje duże ilości danych rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="337e7-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="337e7-163">Dzienniki te nie są przeznaczone do wysłania do rozwiązania SIEM.</span><span class="sxs-lookup"><span data-stu-id="337e7-163">These logs are not meant to be sent to a SIEM.</span></span> <span data-ttu-id="337e7-164">Tylko obsługiwane miejsce docelowe dla dzienników obserwatora sieciowego jest konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="337e7-164">The only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="337e7-165">Integracja z usługą Azure dziennika nie obsługuje odczytywania te dzienniki i udostępnienie ich SIEM.</span><span class="sxs-lookup"><span data-stu-id="337e7-165">Azure Log Integration does not support reading these logs and making them available to a SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
