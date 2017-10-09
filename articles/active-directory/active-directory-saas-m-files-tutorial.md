---
title: 'Samouczek: Integracji Azure Active Directory z plikami M | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i pliki M."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="52460-103">Samouczek: Integracji Azure Active Directory z plikami M</span><span class="sxs-lookup"><span data-stu-id="52460-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="52460-104">Z tego samouczka, dowiesz się, jak toointegrate M-plików w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52460-104">In this tutorial, you learn how toointegrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52460-105">Integrowanie M pliki z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="52460-105">Integrating M-Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="52460-106">Można kontrolować w usłudze Azure AD, który ma dostęp tooM — pliki</span><span class="sxs-lookup"><span data-stu-id="52460-106">You can control in Azure AD who has access tooM-Files</span></span>
- <span data-ttu-id="52460-107">Aby umożliwić użytkownikom tooautomatically get zalogowane tooM — pliki (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="52460-107">You can enable your users tooautomatically get signed-on tooM-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52460-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="52460-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="52460-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52460-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52460-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="52460-110">Prerequisites</span></span>

<span data-ttu-id="52460-111">tooconfigure integracji usługi Azure AD z plikami M, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="52460-111">tooconfigure Azure AD integration with M-Files, you need hello following items:</span></span>

- <span data-ttu-id="52460-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="52460-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52460-113">Pliki M logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="52460-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52460-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="52460-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52460-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="52460-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52460-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="52460-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52460-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52460-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52460-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="52460-118">Scenario description</span></span>
<span data-ttu-id="52460-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="52460-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52460-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="52460-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52460-121">Dodawanie plików M z galerii hello</span><span class="sxs-lookup"><span data-stu-id="52460-121">Adding M-Files from hello gallery</span></span>
2. <span data-ttu-id="52460-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="52460-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-hello-gallery"></a><span data-ttu-id="52460-123">Dodawanie plików M z galerii hello</span><span class="sxs-lookup"><span data-stu-id="52460-123">Adding M-Files from hello gallery</span></span>
<span data-ttu-id="52460-124">tooconfigure hello integracji M plików do usługi Azure AD, należy tooadd M plików z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="52460-124">tooconfigure hello integration of M-Files into Azure AD, you need tooadd M-Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="52460-125">**tooadd M pliki z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="52460-125">**tooadd M-Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="52460-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="52460-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="52460-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="52460-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="52460-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="52460-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="52460-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="52460-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="52460-133">W polu wyszukiwania hello wpisz **pliki M**.</span><span class="sxs-lookup"><span data-stu-id="52460-133">In hello search box, type **M-Files**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="52460-135">W panelu wyników hello, wybierz **M pliki**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="52460-135">In hello results panel, select **M-Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52460-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="52460-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52460-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z plikami M, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="52460-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52460-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w plikach M jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52460-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in M-Files is tooa user in Azure AD.</span></span> <span data-ttu-id="52460-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w plikach M musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="52460-140">In other words, a link relationship between an Azure AD user and hello related user in M-Files needs toobe established.</span></span>

<span data-ttu-id="52460-141">W plikach M, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="52460-141">In M-Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="52460-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z plikami M, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="52460-142">tooconfigure and test Azure AD single sign-on with M-Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="52460-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="52460-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="52460-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="52460-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52460-145">**[Tworzenie użytkownika testowego pliki M](#creating-a-m-files-test-user)**  -toohave odpowiednikiem Britta Simona w plikach M toohello połączonej usługi Azure AD reprezentacja użytkownika.</span><span class="sxs-lookup"><span data-stu-id="52460-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - toohave a counterpart of Britta Simon in M-Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="52460-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="52460-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52460-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="52460-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52460-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="52460-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52460-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji M plików.</span><span class="sxs-lookup"><span data-stu-id="52460-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="52460-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z plikami M, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="52460-150">**tooconfigure Azure AD single sign-on with M-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="52460-151">W portalu Azure na powitania hello **M pliki** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="52460-151">In hello Azure portal, on hello **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="52460-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="52460-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="52460-155">Na powitania **adresy URL i pliki M domeny** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="52460-155">On hello **M-Files Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="52460-157">a.</span><span class="sxs-lookup"><span data-stu-id="52460-157">a.</span></span> <span data-ttu-id="52460-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="52460-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="52460-159">b.</span><span class="sxs-lookup"><span data-stu-id="52460-159">b.</span></span> <span data-ttu-id="52460-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="52460-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52460-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="52460-161">These values are not real.</span></span> <span data-ttu-id="52460-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="52460-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="52460-163">Skontaktuj się z [zespołem pomocy technicznej klienta pliki M](mailto:support@m-files.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="52460-163">Contact [M-Files Client support team](mailto:support@m-files.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="52460-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="52460-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="52460-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="52460-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52460-168">tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [zespołu obsługi plików M](mailto:support@m-files.com) i podaj hello pobrać metadanych.</span><span class="sxs-lookup"><span data-stu-id="52460-168">tooget SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them hello downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="52460-169">Wykonaj kroki dalej hello, jeśli chcesz tooconfigure logowania jednokrotnego dla Ciebie M pliku aplikacji komputerowych.</span><span class="sxs-lookup"><span data-stu-id="52460-169">Follow hello next steps if you want tooconfigure SSO for you M-File desktop application.</span></span> <span data-ttu-id="52460-170">Żadne dodatkowe czynności nie są wymagane, jeśli chcesz tylko tooconfigure logowania jednokrotnego dla wersji web M plików.</span><span class="sxs-lookup"><span data-stu-id="52460-170">No extra steps are required if you only want tooconfigure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="52460-171">Wykonaj hello dalej kroki tooconfigure hello M pliku aplikacji komputerowych tooenable rejestracji Jednokrotnej z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52460-171">Follow hello next steps tooconfigure hello M-File desktop application tooenable SSO with Azure AD.</span></span> <span data-ttu-id="52460-172">toodownload pliki M, przejdź zbyt[pobrać pliki M](https://www.m-files.com/en/download-latest-version) strony.</span><span class="sxs-lookup"><span data-stu-id="52460-172">toodownload M-Files, go too[M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="52460-173">Otwórz hello **ustawienia pulpitu pliki M** okna.</span><span class="sxs-lookup"><span data-stu-id="52460-173">Open hello **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="52460-174">Następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="52460-174">Then, click **Add**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="52460-176">Na powitania **właściwości połączenia magazynu dokumentu** okna, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="52460-176">On hello **Document Vault Connection Properties** window, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="52460-178">W obszarze hello typ sekcji serwera hello wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="52460-178">Under hello Server section type, hello values as follows:</span></span>  

    <span data-ttu-id="52460-179">a.</span><span class="sxs-lookup"><span data-stu-id="52460-179">a.</span></span> <span data-ttu-id="52460-180">Aby uzyskać **nazwa**, typ `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="52460-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="52460-181">b.</span><span class="sxs-lookup"><span data-stu-id="52460-181">b.</span></span> <span data-ttu-id="52460-182">Aby uzyskać **numer portu**, typ **4466**.</span><span class="sxs-lookup"><span data-stu-id="52460-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="52460-183">c.</span><span class="sxs-lookup"><span data-stu-id="52460-183">c.</span></span> <span data-ttu-id="52460-184">Aby uzyskać **protokołu**, wybierz pozycję **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="52460-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="52460-185">d.</span><span class="sxs-lookup"><span data-stu-id="52460-185">d.</span></span> <span data-ttu-id="52460-186">W hello **uwierzytelniania** pól, zaznacz **określonego użytkownika systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="52460-186">In hello **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="52460-187">Następnie zostanie wyświetlony monit o strony podpisywania.</span><span class="sxs-lookup"><span data-stu-id="52460-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="52460-188">Wstaw poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52460-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="52460-189">e.</span><span class="sxs-lookup"><span data-stu-id="52460-189">e.</span></span> <span data-ttu-id="52460-190">Dla hello **magazynu na serwerze**, wybierz hello odpowiedni magazyn na serwerze.</span><span class="sxs-lookup"><span data-stu-id="52460-190">For hello **Vault on Server**,  select hello corresponding vault on server.</span></span>
 
    <span data-ttu-id="52460-191">f.</span><span class="sxs-lookup"><span data-stu-id="52460-191">f.</span></span> <span data-ttu-id="52460-192">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="52460-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="52460-193">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="52460-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="52460-194">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="52460-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="52460-195">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52460-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52460-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="52460-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="52460-197">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="52460-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="52460-199">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="52460-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="52460-200">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="52460-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52460-202">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="52460-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52460-204">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="52460-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52460-206">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="52460-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52460-208">a.</span><span class="sxs-lookup"><span data-stu-id="52460-208">a.</span></span> <span data-ttu-id="52460-209">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52460-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52460-210">b.</span><span class="sxs-lookup"><span data-stu-id="52460-210">b.</span></span> <span data-ttu-id="52460-211">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52460-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52460-212">c.</span><span class="sxs-lookup"><span data-stu-id="52460-212">c.</span></span> <span data-ttu-id="52460-213">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="52460-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="52460-214">d.</span><span class="sxs-lookup"><span data-stu-id="52460-214">d.</span></span> <span data-ttu-id="52460-215">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="52460-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="52460-216">Tworzenie użytkownika testowego M — pliki</span><span class="sxs-lookup"><span data-stu-id="52460-216">Creating a M-Files test user</span></span>

<span data-ttu-id="52460-217">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w plikach M.</span><span class="sxs-lookup"><span data-stu-id="52460-217">hello objective of this section is toocreate a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="52460-218">Praca z [zespołu obsługi plików M](mailto:support@m-files.com) tooadd hello użytkowników w hello M plików.</span><span class="sxs-lookup"><span data-stu-id="52460-218">Work with  [M-Files support team](mailto:support@m-files.com) tooadd hello users in hello M-Files.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="52460-219">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="52460-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="52460-220">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooM — pliki.</span><span class="sxs-lookup"><span data-stu-id="52460-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooM-Files.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="52460-222">**tooassign Simona Britta tooM pliki, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="52460-222">**tooassign Britta Simon tooM-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="52460-223">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="52460-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="52460-225">Z listy aplikacji hello wybierz **pliki M**.</span><span class="sxs-lookup"><span data-stu-id="52460-225">In hello applications list, select **M-Files**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="52460-227">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="52460-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="52460-229">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="52460-229">Click **Add** button.</span></span> <span data-ttu-id="52460-230">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="52460-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="52460-232">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="52460-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="52460-233">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="52460-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52460-234">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="52460-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52460-235">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="52460-235">Testing single sign-on</span></span>

<span data-ttu-id="52460-236">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="52460-236">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="52460-237">Po kliknięciu hello pliki M kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour M pliki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="52460-237">When you click hello M-Files tile in hello Access Panel, you should get automatically signed-on tooyour M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="52460-238">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="52460-238">Additional resources</span></span>

* [<span data-ttu-id="52460-239">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52460-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52460-240">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52460-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

