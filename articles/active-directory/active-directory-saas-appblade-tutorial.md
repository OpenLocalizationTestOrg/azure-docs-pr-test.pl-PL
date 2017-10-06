---
title: 'Samouczek: Integracji Azure Active Directory z AppBlade | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i AppBlade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 06f3d8fcee97945c867bca6f3aebe15ecef04617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="ff17a-103">Samouczek: Integracji Azure Active Directory z AppBlade</span><span class="sxs-lookup"><span data-stu-id="ff17a-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="ff17a-104">Z tego samouczka, dowiesz się, jak toointegrate AppBlade w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff17a-104">In this tutorial, you learn how toointegrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff17a-105">Integracja z usługą Azure AD AppBlade zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ff17a-105">Integrating AppBlade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ff17a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAppBlade</span><span class="sxs-lookup"><span data-stu-id="ff17a-106">You can control in Azure AD who has access tooAppBlade</span></span>
- <span data-ttu-id="ff17a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAppBlade (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff17a-107">You can enable your users tooautomatically get signed-on tooAppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff17a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ff17a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ff17a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff17a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff17a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ff17a-110">Prerequisites</span></span>

<span data-ttu-id="ff17a-111">tooconfigure integracji z usługą Azure AD z AppBlade należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ff17a-111">tooconfigure Azure AD integration with AppBlade, you need hello following items:</span></span>

- <span data-ttu-id="ff17a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff17a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff17a-113">AppBlade jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ff17a-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff17a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ff17a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff17a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ff17a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff17a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ff17a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff17a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff17a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff17a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ff17a-118">Scenario description</span></span>
<span data-ttu-id="ff17a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ff17a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff17a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ff17a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff17a-121">Dodawanie AppBlade z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ff17a-121">Adding AppBlade from hello gallery</span></span>
2. <span data-ttu-id="ff17a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ff17a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-hello-gallery"></a><span data-ttu-id="ff17a-123">Dodawanie AppBlade z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ff17a-123">Adding AppBlade from hello gallery</span></span>
<span data-ttu-id="ff17a-124">tooconfigure hello integracji AppBlade do usługi Azure AD, należy tooadd AppBlade z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ff17a-124">tooconfigure hello integration of AppBlade into Azure AD, you need tooadd AppBlade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ff17a-125">**tooadd AppBlade z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ff17a-125">**tooadd AppBlade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff17a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ff17a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ff17a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ff17a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ff17a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff17a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ff17a-133">W polu wyszukiwania hello wpisz **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-133">In hello search box, type **AppBlade**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="ff17a-135">W panelu wyników hello zaznacz **AppBlade**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ff17a-135">In hello results panel, select **AppBlade**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff17a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ff17a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff17a-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AppBlade na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="ff17a-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ff17a-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w AppBlade jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff17a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppBlade is tooa user in Azure AD.</span></span> <span data-ttu-id="ff17a-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w AppBlade musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ff17a-140">In other words, a link relationship between an Azure AD user and hello related user in AppBlade needs toobe established.</span></span>

