---
title: "Samouczek: Integracji Azure Active Directory z Zscaler prywatny dostęp (ZPA) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Zscaler prywatny dostęp (ZPA)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="f31a2-103">Samouczek: Integracji Azure Active Directory z Zscaler prywatny dostęp (ZPA)</span><span class="sxs-lookup"><span data-stu-id="f31a2-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="f31a2-104">Z tego samouczka, dowiesz się, jak toointegrate Zscaler prywatny dostęp (ZPA) z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f31a2-104">In this tutorial, you learn how toointegrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f31a2-105">Integrowanie Zscaler prywatny dostęp (ZPA) z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f31a2-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f31a2-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooZscaler dostępu prywatnego (ZPA)</span><span class="sxs-lookup"><span data-stu-id="f31a2-106">You can control in Azure AD who has access tooZscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="f31a2-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooZscaler prywatny dostęp (ZPA) (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f31a2-107">You can enable your users tooautomatically get signed-on tooZscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f31a2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="f31a2-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="f31a2-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f31a2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f31a2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f31a2-110">Prerequisites</span></span>

<span data-ttu-id="f31a2-111">tooconfigure integracji z usługą Azure AD z Zscaler prywatny dostęp (ZPA), należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f31a2-111">tooconfigure Azure AD integration with Zscaler Private Access (ZPA), you need hello following items:</span></span>

- <span data-ttu-id="f31a2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f31a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f31a2-113">Zscaler prywatny dostęp (ZPA) jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f31a2-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="f31a2-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f31a2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="f31a2-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f31a2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f31a2-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f31a2-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f31a2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f31a2-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f31a2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f31a2-118">Scenario description</span></span>
<span data-ttu-id="f31a2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f31a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f31a2-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f31a2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f31a2-121">Dodawanie z galerii hello Zscaler prywatny dostęp (ZPA)</span><span class="sxs-lookup"><span data-stu-id="f31a2-121">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
2. <span data-ttu-id="f31a2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f31a2-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a><span data-ttu-id="f31a2-123">Dodawanie z galerii hello Zscaler prywatny dostęp (ZPA)</span><span class="sxs-lookup"><span data-stu-id="f31a2-123">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
<span data-ttu-id="f31a2-124">tooconfigure hello integracji z Zscaler prywatny dostęp (ZPA) do usługi Azure AD, należy tooadd Zscaler prywatny dostęp (ZPA) z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f31a2-124">tooconfigure hello integration of Zscaler Private Access (ZPA) into Azure AD, you need tooadd Zscaler Private Access (ZPA) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f31a2-125">**tooadd Zscaler prywatny dostęp (ZPA) z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="f31a2-125">**tooadd Zscaler Private Access (ZPA) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f31a2-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f31a2-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f31a2-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f31a2-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f31a2-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f31a2-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f31a2-133">W polu wyszukiwania hello wpisz **Zscaler prywatny dostęp (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-133">In hello search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="f31a2-135">W panelu wyników hello, wybierz **Zscaler prywatny dostęp (ZPA)**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f31a2-135">In hello results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f31a2-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f31a2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f31a2-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Zscaler prywatny dostęp (ZPA) w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f31a2-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f31a2-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Zscaler prywatny dostęp (ZPA) jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f31a2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Private Access (ZPA) is tooa user in Azure AD.</span></span> <span data-ttu-id="f31a2-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Zscaler prywatny dostęp (ZPA) musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="f31a2-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Private Access (ZPA) needs toobe established.</span></span>

