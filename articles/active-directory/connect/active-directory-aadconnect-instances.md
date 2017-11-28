---
title: "Azure AD Connect: Wystąpienie usługi synchronizacji | Dokumentacja firmy Microsoft"
description: "Ta strona dokumentów uwagi dotyczące wystąpienia usługi Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="409f7-103">Azure AD Connect: Uwagi dotyczące wystąpienia</span><span class="sxs-lookup"><span data-stu-id="409f7-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="409f7-104">Azure AD Connect jest najczęściej używana z Witaj świecie wystąpienia usługi Azure AD i Office 365.</span><span class="sxs-lookup"><span data-stu-id="409f7-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="409f7-105">Istnieją także inne wystąpienia, ale te mają różne wymagania dotyczące adresów URL i inne uwagi.</span><span class="sxs-lookup"><span data-stu-id="409f7-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="409f7-106">Microsoft Cloud (Niemcy)</span><span class="sxs-lookup"><span data-stu-id="409f7-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="409f7-107">Witaj [Niemcy Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) to chmura suwerennych przez osobę zaufaną niemieckim danych.</span><span class="sxs-lookup"><span data-stu-id="409f7-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="409f7-108">Adresy URL tooopen w serwera proxy</span><span class="sxs-lookup"><span data-stu-id="409f7-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="409f7-109">\*. microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="409f7-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="409f7-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="409f7-110">\*.windows.net</span></span> |
| <span data-ttu-id="409f7-111">+ Listy odwołania certyfikatów</span><span class="sxs-lookup"><span data-stu-id="409f7-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="409f7-112">Po zarejestrowaniu tooyour dzierżawy usługi Azure AD, należy użyć konta w domenie onmicrosoft.de hello.</span><span class="sxs-lookup"><span data-stu-id="409f7-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="409f7-113">Aktualnie nie znajduje się w Niemczech Microsoft Cloud hello funkcje:</span><span class="sxs-lookup"><span data-stu-id="409f7-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="409f7-114">**Azure AD Connect Health** nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="409f7-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="409f7-115">**Aktualizacje automatyczne** nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="409f7-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="409f7-116">**Zapisywanie zwrotne haseł** jest dostępna w wersji zapoznawczej wersji Azure AD Connect 1.1.570.0 i po.</span><span class="sxs-lookup"><span data-stu-id="409f7-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="409f7-117">Inne usługi Azure AD Premium nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="409f7-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="409f7-118">Chmury Microsoft Azure dla instytucji rządowych</span><span class="sxs-lookup"><span data-stu-id="409f7-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="409f7-119">Witaj [chmury Microsoft Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/) to chmura dla instytucji rządowych Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="409f7-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="409f7-120">Ta chmura obsługiwanego przez wcześniejszych wersjach narzędzia DirSync.</span><span class="sxs-lookup"><span data-stu-id="409f7-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="409f7-121">Z 1.1.180 kompilacji programu Azure AD Connect hello generacji chmury hello jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="409f7-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="409f7-122">Tej generacji używa USA — tylko do oparte na punktach końcowych i mieć osobne listy adresów URL tooopen w serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="409f7-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="409f7-123">Adresy URL tooopen w serwera proxy</span><span class="sxs-lookup"><span data-stu-id="409f7-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="409f7-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="409f7-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="409f7-125">\*. microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="409f7-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="409f7-126">\*. gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="409f7-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="409f7-127">+ Listy odwołania certyfikatów</span><span class="sxs-lookup"><span data-stu-id="409f7-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="409f7-128">Azure AD Connect nie jest w stanie tooautomatically wykrywa, że dzierżawy usługi Azure AD znajduje się w chmurze dla instytucji rządowych hello.</span><span class="sxs-lookup"><span data-stu-id="409f7-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="409f7-129">Zamiast tego należy hello tootake następujące akcje po zainstalowaniu usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="409f7-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="409f7-130">Uruchom hello Azure AD Connect instalacji.</span><span class="sxs-lookup"><span data-stu-id="409f7-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="409f7-131">Gdy zostanie wyświetlona strona pierwszy hello, gdzie są powinien hello tooaccept umowy licencyjnej, nie należy kontynuować, ale pozostawić Uruchamianie Kreatora instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="409f7-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="409f7-132">Uruchom regedit i zmienić wartość klucza rejestru hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello wartość `2`.</span><span class="sxs-lookup"><span data-stu-id="409f7-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="409f7-133">Wrócić do poprzedniej strony Kreatora instalacji toohello usługi Azure AD Connect, zaakceptuj umowę licencyjną hello i kontynuować.</span><span class="sxs-lookup"><span data-stu-id="409f7-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="409f7-134">Podczas instalacji, upewnij się, że hello toouse **konfiguracji niestandardowej** ścieżki instalacji (i nie Instalacja ekspresowa).</span><span class="sxs-lookup"><span data-stu-id="409f7-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="409f7-135">Następnie kontynuuj instalację hello w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="409f7-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="409f7-136">Aktualnie nie znajduje się w chmurze Microsoft Azure dla instytucji rządowych hello funkcje:</span><span class="sxs-lookup"><span data-stu-id="409f7-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="409f7-137">**Azure AD Connect Health** nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="409f7-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="409f7-138">**Aktualizacje automatyczne** nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="409f7-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="409f7-139">**Zapisywanie zwrotne haseł** jest dostępna w wersji zapoznawczej wersji Azure AD Connect 1.1.570.0 i po.</span><span class="sxs-lookup"><span data-stu-id="409f7-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="409f7-140">Inne usługi Azure AD Premium nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="409f7-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="409f7-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="409f7-141">Next steps</span></span>
<span data-ttu-id="409f7-142">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="409f7-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
