---
title: "Samouczek: Integrowanie usługi Azure Active Directory z vxMaintain | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="2e7f5-103">Samouczek: Integrowanie usługi Azure Active Directory z vxMaintain</span><span class="sxs-lookup"><span data-stu-id="2e7f5-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="2e7f5-104">Z tego samouczka, dowiesz się, jak vxMaintain toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e7f5-104">In this tutorial, you learn how toointegrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e7f5-105">Integracja ta zapewnia kilka istotnych korzyści.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-105">This integration provides several important benefits.</span></span> <span data-ttu-id="2e7f5-106">Możesz:</span><span class="sxs-lookup"><span data-stu-id="2e7f5-106">You can:</span></span>

- <span data-ttu-id="2e7f5-107">Formant w usłudze Azure AD, kto ma dostęp do toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-107">Control in Azure AD who has access toovxMaintain.</span></span>
- <span data-ttu-id="2e7f5-108">Włącz użytkowników tooautomatically logowania toovxMaintain z logowaniem jednokrotnym (SSO) za pomocą ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-108">Enable your users tooautomatically sign in toovxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="2e7f5-109">Zarządzanie kont w jednej centralnej lokalizacji: hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="2e7f5-110">toolearn więcej informacji na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e7f5-110">toolearn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e7f5-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2e7f5-111">Prerequisites</span></span>

<span data-ttu-id="2e7f5-112">tooconfigure integracji z usługą Azure AD z vxMaintain należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2e7f5-112">tooconfigure Azure AD integration with vxMaintain, you need hello following items:</span></span>

