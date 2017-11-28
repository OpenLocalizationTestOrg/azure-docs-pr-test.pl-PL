---
title: "aaaAzure dziennika integracji z dzienników inspekcji usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall hello Usługa integracji dziennika Azure oraz integrowanie dzienniki z dzienników inspekcji platformy Azure"
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
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="6515c-103">Integracja dzienników inspekcji usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6515c-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="6515c-104">Zdarzenia inspekcji w usłudze Azure Active Directory (Azure AD) pomaga zidentyfikować uprzywilejowanych akcji, które wystąpiły w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6515c-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="6515c-105">Widać hello typy zdarzeń, które można śledzić, przeglądając [zdarzenia raportów inspekcji usługi Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="6515c-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6515c-106">Przed rozpoczęciem powitalne opisanych w tym artykule, należy przejrzeć hello [wprowadzenie](security-azure-log-integration-get-started.md) artykułu i wykonaj kroki hello istnieje.</span><span class="sxs-lookup"><span data-stu-id="6515c-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="6515c-107">Dzienniki inspekcji w usłudze Azure Active directory toointegrate kroki</span><span class="sxs-lookup"><span data-stu-id="6515c-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="6515c-108">Otwórz wiersz polecenia hello i uruchom to polecenie:</span><span class="sxs-lookup"><span data-stu-id="6515c-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="6515c-109">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6515c-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="6515c-110">To polecenie wyświetla monit o podanie logowania do systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="6515c-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="6515c-111">Witaj polecenie następnie tworzy usługi Azure Active Directory nazwy głównej usługi w dzierżawcy usługi Azure AD hello hostujących hello subskrypcji platformy Azure, w których hello zalogowanego użytkownika jest administratora, administratora współpracującego lub właściciela.</span><span class="sxs-lookup"><span data-stu-id="6515c-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="6515c-112">polecenie Hello zakończy się niepowodzeniem, jeśli tylko użytkownik-Gość w dzierżawie usługi Azure AD hello jest hello zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6515c-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="6515c-113">TooAzure uwierzytelnianie odbywa się za pośrednictwem usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6515c-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="6515c-114">Tworzenie nazwy głównej usługi integracji dziennika Azure tworzy hello tożsamości usługi Azure AD, która uzyskuje dostęp tooread z subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6515c-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="6515c-115">Uruchom następujące polecenie tooprovide hello swojego identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="6515c-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="6515c-116">Należy toobe członkiem hello dzierżawy admin roli toorun hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="6515c-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="6515c-117">Przykład:</span><span class="sxs-lookup"><span data-stu-id="6515c-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="6515c-118">Sprawdź, czy powitania po tooconfirm folderów, które hello JSON dziennik inspekcji usługi Azure Active Directory są tworzone w nich:</span><span class="sxs-lookup"><span data-stu-id="6515c-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="6515c-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="6515c-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="6515c-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="6515c-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="6515c-121">Witaj poniżej film wideo przedstawia kroki hello omówione w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="6515c-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="6515c-122">Aby uzyskać szczegółowe instrukcje dotyczące przełączania hello informacji w plikach JSON hello do informacji o zabezpieczeniach i zdarzeń systemu zarządzania (SIEM) skontaktuj się z dostawcą SIEM.</span><span class="sxs-lookup"><span data-stu-id="6515c-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="6515c-123">Społeczność pomoc jest dostępna za pośrednictwem hello [Forum MSDN integracji dziennika Azure](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="6515c-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="6515c-124">Tym forum umożliwia pracownikom hello Azure dziennika integracji społeczności toosupport siebie z pytania, odpowiedzi, porady i wskazówki.</span><span class="sxs-lookup"><span data-stu-id="6515c-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="6515c-125">Ponadto hello Azure dziennika integracji zespołu monitoruje tym forum i pomaga zawsze, gdy mogą go.</span><span class="sxs-lookup"><span data-stu-id="6515c-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="6515c-126">Można również otworzyć [żądania obsługi](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="6515c-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="6515c-127">Wybierz **integracji dziennika** jako usługa hello żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="6515c-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6515c-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6515c-128">Next steps</span></span>
<span data-ttu-id="6515c-129">toolearn więcej informacji na temat integracji dziennika Azure, zobacz:</span><span class="sxs-lookup"><span data-stu-id="6515c-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="6515c-130">[Microsoft Azure dziennika integracji Azure dzienników](https://www.microsoft.com/download/details.aspx?id=53324): strony Centrum pobierania ten zapewnia szczegółowe informacje, wymagania systemowe i instrukcje dotyczące instalacji integracji dziennika Azure.</span><span class="sxs-lookup"><span data-stu-id="6515c-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="6515c-131">[Wprowadzenie tooAzure integracji dziennika](security-azure-log-integration-overview.md): w tym artykule przedstawiono tooAzure integracji dziennika, jego kluczowych możliwości i sposobu działania.</span><span class="sxs-lookup"><span data-stu-id="6515c-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="6515c-132">[Czynności konfiguracyjnych partnera](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): ten wpis w blogu pokazuje, jak rozwiązania Splunk, HP ArcSight i IBM QRadar partnerskie tooconfigure toowork Azure dziennika integracji z.</span><span class="sxs-lookup"><span data-stu-id="6515c-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="6515c-133">[Często zadawane pytania Azure dziennika integracji](security-azure-log-integration-faq.md): w tym artykule odpowiedzi na pytania dotyczące integracji dziennika Azure.</span><span class="sxs-lookup"><span data-stu-id="6515c-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="6515c-134">[Integrowanie alerty Centrum zabezpieczeń Azure dziennika w przypadku integracji](../security-center/security-center-integrating-alerts-with-log-integration.md): w tym artykule opisano, jak alerty Centrum zabezpieczeń toosync, wraz z zebranych przez diagnostyki Azure i dzienników inspekcji platformy Azure, z Twojego analizy dzienników zdarzeń zabezpieczeń maszyny wirtualnej lub Rozwiązania SIEM.</span><span class="sxs-lookup"><span data-stu-id="6515c-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="6515c-135">[Nowe funkcje diagnostyki Azure i Azure dzienniki inspekcji](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): ten wpis w blogu wprowadza tooAzure dzienniki inspekcji i inne funkcje, które ułatwiają uzyskać wgląd w działania hello zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6515c-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
