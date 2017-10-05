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
ms.openlocfilehash: e8321c3d16253226a5931cacbce6fa5d50b697bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="b9608-103">Azure AD Connect: Uwagi dotyczące wystąpienia</span><span class="sxs-lookup"><span data-stu-id="b9608-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="b9608-104">Azure AD Connect jest najczęściej używana z wystąpieniem na całym świecie usługi Azure AD i Office 365.</span><span class="sxs-lookup"><span data-stu-id="b9608-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="b9608-105">Istnieją także inne wystąpienia, ale te mają różne wymagania dotyczące adresów URL i inne uwagi.</span><span class="sxs-lookup"><span data-stu-id="b9608-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="b9608-106">Microsoft Cloud (Niemcy)</span><span class="sxs-lookup"><span data-stu-id="b9608-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="b9608-107">[Niemcy Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) to chmura suwerennych przez osobę zaufaną niemieckim danych.</span><span class="sxs-lookup"><span data-stu-id="b9608-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="b9608-108">Adresy URL, aby otworzyć w serwera proxy</span><span class="sxs-lookup"><span data-stu-id="b9608-108">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="b9608-109">\*. microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="b9608-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="b9608-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="b9608-110">\*.windows.net</span></span> |
| <span data-ttu-id="b9608-111">+ Listy odwołania certyfikatów</span><span class="sxs-lookup"><span data-stu-id="b9608-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="b9608-112">Po zalogowaniu się do dzierżawy usługi Azure AD, należy użyć konta w domenie onmicrosoft.de.</span><span class="sxs-lookup"><span data-stu-id="b9608-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span></span>

<span data-ttu-id="b9608-113">Aktualnie nie znajduje się w Niemczech Microsoft Cloud funkcje:</span><span class="sxs-lookup"><span data-stu-id="b9608-113">Features currently not present in the Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="b9608-114">**Azure AD Connect Health** nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="b9608-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="b9608-115">**Aktualizacje automatyczne** nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="b9608-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="b9608-116">**Zapisywanie zwrotne haseł** jest dostępna w wersji zapoznawczej wersji Azure AD Connect 1.1.570.0 i po.</span><span class="sxs-lookup"><span data-stu-id="b9608-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="b9608-117">Inne usługi Azure AD Premium nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b9608-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="b9608-118">Chmury Microsoft Azure dla instytucji rządowych</span><span class="sxs-lookup"><span data-stu-id="b9608-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="b9608-119">[Chmury Microsoft Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/) to chmura dla instytucji rządowych Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="b9608-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="b9608-120">Ta chmura obsługiwanego przez wcześniejszych wersjach narzędzia DirSync.</span><span class="sxs-lookup"><span data-stu-id="b9608-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="b9608-121">Z 1.1.180 kompilacji programu Azure AD Connect generacji chmury jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="b9608-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span></span> <span data-ttu-id="b9608-122">Tej generacji używa USA — tylko do oparte na punktach końcowych i mieć różne listy adresów URL, aby otworzyć w serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="b9608-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span></span>

| <span data-ttu-id="b9608-123">Adresy URL, aby otworzyć w serwera proxy</span><span class="sxs-lookup"><span data-stu-id="b9608-123">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="b9608-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="b9608-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="b9608-125">\*. microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="b9608-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="b9608-126">\*. gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="b9608-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="b9608-127">+ Listy odwołania certyfikatów</span><span class="sxs-lookup"><span data-stu-id="b9608-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="b9608-128">Azure AD Connect nie będzie mógł automatycznie wykrywa, że dzierżawy usługi Azure AD znajduje się w chmurze dla instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="b9608-128">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span></span> <span data-ttu-id="b9608-129">Zamiast tego należy wykonać następujące czynności, po zainstalowaniu usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b9608-129">Instead you need to take the following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="b9608-130">Uruchom instalację Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b9608-130">Start the Azure AD Connect installation.</span></span>
2. <span data-ttu-id="b9608-131">Gdy pojawi się pierwszej strony, gdzie są powinien zaakceptować umowę licencyjną, nie należy kontynuować, ale pozostawić uruchomiony Kreator instalacji.</span><span class="sxs-lookup"><span data-stu-id="b9608-131">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span></span>
3. <span data-ttu-id="b9608-132">Uruchom regedit i zmienić wartość klucza rejestru `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` wartość `2`.</span><span class="sxs-lookup"><span data-stu-id="b9608-132">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span></span>
4. <span data-ttu-id="b9608-133">Przejdź do Kreatora instalacji usługi Azure AD Connect, należy zaakceptować umowę licencyjną i kontynuować.</span><span class="sxs-lookup"><span data-stu-id="b9608-133">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span></span> <span data-ttu-id="b9608-134">Podczas instalacji, upewnij się użyć **konfiguracji niestandardowej** ścieżki instalacji (i nie Instalacja ekspresowa).</span><span class="sxs-lookup"><span data-stu-id="b9608-134">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="b9608-135">Następnie kontynuować instalację w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="b9608-135">Then continue the installation as usual.</span></span>

<span data-ttu-id="b9608-136">Aktualnie nie znajduje się w chmurze Microsoft Azure dla instytucji rządowych funkcje:</span><span class="sxs-lookup"><span data-stu-id="b9608-136">Features currently not present in the Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="b9608-137">**Azure AD Connect Health** nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="b9608-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="b9608-138">**Aktualizacje automatyczne** nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="b9608-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="b9608-139">**Zapisywanie zwrotne haseł** jest dostępna w wersji zapoznawczej wersji Azure AD Connect 1.1.570.0 i po.</span><span class="sxs-lookup"><span data-stu-id="b9608-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="b9608-140">Inne usługi Azure AD Premium nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b9608-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9608-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b9608-141">Next steps</span></span>
<span data-ttu-id="b9608-142">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="b9608-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