- <span data-ttu-id="2e7f5-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e7f5-113">An Azure AD subscription</span></span>
- <span data-ttu-id="2e7f5-114">VxMaintain logowanie Jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2e7f5-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e7f5-115">Podczas testowania czynności hello w tym samouczku, firma Microsoft zaleca, nie używaj do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-115">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="2e7f5-116">kroki hello tootest w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2e7f5-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="2e7f5-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e7f5-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e7f5-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e7f5-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2e7f5-119">Scenario description</span></span>
<span data-ttu-id="2e7f5-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="2e7f5-121">Scenariusz Hello, w tym samouczku przedstawiono składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2e7f5-121">hello scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="2e7f5-122">Dodawanie vxMaintain z galerii hello</span><span class="sxs-lookup"><span data-stu-id="2e7f5-122">Adding vxMaintain from hello gallery</span></span>
* <span data-ttu-id="2e7f5-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2e7f5-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-hello-gallery"></a><span data-ttu-id="2e7f5-124">Dodaj vxMaintain z galerii hello</span><span class="sxs-lookup"><span data-stu-id="2e7f5-124">Add vxMaintain from hello gallery</span></span>
<span data-ttu-id="2e7f5-125">integracji hello tooconfigure vxMaintain z usługą Azure AD, należy vxMaintain tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-125">tooconfigure hello integration of vxMaintain with Azure AD, you need tooadd vxMaintain from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2e7f5-126">vxMaintain tooadd z galerii hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2e7f5-126">tooadd vxMaintain from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="2e7f5-127">W hello [portalu Azure](https://portal.azure.com), w lewym okienku hello, wybierz hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-127">In hello [Azure portal](https://portal.azure.com), in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="2e7f5-129">Wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![okienko "Aplikacje przedsiębiorstwa" Hello][2]
    
3. <span data-ttu-id="2e7f5-131">tooadd aplikacji, w hello **wszystkie aplikacje** okno dialogowe, wybierz opcję **nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-131">tooadd an application, in hello **All applications** dialog box, select **New application**.</span></span>

    ![Witaj "Nowej aplikacji" przycisku][3]

4. <span data-ttu-id="2e7f5-133">W polu wyszukiwania hello wpisz **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-133">In hello search box, type **vxMaintain**.</span></span>

    ![listy rozwijanej "Pojedynczy znak na tryb" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="2e7f5-135">Na liście wyników hello, wybierz **vxMaintain**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-135">In hello results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![Witaj vxMaintain łącza](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2e7f5-137">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2e7f5-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2e7f5-138">W tej sekcji można skonfigurować i przetestować logowania jednokrotnego programu Azure AD przy użyciu vxMaintain, na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="2e7f5-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2e7f5-139">Dla toowork logowania jednokrotnego usługi Azure AD musi użytkownika tooknow hello vxMaintain odpowiednikiem toohello usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-139">For SSO toowork, Azure AD needs tooknow hello vxMaintain counterpart toohello Azure AD user.</span></span> <span data-ttu-id="2e7f5-140">Oznacza to należy ustanowić relację łącza między hello użytkownika usługi Azure AD i odpowiedniego użytkownika vxMaintain hello.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-140">That is, you must establish a link relationship between hello Azure AD user and hello corresponding vxMaintain user.</span></span>

<span data-ttu-id="2e7f5-141">Relacja linku hello tooestablish, przypisz hello vxMaintain **nazwy użytkownika** wartość jako hello Azure AD **Username** wartość.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-141">tooestablish hello link relationship, assign hello vxMaintain **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="2e7f5-142">tooconfigure i testowania Azure AD logowania jednokrotnego przy użyciu vxMaintain, pełną powitania po bloków konstrukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-142">tooconfigure and test Azure AD SSO by using vxMaintain, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="2e7f5-143">Konfigurowanie usługi Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="2e7f5-144">W tej sekcji można zarówno włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu Azure hello i konfigurowanie logowania jednokrotnego w aplikacji vxMaintain hello następujący:</span><span class="sxs-lookup"><span data-stu-id="2e7f5-144">In this section, you can both enable Azure AD SSO in hello Azure portal and configure SSO in your vxMaintain application by doing hello following:</span></span>

1. <span data-ttu-id="2e7f5-145">W portalu Azure na powitania hello **vxMaintain** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-145">In hello Azure portal, on hello **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![Witaj "Logowanie jednokrotne" polecenia][4]

2. <span data-ttu-id="2e7f5-147">tooenable logowanie Jednokrotne, w hello **tryb rejestracji jednokrotnej** listy rozwijanej wybierz **na języku SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-147">tooenable SSO, in hello **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![polecenie "na podstawie SAML logowania jednokrotnego" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="2e7f5-149">W obszarze **vxMaintain domeny i adres URL**, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2e7f5-149">Under **vxMaintain Domain and URLs**, do hello following:</span></span>

    ![Witaj vxMaintain sekcji domeny i adresy URL](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="2e7f5-151">a.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-151">a.</span></span> <span data-ttu-id="2e7f5-152">W hello **identyfikator** wpisz adres URL, który ma hello następującej składni:`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="2e7f5-152">In hello **Identifier** box, type a URL that has hello following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="2e7f5-153">b.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-153">b.</span></span> <span data-ttu-id="2e7f5-154">W hello **adres URL odpowiedzi** wpisz adres URL, który ma hello następującej składni:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="2e7f5-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e7f5-155">Witaj poprzedniej wartości nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-155">hello preceding values are not real.</span></span> <span data-ttu-id="2e7f5-156">Można aktualizować hello rzeczywisty identyfikator i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-156">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="2e7f5-157">wartości hello tooobtain, skontaktuj się z pomocą hello [zespołem pomocy technicznej vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="2e7f5-157">tooobtain hello values, contact hello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="2e7f5-158">W obszarze **SAML certyfikat podpisywania**, wybierz pozycję **XML metadanych**, a następnie zapisz hello metadanych pliku tooyour komputera.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file tooyour computer.</span></span>

    ![Witaj sekcji "Certyfikat podpisywania SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="2e7f5-160">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-160">Select **Save**.</span></span>

    ![przycisk Zapisz Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2e7f5-162">tooconfigure **vxMaintain** logowania jednokrotnego, Wyślij hello pobrane **XML metadanych** pliku toohello [zespołem pomocy technicznej vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="2e7f5-162">tooconfigure **vxMaintain** SSO, send hello downloaded **Metadata XML** file toohello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="2e7f5-163">Po skonfigurowaniu aplikacji hello może odczytywać zwięzły wersji hello poprzedzających instrukcji w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2e7f5-163">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2e7f5-164">Po dodaniu aplikacji hello z hello **usługi Active Directory** > **aplikacje dla przedsiębiorstw** sekcji, wybierz hello **rejestracji jednokrotnej** kartę, a następnie hello dostępu osadzone dokumentacji z hello **konfiguracji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-164">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab, and then access hello embedded documentation from hello **Configuration** section.</span></span> 
>
><span data-ttu-id="2e7f5-165">toolearn więcej informacji na temat hello osadzonych dokumentacji funkcji, zobacz [Zarządzanie logowanie jednokrotne dla aplikacji przedsiębiorstwa](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="2e7f5-165">toolearn more about hello embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2e7f5-166">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e7f5-166">Create an Azure AD test user</span></span>
<span data-ttu-id="2e7f5-167">W tej sekcji możesz tworzyć użytkownika testowego Simona Britta w hello portalu Azure, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2e7f5-167">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![użytkownika testowego Hello Azure AD][100]

1. <span data-ttu-id="2e7f5-169">W hello **portalu Azure**, w lewym okienku hello, wybierz hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-169">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![przycisk "Azure Active Directory" Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e7f5-171">toodisplay listę użytkowników, przejdź zbyt**użytkowników i grup** > **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-171">toodisplay a list of users, go too**Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="2e7f5-172">![Witaj link "Wszyscy użytkownicy"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="2e7f5-172">![hello "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="2e7f5-173">Witaj **wszyscy użytkownicy** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-173">hello **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="2e7f5-174">Witaj tooopen **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-174">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e7f5-176">W hello **użytkownika** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2e7f5-176">In hello **User** dialog box, do hello following:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e7f5-178">a.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-178">a.</span></span> <span data-ttu-id="2e7f5-179">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-179">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e7f5-180">b.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-180">b.</span></span> <span data-ttu-id="2e7f5-181">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika testowego Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-181">In hello **User name** box, type hello email address of test user Britta Simon.</span></span>

    <span data-ttu-id="2e7f5-182">c.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-182">c.</span></span> <span data-ttu-id="2e7f5-183">Wybierz hello **Pokaż hasło** pole wyboru, a następnie wartość hello Uwaga, który został wygenerowany w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-183">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="2e7f5-184">d.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-184">d.</span></span> <span data-ttu-id="2e7f5-185">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="2e7f5-186">Tworzenie użytkownika testowego vxMaintain</span><span class="sxs-lookup"><span data-stu-id="2e7f5-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="2e7f5-187">W tej sekcji utworzysz użytkownika testowego Simona Britta w vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="2e7f5-188">Użytkownicy tooadd hello vxMaintain platformy, pracować z [zespołem pomocy technicznej vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="2e7f5-188">tooadd users in hello vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="2e7f5-189">Przed użyciem logowania jednokrotnego, Utwórz i Aktywuj hello użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-189">Before you use SSO, create and activate hello users.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2e7f5-190">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e7f5-190">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2e7f5-191">W tej sekcji możesz włączyć użytkownika testowego toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-191">In this section, you enable test user Britta Simon toouse Azure SSO by granting access toovxMaintain.</span></span> <span data-ttu-id="2e7f5-192">toodo tak, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2e7f5-192">toodo so, do hello following:</span></span>

![Użytkownik testowy hello liście Nazwa wyświetlana][200] 

1. <span data-ttu-id="2e7f5-194">W portalu Azure hello **aplikacji** wyświetlić, przejdź do zbyt**katalogu** Widok > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-194">In hello Azure portal **Applications** view, go too**Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![Witaj link "Wszystkie aplikacje"][201] 

2. <span data-ttu-id="2e7f5-196">W hello **aplikacji** listy, wybierz **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-196">In hello **Applications** list, select **vxMaintain**.</span></span>

    ![Witaj vxMaintain łącza](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="2e7f5-198">Wybierz w okienku po lewej stronie powitania **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-198">In hello left pane, select **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. <span data-ttu-id="2e7f5-200">Wybierz **Dodaj** , a następnie w hello **Dodaj przydziału** okienku wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-200">Select **Add** and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][203]

5. <span data-ttu-id="2e7f5-202">W hello **użytkowników i grup** okno dialogowe, w hello **użytkowników** listy, wybierz **Simona Britta**, a następnie wybierz hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-202">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**, and then select hello **Select** button.</span></span>

7. <span data-ttu-id="2e7f5-203">W hello **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-203">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="2e7f5-204">Test z usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2e7f5-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="2e7f5-205">W tej sekcji możesz przetestować konfigurację programu Azure AD z logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-205">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="2e7f5-206">Wybór hello **vxMaintain** kafelka w hello panelu dostępu należy automatycznej rejestracji w aplikacji vxMaintain tooyour.</span><span class="sxs-lookup"><span data-stu-id="2e7f5-206">Selecting hello **vxMaintain** tile in hello Access Panel should sign you in tooyour vxMaintain application automatically.</span></span>

<span data-ttu-id="2e7f5-207">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e7f5-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e7f5-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e7f5-208">Next steps</span></span>

* [<span data-ttu-id="2e7f5-209">Lista samouczków dotyczących integracji aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e7f5-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e7f5-210">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2e7f5-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

