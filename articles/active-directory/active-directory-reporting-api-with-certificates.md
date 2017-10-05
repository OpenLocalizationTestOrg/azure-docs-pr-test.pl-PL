---
title: "Pobieranie danych przy użyciu interfejsu API raportowania usługi Azure AD z certyfikatami | Microsoft Docs"
description: "Opis sposobu użycia interfejsu API raportowania usługi Azure AD przy użyciu poświadczeń certyfikatu w celu pobrania danych z katalogów bez interwencji użytkownika."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: c1345dcda6e52267a8037ffd7207e6bc3b0d3b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-data-using-the-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="e6116-103">Pobieranie danych przy użyciu interfejsu API raportowania usługi Azure AD z certyfikatami</span><span class="sxs-lookup"><span data-stu-id="e6116-103">Get data using the Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="e6116-104">Ten artykuł zawiera opis sposobu użycia interfejsu API raportowania usługi Azure AD przy użyciu poświadczeń certyfikatu w celu pobrania danych z katalogów bez interwencji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e6116-104">This article discusses how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.</span></span> 

## <a name="use-the-azure-ad-reporting-api"></a><span data-ttu-id="e6116-105">Zastosowanie interfejsu API raportowania usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6116-105">Use the Azure AD Reporting API</span></span> 
<span data-ttu-id="e6116-106">Interfejs API raportowania usługi Azure AD wymaga wykonania następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="e6116-106">Azure AD Reporting API requires that you complete the following steps:</span></span>
 *  <span data-ttu-id="e6116-107">Instalacja wymagań wstępnych</span><span class="sxs-lookup"><span data-stu-id="e6116-107">Install prerequisites</span></span>
 *  <span data-ttu-id="e6116-108">Skonfigurowanie certyfikatu w aplikacji</span><span class="sxs-lookup"><span data-stu-id="e6116-108">Set the certificate in your app</span></span>
 *  <span data-ttu-id="e6116-109">Pobranie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="e6116-109">Get an access token</span></span>
 *  <span data-ttu-id="e6116-110">Wykorzystanie tokenu dostępu do wywołania interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="e6116-110">Use the access token to call the Graph API</span></span>

