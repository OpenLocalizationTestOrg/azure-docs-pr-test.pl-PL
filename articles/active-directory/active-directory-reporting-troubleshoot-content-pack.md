---
title: "Rozwiązywanie problemów z działanie usługi Azure Active Directory rejestruje błędy pakiet zawartości | Dokumentacja firmy Microsoft"
description: "Zawiera listę komunikatów o błędach programu hello działanie usługi Azure Active Directory zawartości pakietu i kroki toofix je."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="95c4c-103">Rozwiązywanie problemów z działanie usługi Azure Active Directory rejestruje błędy pakiet zawartości</span><span class="sxs-lookup"><span data-stu-id="95c4c-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="95c4c-104">Podczas pracy z hello pakiet zawartości Power BI dla wersji zapoznawczej usługi Azure Active Directory, możliwe jest funkcjonowaniem hello następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="95c4c-104">When working with hello Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into hello following errors:</span></span> 

- [<span data-ttu-id="95c4c-105">Odświeżanie nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="95c4c-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="95c4c-106">Poświadczenia źródła danych nie powiodło się tooupdate</span><span class="sxs-lookup"><span data-stu-id="95c4c-106">Failed tooupdate data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="95c4c-107">Importowanie danych trwa zbyt długo</span><span class="sxs-lookup"><span data-stu-id="95c4c-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="95c4c-108">Ten temat zawiera informacje o hello możliwe przyczyny i w jaki sposób toofix te błędy.</span><span class="sxs-lookup"><span data-stu-id="95c4c-108">This topic provides you with information about hello possible causes and how toofix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="95c4c-109">Odświeżanie nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="95c4c-109">Refresh failed</span></span> 
 
<span data-ttu-id="95c4c-110">**Sposób ten błąd jest udostępniane**: wiadomości E-mail z usługi Power BI lub stan niepowodzenia w historii odświeżania hello.</span><span class="sxs-lookup"><span data-stu-id="95c4c-110">**How this error is surfaced**: Email from Power BI or failed status in hello refresh history.</span></span> 


| <span data-ttu-id="95c4c-111">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="95c4c-111">Cause</span></span> | <span data-ttu-id="95c4c-112">Jak toofix</span><span class="sxs-lookup"><span data-stu-id="95c4c-112">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="95c4c-113">Odśwież awarii błędy może być spowodowany hello poświadczeń użytkowników hello łączenie pakiet zawartości toohello zostały resetowania, ale nie zostały zaktualizowane w ustawieniach połączenia hello hello hello pakietu zawartości.</span><span class="sxs-lookup"><span data-stu-id="95c4c-113">Refresh failure errors can be caused when hello credentials of hello users connecting toohello content pack have been reset but not updated in hello connection settings of hello of hello content pack.</span></span> | <span data-ttu-id="95c4c-114">W usłudze Power BI zlokalizować odpowiednich toohello dataset hello pulpitu nawigacyjnego dzienniki działanie usługi Azure Active Directory (Dzienniki działanie usługi Azure Active Directory), wybierz pozycję harmonogram odświeżania, a następnie wprowadź poświadczenia usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95c4c-114">In Power BI, locate hello dataset corresponding toohello Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="95c4c-115">Odświeżanie może zakończyć się niepowodzeniem ze względu na problemy toodata w hello bazowy pakiet zawartości.</span><span class="sxs-lookup"><span data-stu-id="95c4c-115">A refresh can fail due toodata issues in hello underlying content pack.</span></span> | <span data-ttu-id="95c4c-116">Plik biletu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="95c4c-116">File a support ticket.</span></span> <span data-ttu-id="95c4c-117">Aby uzyskać więcej informacji, zobacz [jak tooget obsługują usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="95c4c-117">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a><span data-ttu-id="95c4c-118">Poświadczenia źródła danych nie powiodło się tooupdate</span><span class="sxs-lookup"><span data-stu-id="95c4c-118">Failed tooupdate data source credentials</span></span> 
 
<span data-ttu-id="95c4c-119">**Sposób ten błąd jest udostępniane**: W usłudze Power BI, łącząc toohello pakiet zawartości dzienników (wersja zapoznawcza) działanie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95c4c-119">**How this error is surfaced**: In Power BI, when you are connecting toohello Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="95c4c-120">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="95c4c-120">Cause</span></span> | <span data-ttu-id="95c4c-121">Jak toofix</span><span class="sxs-lookup"><span data-stu-id="95c4c-121">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="95c4c-122">użytkownik nawiązujący połączenie Hello jest administratorem globalnym, ani czytnika zabezpieczeń ani administratora zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="95c4c-122">hello connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="95c4c-123">Użyj konta, które jest administratorem globalnym lub czytnik zabezpieczeń lub zabezpieczeń administratora tooaccess hello pakietów zawartości.</span><span class="sxs-lookup"><span data-stu-id="95c4c-123">Use an account that is either a global admin or a security reader or a security admin tooaccess hello content packs.</span></span> |
| <span data-ttu-id="95c4c-124">Dzierżawy nie jest dzierżawa usługi Premium lub nie ma co najmniej jednego użytkownika z licencją Premium pliku.</span><span class="sxs-lookup"><span data-stu-id="95c4c-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="95c4c-125">Plik biletu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="95c4c-125">File a support ticket.</span></span> <span data-ttu-id="95c4c-126">Aby uzyskać więcej informacji, zobacz [jak tooget obsługują usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="95c4c-126">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="95c4c-127">Importowanie danych trwa zbyt długo</span><span class="sxs-lookup"><span data-stu-id="95c4c-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="95c4c-128">**Sposób ten błąd jest udostępniane**: W usłudze Power BI, po połączeniu pakietu zawartości, proces importowania danych hello uruchamia tooprepare pulpitu nawigacyjnego dla dziennika działanie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95c4c-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, hello data import process starts tooprepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="95c4c-129">Zobacz wiadomość hello: "*importowania danych...* "</span><span class="sxs-lookup"><span data-stu-id="95c4c-129">You see hello message: “*Importing data...*”</span></span>  

| <span data-ttu-id="95c4c-130">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="95c4c-130">Cause</span></span> | <span data-ttu-id="95c4c-131">Jak toofix</span><span class="sxs-lookup"><span data-stu-id="95c4c-131">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="95c4c-132">W zależności od rozmiaru hello dzierżawy ten krok może zająć od kilku minut too30 minut.</span><span class="sxs-lookup"><span data-stu-id="95c4c-132">Depending on hello size of your tenant, this step could take anywhere from a few mins too30 minutes.</span></span> | <span data-ttu-id="95c4c-133">Właśnie o cierpliwość.</span><span class="sxs-lookup"><span data-stu-id="95c4c-133">Just be patient.</span></span> <span data-ttu-id="95c4c-134">Jeśli wiadomość hello nie zmienia tooshowing pulpitu nawigacyjnego w ciągu jednej godziny, zgłoś biletu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="95c4c-134">If hello message does not change tooshowing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="95c4c-135">Aby uzyskać więcej informacji, zobacz [jak tooget obsługują usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="95c4c-135">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="95c4c-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95c4c-136">Next steps</span></span>

<span data-ttu-id="95c4c-137">Witaj tooinstall pakiet zawartości Power BI dla Azure Active Directory w wersji zapoznawczej, kliknij przycisk [tutaj](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="95c4c-137">tooinstall hello Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


