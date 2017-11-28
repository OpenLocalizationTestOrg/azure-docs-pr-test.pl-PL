---
title: 'Samouczek: Integracji Azure Active Directory z FreshDesk | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="9e468-103">Samouczek: Integracji Azure Active Directory z FreshDesk</span><span class="sxs-lookup"><span data-stu-id="9e468-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="9e468-104">Z tego samouczka, dowiesz się, jak toointegrate FreshDesk w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e468-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e468-105">Integracja z usługą Azure AD FreshDesk zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9e468-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9e468-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFreshDesk</span><span class="sxs-lookup"><span data-stu-id="9e468-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="9e468-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFreshDesk (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e468-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e468-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="9e468-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9e468-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e468-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e468-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9e468-110">Prerequisites</span></span>

<span data-ttu-id="9e468-111">tooconfigure integracji z usługą Azure AD z FreshDesk należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9e468-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="9e468-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e468-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e468-113">FreshDesk jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9e468-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e468-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9e468-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e468-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9e468-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e468-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9e468-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9e468-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e468-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e468-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9e468-118">Scenario description</span></span>
<span data-ttu-id="9e468-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9e468-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e468-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9e468-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e468-121">Dodawanie FreshDesk z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9e468-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="9e468-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9e468-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="9e468-123">Dodawanie FreshDesk z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9e468-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="9e468-124">tooconfigure hello integracji FreshDesk do usługi Azure AD, należy tooadd FreshDesk z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9e468-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9e468-125">**tooadd FreshDesk z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9e468-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e468-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9e468-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9e468-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9e468-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9e468-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9e468-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9e468-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e468-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9e468-133">W polu wyszukiwania hello wpisz **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="9e468-133">In hello search box, type **FreshDesk**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="9e468-135">W panelu wyników hello zaznacz **FreshDesk**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9e468-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e468-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9e468-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e468-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FreshDesk w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9e468-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e468-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w FreshDesk jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e468-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="9e468-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w FreshDesk musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="9e468-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="9e468-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="9e468-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="9e468-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z FreshDesk, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9e468-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9e468-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9e468-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9e468-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9e468-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e468-145">**[Tworzenie użytkownika testowego FreshDesk](#creating-a-freshdesk-test-user)**  -toohave odpowiednikiem Simona Britta w FreshDesk, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e468-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9e468-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9e468-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e468-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="9e468-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e468-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9e468-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e468-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="9e468-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="9e468-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z FreshDesk, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9e468-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e468-151">W portalu zarządzania Azure hello na powitania **FreshDesk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9e468-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9e468-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9e468-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="9e468-155">Na powitania **FreshDesk domeny i adres URL** sekcji, wprowadź ciąg hello **adres URL logowania** jako: `https://<tenant-name>.freshdesk.com` lub wszelkie inne wartości Freshdesk ma sugerowane.</span><span class="sxs-lookup"><span data-stu-id="9e468-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="9e468-157">Należy pamiętać, że nie jest rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="9e468-157">Please note that this is not the real value.</span></span> <span data-ttu-id="9e468-158">Należy zaktualizować wartości z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="9e468-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="9e468-159">Skontaktuj się z [zespołem pomocy technicznej klienta FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="9e468-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="9e468-160">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie Zapisz certyfikat hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9e468-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="9e468-162">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e468-162">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9e468-164">Na powitania **konfiguracji FreshDesk** kliknij **skonfigurować FreshDesk** okna tooopen Konfigurowanie logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9e468-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="9e468-165">Skopiuj hello SAML pojedynczy znak na adres URL usługi i adres URL Sign-Out z hello **krótkimi opisami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="9e468-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="9e468-167">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Freshdesk jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9e468-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="9e468-168">W menu hello na górze hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="9e468-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="9e468-169">![Administrator](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="9e468-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="9e468-170">W hello **ustawienia ogólne** , kliknij pozycję **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="9e468-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="9e468-171">![Zabezpieczenia](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="9e468-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="9e468-172">W hello **zabezpieczeń** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9e468-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9e468-173">![Jednokrotne](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="9e468-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="9e468-174">a.</span><span class="sxs-lookup"><span data-stu-id="9e468-174">a.</span></span> <span data-ttu-id="9e468-175">Aby uzyskać **pojedynczy znak na rejestracji jednokrotnej (SSO)**, wybierz pozycję **na**.</span><span class="sxs-lookup"><span data-stu-id="9e468-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="9e468-176">b.</span><span class="sxs-lookup"><span data-stu-id="9e468-176">b.</span></span> <span data-ttu-id="9e468-177">Wybierz **logowania jednokrotnego SAML**.</span><span class="sxs-lookup"><span data-stu-id="9e468-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="9e468-178">c.</span><span class="sxs-lookup"><span data-stu-id="9e468-178">c.</span></span> <span data-ttu-id="9e468-179">Typ hello **SAML pojedynczy znak na adres URL usługi** skopiowany z portalu Azure do hello **adres URL logowania SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9e468-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="9e468-180">d.</span><span class="sxs-lookup"><span data-stu-id="9e468-180">d.</span></span> <span data-ttu-id="9e468-181">Typ hello **Sign-Out URL** skopiowany z portalu Azure do hello **adresu URL wylogowania** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="9e468-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="9e468-182">e.</span><span class="sxs-lookup"><span data-stu-id="9e468-182">e.</span></span> <span data-ttu-id="9e468-183">Kopiuj hello **odcisk palca** wartość z certyfikatu hello pobrany z portalu Azure i wklej go do hello **odcisk palca certyfikatu zabezpieczeń** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9e468-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="9e468-184">Aby uzyskać więcej informacji, zobacz [jak tooretrieve wartość odcisku palca certyfikatu](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="9e468-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="9e468-185">f.</span><span class="sxs-lookup"><span data-stu-id="9e468-185">f.</span></span> <span data-ttu-id="9e468-186">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9e468-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e468-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e468-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e468-188">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9e468-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9e468-190">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9e468-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e468-191">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9e468-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e468-193">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9e468-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e468-195">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e468-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e468-197">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9e468-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e468-199">a.</span><span class="sxs-lookup"><span data-stu-id="9e468-199">a.</span></span> <span data-ttu-id="9e468-200">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e468-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e468-201">b.</span><span class="sxs-lookup"><span data-stu-id="9e468-201">b.</span></span> <span data-ttu-id="9e468-202">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9e468-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e468-203">c.</span><span class="sxs-lookup"><span data-stu-id="9e468-203">c.</span></span> <span data-ttu-id="9e468-204">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9e468-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9e468-205">d.</span><span class="sxs-lookup"><span data-stu-id="9e468-205">d.</span></span> <span data-ttu-id="9e468-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9e468-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="9e468-207">Tworzenie użytkownika testowego FreshDesk</span><span class="sxs-lookup"><span data-stu-id="9e468-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="9e468-208">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do FreshDesk muszą mieć przydzielone do FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="9e468-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="9e468-209">W przypadku hello FreshDesk Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="9e468-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="9e468-210">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9e468-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e468-211">Zaloguj się za tooyour **Freshdesk** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="9e468-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="9e468-212">W menu hello na górze hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="9e468-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="9e468-213">![Administrator](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="9e468-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="9e468-214">W hello **ustawienia ogólne** , kliknij pozycję **agentów**.</span><span class="sxs-lookup"><span data-stu-id="9e468-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="9e468-215">![Agenci](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "agentów")</span><span class="sxs-lookup"><span data-stu-id="9e468-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="9e468-216">Kliknij przycisk **nowego agenta**.</span><span class="sxs-lookup"><span data-stu-id="9e468-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="9e468-217">![Nowy Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "nowego agenta")</span><span class="sxs-lookup"><span data-stu-id="9e468-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="9e468-218">W oknie dialogowym informacji o agencie hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9e468-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="9e468-219">![Informacji o agencie](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "informacji o agencie")</span><span class="sxs-lookup"><span data-stu-id="9e468-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="9e468-220">a.</span><span class="sxs-lookup"><span data-stu-id="9e468-220">a.</span></span> <span data-ttu-id="9e468-221">W hello **imię i nazwisko** pole tekstowe, nazwa typu hello hello Azure AD konta tooprovision.</span><span class="sxs-lookup"><span data-stu-id="9e468-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="9e468-222">b.</span><span class="sxs-lookup"><span data-stu-id="9e468-222">b.</span></span> <span data-ttu-id="9e468-223">W hello **E-mail** pole tekstowe, typ hello Azure AD adres e-mail konta usługi Azure AD hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="9e468-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="9e468-224">c.</span><span class="sxs-lookup"><span data-stu-id="9e468-224">c.</span></span> <span data-ttu-id="9e468-225">W hello **tytuł** pole tekstowe, tytuł hello typu konta hello Azure AD, które ma być tooprovision.</span><span class="sxs-lookup"><span data-stu-id="9e468-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="9e468-226">d.</span><span class="sxs-lookup"><span data-stu-id="9e468-226">d.</span></span> <span data-ttu-id="9e468-227">Wybierz **roli agentów**, a następnie kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="9e468-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="9e468-228">e.</span><span class="sxs-lookup"><span data-stu-id="9e468-228">e.</span></span> <span data-ttu-id="9e468-229">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9e468-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="9e468-230">Właściciel konta usługi Azure AD Hello otrzyma wiadomość e-mail zawierającą łącze tooconfirm hello konta, zanim zostanie aktywowany.</span><span class="sxs-lookup"><span data-stu-id="9e468-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="9e468-231">Możesz użyć innych Freshdesk użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Freshdesk tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="9e468-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="9e468-232">tooFreshDesk.</span><span class="sxs-lookup"><span data-stu-id="9e468-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9e468-233">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e468-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9e468-234">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooBox dostępu.</span><span class="sxs-lookup"><span data-stu-id="9e468-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9e468-236">**tooassign tooFreshDesk Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9e468-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e468-237">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9e468-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9e468-239">Z listy aplikacji hello wybierz **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="9e468-239">In hello applications list, select **FreshDesk**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="9e468-241">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9e468-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9e468-243">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e468-243">Click **Add** button.</span></span> <span data-ttu-id="9e468-244">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e468-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9e468-246">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9e468-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9e468-247">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e468-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e468-248">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e468-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e468-249">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9e468-249">Testing single sign-on</span></span>

<span data-ttu-id="9e468-250">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9e468-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9e468-251">Po kliknięciu kafelka FreshDesk hello w hello Panel dostępu, należy pobrać logowania strony tooget zalogowane tooyour FreshDesk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9e468-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9e468-252">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9e468-252">Additional resources</span></span>

* [<span data-ttu-id="9e468-253">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e468-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e468-254">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e468-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

