---
title: 'Samouczek: Integracji Azure Active Directory z Work.com | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="ba89d-103">Samouczek: Integracji Azure Active Directory z Work.com</span><span class="sxs-lookup"><span data-stu-id="ba89d-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="ba89d-104">Z tego samouczka, dowiesz się, jak toointegrate Work.com w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ba89d-104">In this tutorial, you learn how toointegrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba89d-105">Integracja z usługą Azure AD Work.com zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ba89d-105">Integrating Work.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ba89d-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWork.com</span><span class="sxs-lookup"><span data-stu-id="ba89d-106">You can control in Azure AD who has access tooWork.com</span></span>
- <span data-ttu-id="ba89d-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWork.com (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba89d-107">You can enable your users tooautomatically get signed-on tooWork.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ba89d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ba89d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ba89d-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ba89d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba89d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ba89d-110">Prerequisites</span></span>

<span data-ttu-id="ba89d-111">tooconfigure integracji z usługą Azure AD z Work.com należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ba89d-111">tooconfigure Azure AD integration with Work.com, you need hello following items:</span></span>

- <span data-ttu-id="ba89d-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba89d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba89d-113">Work.com logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ba89d-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba89d-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ba89d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba89d-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ba89d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba89d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ba89d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba89d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba89d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba89d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ba89d-118">Scenario description</span></span>
<span data-ttu-id="ba89d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ba89d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba89d-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ba89d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba89d-121">Dodaj Work.com z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ba89d-121">Add Work.com from hello gallery</span></span>
2. <span data-ttu-id="ba89d-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ba89d-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-hello-gallery"></a><span data-ttu-id="ba89d-123">Dodaj Work.com z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ba89d-123">Add Work.com from hello gallery</span></span>
<span data-ttu-id="ba89d-124">tooconfigure hello integracji Work.com do usługi Azure AD, należy tooadd Work.com z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ba89d-124">tooconfigure hello integration of Work.com into Azure AD, you need tooadd Work.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ba89d-125">**tooadd Work.com z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ba89d-125">**tooadd Work.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba89d-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ba89d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ba89d-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ba89d-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ba89d-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ba89d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ba89d-133">W polu wyszukiwania hello wpisz **Work.com**, wybierz pozycję **Work.com** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ba89d-133">In hello search box, type **Work.com**, select **Work.com** from results panel then click **Add** button tooadd hello application.</span></span>

    ![Dodaj z galerii](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ba89d-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ba89d-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ba89d-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Work.com w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ba89d-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ba89d-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Work.com jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba89d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Work.com is tooa user in Azure AD.</span></span> <span data-ttu-id="ba89d-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Work.com musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ba89d-138">In other words, a link relationship between an Azure AD user and hello related user in Work.com needs toobe established.</span></span>

<span data-ttu-id="ba89d-139">W Work.com, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ba89d-139">In Work.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ba89d-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Work.com, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ba89d-140">tooconfigure and test Azure AD single sign-on with Work.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ba89d-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ba89d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ba89d-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ba89d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba89d-143">**[Tworzenie użytkownika testowego Work.com](#create-a-workcom-test-user)**  -toohave odpowiednikiem Simona Britta w Work.com, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ba89d-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - toohave a counterpart of Britta Simon in Work.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ba89d-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ba89d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba89d-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ba89d-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ba89d-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ba89d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ba89d-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Work.com.</span><span class="sxs-lookup"><span data-stu-id="ba89d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="ba89d-148">tooconfigure logowanie jednokrotne, należy toosetup niestandardową nazwę domeny Work.com jeszcze.</span><span class="sxs-lookup"><span data-stu-id="ba89d-148">tooconfigure single sign-on, you need toosetup a custom Work.com domain name yet.</span></span> <span data-ttu-id="ba89d-149">Należy toodefine co najmniej domeny nazwy, przetestować nazwę domeny i wdrożyć ją tooyour całej organizacji.</span><span class="sxs-lookup"><span data-stu-id="ba89d-149">You need toodefine at least a domain name, test your domain name, and deploy it tooyour entire organization.</span></span>

<span data-ttu-id="ba89d-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Work.com, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ba89d-150">**tooconfigure Azure AD single sign-on with Work.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba89d-151">W portalu Azure na powitania hello **Work.com** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-151">In hello Azure portal, on hello **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ba89d-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ba89d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="ba89d-155">Na powitania **Work.com domeny i adres URL** sekcji, wykonaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ba89d-155">On hello **Work.com Domain and URLs** section, perform hello following:</span></span>

    ![Sekcja Work.com domeny i adresy URL](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="ba89d-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="ba89d-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ba89d-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ba89d-158">This value is not real.</span></span> <span data-ttu-id="ba89d-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="ba89d-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ba89d-160">Skontaktuj się z [zespołem pomocy technicznej klienta Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="ba89d-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) tooget this value.</span></span> 

4. <span data-ttu-id="ba89d-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ba89d-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="ba89d-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ba89d-163">Click **Save** button.</span></span>

    ![Przycisk Zapisz](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ba89d-165">Na powitania **konfiguracji Work.com** kliknij **skonfigurować Work.com** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ba89d-165">On hello **Work.com Configuration** section, click **Configure Work.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ba89d-166">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ba89d-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sekcja konfiguracji Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="ba89d-168">Zaloguj się za tooyour Work.com dzierżawy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ba89d-168">Log in tooyour Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="ba89d-169">Przejdź za**Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-169">Go too**Setup**.</span></span>
   
    <span data-ttu-id="ba89d-170">![Instalator](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="ba89d-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="ba89d-171">W okienku nawigacji po lewej stronie powitania w hello **Administruj** , kliknij przycisk **Zarządzanie domenami** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **Moje domeny** tooopen hello  **Mojej domeny** strony.</span><span class="sxs-lookup"><span data-stu-id="ba89d-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
    <span data-ttu-id="ba89d-172">![Mojej domeny](./media/active-directory-saas-work-com-tutorial/ic767825.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="ba89d-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="ba89d-173">tooverify, który domeny nie został skonfigurowany prawidłowo, upewnij się, że jest on "**krok 4 wdrożone tooUsers**" i zapoznaj się z "**Moje ustawienia domeny**".</span><span class="sxs-lookup"><span data-stu-id="ba89d-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="ba89d-174">![Domeny wdrożono tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser wdrożone domeny")</span><span class="sxs-lookup"><span data-stu-id="ba89d-174">![Domain Deployed tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="ba89d-175">Zaloguj się za tooyour Work.com dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="ba89d-175">Log in tooyour Work.com tenant.</span></span>

12. <span data-ttu-id="ba89d-176">Przejdź za**Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-176">Go too**Setup**.</span></span>
    
    <span data-ttu-id="ba89d-177">![Instalator](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="ba89d-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="ba89d-178">Rozwiń węzeł hello **kontroli bezpieczeństwa** menu, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-178">Expand hello **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="ba89d-179">![Single Sign-On ustawienia](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="ba89d-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="ba89d-180">Na powitania **ustawień rejestracji jednokrotnej** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ba89d-180">On hello **Single Sign-On Settings** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="ba89d-181">![Włączone SAML](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML włączone")</span><span class="sxs-lookup"><span data-stu-id="ba89d-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="ba89d-182">a.</span><span class="sxs-lookup"><span data-stu-id="ba89d-182">a.</span></span> <span data-ttu-id="ba89d-183">Wybierz **SAML włączone**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="ba89d-184">b.</span><span class="sxs-lookup"><span data-stu-id="ba89d-184">b.</span></span> <span data-ttu-id="ba89d-185">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-185">Click **New**.</span></span>

15. <span data-ttu-id="ba89d-186">W hello **SAML pojedynczego logowania jednokrotnego ustawienia** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ba89d-186">In hello **SAML Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="ba89d-187">![SAML pojedynczy znak na ustawienie](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML pojedynczy znak na ustawienie")</span><span class="sxs-lookup"><span data-stu-id="ba89d-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="ba89d-188">a.</span><span class="sxs-lookup"><span data-stu-id="ba89d-188">a.</span></span> <span data-ttu-id="ba89d-189">W hello **nazwa** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ba89d-189">In hello **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="ba89d-190">Wartość dla **nazwa** automatycznie wypełnić hello **Nazwa interfejsu API** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ba89d-190">Providing a value for **Name** does automatically populate hello **API Name** textbox.</span></span>
    
    <span data-ttu-id="ba89d-191">b.</span><span class="sxs-lookup"><span data-stu-id="ba89d-191">b.</span></span> <span data-ttu-id="ba89d-192">W **wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ba89d-192">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ba89d-193">c.</span><span class="sxs-lookup"><span data-stu-id="ba89d-193">c.</span></span> <span data-ttu-id="ba89d-194">tooupload certyfikatu hello pobrany z portalu Azure, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-194">tooupload hello downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="ba89d-195">d.</span><span class="sxs-lookup"><span data-stu-id="ba89d-195">d.</span></span> <span data-ttu-id="ba89d-196">W hello **identyfikator jednostki** pole tekstowe, typ `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="ba89d-196">In hello **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="ba89d-197">e.</span><span class="sxs-lookup"><span data-stu-id="ba89d-197">e.</span></span> <span data-ttu-id="ba89d-198">Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera hello identyfikator federacyjnej z obiektu użytkownika hello**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-198">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
    
    <span data-ttu-id="ba89d-199">f.</span><span class="sxs-lookup"><span data-stu-id="ba89d-199">f.</span></span> <span data-ttu-id="ba89d-200">Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentfier hello hello instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-200">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>
    
    <span data-ttu-id="ba89d-201">g.</span><span class="sxs-lookup"><span data-stu-id="ba89d-201">g.</span></span> <span data-ttu-id="ba89d-202">W **adresu URL logowania do dostawcy tożsamości** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ba89d-202">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ba89d-203">h.</span><span class="sxs-lookup"><span data-stu-id="ba89d-203">h.</span></span> <span data-ttu-id="ba89d-204">W **adres URL wylogowania dostawcy tożsamości** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ba89d-204">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ba89d-205">i.</span><span class="sxs-lookup"><span data-stu-id="ba89d-205">i.</span></span> <span data-ttu-id="ba89d-206">Jako **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="ba89d-207">j.</span><span class="sxs-lookup"><span data-stu-id="ba89d-207">j.</span></span> <span data-ttu-id="ba89d-208">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-208">Click **Save**.</span></span>

16. <span data-ttu-id="ba89d-209">W portalu klasycznym Work.com, w okienku nawigacji po lewej stronie powitania kliknij **Zarządzanie domenami** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **Moje domeny** tooopen hello **Moje domeny**strony.</span><span class="sxs-lookup"><span data-stu-id="ba89d-209">In your Work.com classic portal, on hello left navigation pane, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="ba89d-210">![Mojej domeny](./media/active-directory-saas-work-com-tutorial/ic794115.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="ba89d-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="ba89d-211">Na powitania **Moje domeny** strony w hello **znakowanie strony logowania** kliknij **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-211">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="ba89d-212">![Znakowanie strony logowania](./media/active-directory-saas-work-com-tutorial/ic767826.png "znakowanie strony logowania")</span><span class="sxs-lookup"><span data-stu-id="ba89d-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="ba89d-213">Na powitania **znakowanie strony logowania** strony w hello **usługi uwierzytelniania** sekcji, hello nazwę Twojej **ustawienia logowania jednokrotnego SAML** jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="ba89d-213">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="ba89d-214">Wybierz go, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="ba89d-215">![Znakowanie strony logowania](./media/active-directory-saas-work-com-tutorial/ic784366.png "znakowanie strony logowania")</span><span class="sxs-lookup"><span data-stu-id="ba89d-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="ba89d-216">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ba89d-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ba89d-217">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ba89d-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ba89d-218">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ba89d-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ba89d-219">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba89d-219">Create an Azure AD test user</span></span>
<span data-ttu-id="ba89d-220">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ba89d-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ba89d-222">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ba89d-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba89d-223">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ba89d-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ba89d-225">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Użytkownicy i grupy -> Wszyscy użytkownicy](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ba89d-227">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ba89d-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Add](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ba89d-229">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ba89d-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Strony okna dialogowego użytkownika](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ba89d-231">a.</span><span class="sxs-lookup"><span data-stu-id="ba89d-231">a.</span></span> <span data-ttu-id="ba89d-232">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba89d-233">b.</span><span class="sxs-lookup"><span data-stu-id="ba89d-233">b.</span></span> <span data-ttu-id="ba89d-234">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ba89d-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ba89d-235">c.</span><span class="sxs-lookup"><span data-stu-id="ba89d-235">c.</span></span> <span data-ttu-id="ba89d-236">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ba89d-237">d.</span><span class="sxs-lookup"><span data-stu-id="ba89d-237">d.</span></span> <span data-ttu-id="ba89d-238">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="ba89d-239">Tworzenie użytkownika testowego Work.com</span><span class="sxs-lookup"><span data-stu-id="ba89d-239">Create a Work.com test user</span></span>
<span data-ttu-id="ba89d-240">Dla usługi Azure Active Directory użytkowników toobe stanie toosign w muszą być tooWork.com elastycznie. W przypadku hello Work.com Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ba89d-240">For Azure Active Directory users toobe able toosign in, they must be provisioned tooWork.com. In hello case of Work.com, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="ba89d-241">tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ba89d-241">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="ba89d-242">Rejestracja tooyour Work.com witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ba89d-242">Sign on tooyour Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="ba89d-243">Przejdź za**Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-243">Go too**Setup**.</span></span>
   
    <span data-ttu-id="ba89d-244">![Instalator](./media/active-directory-saas-work-com-tutorial/IC794108.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="ba89d-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="ba89d-245">Przejdź za**Zarządzanie użytkownikami \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-245">Go too**Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="ba89d-246">![Zarządzaj użytkownikami](./media/active-directory-saas-work-com-tutorial/IC784369.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="ba89d-246">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="ba89d-247">Kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-247">Click **New User**.</span></span>
   
    <span data-ttu-id="ba89d-248">![Wszyscy użytkownicy](./media/active-directory-saas-work-com-tutorial/IC794117.png "wszyscy użytkownicy")</span><span class="sxs-lookup"><span data-stu-id="ba89d-248">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="ba89d-249">W hello sekcji Edytuj użytkowników, wykonaj następujące kroki w przypadku atrybutów elementów prawidłową Azure hello konta AD mają tooprovision w hello związane z pól tekstowych:</span><span class="sxs-lookup"><span data-stu-id="ba89d-249">In hello User Edit section, perform hello following steps, in attributes of a valid Azure AD account you want tooprovision into hello related textboxes:</span></span>
   
    <span data-ttu-id="ba89d-250">![Edycja użytkownika](./media/active-directory-saas-work-com-tutorial/ic794118.png "Edycja użytkownika")</span><span class="sxs-lookup"><span data-stu-id="ba89d-250">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="ba89d-251">a.</span><span class="sxs-lookup"><span data-stu-id="ba89d-251">a.</span></span> <span data-ttu-id="ba89d-252">W hello **imię** pole tekstowe, hello typu **imię** użytkownika hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-252">In hello **First Name** textbox, type hello **first name** of hello user **Britta**.</span></span>
    
    <span data-ttu-id="ba89d-253">b.</span><span class="sxs-lookup"><span data-stu-id="ba89d-253">b.</span></span> <span data-ttu-id="ba89d-254">W hello **nazwisko** pole tekstowe, hello typu **nazwisko** użytkownika hello **Simona**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-254">In hello **Last Name** textbox, type hello **last name** of hello user **Simon**.</span></span>
    
    <span data-ttu-id="ba89d-255">c.</span><span class="sxs-lookup"><span data-stu-id="ba89d-255">c.</span></span> <span data-ttu-id="ba89d-256">W hello **Alias** pole tekstowe, hello typu **nazwa** użytkownika hello **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-256">In hello **Alias** textbox, type hello **name** of hello user **BrittaS**.</span></span>
    
    <span data-ttu-id="ba89d-257">d.</span><span class="sxs-lookup"><span data-stu-id="ba89d-257">d.</span></span> <span data-ttu-id="ba89d-258">W hello **E-mail** pole tekstowe, hello typu **adres e-mail** użytkownika  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ba89d-258">In hello **Email** textbox, type hello **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="ba89d-259">e.</span><span class="sxs-lookup"><span data-stu-id="ba89d-259">e.</span></span> <span data-ttu-id="ba89d-260">W hello **nazwy użytkownika** tekstowym, wpisz nazwę użytkownika użytkownika, takich jak  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ba89d-260">In hello **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="ba89d-261">f.</span><span class="sxs-lookup"><span data-stu-id="ba89d-261">f.</span></span> <span data-ttu-id="ba89d-262">W hello **pseudonim** pola tekstowego, a typ **pseudonim** użytkownika **Simona**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-262">In hello **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="ba89d-263">g.</span><span class="sxs-lookup"><span data-stu-id="ba89d-263">g.</span></span> <span data-ttu-id="ba89d-264">Wybierz **roli**, **licencji użytkownika**, i **profilu**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-264">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="ba89d-265">h.</span><span class="sxs-lookup"><span data-stu-id="ba89d-265">h.</span></span> <span data-ttu-id="ba89d-266">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-266">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="ba89d-267">Właściciel konta usługi Azure AD Hello otrzymają wiadomość e-mail z tym kontem hello tooconfirm łącze zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="ba89d-267">hello Azure AD account holder will get an email including a link tooconfirm hello account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ba89d-268">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba89d-268">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ba89d-269">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWork.com.</span><span class="sxs-lookup"><span data-stu-id="ba89d-269">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWork.com.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ba89d-271">**tooassign tooWork.com Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ba89d-271">**tooassign Britta Simon tooWork.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba89d-272">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-272">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ba89d-274">Z listy aplikacji hello wybierz **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-274">In hello applications list, select **Work.com**.</span></span>

    ![Work.com na liście aplikacji](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="ba89d-276">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ba89d-276">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ba89d-278">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ba89d-278">Click **Add** button.</span></span> <span data-ttu-id="ba89d-279">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ba89d-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ba89d-281">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ba89d-281">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ba89d-282">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ba89d-282">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba89d-283">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ba89d-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ba89d-284">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ba89d-284">Test single sign-on</span></span>

<span data-ttu-id="ba89d-285">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ba89d-285">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ba89d-286">Po kliknięciu kafelka Work.com hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Work.com aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ba89d-286">When you click hello Work.com tile in hello Access Panel, you should get automatically signed-on tooyour Work.com application.</span></span>
<span data-ttu-id="ba89d-287">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ba89d-287">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba89d-288">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ba89d-288">Additional resources</span></span>

* [<span data-ttu-id="ba89d-289">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba89d-289">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba89d-290">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ba89d-290">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

