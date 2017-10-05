---
title: "Rozwiązywanie problemów z działanie usługi Azure Active Directory rejestruje błędy pakiet zawartości | Dokumentacja firmy Microsoft"
description: "Udostępnia listę komunikatów o błędach pakiet zawartości działanie usługi Azure Active Directory i kroki rozwiązywania tych problemów."
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
ms.openlocfilehash: c880e9eb6d48bd1e38075fbd867d3906ec67b547
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="a4132-103">Rozwiązywanie problemów z działanie usługi Azure Active Directory rejestruje błędy pakiet zawartości</span><span class="sxs-lookup"><span data-stu-id="a4132-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="a4132-104">Podczas pracy z pakiet zawartości Power BI dla wersji zapoznawczej usługi Azure Active Directory, możliwe jest wystąpiły następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="a4132-104">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span></span> 

- [<span data-ttu-id="a4132-105">Odświeżanie nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="a4132-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="a4132-106">Nie można zaktualizować poświadczeń źródła danych</span><span class="sxs-lookup"><span data-stu-id="a4132-106">Failed to update data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="a4132-107">Importowanie danych trwa zbyt długo</span><span class="sxs-lookup"><span data-stu-id="a4132-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="a4132-108">Ten temat zawiera informacje o możliwych przyczyn i jak te błędy.</span><span class="sxs-lookup"><span data-stu-id="a4132-108">This topic provides you with information about the possible causes and how to fix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="a4132-109">Odświeżanie nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="a4132-109">Refresh failed</span></span> 
 
<span data-ttu-id="a4132-110">**Sposób ten błąd jest udostępniane**: wiadomości E-mail z usługi Power BI lub stan niepowodzenia w historii odświeżania.</span><span class="sxs-lookup"><span data-stu-id="a4132-110">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span></span> 


| <span data-ttu-id="a4132-111">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="a4132-111">Cause</span></span> | <span data-ttu-id="a4132-112">Jak rozwiązać</span><span class="sxs-lookup"><span data-stu-id="a4132-112">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="a4132-113">Odśwież awarii może być spowodowany błędy, gdy poświadczenia użytkowników łączących się pakiet zawartości zostały resetowania, ale nie zostały zaktualizowane w ustawieniach połączenia pakietu zawartości.</span><span class="sxs-lookup"><span data-stu-id="a4132-113">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the of the content pack.</span></span> | <span data-ttu-id="a4132-114">W usłudze Power BI zestawu danych odpowiadające pulpitu nawigacyjnego dzienniki działanie usługi Azure Active Directory (Dzienniki działanie usługi Azure Active Directory), wybierz pozycję harmonogram odświeżania, a następnie wprowadź poświadczenia usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4132-114">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="a4132-115">Odświeżanie może zakończyć się niepowodzeniem z powodu problemów danych w podstawowej pakietu zawartości.</span><span class="sxs-lookup"><span data-stu-id="a4132-115">A refresh can fail due to data issues in the underlying content pack.</span></span> | <span data-ttu-id="a4132-116">Plik biletu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="a4132-116">File a support ticket.</span></span> <span data-ttu-id="a4132-117">Aby uzyskać więcej informacji, zobacz [jak uzyskać pomoc techniczną dotyczącą usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="a4132-117">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-to-update-data-source-credentials"></a><span data-ttu-id="a4132-118">Nie można zaktualizować poświadczeń źródła danych</span><span class="sxs-lookup"><span data-stu-id="a4132-118">Failed to update data source credentials</span></span> 
 
<span data-ttu-id="a4132-119">**Sposób ten błąd jest udostępniane**: W usłudze Power BI, jeśli łączysz się z pakietu zawartości dzienników (wersja zapoznawcza) działanie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4132-119">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="a4132-120">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="a4132-120">Cause</span></span> | <span data-ttu-id="a4132-121">Jak rozwiązać</span><span class="sxs-lookup"><span data-stu-id="a4132-121">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="a4132-122">Użytkownik nawiązujący połączenie jest administratorem globalnym, ani czytnika zabezpieczeń ani administratora zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a4132-122">The connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="a4132-123">Użyj konta, które jest administratorem globalnym lub czytnik zabezpieczeń lub administratora zabezpieczeń można uzyskać dostępu do zawartości pakietów.</span><span class="sxs-lookup"><span data-stu-id="a4132-123">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span></span> |
| <span data-ttu-id="a4132-124">Dzierżawy nie jest dzierżawa usługi Premium lub nie ma co najmniej jednego użytkownika z licencją Premium pliku.</span><span class="sxs-lookup"><span data-stu-id="a4132-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="a4132-125">Plik biletu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="a4132-125">File a support ticket.</span></span> <span data-ttu-id="a4132-126">Aby uzyskać więcej informacji, zobacz [jak uzyskać pomoc techniczną dotyczącą usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="a4132-126">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="a4132-127">Importowanie danych trwa zbyt długo</span><span class="sxs-lookup"><span data-stu-id="a4132-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="a4132-128">**Sposób ten błąd jest udostępniane**: W usłudze Power BI, po połączeniu pakietu zawartości, proces importowania danych rozpoczyna się przygotować pulpitu nawigacyjnego dla dziennika działanie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4132-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="a4132-129">Zostanie wyświetlony komunikat: "*importowania danych...* "</span><span class="sxs-lookup"><span data-stu-id="a4132-129">You see the message: “*Importing data...*”</span></span>  

| <span data-ttu-id="a4132-130">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="a4132-130">Cause</span></span> | <span data-ttu-id="a4132-131">Jak rozwiązać</span><span class="sxs-lookup"><span data-stu-id="a4132-131">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="a4132-132">W zależności od wielkości dzierżawy ten krok może potrwać od w ciągu kilku minut do 30 minut.</span><span class="sxs-lookup"><span data-stu-id="a4132-132">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span></span> | <span data-ttu-id="a4132-133">Właśnie o cierpliwość.</span><span class="sxs-lookup"><span data-stu-id="a4132-133">Just be patient.</span></span> <span data-ttu-id="a4132-134">Jeśli wiadomość nie zmienia się na wyświetlanie pulpitu nawigacyjnego w ciągu jednej godziny, zgłoś biletu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="a4132-134">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="a4132-135">Aby uzyskać więcej informacji, zobacz [jak uzyskać pomoc techniczną dotyczącą usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="a4132-135">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="a4132-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4132-136">Next steps</span></span>

<span data-ttu-id="a4132-137">Aby zainstalować pakiet zawartości Power BI dla wersji zapoznawczej usługi Azure Active Directory, kliknij przycisk [tutaj](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="a4132-137">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


