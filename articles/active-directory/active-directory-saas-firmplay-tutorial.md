---
title: 'Samouczek: Integracji Azure Active Directory z FirmPlay - propagowanie pracownika dla Rekrutacja | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i FirmPlay - propagowanie pracownika dla Rekrutacja."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="20e47-103">Samouczek: Integracji Azure Active Directory z FirmPlay - propagowanie pracownika dla Rekrutacja</span><span class="sxs-lookup"><span data-stu-id="20e47-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="20e47-104">Z tego samouczka, dowiesz się, jak toointegrate FirmPlay - propagowanie pracownika dla Rekrutacja w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="20e47-104">In this tutorial, you learn how toointegrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="20e47-105">Integrowanie FirmPlay - propagowanie pracownika dla Rekrutacja z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="20e47-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="20e47-106">Można kontrolować w usłudze Azure AD mającego dostęp tooFirmPlay - propagowanie pracownika dla Rekrutacja</span><span class="sxs-lookup"><span data-stu-id="20e47-106">You can control in Azure AD who has access tooFirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="20e47-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFirmPlay - propagowanie pracownika dla Rekrutacja (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e47-107">You can enable your users tooautomatically get signed-on tooFirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="20e47-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="20e47-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="20e47-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="20e47-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20e47-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="20e47-110">Prerequisites</span></span>

<span data-ttu-id="20e47-111">tooconfigure integracji usługi Azure AD z FirmPlay - propagowanie pracownika dla Rekrutacja, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="20e47-111">tooconfigure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need hello following items:</span></span>

- <span data-ttu-id="20e47-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="20e47-113">FirmPlay - propagowanie pracownika dla rekrutacji jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="20e47-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="20e47-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="20e47-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="20e47-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="20e47-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="20e47-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="20e47-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="20e47-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20e47-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="20e47-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="20e47-118">Scenario description</span></span>
<span data-ttu-id="20e47-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="20e47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="20e47-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="20e47-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="20e47-121">Dodawanie FirmPlay - propagowanie pracownika dla Rekrutacja z galerii hello</span><span class="sxs-lookup"><span data-stu-id="20e47-121">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
2. <span data-ttu-id="20e47-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="20e47-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a><span data-ttu-id="20e47-123">Dodawanie FirmPlay - propagowanie pracownika dla Rekrutacja z galerii hello</span><span class="sxs-lookup"><span data-stu-id="20e47-123">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
<span data-ttu-id="20e47-124">Integracja hello tooconfigure FirmPlay - propagowanie pracownika dla Rekrutacja do usługi Azure AD, należy tooadd FirmPlay - propagowanie pracownika dla Rekrutacja z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="20e47-124">tooconfigure hello integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="20e47-125">**tooadd FirmPlay - propagowanie pracownika dla Rekrutacja z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="20e47-125">**tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="20e47-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="20e47-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="20e47-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="20e47-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="20e47-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="20e47-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="20e47-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20e47-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="20e47-133">W polu wyszukiwania hello wpisz **FirmPlay - propagowanie pracownika dla Rekrutacja**.</span><span class="sxs-lookup"><span data-stu-id="20e47-133">In hello search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="20e47-135">W panelu wyników hello, wybierz **FirmPlay - propagowanie pracownika dla Rekrutacja**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="20e47-135">In hello results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="20e47-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="20e47-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="20e47-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FirmPlay - propagowanie pracownika dla Rekrutacja w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="20e47-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="20e47-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w FirmPlay - propagowanie pracownika dla Rekrutacja jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20e47-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FirmPlay - Employee Advocacy for Recruiting is tooa user in Azure AD.</span></span> <span data-ttu-id="20e47-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w FirmPlay - propagowanie pracownika dla Rekrutacja musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="20e47-140">In other words, a link relationship between an Azure AD user and hello related user in FirmPlay - Employee Advocacy for Recruiting needs toobe established.</span></span>

