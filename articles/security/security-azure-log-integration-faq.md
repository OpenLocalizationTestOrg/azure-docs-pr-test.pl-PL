---
title: "aaaAzure dziennika integracji — często zadawane pytania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="96757-103">Integracja dzienników Azure — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="96757-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="96757-104">Ten artykuł zawiera odpowiedzi na często zadawane pytania (FAQ) dotyczące integracji dziennika Azure.</span><span class="sxs-lookup"><span data-stu-id="96757-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="96757-105">Integracja dziennika Azure to usługa systemu operacyjnego Windows czy można użyć toointegrate raw dzienników z zasobów platformy Azure w sieci lokalnej zabezpieczeń informacji i zdarzenia (SIEM) systemów zarządzania.</span><span class="sxs-lookup"><span data-stu-id="96757-105">Azure Log Integration is a Windows operating system service that you can use toointegrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="96757-106">Integracja ta zapewnia jednolity pulpit nawigacyjny dla wszystkich zasobów, lokalnie lub w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="96757-106">This integration provides a unified dashboard for all your assets, on-premises or in hello cloud.</span></span> <span data-ttu-id="96757-107">Możesz agregować, skorelowania, analizowanie i alertów zdarzeń zabezpieczeń skojarzonych z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="96757-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-hello-azure-log-integration-software-free"></a><span data-ttu-id="96757-108">Zwolnieniu hello Azure dziennika integracji oprogramowania?</span><span class="sxs-lookup"><span data-stu-id="96757-108">Is hello Azure Log Integration software free?</span></span>
<span data-ttu-id="96757-109">Tak.</span><span class="sxs-lookup"><span data-stu-id="96757-109">Yes.</span></span> <span data-ttu-id="96757-110">Brak bezpłatne hello Azure dziennika integracji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="96757-110">There is no charge for hello Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="96757-111">Gdzie jest integracja dziennika Azure?</span><span class="sxs-lookup"><span data-stu-id="96757-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="96757-112">Jest obecnie dostępna w Azure handlowych i Azure dla instytucji rządowych i nie jest dostępny w Chinach lub Niemczech.</span><span class="sxs-lookup"><span data-stu-id="96757-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="96757-113">Jak można wyświetlić hello kont magazynu, z których integracji dziennika Azure jest ściąganie dzienniki maszyny Wirtualnej platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="96757-113">How can I see hello storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="96757-114">Uruchom polecenie hello **listy źródeł azlog**.</span><span class="sxs-lookup"><span data-stu-id="96757-114">Run hello command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a><span data-ttu-id="96757-115">Jak sprawdzić, które subskrypcji hello Azure integracji dziennika są dzienniki z?</span><span class="sxs-lookup"><span data-stu-id="96757-115">How can I tell which subscription hello Azure Log Integration logs are from?</span></span>

<span data-ttu-id="96757-116">W przypadku hello dzienników inspekcji, które są umieszczone w hello **AzureResourcemanagerJson** katalogów, identyfikator subskrypcji hello jest nazwa pliku dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="96757-116">In hello case of audit logs that are placed in hello **AzureResourcemanagerJson** directories, hello subscription ID is in hello log file name.</span></span> <span data-ttu-id="96757-117">Dotyczy to również dzienniki w hello **AzureSecurityCenterJson** folderu.</span><span class="sxs-lookup"><span data-stu-id="96757-117">This is also true for logs in hello **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="96757-118">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="96757-118">For example:</span></span>

<span data-ttu-id="96757-119">20170407T070805_2768037.0000000023. **1111e5ee-1111-111b-a11e-1e111e1111dc**JSON</span><span class="sxs-lookup"><span data-stu-id="96757-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="96757-120">Dzienniki inspekcji w usłudze Azure Active Directory obejmować identyfikator dzierżawy hello jako część nazwy hello.</span><span class="sxs-lookup"><span data-stu-id="96757-120">Azure Active Directory audit logs include hello tenant ID as part of hello name.</span></span>

<span data-ttu-id="96757-121">Dzienniki diagnostyczne, które są odczytywane z Centrum zdarzeń nie ma identyfikator subskrypcji hello jako część nazwy hello.</span><span class="sxs-lookup"><span data-stu-id="96757-121">Diagnostic logs that are read from an event hub do not include hello subscription ID as part of hello name.</span></span> <span data-ttu-id="96757-122">Zamiast tego zawierają hello przyjazną nazwę określony jako część hello utworzeniu źródła Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="96757-122">Instead, they include hello friendly name specified as part of hello creation of hello event hub source.</span></span> 

