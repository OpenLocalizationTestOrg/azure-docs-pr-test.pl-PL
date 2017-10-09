---
title: 'Samouczek: Integracji Azure Active Directory z IdeaScale | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="8b5d2-103">Samouczek: Integracji Azure Active Directory z IdeaScale</span><span class="sxs-lookup"><span data-stu-id="8b5d2-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="8b5d2-104">Z tego samouczka, dowiesz się, jak toointegrate IdeaScale w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b5d2-104">In this tutorial, you learn how toointegrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b5d2-105">Integracja z usługą Azure AD IdeaScale zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8b5d2-105">Integrating IdeaScale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8b5d2-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooIdeaScale</span><span class="sxs-lookup"><span data-stu-id="8b5d2-106">You can control in Azure AD who has access tooIdeaScale</span></span>
- <span data-ttu-id="8b5d2-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooIdeaScale (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b5d2-107">You can enable your users tooautomatically get signed-on tooIdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b5d2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8b5d2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8b5d2-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b5d2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b5d2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8b5d2-110">Prerequisites</span></span>

<span data-ttu-id="8b5d2-111">tooconfigure integracji z usługą Azure AD z IdeaScale należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8b5d2-111">tooconfigure Azure AD integration with IdeaScale, you need hello following items:</span></span>

- <span data-ttu-id="8b5d2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b5d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b5d2-113">IdeaScale jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8b5d2-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b5d2-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b5d2-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8b5d2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b5d2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b5d2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b5d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b5d2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8b5d2-118">Scenario description</span></span>
<span data-ttu-id="8b5d2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b5d2-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8b5d2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b5d2-121">Dodawanie IdeaScale z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8b5d2-121">Adding IdeaScale from hello gallery</span></span>
2. <span data-ttu-id="8b5d2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8b5d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-hello-gallery"></a><span data-ttu-id="8b5d2-123">Dodawanie IdeaScale z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8b5d2-123">Adding IdeaScale from hello gallery</span></span>
<span data-ttu-id="8b5d2-124">tooconfigure hello integracji IdeaScale do usługi Azure AD, należy tooadd IdeaScale z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-124">tooconfigure hello integration of IdeaScale into Azure AD, you need tooadd IdeaScale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8b5d2-125">**tooadd IdeaScale z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8b5d2-125">**tooadd IdeaScale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b5d2-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8b5d2-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8b5d2-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8b5d2-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8b5d2-133">W polu wyszukiwania hello wpisz **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-133">In hello search box, type **IdeaScale**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="8b5d2-135">W panelu wyników hello zaznacz **IdeaScale**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-135">In hello results panel, select **IdeaScale**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b5d2-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8b5d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b5d2-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z IdeaScale na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="8b5d2-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8b5d2-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w IdeaScale jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IdeaScale is tooa user in Azure AD.</span></span> <span data-ttu-id="8b5d2-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w IdeaScale musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-140">In other words, a link relationship between an Azure AD user and hello related user in IdeaScale needs toobe established.</span></span>