<span data-ttu-id="f31a2-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **nazwy użytkownika** w Zscaler prywatny dostęp (ZPA).</span><span class="sxs-lookup"><span data-stu-id="f31a2-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="f31a2-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Zscaler prywatny dostęp (ZPA), należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f31a2-142">tooconfigure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f31a2-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f31a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f31a2-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f31a2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f31a2-145">**[Tworzenie użytkownika testowego Zscaler prywatny dostęp (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave odpowiednikiem Simona Britta w Zscaler prywatny dostęp (ZPA) będącego jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f31a2-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - toohave a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f31a2-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f31a2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f31a2-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="f31a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f31a2-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f31a2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f31a2-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Zscaler prywatny dostęp (ZPA).</span><span class="sxs-lookup"><span data-stu-id="f31a2-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="f31a2-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Zscaler prywatny dostęp (ZPA), wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f31a2-150">**tooconfigure Azure AD single sign-on with Zscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="f31a2-151">W portalu zarządzania Azure hello na powitania **Zscaler prywatny dostęp (ZPA)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-151">In hello Azure Management portal, on hello **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f31a2-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="f31a2-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="f31a2-155">Na powitania **domeny Zscaler prywatny dostęp (ZPA) i adresy URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f31a2-155">On hello **Zscaler Private Access (ZPA) Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="f31a2-157">a.</span><span class="sxs-lookup"><span data-stu-id="f31a2-157">a.</span></span> <span data-ttu-id="f31a2-158">W hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="f31a2-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="f31a2-159">b.</span><span class="sxs-lookup"><span data-stu-id="f31a2-159">b.</span></span> <span data-ttu-id="f31a2-160">W hello **identyfikator** tekstowym, wpisz:`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="f31a2-160">In hello **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f31a2-161">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="f31a2-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="f31a2-162">Masz tooupdate tych wartości za pomocą hello rzeczywiste Zaloguj się na adres URL i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="f31a2-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="f31a2-163">W tym miejscu zalecamy możesz toouse hello unikatową wartość adresu URL w hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="f31a2-163">Here we suggest you toouse hello unique value of URL in hello Identifier.</span></span> <span data-ttu-id="f31a2-164">Skontaktuj się z [zespołem pomocy technicznej Zscaler prywatny dostęp (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="f31a2-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooget these values.</span></span>

4. <span data-ttu-id="f31a2-165">Na powitania **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-165">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="f31a2-167">Na powitania **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza hello i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-167">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="f31a2-168">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f31a2-168">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="f31a2-170">Na powitania **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f31a2-170">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="f31a2-172">W oknie podręcznym hello **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-172">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="f31a2-174">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f31a2-174">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="f31a2-176">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Zscaler prywatny dostęp (ZPA) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f31a2-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="f31a2-177">Przejdź za**administratora** , a następnie kliknij przycisk **konfiguracji Idp**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-177">Navigate too**Administrator** and then click **Idp Configuration**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="f31a2-179">W hello **konfiguracji Idp** kliknij **dodać nową konfigurację IDP**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-179">In hello **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="f31a2-181">W hello **nowej konfiguracji IDP** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f31a2-181">In hello **New IDP Configuration** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="f31a2-183">a.</span><span class="sxs-lookup"><span data-stu-id="f31a2-183">a.</span></span> <span data-ttu-id="f31a2-184">Kliknij przycisk **wybierz plik** i przesłać plik pobrany metadanych.</span><span class="sxs-lookup"><span data-stu-id="f31a2-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="f31a2-185">b.</span><span class="sxs-lookup"><span data-stu-id="f31a2-185">b.</span></span> <span data-ttu-id="f31a2-186">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f31a2-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f31a2-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f31a2-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f31a2-188">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f31a2-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f31a2-190">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f31a2-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f31a2-191">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f31a2-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f31a2-193">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f31a2-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f31a2-195">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f31a2-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f31a2-197">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f31a2-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f31a2-199">a.</span><span class="sxs-lookup"><span data-stu-id="f31a2-199">a.</span></span> <span data-ttu-id="f31a2-200">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f31a2-201">b.</span><span class="sxs-lookup"><span data-stu-id="f31a2-201">b.</span></span> <span data-ttu-id="f31a2-202">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f31a2-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f31a2-203">c.</span><span class="sxs-lookup"><span data-stu-id="f31a2-203">c.</span></span> <span data-ttu-id="f31a2-204">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f31a2-205">d.</span><span class="sxs-lookup"><span data-stu-id="f31a2-205">d.</span></span> <span data-ttu-id="f31a2-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="f31a2-207">Tworzenie użytkownika testowego Zscaler prywatny dostęp (ZPA)</span><span class="sxs-lookup"><span data-stu-id="f31a2-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="f31a2-208">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Zscaler prywatny dostęp (ZPA).</span><span class="sxs-lookup"><span data-stu-id="f31a2-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="f31a2-209">We współpracy z [zespołem pomocy technicznej Zscaler prywatny dostęp (ZPA)](https://help.zscaler.com/zpa-submit-ticket) użytkowników hello tooadd hello Zscaler prywatny dostęp (ZPA) platformy.</span><span class="sxs-lookup"><span data-stu-id="f31a2-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooadd hello users in hello Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f31a2-210">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f31a2-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f31a2-211">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooZscaler dostępu prywatnego dostępu (ZPA).</span><span class="sxs-lookup"><span data-stu-id="f31a2-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooZscaler Private Access (ZPA).</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f31a2-213">**tooassign tooZscaler Simona Britta prywatny dostęp (ZPA) wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="f31a2-213">**tooassign Britta Simon tooZscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="f31a2-214">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-214">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f31a2-216">Z listy aplikacji hello wybierz **Zscaler prywatny dostęp (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-216">In hello applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="f31a2-218">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f31a2-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f31a2-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f31a2-220">Click **Add** button.</span></span> <span data-ttu-id="f31a2-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f31a2-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f31a2-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f31a2-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f31a2-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f31a2-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f31a2-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f31a2-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="f31a2-226">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f31a2-226">Testing single sign-on</span></span>

<span data-ttu-id="f31a2-227">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f31a2-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f31a2-228">Po kliknięciu kafelka Zscaler prywatny dostęp (ZPA) hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Zscaler prywatny dostęp (ZPA) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f31a2-228">When you click hello Zscaler Private Access (ZPA) tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f31a2-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f31a2-229">Additional resources</span></span>

* [<span data-ttu-id="f31a2-230">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f31a2-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f31a2-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f31a2-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png