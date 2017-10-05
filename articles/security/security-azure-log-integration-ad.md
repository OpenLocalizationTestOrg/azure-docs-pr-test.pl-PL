---
title: "Integracja dziennika Azure z dzienników inspekcji usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zainstalować usługę Azure dziennika integracji oraz integrowanie dzienniki z dzienników inspekcji platformy Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 8a1295cc86057ed72940e774d0bd423d61142e31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="de222-103">Integracja dzienników inspekcji usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de222-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="de222-104">Zdarzenia inspekcji w usłudze Azure Active Directory (Azure AD) pomaga zidentyfikować uprzywilejowanych akcji, które wystąpiły w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de222-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="de222-105">Można wyświetlić typy zdarzeń, które można śledzić, przeglądając [zdarzenia raportów inspekcji usługi Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="de222-105">You can see the types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="de222-106">Przed podjęciem próby kroki opisane w tym artykule, należy przejrzeć [wprowadzenie](security-azure-log-integration-get-started.md) artykułu i wykonaj kroki istnieje.</span><span class="sxs-lookup"><span data-stu-id="de222-106">Before you attempt the steps in this article, you must review the [Get started](security-azure-log-integration-get-started.md) article and complete the steps there.</span></span>

## <a name="steps-to-integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="de222-107">Kroki integracji dzienników inspekcji usługi Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="de222-107">Steps to integrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="de222-108">Otwórz wiersz polecenia i uruchom to polecenie:</span><span class="sxs-lookup"><span data-stu-id="de222-108">Open the command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="de222-109">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="de222-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="de222-110">To polecenie wyświetla monit o podanie logowania do systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="de222-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="de222-111">Polecenie następnie tworzy usługi Azure Active Directory nazwy głównej usługi w dzierżaw usługi Azure AD, które subskrypcji platformy Azure, w których zalogowany użytkownik jest administratora, administratora współpracującego lub właściciela hosta.</span><span class="sxs-lookup"><span data-stu-id="de222-111">The command then creates an Azure Active Directory service principal in the Azure AD tenants that host the Azure subscriptions in which the logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="de222-112">Polecenie zakończy się niepowodzeniem, jeśli tylko użytkownik-Gość w dzierżawie usługi Azure AD jest zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="de222-112">The command will fail if the logged-in user is only a guest user in the Azure AD tenant.</span></span> <span data-ttu-id="de222-113">Uwierzytelnianie na platformie Azure odbywa się za pośrednictwem usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de222-113">Authentication to Azure is done through Azure AD.</span></span> <span data-ttu-id="de222-114">Tworzenie nazwy głównej usługi integracji dziennika Azure tworzy tożsamości usługi Azure AD, która uzyskuje dostęp do odczytu z subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de222-114">Creating a service principal for Azure Log Integration creates the Azure AD identity that is given access to read from Azure subscriptions.</span></span>

3. <span data-ttu-id="de222-115">Uruchom następujące polecenie, aby zapewnić swojego identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="de222-115">Run the following command to provide your tenant ID.</span></span> <span data-ttu-id="de222-116">Musisz być członkiem roli administratora dzierżawy o uruchomienie polecenia.</span><span class="sxs-lookup"><span data-stu-id="de222-116">You need to be member of the tenant admin role to run the command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="de222-117">Przykład:</span><span class="sxs-lookup"><span data-stu-id="de222-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="de222-118">Sprawdź następujące foldery, aby upewnić się, że pliki JSON dziennika inspekcji usługi Azure Active Directory są tworzone w nich:</span><span class="sxs-lookup"><span data-stu-id="de222-118">Check the following folders to confirm that the Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="de222-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="de222-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="de222-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="de222-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="de222-121">Poniżej film wideo przedstawia kroki omówione w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="de222-121">The following video demonstrates the steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="de222-122">Aby uzyskać szczegółowe instrukcje dotyczące przełączania informacji w plikach JSON do informacji o zabezpieczeniach i zdarzeń systemu zarządzania (SIEM) skontaktuj się z dostawcą SIEM.</span><span class="sxs-lookup"><span data-stu-id="de222-122">For specific instructions on bringing the information in the JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="de222-123">Społeczność pomoc jest dostępna za pośrednictwem [Forum MSDN integracji dziennika Azure](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="de222-123">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="de222-124">Forum to umożliwia użytkownikom w społeczności integracji dziennika Azure do obsługi siebie z pytania, odpowiedzi, porady i wskazówki.</span><span class="sxs-lookup"><span data-stu-id="de222-124">This forum enables people in the Azure Log Integration community to support each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="de222-125">Ponadto zespół Azure dziennika integracji monitoruje tym forum i pomaga zawsze, gdy mogą go.</span><span class="sxs-lookup"><span data-stu-id="de222-125">In addition, the Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="de222-126">Można również otworzyć [żądania obsługi](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="de222-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="de222-127">Wybierz **integracji dziennika** jako usługa żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="de222-127">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de222-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de222-128">Next steps</span></span>
<span data-ttu-id="de222-129">Aby dowiedzieć się więcej na temat integracji dziennika Azure, zobacz:</span><span class="sxs-lookup"><span data-stu-id="de222-129">To learn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="de222-130">[Microsoft Azure dziennika integracji Azure dzienników](https://www.microsoft.com/download/details.aspx?id=53324): strony Centrum pobierania ten zapewnia szczegółowe informacje, wymagania systemowe i instrukcje dotyczące instalacji integracji dziennika Azure.</span><span class="sxs-lookup"><span data-stu-id="de222-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="de222-131">[Wprowadzenie do integracji dziennika Azure](security-azure-log-integration-overview.md): w tym artykule przedstawiono integracji dziennika Azure, jego kluczowych możliwości i jak działa.</span><span class="sxs-lookup"><span data-stu-id="de222-131">[Introduction to Azure Log Integration](security-azure-log-integration-overview.md): This article introduces you to Azure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="de222-132">[Czynności konfiguracyjnych partnera](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): ten wpis w blogu przedstawiono sposób konfigurowania integracji dziennika Azure do pracy z rozwiązań partnerskich Splunk HP ArcSight i IBM QRadar.</span><span class="sxs-lookup"><span data-stu-id="de222-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how to configure Azure Log Integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="de222-133">[Często zadawane pytania Azure dziennika integracji](security-azure-log-integration-faq.md): w tym artykule odpowiedzi na pytania dotyczące integracji dziennika Azure.</span><span class="sxs-lookup"><span data-stu-id="de222-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="de222-134">[Integrowanie alerty Centrum zabezpieczeń Azure dziennika w przypadku integracji](../security-center/security-center-integrating-alerts-with-log-integration.md): w tym artykule przedstawiono sposób synchronizować alerty Centrum zabezpieczeń, wraz z maszyny wirtualnej zdarzenia zabezpieczeń zebrane przez diagnostyki Azure i inspekcji Azure dzienniki z rozwiązania SIEM lub analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="de222-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how to sync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="de222-135">[Nowe funkcje diagnostyki Azure i Azure dzienniki inspekcji](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): ten wpis w blogu stanowi wprowadzenie do dzienników inspekcji platformy Azure i inne funkcje, które ułatwiają uzyskać wgląd w funkcjonowanie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de222-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you to Azure audit logs and other features that help you gain insights into the operations of your Azure resources.</span></span>