<span data-ttu-id="20e47-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w FirmPlay - propagowanie pracownika dla Rekrutacja.</span><span class="sxs-lookup"><span data-stu-id="20e47-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="20e47-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z FirmPlay - propagowanie pracownika dla Rekrutacja, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="20e47-142">tooconfigure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="20e47-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="20e47-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="20e47-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="20e47-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="20e47-145">**[Tworzenie FirmPlay - propagowanie pracownika dla użytkownika testowego Rekrutacja](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave odpowiednikiem Simona Britta w FirmPlay: propagowanie pracownika dla rekrutacji, który jest połączony jej reprezentacji toohello usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20e47-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - toohave a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="20e47-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="20e47-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="20e47-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="20e47-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="20e47-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="20e47-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="20e47-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w sieci FirmPlay - propagowanie pracownika Rekrutacja aplikacji.</span><span class="sxs-lookup"><span data-stu-id="20e47-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="20e47-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z FirmPlay - propagowanie pracownika dla Rekrutacja, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="20e47-150">**tooconfigure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="20e47-151">W portalu zarządzania Azure hello na powitania **FirmPlay - propagowanie pracownika dla Rekrutacja** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="20e47-151">In hello Azure Management portal, on hello **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="20e47-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="20e47-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="20e47-155">Na powitania **FirmPlay - propagowanie pracownika rekrutacji domeny i adresów URL** części hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="20e47-155">On hello **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="20e47-157">Należy pamiętać, że nie jest hello rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="20e47-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="20e47-158">Masz tooupdate tej wartości z rzeczywistego hello Zaloguj się na adres URL.</span><span class="sxs-lookup"><span data-stu-id="20e47-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="20e47-159">Skontaktuj się z [FirmPlay - propagowanie pracowników zespołu pomocy technicznej Rekrutacja](mailto:engineering@firmplay.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="20e47-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooget this value.</span></span> 

4. <span data-ttu-id="20e47-160">Na powitania **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="20e47-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="20e47-162">Na powitania **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza hello i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="20e47-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="20e47-163">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20e47-163">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="20e47-165">Na powitania **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20e47-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="20e47-167">W oknie podręcznym hello **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="20e47-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="20e47-169">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="20e47-169">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="20e47-171">Na powitania **FirmPlay - propagowanie pracownika rekrutacji konfiguracji** kliknij **skonfigurować FirmPlay - propagowanie pracownika dla Rekrutacja** tooopen **Konfigurowanie logowania jednokrotnego**okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20e47-171">On hello **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** tooopen **Configure sign-on** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="20e47-174">tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [FirmPlay - propagowanie pracowników zespołu pomocy technicznej Rekrutacja](mailto:engineering@firmplay.com) i podaj następujący hello:</span><span class="sxs-lookup"><span data-stu-id="20e47-174">tooget SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with hello following:</span></span> 

    <span data-ttu-id="20e47-175">• hello pobrane **plik certyfikatu**</span><span class="sxs-lookup"><span data-stu-id="20e47-175">•  hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="20e47-176">• hello **SAML pojedynczy znak na adres URL usługi**</span><span class="sxs-lookup"><span data-stu-id="20e47-176">•  hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="20e47-177">• hello **identyfikator jednostki SAML**</span><span class="sxs-lookup"><span data-stu-id="20e47-177">•  hello **SAML Entity ID**</span></span>

    <span data-ttu-id="20e47-178">• hello **Sign-Out adresu URL**</span><span class="sxs-lookup"><span data-stu-id="20e47-178">•  hello **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="20e47-179">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e47-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="20e47-180">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="20e47-180">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="20e47-182">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="20e47-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="20e47-183">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="20e47-183">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="20e47-185">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="20e47-185">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="20e47-187">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20e47-187">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="20e47-189">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="20e47-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="20e47-191">a.</span><span class="sxs-lookup"><span data-stu-id="20e47-191">a.</span></span> <span data-ttu-id="20e47-192">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="20e47-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="20e47-193">b.</span><span class="sxs-lookup"><span data-stu-id="20e47-193">b.</span></span> <span data-ttu-id="20e47-194">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="20e47-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="20e47-195">c.</span><span class="sxs-lookup"><span data-stu-id="20e47-195">c.</span></span> <span data-ttu-id="20e47-196">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="20e47-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="20e47-197">d.</span><span class="sxs-lookup"><span data-stu-id="20e47-197">d.</span></span> <span data-ttu-id="20e47-198">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="20e47-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="20e47-199">Tworzenie FirmPlay - propagowanie pracownika dla użytkownika testowego Rekrutacja</span><span class="sxs-lookup"><span data-stu-id="20e47-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="20e47-200">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w FirmPlay - propagowanie pracownika dla Rekrutacja.</span><span class="sxs-lookup"><span data-stu-id="20e47-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="20e47-201">We współpracy z [FirmPlay - propagowanie pracowników zespołu pomocy technicznej Rekrutacja](mailto:engineering@firmplay.com) tooadd hello użytkowników w hello FirmPlay - propagowanie pracownika Rekrutacja platformy.</span><span class="sxs-lookup"><span data-stu-id="20e47-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooadd hello users in hello FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="20e47-202">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e47-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="20e47-203">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooFirmPlay dostępu - propagowanie pracownika dla Rekrutacja.</span><span class="sxs-lookup"><span data-stu-id="20e47-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFirmPlay - Employee Advocacy for Recruiting.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="20e47-205">**tooassign tooFirmPlay Simona Britta - propagowanie pracownika dla Rekrutacja, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="20e47-205">**tooassign Britta Simon tooFirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="20e47-206">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="20e47-206">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="20e47-208">Z listy aplikacji hello wybierz **FirmPlay - propagowanie pracownika dla Rekrutacja**.</span><span class="sxs-lookup"><span data-stu-id="20e47-208">In hello applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="20e47-210">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="20e47-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="20e47-212">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20e47-212">Click **Add** button.</span></span> <span data-ttu-id="20e47-213">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20e47-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="20e47-215">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="20e47-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="20e47-216">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20e47-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="20e47-217">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="20e47-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="20e47-218">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="20e47-218">Testing single sign-on</span></span>

<span data-ttu-id="20e47-219">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="20e47-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="20e47-220">Po kliknięciu hello FirmPlay - propagowanie pracownika Rekrutacja kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour FirmPlay - propagowanie pracownika Rekrutacja aplikacji.</span><span class="sxs-lookup"><span data-stu-id="20e47-220">When you click hello FirmPlay - Employee Advocacy for Recruiting tile in hello Access Panel, you should get automatically signed-on tooyour FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="20e47-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="20e47-221">Additional resources</span></span>

* [<span data-ttu-id="20e47-222">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="20e47-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="20e47-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="20e47-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png