---
title: 'Samouczek: Azure Active Directory integracji z portalu osobiste Mimecast | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między Mimecast osobistych portalu i usługi Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="e9780-103">Samouczek: Integracji Azure Active Directory z Mimecast osobistych portalu</span><span class="sxs-lookup"><span data-stu-id="e9780-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="e9780-104">Z tego samouczka, dowiesz się, jak toointegrate Mimecast Portal osobiste z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9780-104">In this tutorial, you learn how toointegrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9780-105">Integrowanie portalu osobiste Mimecast z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e9780-105">Integrating Mimecast Personal Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e9780-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooMimecast osobistych portalu</span><span class="sxs-lookup"><span data-stu-id="e9780-106">You can control in Azure AD who has access tooMimecast Personal Portal</span></span>
- <span data-ttu-id="e9780-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMimecast osobistych Portal (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9780-107">You can enable your users tooautomatically get signed-on tooMimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9780-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e9780-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e9780-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9780-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9780-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e9780-110">Prerequisites</span></span>

<span data-ttu-id="e9780-111">tooconfigure integracji usługi Azure AD z portalu osobiste Mimecast należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e9780-111">tooconfigure Azure AD integration with Mimecast Personal Portal, you need hello following items:</span></span>

- <span data-ttu-id="e9780-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9780-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9780-113">Mimecast osobistych portalu rejestracji jednokrotnej włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e9780-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9780-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e9780-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9780-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e9780-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9780-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e9780-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9780-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9780-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9780-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e9780-118">Scenario description</span></span>
<span data-ttu-id="e9780-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e9780-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9780-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e9780-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9780-121">Dodawanie portalu osobiste Mimecast z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e9780-121">Adding Mimecast Personal Portal from hello gallery</span></span>
2. <span data-ttu-id="e9780-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e9780-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a><span data-ttu-id="e9780-123">Dodawanie portalu osobiste Mimecast z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e9780-123">Adding Mimecast Personal Portal from hello gallery</span></span>
<span data-ttu-id="e9780-124">tooconfigure hello integrację Mimecast osobistych portalu usługi Azure AD, należy tooadd Mimecast Portal osobistych z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e9780-124">tooconfigure hello integration of Mimecast Personal Portal into Azure AD, you need tooadd Mimecast Personal Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e9780-125">**tooadd Mimecast Portal osobistych z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e9780-125">**tooadd Mimecast Personal Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9780-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e9780-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e9780-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e9780-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e9780-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e9780-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e9780-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9780-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e9780-133">W polu wyszukiwania hello wpisz **Portal osobiste Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="e9780-133">In hello search box, type **Mimecast Personal Portal**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="e9780-135">W panelu wyników hello, wybierz **Mimecast osobistych portalu**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e9780-135">In hello results panel, select **Mimecast Personal Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9780-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e9780-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9780-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z portalem osobiste Mimecast w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e9780-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9780-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w portalu osobiste Mimecast jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9780-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Personal Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="e9780-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w portalu osobiste Mimecast musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e9780-140">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Personal Portal needs toobe established.</span></span>

