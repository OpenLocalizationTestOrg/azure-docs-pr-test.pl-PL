---
title: 'Samouczek: Integracji Azure Active Directory z PlanMyLeave | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="f4389-103">Samouczek: Integracji Azure Active Directory z PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="f4389-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="f4389-104">Z tego samouczka, dowiesz się, jak toointegrate PlanMyLeave w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4389-104">In this tutorial, you learn how toointegrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4389-105">Integracja z usługą Azure AD PlanMyLeave zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f4389-105">Integrating PlanMyLeave with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f4389-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="f4389-106">You can control in Azure AD who has access tooPlanMyLeave</span></span>
- <span data-ttu-id="f4389-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPlanMyLeave (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4389-107">You can enable your users tooautomatically get signed-on tooPlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f4389-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="f4389-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="f4389-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4389-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4389-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f4389-110">Prerequisites</span></span>

<span data-ttu-id="f4389-111">tooconfigure integracji z usługą Azure AD z PlanMyLeave należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f4389-111">tooconfigure Azure AD integration with PlanMyLeave, you need hello following items:</span></span>

- <span data-ttu-id="f4389-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4389-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4389-113">PlanMyLeave jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f4389-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="f4389-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f4389-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="f4389-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f4389-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4389-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f4389-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f4389-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4389-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f4389-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f4389-118">Scenario description</span></span>
<span data-ttu-id="f4389-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f4389-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4389-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f4389-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4389-121">Dodawanie PlanMyLeave z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f4389-121">Adding PlanMyLeave from hello gallery</span></span>
2. <span data-ttu-id="f4389-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f4389-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-hello-gallery"></a><span data-ttu-id="f4389-123">Dodawanie PlanMyLeave z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f4389-123">Adding PlanMyLeave from hello gallery</span></span>
<span data-ttu-id="f4389-124">tooconfigure hello integracji PlanMyLeave do usługi Azure AD, należy tooadd PlanMyLeave z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f4389-124">tooconfigure hello integration of PlanMyLeave into Azure AD, you need tooadd PlanMyLeave from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f4389-125">**tooadd PlanMyLeave z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f4389-125">**tooadd PlanMyLeave from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4389-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f4389-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f4389-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f4389-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f4389-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f4389-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f4389-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f4389-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f4389-133">W polu wyszukiwania hello wpisz **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="f4389-133">In hello search box, type **PlanMyLeave**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="f4389-135">W panelu wyników hello zaznacz **PlanMyLeave**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f4389-135">In hello results panel, select **PlanMyLeave**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f4389-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f4389-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f4389-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PlanMyLeave w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f4389-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f4389-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w PlanMyLeave jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4389-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PlanMyLeave is tooa user in Azure AD.</span></span> <span data-ttu-id="f4389-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w PlanMyLeave musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="f4389-140">In other words, a link relationship between an Azure AD user and hello related user in PlanMyLeave needs toobe established.</span></span>

<span data-ttu-id="f4389-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="f4389-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="f4389-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z PlanMyLeave, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f4389-142">tooconfigure and test Azure AD single sign-on with PlanMyLeave, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f4389-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f4389-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f4389-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f4389-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4389-145">**[Tworzenie użytkownika testowego PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave odpowiednikiem Simona Britta w PlanMyLeave, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4389-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - toohave a counterpart of Britta Simon in PlanMyLeave that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f4389-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f4389-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4389-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="f4389-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f4389-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f4389-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f4389-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="f4389-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="f4389-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z PlanMyLeave, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f4389-150">**tooconfigure Azure AD single sign-on with PlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4389-151">W portalu zarządzania Azure hello na powitania **PlanMyLeave** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f4389-151">In hello Azure Management portal, on hello **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f4389-153">Na powitania **logowanie jednokrotne** strony okna dialogowego jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="f4389-153">On hello **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="f4389-155">Na powitania **PlanMyLeave domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f4389-155">On hello **PlanMyLeave Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="f4389-157">a.</span><span class="sxs-lookup"><span data-stu-id="f4389-157">a.</span></span> <span data-ttu-id="f4389-158">W hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="f4389-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="f4389-159">b.</span><span class="sxs-lookup"><span data-stu-id="f4389-159">b.</span></span> <span data-ttu-id="f4389-160">W hello **identyfikatorem** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="f4389-160">In hello **Identifer** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f4389-161">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="f4389-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="f4389-162">Masz tooupdate tych wartości za pomocą hello rzeczywiste Zaloguj się na adres URL i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="f4389-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="f4389-163">Skontaktuj się z [zespołem pomocy technicznej PlanMyLeave](mailto:support@planmyleave.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="f4389-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) tooget these values.</span></span>