<span data-ttu-id="ff17a-141">W AppBlade, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ff17a-141">In AppBlade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ff17a-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z AppBlade, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ff17a-142">tooconfigure and test Azure AD single sign-on with AppBlade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ff17a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ff17a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ff17a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ff17a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff17a-145">**[Tworzenie użytkownika testowego AppBlade](#creating-an-appblade-test-user)**  -toohave odpowiednikiem Simona Britta w AppBlade, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ff17a-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - toohave a counterpart of Britta Simon in AppBlade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ff17a-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ff17a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff17a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ff17a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff17a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ff17a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff17a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji AppBlade.</span><span class="sxs-lookup"><span data-stu-id="ff17a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="ff17a-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z AppBlade, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ff17a-150">**tooconfigure Azure AD single sign-on with AppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff17a-151">W portalu Azure na powitania hello **AppBlade** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-151">In hello Azure portal, on hello **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ff17a-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ff17a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="ff17a-155">Na powitania **AppBlade domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ff17a-155">On hello **AppBlade Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="ff17a-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="ff17a-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ff17a-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ff17a-158">This value is not real.</span></span> <span data-ttu-id="ff17a-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="ff17a-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ff17a-160">Skontaktuj się z [zespołem pomocy technicznej klienta AppBlade](mailto:support@appblade.com) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="ff17a-160">Contact [AppBlade Client support team](mailto:support@appblade.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="ff17a-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ff17a-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="ff17a-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff17a-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ff17a-165">tooconfigure rejestracji jednokrotnej w **AppBlade** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="ff17a-165">tooconfigure single sign-on on **AppBlade** side, you need toosend hello downloaded **Metadata XML** too[AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="ff17a-166">Ponadto poproś ich tooconfigure hello **adres URL wystawcy logowania jednokrotnego** jako `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="ff17a-166">Also, please ask them tooconfigure hello **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="ff17a-167">To ustawienie jest wymagane dla toowork rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ff17a-167">This setting is required for single sign-on toowork.</span></span>


> [!TIP]
> <span data-ttu-id="ff17a-168">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ff17a-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ff17a-169">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ff17a-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ff17a-170">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ff17a-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff17a-171">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff17a-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff17a-172">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ff17a-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ff17a-174">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ff17a-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff17a-175">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ff17a-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff17a-177">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff17a-179">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff17a-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff17a-181">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ff17a-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff17a-183">a.</span><span class="sxs-lookup"><span data-stu-id="ff17a-183">a.</span></span> <span data-ttu-id="ff17a-184">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff17a-185">b.</span><span class="sxs-lookup"><span data-stu-id="ff17a-185">b.</span></span> <span data-ttu-id="ff17a-186">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ff17a-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff17a-187">c.</span><span class="sxs-lookup"><span data-stu-id="ff17a-187">c.</span></span> <span data-ttu-id="ff17a-188">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ff17a-189">d.</span><span class="sxs-lookup"><span data-stu-id="ff17a-189">d.</span></span> <span data-ttu-id="ff17a-190">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="ff17a-191">Tworzenie użytkownika testowego AppBlade</span><span class="sxs-lookup"><span data-stu-id="ff17a-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="ff17a-192">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w AppBlade.</span><span class="sxs-lookup"><span data-stu-id="ff17a-192">hello objective of this section is toocreate a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="ff17a-193">AppBlade obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="ff17a-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="ff17a-194">**Upewnij się, że nazwa domeny jest skonfigurowany z AppBlade dla Inicjowanie obsługi użytkowników. Po tym tylko hello just in time aprowizacji użytkowników działa.**</span><span class="sxs-lookup"><span data-stu-id="ff17a-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only hello just-in-time user provisioning works.**</span></span>

<span data-ttu-id="ff17a-195">Jeśli adres e-mail kończąc domeny hello skonfigurowanych przez AppBlade dla tego konta, a następnie hello użytkownika zostaną automatycznie dołączone jako element członkowski o hello poziomu uprawnień, które można określić konta hello jest hello użytkownika, które jest jednym z "Basic" (podstawowe użytkownika, który można zainstalować tylko aplikacje), "Członek zespołu" (użytkownik, który można przesłać nowe wersje aplikacji i zarządzanie projektami) lub "Administrator" (Administrator o pełnych uprawnieniach uprawnienia toohello konto).</span><span class="sxs-lookup"><span data-stu-id="ff17a-195">If hello user has an email address ending with hello domain configured by AppBlade for your account, then hello user will automatically join hello account as a member with hello permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges toohello account).</span></span> <span data-ttu-id="ff17a-196">Zwykle będzie wybierz Basic i promować użytkowników ręcznie za pośrednictwem logowania administratora (AppBlade wcześniej musi tooconfigure logowania administratora pocztą e-mail lub podwyższyć poziom użytkownika w imieniu klienta na powitania po logowania).</span><span class="sxs-lookup"><span data-stu-id="ff17a-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs tooconfigure either an email-based admin login in advance or promote a user on behalf of hello customer after login).</span></span>

<span data-ttu-id="ff17a-197">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ff17a-197">There is no action item for you in this section.</span></span> <span data-ttu-id="ff17a-198">Nowy użytkownik jest tworzona podczas próby tooaccess AppBlade, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="ff17a-198">A new user is created during an attempt tooaccess AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="ff17a-199">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="ff17a-199">If you need toocreate a user manually, you need toocontact hello [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ff17a-200">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff17a-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ff17a-201">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAppBlade.</span><span class="sxs-lookup"><span data-stu-id="ff17a-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppBlade.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ff17a-203">**tooassign tooAppBlade Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ff17a-203">**tooassign Britta Simon tooAppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff17a-204">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ff17a-206">Z listy aplikacji hello wybierz **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-206">In hello applications list, select **AppBlade**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="ff17a-208">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ff17a-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ff17a-210">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff17a-210">Click **Add** button.</span></span> <span data-ttu-id="ff17a-211">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff17a-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ff17a-213">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ff17a-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ff17a-214">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff17a-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff17a-215">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff17a-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ff17a-216">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ff17a-216">Testing single sign-on</span></span>

<span data-ttu-id="ff17a-217">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ff17a-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="ff17a-218">Po kliknięciu kafelka AppBlade hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour AppBlade aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ff17a-218">When you click hello AppBlade tile in hello Access Panel, you should get automatically signed-on tooyour AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ff17a-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ff17a-219">Additional resources</span></span>

* [<span data-ttu-id="ff17a-220">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff17a-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff17a-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff17a-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