<span data-ttu-id="e6116-111">Aby uzyskać informacje o kodzie źródłowym, zobacz [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Wykorzystanie modułu interfejsu API raportowania).</span><span class="sxs-lookup"><span data-stu-id="e6116-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="e6116-112">Instalacja wymagań wstępnych</span><span class="sxs-lookup"><span data-stu-id="e6116-112">Install prerequisites</span></span>
<span data-ttu-id="e6116-113">Konieczne jest zainstalowanie programu Azure AD PowerShell V2 i modułu AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="e6116-113">You will need to have Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="e6116-114">Pobierz i zainstaluj program Azure AD Powershell V2, postępując zgodnie z instrukcjami w temacie [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="e6116-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="e6116-115">Pobierz moduł Azure AD Utils z lokalizacji [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="e6116-115">Download the Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="e6116-116">Ten moduł zapewnia kilka poleceń cmdlet narzędzi, w tym:</span><span class="sxs-lookup"><span data-stu-id="e6116-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="e6116-117">Najnowszą wersję bibliotek ADAL korzystających z narzędzia Nuget</span><span class="sxs-lookup"><span data-stu-id="e6116-117">The latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="e6116-118">Tokeny dostępu użytkownika, kluczy aplikacji i certyfikatów korzystających z bibliotek ADAL</span><span class="sxs-lookup"><span data-stu-id="e6116-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="e6116-119">Stronicowane wyniki obsługi interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="e6116-119">Graph API handling paged results</span></span>

<span data-ttu-id="e6116-120">**Aby zainstalować moduł Azure AD Utils:**</span><span class="sxs-lookup"><span data-stu-id="e6116-120">**To install the Azure AD Utils module:**</span></span>

1. <span data-ttu-id="e6116-121">Utwórz katalog w celu zapisania modułu narzędzi (na przykład c:\azureAD) i pobierz moduł z serwisu GitHub.</span><span class="sxs-lookup"><span data-stu-id="e6116-121">Create a directory to save the utilities module (for example, c:\azureAD) and download the module from GitHub.</span></span>
2. <span data-ttu-id="e6116-122">Otwórz sesję programu PowerShell i przejdź do utworzonego właśnie katalogu.</span><span class="sxs-lookup"><span data-stu-id="e6116-122">Open a PowerShell session, and go to the directory you just created.</span></span> 
3. <span data-ttu-id="e6116-123">Zaimportuj moduł i zainstaluj go w ścieżce modułu programu PowerShell za pomocą polecenia cmdlet Install-AzureADUtilsModule.</span><span class="sxs-lookup"><span data-stu-id="e6116-123">Import the module, and install it in the PowerShell module path using the Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="e6116-124">Sesja powinna wyglądać podobnie do tego ekranu:</span><span class="sxs-lookup"><span data-stu-id="e6116-124">The session should look similar to this screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-the-certificate-in-your-app"></a><span data-ttu-id="e6116-126">Skonfigurowanie certyfikatu w aplikacji</span><span class="sxs-lookup"><span data-stu-id="e6116-126">Set the certificate in your app</span></span>
1. <span data-ttu-id="e6116-127">Jeśli masz już aplikację, pobierz jej identyfikator obiektu z witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e6116-127">If you already have an app, get its Object ID from the Azure Portal.</span></span> 

  ![Portal Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="e6116-129">Otwórz sesję programu PowerShell i nawiąż połączenie z usługą Azure AD za pomocą polecenia cmdlet Connect-AzureAD.</span><span class="sxs-lookup"><span data-stu-id="e6116-129">Open a PowerShell session and connect to Azure AD using the Connect-AzureAD cmdlet.</span></span>

  ![Portal Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="e6116-131">Użyj polecenia cmdlet New-AzureADApplicationCertificateCredential z modułu AzureADUtils, aby dodać do niego poświadczenie certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e6116-131">Use the New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils to add a certificate credential to it.</span></span> 

>[!Note]
><span data-ttu-id="e6116-132">Należy podać zarejestrowany wcześniej identyfikator obiektu aplikacji, a także obiekt certyfikatu (służy do tego polecenie Cert: drive).</span><span class="sxs-lookup"><span data-stu-id="e6116-132">You need to provide the application Object ID that you captured earlier, as well as the certificate object (get this using the Cert: drive).</span></span>
>


  ![Portal Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="e6116-134">Pobranie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="e6116-134">Get an access token</span></span>

<span data-ttu-id="e6116-135">Aby uzyskać token dostępu, użyj polecenia cmdlet Get-AzureADGraphAPIAccessTokenFromCert z modułu AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="e6116-135">To get an access token, use the Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="e6116-136">Należy użyć identyfikatora aplikacji zamiast identyfikatora obiektu użytego w ostatniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e6116-136">You need to use the Application ID instead of the Object ID that you used in the last section.</span></span>
>

 ![Portal Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-the-access-token-to-call-the-graph-api"></a><span data-ttu-id="e6116-138">Wykorzystanie tokenu dostępu do wywołania interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="e6116-138">Use the access token to call the Graph API</span></span>

<span data-ttu-id="e6116-139">Teraz można utworzyć skrypt.</span><span class="sxs-lookup"><span data-stu-id="e6116-139">Now you can create the script.</span></span> <span data-ttu-id="e6116-140">Poniżej zamieszczono przykład korzystający z polecenia Invoke-AzureADGraphAPIQuery z modułu AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="e6116-140">Below is an example using the Invoke-AzureADGraphAPIQuery cmdlet from the AzureADUtils.</span></span> <span data-ttu-id="e6116-141">To polecenie cmdlet obsługuje wyniki wielostronicowe, a następnie wysyła te wyniki do potoku programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6116-141">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span></span> 

 ![Portal Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="e6116-143">Teraz można przystąpić do eksportowania wyników do formatu CSV i zapisu w systemie SIEM.</span><span class="sxs-lookup"><span data-stu-id="e6116-143">You are now ready to export to a CSV and save to a SIEM system.</span></span> <span data-ttu-id="e6116-144">Skrypt można również opakować w zaplanowane zadanie, aby okresowo uzyskiwać dane usługi Azure AD od dzierżawcy bez konieczności przechowywania kluczy aplikacji w kodzie źródłowym.</span><span class="sxs-lookup"><span data-stu-id="e6116-144">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e6116-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6116-145">Next steps</span></span>
<span data-ttu-id="e6116-146">[The fundamentals of Azure identity management](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity) (Podstawy zarządzania tożsamościami w usłudze Azure)</span><span class="sxs-lookup"><span data-stu-id="e6116-146">[The fundamentals of Azure identity management](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)</span></span><br>



