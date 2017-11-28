---
title: "aaaGet danych przy użyciu hello Azure AD interfejsu API raportowania z certyfikatami | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak toouse hello Azure AD interfejsu API raportowania certyfikat poświadczeń tooget danymi z katalogów bez interwencji użytkownika."
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
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="b182b-103">Pobierz dane przy użyciu interfejsu API raportowania usługi Azure AD hello z certyfikatami</span><span class="sxs-lookup"><span data-stu-id="b182b-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="b182b-104">W tym artykule opisano, jak toouse hello Azure AD interfejsu API raportowania certyfikat poświadczeń tooget danymi z katalogów bez interwencji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b182b-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="b182b-105">Użyj hello Azure AD interfejsu API raportowania</span><span class="sxs-lookup"><span data-stu-id="b182b-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="b182b-106">Azure AD interfejsu API raportowania wymaga wykonanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b182b-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="b182b-107">Instalacja wymagań wstępnych</span><span class="sxs-lookup"><span data-stu-id="b182b-107">Install prerequisites</span></span>
 *  <span data-ttu-id="b182b-108">Ustaw hello certyfikatu w aplikacji</span><span class="sxs-lookup"><span data-stu-id="b182b-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="b182b-109">Pobranie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="b182b-109">Get an access token</span></span>
 *  <span data-ttu-id="b182b-110">Użyj hello toocall tokenu dostępu hello interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="b182b-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="b182b-111">Aby uzyskać informacje o kodzie źródłowym, zobacz [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Wykorzystanie modułu interfejsu API raportowania).</span><span class="sxs-lookup"><span data-stu-id="b182b-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="b182b-112">Instalacja wymagań wstępnych</span><span class="sxs-lookup"><span data-stu-id="b182b-112">Install prerequisites</span></span>
<span data-ttu-id="b182b-113">Konieczne będzie toohave programu Azure AD PowerShell V2 i zainstalowany moduł AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="b182b-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="b182b-114">Pobieranie i instalowanie programu Azure AD Powershell V2, postępując zgodnie z instrukcjami hello na [środowiska PowerShell usługi Azure Active Directory](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="b182b-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="b182b-115">Pobierz moduł Azure AD witryny hello z [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="b182b-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="b182b-116">Ten moduł zapewnia kilka poleceń cmdlet narzędzi, w tym:</span><span class="sxs-lookup"><span data-stu-id="b182b-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="b182b-117">Witaj najnowszej wersji biblioteki adal przy użyciu narzędzia Nuget</span><span class="sxs-lookup"><span data-stu-id="b182b-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="b182b-118">Tokeny dostępu użytkownika, kluczy aplikacji i certyfikatów korzystających z bibliotek ADAL</span><span class="sxs-lookup"><span data-stu-id="b182b-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="b182b-119">Stronicowane wyniki obsługi interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="b182b-119">Graph API handling paged results</span></span>

<span data-ttu-id="b182b-120">**Moduł Azure AD witryny hello tooinstall:**</span><span class="sxs-lookup"><span data-stu-id="b182b-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="b182b-121">Utwórz moduł narzędzia hello toosave katalog (na przykład c:\azureAD) i Pobierz hello modułu z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="b182b-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="b182b-122">Otwórz sesję programu PowerShell, a następnie przejdź do katalogu toohello, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="b182b-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="b182b-123">Zaimportuj moduł hello i zainstaluj go w ścieżce modułu programu PowerShell hello przy użyciu polecenia cmdlet hello AzureADUtilsModule instalacji.</span><span class="sxs-lookup"><span data-stu-id="b182b-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="b182b-124">Hello sesji powinien wyglądać podobnie toothis ekranu:</span><span class="sxs-lookup"><span data-stu-id="b182b-124">hello session should look similar toothis screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="b182b-126">Ustaw hello certyfikatu w aplikacji</span><span class="sxs-lookup"><span data-stu-id="b182b-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="b182b-127">Jeśli już masz aplikację, należy pobrać Identyfikatora obiektu z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b182b-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Azure Portal](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="b182b-129">Otwórz sesję programu PowerShell i połącz tooAzure AD za pomocą polecenia cmdlet Connect-AzureAD hello.</span><span class="sxs-lookup"><span data-stu-id="b182b-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Azure Portal](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="b182b-131">Użyj polecenia cmdlet New-AzureADApplicationCertificateCredential hello tooadd AzureADUtils tooit poświadczenie certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="b182b-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="b182b-132">Możesz muszą aplikacji hello tooprovide Identyfikatora obiektu, która została przechwycona wcześniej, a także hello obiektu certyfikatu (przy użyciu tego hello Cert: dysk).</span><span class="sxs-lookup"><span data-stu-id="b182b-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Azure Portal](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="b182b-134">Pobranie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="b182b-134">Get an access token</span></span>

<span data-ttu-id="b182b-135">tooget tokenu dostępu, użyj polecenia cmdlet Get-AzureADGraphAPIAccessTokenFromCert hello AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="b182b-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="b182b-136">Należy toouse hello identyfikator aplikacji zamiast hello Identyfikatora obiektu, który został użyty w ostatniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="b182b-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Azure Portal](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="b182b-138">Użyj hello toocall tokenu dostępu hello interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="b182b-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="b182b-139">Teraz możesz utworzyć hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="b182b-139">Now you can create hello script.</span></span> <span data-ttu-id="b182b-140">Poniżej przedstawiono przykład za pomocą polecenia cmdlet Invoke-AzureADGraphAPIQuery hello hello AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="b182b-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="b182b-141">To polecenie cmdlet obsługuje wyników wielu stronicowania, a następnie wysyła te wyniki toohello PowerShell potoku.</span><span class="sxs-lookup"><span data-stu-id="b182b-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Azure Portal](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="b182b-143">Są teraz gotowe tooexport tooa CSV i zapisać tooa SIEM system.</span><span class="sxs-lookup"><span data-stu-id="b182b-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="b182b-144">Można również zawijać skryptu w tooget zaplanowane zadanie danych usługi Azure AD z dzierżawą okresowo bez konieczności toostore kluczy aplikacji hello kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="b182b-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b182b-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b182b-145">Next steps</span></span>
[<span data-ttu-id="b182b-146">Witaj podstawowe informacje na temat zarządzania tożsamość platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b182b-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