## <a name="how-can-i-update-hello-proxy-configuration"></a><span data-ttu-id="96757-123">Jak można zaktualizować konfiguracji serwera proxy hello?</span><span class="sxs-lookup"><span data-stu-id="96757-123">How can I update hello proxy configuration?</span></span>
<span data-ttu-id="96757-124">Jeśli ustawienie serwera proxy nie zezwalają na dostęp do magazynu Azure bezpośrednio, otwórz hello **AZLOG. WYWOŁANIE PLIKU EXE. CONFIG** w pliku **c:\Program Files\Microsoft Azure dziennika integracji**.</span><span class="sxs-lookup"><span data-stu-id="96757-124">If your proxy setting does not allow Azure storage access directly, open hello **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="96757-125">Aktualizacja hello pliku tooinclude hello **defaultProxy —** sekcji o adresie serwera proxy hello Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="96757-125">Update hello file tooinclude hello **defaultProxy** section with hello proxy address of your organization.</span></span> <span data-ttu-id="96757-126">Po ukończeniu aktualizacji hello, zatrzymać i uruchomić usługę hello za pomocą poleceń hello **azlog net stop** i **net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="96757-126">After hello update is done, stop and start hello service by using hello commands **net stop azlog** and **net start azlog**.</span></span>

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

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a><span data-ttu-id="96757-127">Jak można wyświetlić informacji o subskrypcji hello w zdarzeń systemu Windows?</span><span class="sxs-lookup"><span data-stu-id="96757-127">How can I see hello subscription information in Windows events?</span></span>
<span data-ttu-id="96757-128">Dołącz hello subskrypcji identyfikator toohello przyjaznej nazwy podczas dodawania źródła hello:</span><span class="sxs-lookup"><span data-stu-id="96757-128">Append hello subscription ID toohello friendly name while adding hello source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="96757-129">Zdarzenie Hello XML ma powitania po metadanych, w tym hello identyfikator subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="96757-129">hello event XML has hello following metadata, including hello subscription ID:</span></span>

![Zdarzenie XML][1]

## <a name="error-messages"></a><span data-ttu-id="96757-131">Komunikaty o błędach</span><span class="sxs-lookup"><span data-stu-id="96757-131">Error messages</span></span>
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a><span data-ttu-id="96757-132">Po uruchomieniu polecenia hello **azlog createazureid**, dlaczego uzyskać hello następujący błąd?</span><span class="sxs-lookup"><span data-stu-id="96757-132">When I run hello command **azlog createazureid**, why do I get hello following error?</span></span>
<span data-ttu-id="96757-133">Błąd:</span><span class="sxs-lookup"><span data-stu-id="96757-133">Error:</span></span>

  <span data-ttu-id="96757-134">*Nie powiodło się toocreate aplikacji AAD - dzierżawy 72f988bf-86f1-41af-91ab-2d7cd011db37 - Przyczyna = "Zabronione" - komunikat = "Operacja hello toocomplete niewystarczające uprawnienia".*</span><span class="sxs-lookup"><span data-stu-id="96757-134">*Failed toocreate AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges toocomplete hello operation.'*</span></span>

<span data-ttu-id="96757-135">Witaj **azlog createazureid** polecenie podejmuje toocreate nazwy głównej usługi w wszystkich dzierżaw hello Azure AD dla subskrypcji hello, które hello Azure logowania ma dostęp.</span><span class="sxs-lookup"><span data-stu-id="96757-135">hello **azlog createazureid** command attempts toocreate a service principal in all hello Azure AD tenants for hello subscriptions that hello Azure login has access to.</span></span> <span data-ttu-id="96757-136">Jeśli logowanie w usłudze Azure jest tylko użytkownik-Gość w tej dzierżawie usługi Azure AD, hello polecenia nie powiodło się "Operacja hello toocomplete niewystarczające uprawnienia".</span><span class="sxs-lookup"><span data-stu-id="96757-136">If your Azure login is only a guest user in that Azure AD tenant, hello command fails with "Insufficient privileges toocomplete hello operation."</span></span> <span data-ttu-id="96757-137">Poproś administratora tooadd dzierżawy hello Twojego konta jako użytkownik w dzierżawie powitalnych.</span><span class="sxs-lookup"><span data-stu-id="96757-137">Ask hello tenant admin tooadd your account as a user in hello tenant.</span></span>

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a><span data-ttu-id="96757-138">Po uruchomieniu polecenia hello **azlog autoryzować**, dlaczego uzyskać hello następujący błąd?</span><span class="sxs-lookup"><span data-stu-id="96757-138">When I run hello command **azlog authorize**, why do I get hello following error?</span></span>
<span data-ttu-id="96757-139">Błąd:</span><span class="sxs-lookup"><span data-stu-id="96757-139">Error:</span></span>

  <span data-ttu-id="96757-140">*Ostrzeżenie tworzenia przypisania roli - AuthorizationFailed: powitania klienta janedo@microsoft.com"z obiektem id"fe9e03e4-4dad-4328-910f-fd24a9660bd2"nie ma autoryzacji tooperform akcji"Microsoft.Authorization/roleAssignments/write"w zakresie" / Subskrypcje / 70d 95299-d689-4c 97-b971-0d8ff0000000 ".*</span><span class="sxs-lookup"><span data-stu-id="96757-140">*Warning creating Role Assignment - AuthorizationFailed: hello client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="96757-141">Hello **autoryzować azlog** polecenia przypisuje hello roli nazwy głównej usługi Azure AD toohello czytnika (utworzone za pomocą **azlog createazureid**) toohello podane subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="96757-141">hello **azlog authorize** command assigns hello role of reader toohello Azure AD service principal (created with **azlog createazureid**) toohello provided subscriptions.</span></span> <span data-ttu-id="96757-142">Jeśli hello Azure logowania nie jest administratora współpracującego lub właściciela subskrypcji hello, jego kończy się niepowodzeniem z komunikatem o błędzie "Autoryzacja nie powiodła się.".</span><span class="sxs-lookup"><span data-stu-id="96757-142">If hello Azure login is not a co-administrator or an owner of hello subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="96757-143">Azure opartej na rolach kontroli dostępu (RBAC) administratora współpracującego lub właściciela jest wymagane toocomplete tej akcji.</span><span class="sxs-lookup"><span data-stu-id="96757-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed toocomplete this action.</span></span>

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a><span data-ttu-id="96757-144">Gdzie mogę znaleźć hello definicji właściwości hello w dzienniku inspekcji hello?</span><span class="sxs-lookup"><span data-stu-id="96757-144">Where can I find hello definition of hello properties in hello audit log?</span></span>
<span data-ttu-id="96757-145">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="96757-145">See:</span></span>

