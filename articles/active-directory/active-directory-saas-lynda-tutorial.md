---
title: 'Samouczek: Integracji Azure Active Directory z witryny Lynda.com | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i witryny Lynda.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: fb8d7824e5121da79e9248393b0cbcb0efaffec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="4a2fb-103">Samouczek: Integracji Azure Active Directory z witryny Lynda.com</span><span class="sxs-lookup"><span data-stu-id="4a2fb-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="4a2fb-104">Z tego samouczka, dowiesz się, jak toointegrate witryny Lynda.com w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a2fb-104">In this tutorial, you learn how toointegrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a2fb-105">Integracja z usługą Azure AD witryny Lynda.com zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4a2fb-105">Integrating Lynda.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4a2fb-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLynda.com</span><span class="sxs-lookup"><span data-stu-id="4a2fb-106">You can control in Azure AD who has access tooLynda.com</span></span>
- <span data-ttu-id="4a2fb-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLynda.com (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a2fb-107">You can enable your users tooautomatically get signed-on tooLynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a2fb-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4a2fb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4a2fb-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a2fb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a2fb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4a2fb-110">Prerequisites</span></span>

<span data-ttu-id="4a2fb-111">tooconfigure integracji z usługą Azure AD z witryny Lynda.com należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4a2fb-111">tooconfigure Azure AD integration with Lynda.com, you need hello following items:</span></span>

- <span data-ttu-id="4a2fb-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a2fb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a2fb-113">Witryny Lynda.com jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4a2fb-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a2fb-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a2fb-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4a2fb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a2fb-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a2fb-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a2fb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a2fb-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4a2fb-118">Scenario description</span></span>
<span data-ttu-id="4a2fb-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a2fb-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4a2fb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a2fb-121">Dodawanie witryny Lynda.com z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4a2fb-121">Adding Lynda.com from hello gallery</span></span>
2. <span data-ttu-id="4a2fb-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4a2fb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-hello-gallery"></a><span data-ttu-id="4a2fb-123">Dodawanie witryny Lynda.com z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4a2fb-123">Adding Lynda.com from hello gallery</span></span>
<span data-ttu-id="4a2fb-124">tooconfigure hello integracji witryny Lynda.com do usługi Azure AD, należy tooadd witryny Lynda.com z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-124">tooconfigure hello integration of Lynda.com into Azure AD, you need tooadd Lynda.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4a2fb-125">**tooadd witryny Lynda.com z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4a2fb-125">**tooadd Lynda.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a2fb-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4a2fb-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4a2fb-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4a2fb-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4a2fb-133">W polu wyszukiwania hello wpisz **witryny Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-133">In hello search box, type **Lynda.com**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="4a2fb-135">W panelu wyników hello zaznacz **witryny Lynda.com**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-135">In hello results panel, select **Lynda.com**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a2fb-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4a2fb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a2fb-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z witryny Lynda.com oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="4a2fb-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4a2fb-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w witryny Lynda.com jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lynda.com is tooa user in Azure AD.</span></span> <span data-ttu-id="4a2fb-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w witryny Lynda.com musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-140">In other words, a link relationship between an Azure AD user and hello related user in Lynda.com needs toobe established.</span></span>

<span data-ttu-id="4a2fb-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w witryny Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lynda.com.</span></span>

<span data-ttu-id="4a2fb-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z witryny Lynda.com, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4a2fb-142">tooconfigure and test Azure AD single sign-on with Lynda.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4a2fb-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4a2fb-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4a2fb-145">**[Tworzenie użytkownika testowego witryny Lynda.com](#creating-a-lyndacom-test-user)**  -toohave odpowiednikiem Simona Britta w witryny Lynda.com, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - toohave a counterpart of Britta Simon in Lynda.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4a2fb-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4a2fb-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a2fb-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4a2fb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a2fb-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji witryny Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="4a2fb-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z witryny Lynda.com, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4a2fb-150">**tooconfigure Azure AD single sign-on with Lynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a2fb-151">W portalu Azure na powitania hello **witryny Lynda.com** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-151">In hello Azure portal, on hello **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4a2fb-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="4a2fb-155">Na powitania **witryny Lynda.com domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4a2fb-155">On hello **Lynda.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="4a2fb-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="4a2fb-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4a2fb-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-158">This value is not real.</span></span> <span data-ttu-id="4a2fb-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4a2fb-160">Skontaktuj się z [zespołem pomocy technicznej witryny Lynda.com klienta](https://www.linkedin.com/help/lynda/ask) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) tooget these values.</span></span> 
 
4. <span data-ttu-id="4a2fb-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="4a2fb-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4a2fb-165">tooconfigure rejestracji jednokrotnej w **witryny Lynda.com** strony, należy pobrać hello toosend **XML metadanych** [pomocy technicznej witryny Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="4a2fb-165">tooconfigure single sign-on on **Lynda.com** side, you need toosend hello downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a2fb-166">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a2fb-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a2fb-167">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4a2fb-169">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4a2fb-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a2fb-170">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a2fb-172">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a2fb-174">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a2fb-176">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4a2fb-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a2fb-178">a.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-178">a.</span></span> <span data-ttu-id="4a2fb-179">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a2fb-180">b.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-180">b.</span></span> <span data-ttu-id="4a2fb-181">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a2fb-182">c.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-182">c.</span></span> <span data-ttu-id="4a2fb-183">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4a2fb-184">d.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-184">d.</span></span> <span data-ttu-id="4a2fb-185">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="4a2fb-186">Tworzenie użytkownika testowego witryny Lynda.com</span><span class="sxs-lookup"><span data-stu-id="4a2fb-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="4a2fb-187">Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-187">There is no action item for you tooconfigure user provisioning tooLynda.com.</span></span>  
<span data-ttu-id="4a2fb-188">Gdy przypisany użytkownik podejmie próbę toolog w tooLynda.com za pomocą panelu dostępu hello, witryny Lynda.com sprawdza, czy istnieje hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-188">When an assigned user tries toolog in tooLynda.com using hello access panel, Lynda.com checks whether hello user exists.</span></span>  

<span data-ttu-id="4a2fb-189">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez witryny Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="4a2fb-190">Możesz użyć innych witryny Lynda.com użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision witryny Lynda.com kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4a2fb-191">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a2fb-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4a2fb-192">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLynda.com.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4a2fb-194">**tooassign tooLynda.com Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4a2fb-194">**tooassign Britta Simon tooLynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a2fb-195">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4a2fb-197">Z listy aplikacji hello wybierz **witryny Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-197">In hello applications list, select **Lynda.com**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="4a2fb-199">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4a2fb-201">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-201">Click **Add** button.</span></span> <span data-ttu-id="4a2fb-202">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4a2fb-204">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4a2fb-205">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4a2fb-206">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4a2fb-207">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4a2fb-207">Testing single sign-on</span></span>

<span data-ttu-id="4a2fb-208">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="4a2fb-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="4a2fb-209">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4a2fb-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4a2fb-210">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4a2fb-210">Additional resources</span></span>

* [<span data-ttu-id="4a2fb-211">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a2fb-211">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a2fb-212">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4a2fb-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

