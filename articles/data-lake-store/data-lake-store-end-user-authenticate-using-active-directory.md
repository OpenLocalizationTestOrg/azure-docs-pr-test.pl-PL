---
title: "Uwierzytelnianie użytkownika końcowego: usługi Data Lake Store w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooachieve uwierzytelniania użytkowników końcowych za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="783e0-103">Uwierzytelnianie użytkownika końcowego za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="783e0-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="783e0-104">Uwierzytelnianie między usługami</span><span class="sxs-lookup"><span data-stu-id="783e0-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="783e0-105">Uwierzytelnianie użytkowników końcowych</span><span class="sxs-lookup"><span data-stu-id="783e0-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="783e0-106">Azure Data Lake Store używa usługi Azure Active Directory do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="783e0-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="783e0-107">Przed tworzenia aplikacji, która współdziała z usługi Azure Data Lake Store i usługą Azure Data Lake Analytics, należy najpierw określić, jak tooauthenticate aplikacji z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="783e0-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="783e0-108">Witaj głównego dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="783e0-108">hello two main options available are:</span></span>

* <span data-ttu-id="783e0-109">Uwierzytelnianie użytkownika końcowego (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="783e0-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="783e0-110">Uwierzytelnianie między usługami</span><span class="sxs-lookup"><span data-stu-id="783e0-110">Service-to-service authentication</span></span>

<span data-ttu-id="783e0-111">Obie te opcje spowodować aplikacji dostarczanej z token OAuth 2.0, który pobiera dołączonych tooeach żądania tooAzure usługi Data Lake Store lub usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="783e0-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="783e0-112">Ten artykuł omówiono sposób tworzenia **natywnych aplikacji usługi Azure AD do uwierzytelniania użytkowników końcowych**.</span><span class="sxs-lookup"><span data-stu-id="783e0-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="783e0-113">Instrukcje konfiguracji aplikacji usługi Azure AD do usługi uwierzytelniania można znaleźć [do usługi uwierzytelniania za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="783e0-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="783e0-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="783e0-114">Prerequisites</span></span>
* <span data-ttu-id="783e0-115">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="783e0-115">An Azure subscription.</span></span> <span data-ttu-id="783e0-116">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="783e0-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="783e0-117">Do identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="783e0-117">Your subscription ID.</span></span> <span data-ttu-id="783e0-118">Można go pobrać z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="783e0-118">You can retrieve it from hello Azure Portal.</span></span> <span data-ttu-id="783e0-119">Na przykład jest dostępny w bloku konta usługi Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="783e0-119">For example, it is available from hello Data Lake Store account blade.</span></span>
  
    ![Pobierz identyfikator subskrypcji](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="783e0-121">Nazwa domeny usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="783e0-121">Your Azure AD domain name.</span></span> <span data-ttu-id="783e0-122">Można go pobrać aktywowania myszy hello w hello prawym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="783e0-122">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure Portal.</span></span> <span data-ttu-id="783e0-123">W poniższym zrzucie ekranu hello, nazwa domeny hello jest **contoso.onmicrosoft.com**, i hello identyfikatora GUID w nawiasach kwadratowych jest identyfikatorem hello dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="783e0-123">From hello screenshot below, hello domain name is **contoso.onmicrosoft.com**, and hello GUID within brackets is hello tenant ID.</span></span> 
  
    ![Uzyskaj domenę usługi AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="783e0-125">Uwierzytelnianie użytkowników końcowych</span><span class="sxs-lookup"><span data-stu-id="783e0-125">End-user authentication</span></span>
<span data-ttu-id="783e0-126">Jest to hello zalecane podejście, jeśli chcesz, aby toolog użytkowników końcowych w aplikacji tooyour za pomocą usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="783e0-126">This is hello recommended approach if you want an end-user toolog in tooyour application via Azure AD.</span></span> <span data-ttu-id="783e0-127">Aplikacja będzie w stanie tooaccess zasobów platformy Azure z hello poziomu dostępu hello przez użytkownika końcowego, który jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="783e0-127">Your application will be able tooaccess Azure resources with hello same level of access as hello end-user that logged in.</span></span> <span data-ttu-id="783e0-128">Użytkownik końcowy musi tooprovide poświadczeń okresowo w kolejności dla programu access toomaintain aplikacji.</span><span class="sxs-lookup"><span data-stu-id="783e0-128">Your end-user will need tooprovide their credentials periodically in order for your application toomaintain access.</span></span>

<span data-ttu-id="783e0-129">wynik Hello o hello przez użytkownika końcowego, zaloguj się za jest, że aplikacji znajduje się token dostępu i token odświeżania.</span><span class="sxs-lookup"><span data-stu-id="783e0-129">hello result of having hello end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="783e0-130">token dostępu Hello pobiera żądania dołączonych tooeach tooData Lake Store lub usługi Data Lake Analytics i jest ważna przez jedną godzinę domyślnie.</span><span class="sxs-lookup"><span data-stu-id="783e0-130">hello access token gets attached tooeach request made tooData Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="783e0-131">token odświeżania Hello mogą być używane tooobtain nowy token dostępu który jest ważne dla tygodni tootwo domyślnie, jeśli regularnie używane.</span><span class="sxs-lookup"><span data-stu-id="783e0-131">hello refresh token can be used tooobtain a new access token, and it is valid for up tootwo weeks by default, if used regularly.</span></span> <span data-ttu-id="783e0-132">Dwa różne podejścia służy do logowania użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="783e0-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-hello-oauth-20-pop-up"></a><span data-ttu-id="783e0-133">Za pomocą menu podręczne hello OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="783e0-133">Using hello OAuth 2.0 pop-up</span></span>
<span data-ttu-id="783e0-134">Aplikacja może wyzwolić podręczne autoryzacji OAuth 2.0, w których hello użytkownika końcowego można wprowadzić swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="783e0-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which hello end-user can enter their credentials.</span></span> <span data-ttu-id="783e0-135">Są one współdziała również z hello procesu uwierzytelniania dwuskładnikowego Azure AD (2FA), jeśli jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="783e0-135">This pop-up also works with hello Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="783e0-136">Ta metoda nie jest jeszcze obsługiwana w hello Azure AD Authentication Library (ADAL) dla języka Python lub Java.</span><span class="sxs-lookup"><span data-stu-id="783e0-136">This method is not yet supported in hello Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="783e0-137">Przekazywanie bezpośrednio w poświadczeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="783e0-137">Directly passing in user credentials</span></span>
<span data-ttu-id="783e0-138">Aplikacja może zapewnić bezpośrednio tooAzure poświadczeń użytkownika usługi AD.</span><span class="sxs-lookup"><span data-stu-id="783e0-138">Your application can directly provide user credentials tooAzure AD.</span></span> <span data-ttu-id="783e0-139">Ta metoda działa tylko z kontami użytkowników w organizacji identyfikator; nie jest zgodny z osobistego / kończy się rozszerzeniem "live ID" kont użytkowników, łącznie z tymi @outlook.com lub @live.com. Ponadto ta metoda nie jest zgodny z kontami użytkowników, które wymagają uwierzytelniania dwuskładnikowego Azure AD (2FA).</span><span class="sxs-lookup"><span data-stu-id="783e0-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com. Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-toouse-this-approach"></a><span data-ttu-id="783e0-140">Czego potrzebuję toouse to rozwiązanie?</span><span class="sxs-lookup"><span data-stu-id="783e0-140">What do I need toouse this approach?</span></span>
* <span data-ttu-id="783e0-141">Nazwa domeny w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="783e0-141">Azure AD domain name.</span></span> <span data-ttu-id="783e0-142">Jest to wymienione w hello wymaganie wstępne w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="783e0-142">This is already listed in hello prerequisite of this article.</span></span>
* <span data-ttu-id="783e0-143">Usługi Azure AD **aplikacji natywnej**</span><span class="sxs-lookup"><span data-stu-id="783e0-143">Azure AD **native application**</span></span>
* <span data-ttu-id="783e0-144">Identyfikator aplikacji natywnych aplikacji hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="783e0-144">Application ID for hello Azure AD native application</span></span>
* <span data-ttu-id="783e0-145">Identyfikator URI przekierowania dla hello natywnych aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="783e0-145">Redirect URI for hello Azure AD native application</span></span>
* <span data-ttu-id="783e0-146">Ustaw uprawnienia delegowane.</span><span class="sxs-lookup"><span data-stu-id="783e0-146">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="783e0-147">Krok 1: Tworzenie natywnych aplikacji usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="783e0-147">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="783e0-148">Tworzenie i konfigurowanie usługi Azure AD aplikacji natywnej do uwierzytelniania użytkowników końcowych z usługi Azure Data Lake Store za pomocą usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="783e0-148">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="783e0-149">Aby uzyskać instrukcje, zobacz [tworzy aplikację usługi Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="783e0-149">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="783e0-150">Podczas instrukcjami hello na powitania powyżej łącze, upewnij się, że wybrano **natywnego** dla typu aplikacji, jak pokazano na poniższym zrzucie ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="783e0-150">While following hello instructions at hello above link, make sure you select **Native** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="783e0-151">![Tworzenie aplikacji sieci web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "tworzenie natywnych aplikacji")</span><span class="sxs-lookup"><span data-stu-id="783e0-151">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="783e0-152">Krok 2: Uzyskiwanie identyfikatora aplikacji i identyfikator URI przekierowania</span><span class="sxs-lookup"><span data-stu-id="783e0-152">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="783e0-153">Zobacz [uzyskiwanie Identyfikatora aplikacji hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello identyfikator aplikacji (nazywane również identyfikator klienta hello w hello klasyczny portal Azure) natywnych aplikacji hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="783e0-153">See [Get hello application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello application id (also called hello client ID in hello Azure classic portal) of hello Azure AD native application.</span></span>

<span data-ttu-id="783e0-154">tooretrieve hello identyfikator URI przekierowania, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="783e0-154">tooretrieve hello redirect URI, follow hello steps below.</span></span>

1. <span data-ttu-id="783e0-155">Z hello portalu Azure, wybierz **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, a następnie znajdź i kliknij natywnych aplikacji hello Azure AD, nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="783e0-155">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="783e0-156">Z hello **ustawienia** kliknij bloku dla aplikacji hello **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="783e0-156">From hello **Settings** blade for hello application, click **Redirect URIs**.</span></span>

    ![Identyfikator URI przekierowania Get](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="783e0-158">Skopiuj wartość hello wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="783e0-158">Copy hello value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="783e0-159">Krok 3: Ustawianie uprawnień</span><span class="sxs-lookup"><span data-stu-id="783e0-159">Step 3: Set permissions</span></span>

1. <span data-ttu-id="783e0-160">Z hello portalu Azure, wybierz **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, a następnie znajdź i kliknij natywnych aplikacji hello Azure AD, nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="783e0-160">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="783e0-161">Z hello **ustawienia** kliknij bloku dla aplikacji hello **wymagane uprawnienia**, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="783e0-161">From hello **Settings** blade for hello application, click **Required permissions**, and then click **Add**.</span></span>

    ![Identyfikator klienta](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="783e0-163">W hello **dodać dostępu do interfejsu API** bloku, kliknij przycisk **wybierz interfejs API**, kliknij przycisk **usługi Azure Data Lake**, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="783e0-163">In hello **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![Identyfikator klienta](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="783e0-165">W hello **dodać dostępu do interfejsu API** bloku, kliknij przycisk **wybierz uprawnienia**, wybierz hello toogive pole wyboru **pełnego dostępu tooData Lake Store**, a następnie kliknij przycisk **wybierz** .</span><span class="sxs-lookup"><span data-stu-id="783e0-165">In hello **Add API Access** blade, click **Select permissions**, select hello check box toogive **Full access tooData Lake Store**, and then click **Select**.</span></span>

    ![Identyfikator klienta](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="783e0-167">Kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="783e0-167">Click **Done**.</span></span>

5. <span data-ttu-id="783e0-168">Powtarzania hello ostatnie dwa kroki toogrant uprawnienia dla **interfejs API zarządzania usługami Windows Azure** również.</span><span class="sxs-lookup"><span data-stu-id="783e0-168">Repeat hello last two steps toogrant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="783e0-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="783e0-169">Next steps</span></span>
<span data-ttu-id="783e0-170">W tym artykule tworzone natywnych aplikacji usługi Azure AD i zebranych informacji hello w aplikacjach klienckich tworzyć przy użyciu zestawu .NET SDK, zestaw SDK Java, interfejsu API REST,... itd. Można teraz kontynuować toohello następujące artykuły, które porozmawiać na temat sposobu toouse hello Azure AD w sieci web aplikacji toofirst uwierzytelniania w usłudze Data Lake Store i wykonywać inne operacje na powitania magazynu.</span><span class="sxs-lookup"><span data-stu-id="783e0-170">In this article you created an Azure AD native application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="783e0-171">Rozpoczynanie pracy z usługą Azure Data Lake Store z użyciem zestawu SDK .NET</span><span class="sxs-lookup"><span data-stu-id="783e0-171">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="783e0-172">Wprowadzenie do usługi Azure Data Lake Store przy użyciu zestawu SDK Java</span><span class="sxs-lookup"><span data-stu-id="783e0-172">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="783e0-173">Wprowadzenie do usługi Azure Data Lake Store za pomocą interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="783e0-173">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