4. <span data-ttu-id="f4389-164">Na powitania **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="f4389-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="f4389-166">Na powitania **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza hello i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="f4389-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="f4389-167">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f4389-167">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="f4389-169">Na powitania **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f4389-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="f4389-171">W oknie podręcznym hello **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4389-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f4389-173">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f4389-173">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="f4389-175">Na powitania **konfiguracji PlanMyLeave** kliknij **skonfigurować PlanMyLeave** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f4389-175">On hello **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** tooopen **Configure sign-on** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="f4389-178">W oknie przeglądarki innej witryny sieci web Zaloguj się do dzierżawy PlanMyLeave jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f4389-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="f4389-179">Przejdź za**konfiguracji systemu**.</span><span class="sxs-lookup"><span data-stu-id="f4389-179">Go too**System Setup**.</span></span> <span data-ttu-id="f4389-180">Następnie na powitania **zarządzania zabezpieczeniami** kliknij sekcję **ustawienia SAML firmy** .</span><span class="sxs-lookup"><span data-stu-id="f4389-180">Then on hello **Security Management** section click **Company SAML settings** .</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="f4389-182">Na powitania **ustawienia SAML** sekcji, kliknij ikonę edytora.</span><span class="sxs-lookup"><span data-stu-id="f4389-182">On hello **SAML Settings** section, click editor icon.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="f4389-184">Na powitania **ustawienia SAML aktualizacji** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f4389-184">On hello **Update SAML Settings** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="f4389-186">a.</span><span class="sxs-lookup"><span data-stu-id="f4389-186">a.</span></span>  <span data-ttu-id="f4389-187">W hello **adres URL logowania** pole tekstowe, umieść wartość hello **SAML pojedynczy znak na adres URL usługi** z okna konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4389-187">In hello **Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="f4389-188">b.</span><span class="sxs-lookup"><span data-stu-id="f4389-188">b.</span></span>  <span data-ttu-id="f4389-189">Otwórz w Notatniku plik certyfikatu pobrane, tylko hello zawartości między hello---rozpocząć certyfikatu---i---koniec certyfikatu---go do Schowka, skopiuj i wklej go po toohello **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="f4389-189">Open your downloaded certificate file in notepad, copy only hello content between hello ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>

    <span data-ttu-id="f4389-190">c.</span><span class="sxs-lookup"><span data-stu-id="f4389-190">c.</span></span> <span data-ttu-id="f4389-191">Ustawianie"**jest włączona**"za"**tak**".</span><span class="sxs-lookup"><span data-stu-id="f4389-191">Set "**Is Enable**" too"**Yes**".</span></span>

    <span data-ttu-id="f4389-192">d.</span><span class="sxs-lookup"><span data-stu-id="f4389-192">d.</span></span> <span data-ttu-id="f4389-193">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="f4389-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f4389-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4389-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="f4389-195">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f4389-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f4389-197">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f4389-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4389-198">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f4389-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f4389-200">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f4389-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f4389-202">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f4389-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f4389-204">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f4389-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f4389-206">a.</span><span class="sxs-lookup"><span data-stu-id="f4389-206">a.</span></span> <span data-ttu-id="f4389-207">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f4389-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4389-208">b.</span><span class="sxs-lookup"><span data-stu-id="f4389-208">b.</span></span> <span data-ttu-id="f4389-209">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f4389-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f4389-210">c.</span><span class="sxs-lookup"><span data-stu-id="f4389-210">c.</span></span> <span data-ttu-id="f4389-211">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f4389-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f4389-212">d.</span><span class="sxs-lookup"><span data-stu-id="f4389-212">d.</span></span> <span data-ttu-id="f4389-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f4389-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="f4389-214">Tworzenie użytkownika testowego PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="f4389-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="f4389-215">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="f4389-215">hello objective of this section is toocreate a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="f4389-216">PlanMyLeave obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="f4389-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f4389-217">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f4389-217">There is no action item for you in this section.</span></span> <span data-ttu-id="f4389-218">Nowy użytkownik zostanie utworzony podczas próby tooaccess PlanMyLeave, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f4389-218">A new user will be created during an attempt tooaccess PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="f4389-219">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact [zespołem pomocy technicznej PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="f4389-219">If you need toocreate an user manually, you need toocontact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f4389-220">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4389-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f4389-221">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooPlanMyLeave dostępu.</span><span class="sxs-lookup"><span data-stu-id="f4389-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPlanMyLeave.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f4389-223">**tooassign tooPlanMyLeave Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="f4389-223">**tooassign Britta Simon tooPlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4389-224">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f4389-224">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f4389-226">Z listy aplikacji hello wybierz **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="f4389-226">In hello applications list, select **PlanMyLeave**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="f4389-228">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f4389-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f4389-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f4389-230">Click **Add** button.</span></span> <span data-ttu-id="f4389-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f4389-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f4389-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f4389-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f4389-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f4389-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4389-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f4389-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="f4389-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f4389-236">Testing single sign-on</span></span>

<span data-ttu-id="f4389-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f4389-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f4389-238">Po kliknięciu kafelka PlanMyLeave hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour PlanMyLeave aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4389-238">When you click hello PlanMyLeave tile in hello Access Panel, you should get automatically signed-on tooyour PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f4389-239">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f4389-239">Additional resources</span></span>

* [<span data-ttu-id="f4389-240">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4389-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4389-241">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4389-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png