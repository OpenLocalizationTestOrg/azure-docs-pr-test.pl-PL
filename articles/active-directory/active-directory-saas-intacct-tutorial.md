---
title: 'Samouczek: Integracji Azure Active Directory z Intacct | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="e921e-103">Samouczek: Integracji Azure Active Directory z Intacct</span><span class="sxs-lookup"><span data-stu-id="e921e-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="e921e-104">Z tego samouczka, dowiesz się, jak toointegrate Intacct w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e921e-104">In this tutorial, you learn how toointegrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e921e-105">Integracja z usługą Azure AD Intacct zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e921e-105">Integrating Intacct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e921e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooIntacct</span><span class="sxs-lookup"><span data-stu-id="e921e-106">You can control in Azure AD who has access tooIntacct</span></span>
- <span data-ttu-id="e921e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooIntacct (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e921e-107">You can enable your users tooautomatically get signed-on tooIntacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e921e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e921e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e921e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e921e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e921e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e921e-110">Prerequisites</span></span>

<span data-ttu-id="e921e-111">tooconfigure integracji z usługą Azure AD z Intacct należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e921e-111">tooconfigure Azure AD integration with Intacct, you need hello following items:</span></span>

- <span data-ttu-id="e921e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e921e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e921e-113">Intacct logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e921e-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e921e-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e921e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e921e-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e921e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e921e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e921e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e921e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e921e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e921e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e921e-118">Scenario description</span></span>
<span data-ttu-id="e921e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e921e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e921e-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e921e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e921e-121">Dodawanie Intacct z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e921e-121">Adding Intacct from hello gallery</span></span>
2. <span data-ttu-id="e921e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e921e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-hello-gallery"></a><span data-ttu-id="e921e-123">Dodawanie Intacct z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e921e-123">Adding Intacct from hello gallery</span></span>
<span data-ttu-id="e921e-124">tooconfigure hello integracji Intacct do usługi Azure AD, należy tooadd Intacct z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e921e-124">tooconfigure hello integration of Intacct into Azure AD, you need tooadd Intacct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e921e-125">**tooadd Intacct z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e921e-125">**tooadd Intacct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e921e-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e921e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e921e-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e921e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e921e-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e921e-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e921e-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e921e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e921e-133">W polu wyszukiwania hello wpisz **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="e921e-133">In hello search box, type **Intacct**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="e921e-135">W panelu wyników hello zaznacz **Intacct**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e921e-135">In hello results panel, select **Intacct**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e921e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e921e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e921e-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Intacct w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e921e-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e921e-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Intacct jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e921e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intacct is tooa user in Azure AD.</span></span> <span data-ttu-id="e921e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Intacct musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e921e-140">In other words, a link relationship between an Azure AD user and hello related user in Intacct needs toobe established.</span></span>

<span data-ttu-id="e921e-141">W Intacct, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e921e-141">In Intacct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e921e-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Intacct, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e921e-142">tooconfigure and test Azure AD single sign-on with Intacct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e921e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e921e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e921e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e921e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e921e-145">**[Tworzenie użytkownika testowego Intacct](#creating-an-intacct-test-user)**  -toohave odpowiednikiem Simona Britta w Intacct, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e921e-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - toohave a counterpart of Britta Simon in Intacct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e921e-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e921e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e921e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e921e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e921e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e921e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e921e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Intacct.</span><span class="sxs-lookup"><span data-stu-id="e921e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="e921e-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Intacct, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e921e-150">**tooconfigure Azure AD single sign-on with Intacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="e921e-151">W portalu Azure na powitania hello **Intacct** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e921e-151">In hello Azure portal, on hello **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e921e-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e921e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="e921e-155">Na powitania **Intacct domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e921e-155">On hello **Intacct Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="e921e-157">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="e921e-157">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="e921e-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e921e-158">This value is not real.</span></span> <span data-ttu-id="e921e-159">Zaktualizuj tę wartość przy hello rzeczywisty adres URL odpowiedzi służący.</span><span class="sxs-lookup"><span data-stu-id="e921e-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="e921e-160">Skontaktuj się z [zespołem pomocy technicznej Intacct](https://us.intacct.com/support) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="e921e-160">Contact [Intacct support team](https://us.intacct.com/support) tooget this value.</span></span>