<span data-ttu-id="e9780-141">W portalu osobiste Mimecast, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e9780-141">In Mimecast Personal Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e9780-142">tooconfigure i test usługi Azure AD rejestracji jednokrotnej z portalu osobiste Mimecast należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="e9780-142">tooconfigure and test Azure AD single sign-on with Mimecast Personal Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e9780-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e9780-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e9780-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e9780-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9780-145">**[Tworzenie użytkownika testowego portalu osobiste Mimecast](#creating-a-mimecast-personal-portal-test-user)**  -toohave odpowiednikiem Simona Britta w portalu osobiste Mimecast, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e9780-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - toohave a counterpart of Britta Simon in Mimecast Personal Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9780-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e9780-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9780-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e9780-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9780-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e9780-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9780-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Portal osobiste Mimecast.</span><span class="sxs-lookup"><span data-stu-id="e9780-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="e9780-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Mimecast osobistych portalu, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e9780-150">**tooconfigure Azure AD single sign-on with Mimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9780-151">W portalu Azure na powitania hello **Portal osobiste Mimecast** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e9780-151">In hello Azure portal, on hello **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e9780-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e9780-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="e9780-155">Na powitania **Mimecast osobistych portalu domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e9780-155">On hello **Mimecast Personal Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="e9780-157">a.</span><span class="sxs-lookup"><span data-stu-id="e9780-157">a.</span></span> <span data-ttu-id="e9780-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="e9780-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="e9780-159">b.</span><span class="sxs-lookup"><span data-stu-id="e9780-159">b.</span></span> <span data-ttu-id="e9780-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="e9780-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="e9780-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e9780-161">These values are not real.</span></span> <span data-ttu-id="e9780-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="e9780-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e9780-163">Skontaktuj się z [zespołem pomocy technicznej osobiste klienta portalu Mimecast](https://www.mimecast.com/customer-success/technical-support/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e9780-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) tooget these values.</span></span> 
 


4. <span data-ttu-id="e9780-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e9780-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="e9780-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e9780-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e9780-168">Na powitania **Mimecast osobistych konfiguracji portalu** kliknij **skonfigurować Portal osobiste Mimecast** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e9780-168">On hello **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e9780-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e9780-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="e9780-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do portalu osobiste Mimecast jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e9780-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="e9780-172">Przejdź za**usług \> aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e9780-172">Go too**Services \> Applications**.</span></span>
   
    <span data-ttu-id="e9780-173">![Aplikacje](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="e9780-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="e9780-174">Kliknij przycisk **profile uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="e9780-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="e9780-175">![Profile uwierzytelniania](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "profile uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="e9780-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="e9780-176">Kliknij przycisk **nowy profil uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="e9780-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="e9780-177">![Nowy profil uwierzytelniania](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "nowy profil uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="e9780-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="e9780-178">W hello **profilu uwierzytelniania** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e9780-178">In hello **Authentication Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e9780-179">![Profil uwierzytelniania](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "profilu uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="e9780-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="e9780-180">a.</span><span class="sxs-lookup"><span data-stu-id="e9780-180">a.</span></span> <span data-ttu-id="e9780-181">W hello **opis** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e9780-181">In hello **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="e9780-182">b.</span><span class="sxs-lookup"><span data-stu-id="e9780-182">b.</span></span> <span data-ttu-id="e9780-183">Wybierz **wymusić uwierzytelnianie SAML portalu osobiste Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="e9780-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="e9780-184">c.</span><span class="sxs-lookup"><span data-stu-id="e9780-184">c.</span></span> <span data-ttu-id="e9780-185">Jako **dostawcy**, wybierz pozycję **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9780-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="e9780-186">d.</span><span class="sxs-lookup"><span data-stu-id="e9780-186">d.</span></span> <span data-ttu-id="e9780-187">W **adres URL wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e9780-187">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e9780-188">e.</span><span class="sxs-lookup"><span data-stu-id="e9780-188">e.</span></span> <span data-ttu-id="e9780-189">W **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e9780-189">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e9780-190">f.</span><span class="sxs-lookup"><span data-stu-id="e9780-190">f.</span></span> <span data-ttu-id="e9780-191">W **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e9780-191">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e9780-192">g.</span><span class="sxs-lookup"><span data-stu-id="e9780-192">g.</span></span> <span data-ttu-id="e9780-193">Otwórz z **base-64** zakodowany certyfikat w Notatniku pobrany z portalu Azure, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy tożsamości (metadanymi)** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="e9780-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="e9780-194">h.</span><span class="sxs-lookup"><span data-stu-id="e9780-194">h.</span></span> <span data-ttu-id="e9780-195">Wybierz **Zezwalaj funkcji logowania jednokrotnego w**.</span><span class="sxs-lookup"><span data-stu-id="e9780-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="e9780-196">i.</span><span class="sxs-lookup"><span data-stu-id="e9780-196">i.</span></span> <span data-ttu-id="e9780-197">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e9780-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e9780-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e9780-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e9780-199">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e9780-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e9780-200">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9780-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9780-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9780-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9780-202">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e9780-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e9780-204">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e9780-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9780-205">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e9780-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9780-207">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e9780-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9780-209">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9780-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9780-211">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e9780-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9780-213">a.</span><span class="sxs-lookup"><span data-stu-id="e9780-213">a.</span></span> <span data-ttu-id="e9780-214">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9780-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9780-215">b.</span><span class="sxs-lookup"><span data-stu-id="e9780-215">b.</span></span> <span data-ttu-id="e9780-216">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e9780-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9780-217">c.</span><span class="sxs-lookup"><span data-stu-id="e9780-217">c.</span></span> <span data-ttu-id="e9780-218">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e9780-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e9780-219">d.</span><span class="sxs-lookup"><span data-stu-id="e9780-219">d.</span></span> <span data-ttu-id="e9780-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e9780-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="e9780-221">Tworzenie użytkownika testowego Mimecast osobistych portalu</span><span class="sxs-lookup"><span data-stu-id="e9780-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="e9780-222">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do portalu osobiste Mimecast muszą mieć przydzielone do portalu osobiste Mimecast.</span><span class="sxs-lookup"><span data-stu-id="e9780-222">In order tooenable Azure AD users toolog into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="e9780-223">W przypadku hello Mimecast osobistych portalu inicjowania obsługi administracyjnej jest zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="e9780-223">In hello case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="e9780-224">Należy tooregister domeny, przed przystąpieniem do tworzenia użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e9780-224">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="e9780-225">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e9780-225">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9780-226">Zaloguj się na tooyour **Portal osobiste Mimecast** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e9780-226">Sign on tooyour **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="e9780-227">Przejdź za**katalogów \> wewnętrzne**.</span><span class="sxs-lookup"><span data-stu-id="e9780-227">Go too**Directories \> Internal**.</span></span>
   
    <span data-ttu-id="e9780-228">![Katalogi](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "katalogów")</span><span class="sxs-lookup"><span data-stu-id="e9780-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="e9780-229">Kliknij przycisk **zarejestrować nową domenę**.</span><span class="sxs-lookup"><span data-stu-id="e9780-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="e9780-230">![Zarejestrować nową domenę](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "zarejestrować nową domenę")</span><span class="sxs-lookup"><span data-stu-id="e9780-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="e9780-231">Po utworzeniu nowej domeny, kliknij przycisk **nowy adres**.</span><span class="sxs-lookup"><span data-stu-id="e9780-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="e9780-232">![Nowy adres](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "nowy adres")</span><span class="sxs-lookup"><span data-stu-id="e9780-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="e9780-233">W hello nowego okna dialogowego adres i wykonaj następujące kroki prawidłowy Azure hello konta AD ma tooprovision:</span><span class="sxs-lookup"><span data-stu-id="e9780-233">In hello new address dialog, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="e9780-234">![Zapisz](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Zapisz")</span><span class="sxs-lookup"><span data-stu-id="e9780-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="e9780-235">a.</span><span class="sxs-lookup"><span data-stu-id="e9780-235">a.</span></span> <span data-ttu-id="e9780-236">W hello **adres E-mail** pole tekstowe, typ **adres E-mail** hello użytkownika jako  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="e9780-236">In hello **Email Address** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="e9780-237">b.</span><span class="sxs-lookup"><span data-stu-id="e9780-237">b.</span></span> <span data-ttu-id="e9780-238">W hello **globalną nazwę** pole tekstowe, hello typu **username** jako **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9780-238">In hello **Global Name** textbox, type hello **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="e9780-239">c.</span><span class="sxs-lookup"><span data-stu-id="e9780-239">c.</span></span> <span data-ttu-id="e9780-240">W hello **hasło**, i **Potwierdź hasło** pól tekstowych, hello typu **hasło** hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e9780-240">In hello **Password**, and **Confirm Password** textboxes, type hello **Password** of hello user.</span></span>
   
    <span data-ttu-id="e9780-241">b.</span><span class="sxs-lookup"><span data-stu-id="e9780-241">b.</span></span> <span data-ttu-id="e9780-242">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e9780-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="e9780-243">Można użyć dowolnego inne narzędzia do tworzenia konta użytkownika portalu osobiste Mimecast lub interfejsów API dostarczonych przez konta użytkowników usługi Azure AD tooprovision Mimecast osobistych portalu.</span><span class="sxs-lookup"><span data-stu-id="e9780-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e9780-244">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9780-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e9780-245">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMimecast osobistych portalu.</span><span class="sxs-lookup"><span data-stu-id="e9780-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Personal Portal.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e9780-247">**tooassign tooMimecast Simona Britta osobistych portalu, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e9780-247">**tooassign Britta Simon tooMimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9780-248">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e9780-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e9780-250">Z listy aplikacji hello wybierz **Portal osobiste Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="e9780-250">In hello applications list, select **Mimecast Personal Portal**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="e9780-252">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e9780-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e9780-254">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e9780-254">Click **Add** button.</span></span> <span data-ttu-id="e9780-255">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9780-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e9780-257">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e9780-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e9780-258">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9780-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9780-259">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9780-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e9780-260">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e9780-260">Testing single sign-on</span></span>
<span data-ttu-id="e9780-261">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e9780-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e9780-262">Po kliknięciu kafelka portalu osobiste Mimecast hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Portal osobiste Mimecast aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e9780-262">When you click hello Mimecast Personal Portal tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Personal Portal application.</span></span> <span data-ttu-id="e9780-263">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e9780-263">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e9780-264">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e9780-264">Additional resources</span></span>

* [<span data-ttu-id="e9780-265">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9780-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9780-266">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9780-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