<span data-ttu-id="8b5d2-141">W IdeaScale, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-141">In IdeaScale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8b5d2-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z IdeaScale, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8b5d2-142">tooconfigure and test Azure AD single sign-on with IdeaScale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8b5d2-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8b5d2-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b5d2-145">**[Tworzenie użytkownika testowego IdeaScale](#creating-an-ideascale-test-user)**  -toohave odpowiednikiem Simona Britta w IdeaScale, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - toohave a counterpart of Britta Simon in IdeaScale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b5d2-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b5d2-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b5d2-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8b5d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b5d2-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="8b5d2-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z IdeaScale, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8b5d2-150">**tooconfigure Azure AD single sign-on with IdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b5d2-151">W portalu Azure na powitania hello **IdeaScale** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-151">In hello Azure portal, on hello **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8b5d2-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="8b5d2-155">Na powitania **IdeaScale domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8b5d2-155">On hello **IdeaScale Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="8b5d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-157">a.</span></span> <span data-ttu-id="8b5d2-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="8b5d2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="8b5d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-159">b.</span></span> <span data-ttu-id="8b5d2-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="8b5d2-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="8b5d2-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-161">These values are not real.</span></span> <span data-ttu-id="8b5d2-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8b5d2-163">Skontaktuj się z [zespołem pomocy technicznej klienta IdeaScale](http://support.ideascale.com/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="8b5d2-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="8b5d2-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8b5d2-168">Na powitania **konfiguracji IdeaScale** kliknij **skonfigurować IdeaScale** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-168">On hello **IdeaScale Configuration** section, click **Configure IdeaScale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8b5d2-169">Kopiuj hello **Sign-Out adresu URL i identyfikator jednostki SAML** z hello **sekcji krótki przewodnik**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="8b5d2-171">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy IdeaScale tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-171">In a different web browser window, log in tooyour IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="8b5d2-172">Przejdź za**ustawienia społeczności**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-172">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="8b5d2-173">![Ustawienia społeczności](./media/active-directory-saas-ideascale-tutorial/ic790847.png "ustawienia społeczności")</span><span class="sxs-lookup"><span data-stu-id="8b5d2-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="8b5d2-174">Przejdź za**zabezpieczeń \> jednego ustawienia logować**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-174">Go too**Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="8b5d2-175">![Pojedyncze ustawienia logować](./media/active-directory-saas-ideascale-tutorial/ic790848.png "pojedynczy logować ustawienia")</span><span class="sxs-lookup"><span data-stu-id="8b5d2-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="8b5d2-176">Jako **typu Pojedyncza**, wybierz pozycję **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="8b5d2-177">![Pojedynczy typ logować](./media/active-directory-saas-ideascale-tutorial/ic790849.png "pojedynczy typ logować")</span><span class="sxs-lookup"><span data-stu-id="8b5d2-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="8b5d2-178">Na powitania **jednego ustawienia logować** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8b5d2-178">On hello **Single Signon Settings** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="8b5d2-179">![Pojedyncze ustawienia logować](./media/active-directory-saas-ideascale-tutorial/ic790850.png "pojedynczy logować ustawienia")</span><span class="sxs-lookup"><span data-stu-id="8b5d2-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="8b5d2-180">a.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-180">a.</span></span> <span data-ttu-id="8b5d2-181">W **identyfikator jednostki IdP SAML** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-181">In **SAML IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8b5d2-182">b.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-182">b.</span></span> <span data-ttu-id="8b5d2-183">Kopiowanie zawartości hello pliku metadanych pobranych z portalu Azure i wklej go do hello **metadanych IdP SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-183">Copy hello content of your downloaded metadata file from Azure portal, and paste it into hello **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="8b5d2-184">c.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-184">c.</span></span> <span data-ttu-id="8b5d2-185">W **URL Powodzenie wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-185">In **Logout Success URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8b5d2-186">d.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-186">d.</span></span> <span data-ttu-id="8b5d2-187">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="8b5d2-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8b5d2-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8b5d2-189">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8b5d2-190">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8b5d2-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b5d2-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b5d2-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b5d2-192">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8b5d2-194">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8b5d2-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b5d2-195">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b5d2-197">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b5d2-199">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b5d2-201">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8b5d2-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b5d2-203">a.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-203">a.</span></span> <span data-ttu-id="8b5d2-204">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b5d2-205">b.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-205">b.</span></span> <span data-ttu-id="8b5d2-206">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b5d2-207">c.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-207">c.</span></span> <span data-ttu-id="8b5d2-208">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8b5d2-209">d.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-209">d.</span></span> <span data-ttu-id="8b5d2-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="8b5d2-211">Tworzenie użytkownika testowego IdeaScale</span><span class="sxs-lookup"><span data-stu-id="8b5d2-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="8b5d2-212">tooenable usługi Azure AD użytkownicy toolog do IdeaScale, muszą mieć przydzielone w tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-212">tooenable Azure AD users toolog into IdeaScale, they must be provisioned in tooIdeaScale.</span></span> <span data-ttu-id="8b5d2-213">W przypadku hello IdeaScale Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-213">In hello case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="8b5d2-214">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8b5d2-214">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b5d2-215">Zaloguj się za tooyour **IdeaScale** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-215">Log in tooyour **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="8b5d2-216">Przejdź za**ustawienia społeczności**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-216">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="8b5d2-217">![Ustawienia społeczności](./media/active-directory-saas-ideascale-tutorial/ic790847.png "ustawienia społeczności")</span><span class="sxs-lookup"><span data-stu-id="8b5d2-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="8b5d2-218">Przejdź za**podstawowe ustawienia \> zarządzania elementu członkowskiego**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-218">Go too**Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="8b5d2-219">Kliknij przycisk **dodać członka**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="8b5d2-220">![Element członkowski zarządzania](./media/active-directory-saas-ideascale-tutorial/ic790852.png "zarządzania elementu członkowskiego")</span><span class="sxs-lookup"><span data-stu-id="8b5d2-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="8b5d2-221">W sekcji Dodaj nowy element członkowski hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8b5d2-221">In hello Add New Member section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8b5d2-222">![Dodaj nowy element członkowski](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Dodaj nowy element członkowski")</span><span class="sxs-lookup"><span data-stu-id="8b5d2-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="8b5d2-223">a.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-223">a.</span></span> <span data-ttu-id="8b5d2-224">W hello **adresy E-mail** pole tekstowe, typ hello adres e-mail ma tooprovision prawidłowe konto usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-224">In hello **Email Addresses** textbox, type hello email address of a valid AAD account you want tooprovision.</span></span>
   
    <span data-ttu-id="8b5d2-225">b.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-225">b.</span></span> <span data-ttu-id="8b5d2-226">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="8b5d2-227">Właściciel konta usługi Azure Active Directory Hello pobiera wiadomości e-mail przy użyciu konta hello tooconfirm łącza, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-227">hello Azure Active Directory account holder gets an email with a link tooconfirm hello account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="8b5d2-228">Możesz użyć innych IdeaScale użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez IdeaScale tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8b5d2-229">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b5d2-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8b5d2-230">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIdeaScale.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8b5d2-232">**tooassign tooIdeaScale Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8b5d2-232">**tooassign Britta Simon tooIdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b5d2-233">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8b5d2-235">Z listy aplikacji hello wybierz **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-235">In hello applications list, select **IdeaScale**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="8b5d2-237">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8b5d2-239">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-239">Click **Add** button.</span></span> <span data-ttu-id="8b5d2-240">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8b5d2-242">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8b5d2-243">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b5d2-244">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8b5d2-245">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8b5d2-245">Testing single sign-on</span></span>


<span data-ttu-id="8b5d2-246">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8b5d2-247">Po kliknięciu kafelka IdeaScale hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour IdeaScale aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8b5d2-247">When you click hello IdeaScale tile in hello Access Panel, you should get automatically signed-on tooyour IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b5d2-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8b5d2-248">Additional resources</span></span>

* [<span data-ttu-id="8b5d2-249">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b5d2-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b5d2-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8b5d2-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