4. <span data-ttu-id="e921e-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e921e-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="e921e-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e921e-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e921e-165">Na powitania **konfiguracji Intacct** kliknij **skonfigurować Intacct** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e921e-165">On hello **Intacct Configuration** section, click **Configure Intacct** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e921e-166">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e921e-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="e921e-168">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Intacct tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e921e-168">In a different web browser window, sign in tooyour Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="e921e-169">Kliknij przycisk hello **firmy** , a następnie kliknij pozycję **informacje o firmie**.</span><span class="sxs-lookup"><span data-stu-id="e921e-169">Click hello **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="e921e-170">![Firmy](./media/active-directory-saas-intacct-tutorial/ic790037.png "firmy")</span><span class="sxs-lookup"><span data-stu-id="e921e-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="e921e-171">Kliknij przycisk hello **zabezpieczeń** , a następnie kliknij pozycję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="e921e-171">Click hello **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="e921e-172">![Zabezpieczenia](./media/active-directory-saas-intacct-tutorial/ic790038.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="e921e-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="e921e-173">W hello **logowania (SSO) z jednym** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e921e-173">In hello **Single sign on (SSO)** section, perform hello following steps:</span></span>

    <span data-ttu-id="e921e-174">![Jednokrotne](./media/active-directory-saas-intacct-tutorial/ic790039.png "jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="e921e-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="e921e-175">a.</span><span class="sxs-lookup"><span data-stu-id="e921e-175">a.</span></span> <span data-ttu-id="e921e-176">Wybierz **włączenia funkcji logowania jednokrotnego w**.</span><span class="sxs-lookup"><span data-stu-id="e921e-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="e921e-177">b.</span><span class="sxs-lookup"><span data-stu-id="e921e-177">b.</span></span> <span data-ttu-id="e921e-178">Jako **typ dostawcy tożsamości**, wybierz pozycję **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="e921e-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="e921e-179">c.</span><span class="sxs-lookup"><span data-stu-id="e921e-179">c.</span></span> <span data-ttu-id="e921e-180">W **adres URL wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e921e-180">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e921e-181">d.</span><span class="sxs-lookup"><span data-stu-id="e921e-181">d.</span></span> <span data-ttu-id="e921e-182">W **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e921e-182">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e921e-183">e.</span><span class="sxs-lookup"><span data-stu-id="e921e-183">e.</span></span> <span data-ttu-id="e921e-184">Otwórz z **base-64** zakodowany certyfikat w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu** pole.</span><span class="sxs-lookup"><span data-stu-id="e921e-184">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** box.</span></span>
   
    <span data-ttu-id="e921e-185">f.</span><span class="sxs-lookup"><span data-stu-id="e921e-185">f.</span></span> <span data-ttu-id="e921e-186">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e921e-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e921e-187">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e921e-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e921e-188">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e921e-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e921e-189">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e921e-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e921e-190">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e921e-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="e921e-191">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e921e-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e921e-193">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e921e-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e921e-194">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e921e-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e921e-196">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e921e-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e921e-198">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e921e-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e921e-200">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e921e-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e921e-202">a.</span><span class="sxs-lookup"><span data-stu-id="e921e-202">a.</span></span> <span data-ttu-id="e921e-203">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e921e-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e921e-204">b.</span><span class="sxs-lookup"><span data-stu-id="e921e-204">b.</span></span> <span data-ttu-id="e921e-205">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e921e-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e921e-206">c.</span><span class="sxs-lookup"><span data-stu-id="e921e-206">c.</span></span> <span data-ttu-id="e921e-207">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e921e-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e921e-208">d.</span><span class="sxs-lookup"><span data-stu-id="e921e-208">d.</span></span> <span data-ttu-id="e921e-209">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e921e-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="e921e-210">Tworzenie użytkownika testowego Intacct</span><span class="sxs-lookup"><span data-stu-id="e921e-210">Creating an Intacct test user</span></span>

<span data-ttu-id="e921e-211">tooset użytkowników usługi Azure AD, aby móc zalogować się tooIntacct, ich muszą mieć przydzielone do Intacct.</span><span class="sxs-lookup"><span data-stu-id="e921e-211">tooset up Azure AD users so they can sign in tooIntacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="e921e-212">Dla Intacct Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="e921e-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="e921e-213">**tooprovision kont użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e921e-213">**tooprovision user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="e921e-214">Zaloguj się tooyour **Intacct** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="e921e-214">Sign in tooyour **Intacct** tenant.</span></span>

2. <span data-ttu-id="e921e-215">Kliknij przycisk hello **firmy** , a następnie kliknij pozycję **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="e921e-215">Click hello **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="e921e-216">![Użytkownicy](./media/active-directory-saas-intacct-tutorial/ic790041.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="e921e-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="e921e-217">Kliknij przycisk hello **Dodaj** kartę.</span><span class="sxs-lookup"><span data-stu-id="e921e-217">Click hello **Add** tab.</span></span>

    <span data-ttu-id="e921e-218">![Dodaj](./media/active-directory-saas-intacct-tutorial/ic790042.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="e921e-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="e921e-219">W hello **informacje o użytkowniku** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e921e-219">In hello **User Information** section, perform hello following steps:</span></span>

    <span data-ttu-id="e921e-220">![Informacje o użytkowniku](./media/active-directory-saas-intacct-tutorial/ic790043.png "informacje o użytkowniku")</span><span class="sxs-lookup"><span data-stu-id="e921e-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="e921e-221">a.</span><span class="sxs-lookup"><span data-stu-id="e921e-221">a.</span></span> <span data-ttu-id="e921e-222">Wprowadź hello **identyfikator użytkownika**, hello **nazwisko**, **imię**, hello **adres E-mail**, hello **tytuł**, i hello **Phone** konta usługi Azure AD mają tooprovision w hello **informacje o użytkowniku** sekcji.</span><span class="sxs-lookup"><span data-stu-id="e921e-222">Enter hello **User ID**, hello **Last name**, **First name**, hello **Email address**, hello **Title**, and hello **Phone** of an Azure AD account that you want tooprovision into hello **User Information** section.</span></span>

    <span data-ttu-id="e921e-223">b.</span><span class="sxs-lookup"><span data-stu-id="e921e-223">b.</span></span> <span data-ttu-id="e921e-224">Wybierz hello **uprawnień administratora** konta usługi Azure AD, które mają tooprovision.</span><span class="sxs-lookup"><span data-stu-id="e921e-224">Select hello **Admin privileges** of an Azure AD account that you want tooprovision.</span></span>
   
    <span data-ttu-id="e921e-225">c.</span><span class="sxs-lookup"><span data-stu-id="e921e-225">c.</span></span> <span data-ttu-id="e921e-226">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e921e-226">Click **Save**.</span></span> <span data-ttu-id="e921e-227">Właściciel konta usługi Azure AD Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="e921e-227">hello Azure AD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="e921e-228">tooprovision kont użytkowników usługi Azure AD, można użyć innych narzędzi tworzenia konta użytkownika Intacct lub interfejsów API, które są dostarczane przez Intacct.</span><span class="sxs-lookup"><span data-stu-id="e921e-228">tooprovision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e921e-229">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e921e-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e921e-230">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooIntacct.</span><span class="sxs-lookup"><span data-stu-id="e921e-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntacct.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e921e-232">**tooassign tooIntacct Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e921e-232">**tooassign Britta Simon tooIntacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="e921e-233">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e921e-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e921e-235">Z listy aplikacji hello wybierz **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="e921e-235">In hello applications list, select **Intacct**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="e921e-237">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e921e-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e921e-239">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e921e-239">Click **Add** button.</span></span> <span data-ttu-id="e921e-240">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e921e-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e921e-242">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e921e-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e921e-243">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e921e-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e921e-244">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e921e-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e921e-245">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e921e-245">Testing single sign-on</span></span>

<span data-ttu-id="e921e-246">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e921e-246">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="e921e-247">Po kliknięciu kafelka Intacct hello w panelu dostępu hello powinny być automatycznie zalogowano tooyour Intacct aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e921e-247">When you click hello Intacct tile in hello Access Panel, you should be automatically signed in tooyour Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e921e-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e921e-248">Additional resources</span></span>

* [<span data-ttu-id="e921e-249">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e921e-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e921e-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e921e-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