* [<span data-ttu-id="96757-146">Operacje inspekcji z usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="96757-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="96757-147">Lista zdarzeń zarządzania hello w ramach subskrypcji w hello interfejsu API REST Monitor Azure</span><span class="sxs-lookup"><span data-stu-id="96757-147">List hello management events in a subscription in hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="96757-148">Gdzie znaleźć szczegółowe informacje o alertach Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="96757-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="96757-149">Zobacz [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="96757-149">See [Managing and responding toosecurity alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="96757-150">Jak zmodyfikować, jakie informacje są zbierane z diagnostyki maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="96757-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="96757-151">Szczegółowe informacje w sposób tooget, modyfikować i konfiguracji hello diagnostyki Azure, możesz znaleźć [tooenable Użyj programu PowerShell diagnostyki Azure na maszynie wirtualnej z systemem Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96757-151">For details on how tooget, modify, and set hello Azure Diagnostics configuration, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="96757-152">Poniższy przykład Hello pobiera konfigurację diagnostyki Azure hello:</span><span class="sxs-lookup"><span data-stu-id="96757-152">hello following example gets hello Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="96757-153">Poniższy przykład Hello modyfikuje hello Azure Diagnostics konfigurację.</span><span class="sxs-lookup"><span data-stu-id="96757-153">hello following example modifies hello Azure Diagnostics configuration.</span></span> <span data-ttu-id="96757-154">W tej konfiguracji tylko zdarzeń 4624 identyfikator i identyfikator 4625 są zbierane z dziennika zdarzeń zabezpieczeń hello.</span><span class="sxs-lookup"><span data-stu-id="96757-154">In this configuration, only event ID 4624 and event ID 4625 are collected from hello security event log.</span></span> <span data-ttu-id="96757-155">Antimalware Microsoft Azure zdarzenia są zbierane z hello w dzienniku zdarzeń systemowych.</span><span class="sxs-lookup"><span data-stu-id="96757-155">Microsoft Antimalware for Azure events are collected from hello system event log.</span></span> <span data-ttu-id="96757-156">Aby uzyskać szczegółowe informacje z użyciem wyrażenia XPath hello, zobacz [wykorzystywanie zdarzenia](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="96757-156">For details on hello use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="96757-157">Witaj poniższy przykład przedstawia hello Azure Diagnostics konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="96757-157">hello following example sets hello Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="96757-158">Po wprowadzeniu zmian Sprawdź tooensure konta magazynu hello tego hello poprawny są zbierane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="96757-158">After you make changes, check hello storage account tooensure that hello correct events are collected.</span></span>

<span data-ttu-id="96757-159">Jeśli masz problemy podczas hello instalacji i konfiguracji, otwórz [żądania obsługi](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="96757-159">If you have any issues during hello installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="96757-160">Wybierz **integracji dziennika** jako usługa hello żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="96757-160">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="96757-161">Dzienniki obserwatora sieciowego toointegrate integracji dziennika Azure można używać do mojego SIEM?</span><span class="sxs-lookup"><span data-stu-id="96757-161">Can I use Azure Log Integration toointegrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="96757-162">Azure obserwatora sieciowego generuje duże ilości danych rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="96757-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="96757-163">Dzienniki te nie są przeznaczone toobe wysyłane tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="96757-163">These logs are not meant toobe sent tooa SIEM.</span></span> <span data-ttu-id="96757-164">miejsce docelowe Hello obsługiwane tylko dla dzienników obserwatora sieciowego jest konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="96757-164">hello only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="96757-165">Integracja z usługą Azure dziennika nie obsługuje odczytywania te dzienniki i udostępnia je tooa dostępne rozwiązania SIEM.</span><span class="sxs-lookup"><span data-stu-id="96757-165">Azure Log Integration does not support reading these logs and making them available tooa SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
