---
title: 'Samouczek: Azure Active Directory integracji z pakietem Office wirtualnej 8 x 8 | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Office wirtualnej 8 x 8."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: df5c5de77285cd3912b68cc3b1e3eee274aa951c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="1e7a5-103">Samouczek: Azure Active Directory integracji z pakietem Office wirtualnej 8 x 8</span><span class="sxs-lookup"><span data-stu-id="1e7a5-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="1e7a5-104">Z tego samouczka, dowiesz się, jak toointegrate 8 x 8 wirtualnych Office z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e7a5-104">In this tutorial, you learn how toointegrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e7a5-105">Integrowanie 8 x 8 wirtualnych Office z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1e7a5-105">Integrating 8x8 Virtual Office with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1e7a5-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do too8x8 wirtualnej pakietu Office</span><span class="sxs-lookup"><span data-stu-id="1e7a5-106">You can control in Azure AD who has access too8x8 Virtual Office</span></span>
- <span data-ttu-id="1e7a5-107">Aby umożliwić użytkownikom uzyskać tooautomatically zalogowane too8x8 wirtualnych pakietu Office (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7a5-107">You can enable your users tooautomatically get signed-on too8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e7a5-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1e7a5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1e7a5-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e7a5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e7a5-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1e7a5-110">Prerequisites</span></span>

<span data-ttu-id="1e7a5-111">tooconfigure integracji usługi Azure AD z pakietem Office wirtualnej 8 x 8 należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1e7a5-111">tooconfigure Azure AD integration with 8x8 Virtual Office, you need hello following items:</span></span>

- <span data-ttu-id="1e7a5-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e7a5-113">8 x 8 wirtualnych Office logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1e7a5-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e7a5-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e7a5-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1e7a5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e7a5-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e7a5-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e7a5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e7a5-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1e7a5-118">Scenario description</span></span>
<span data-ttu-id="1e7a5-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e7a5-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1e7a5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e7a5-121">Dodawanie pakietu Office wirtualnej 8 x 8 z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1e7a5-121">Adding 8x8 Virtual Office from hello gallery</span></span>
2. <span data-ttu-id="1e7a5-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1e7a5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-hello-gallery"></a><span data-ttu-id="1e7a5-123">Dodawanie pakietu Office wirtualnej 8 x 8 z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1e7a5-123">Adding 8x8 Virtual Office from hello gallery</span></span>
<span data-ttu-id="1e7a5-124">tooconfigure hello integracji 8 x 8 wirtualnych Office z usługą Azure AD, należy tooadd 8 x 8 wirtualnych Office z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-124">tooconfigure hello integration of 8x8 Virtual Office into Azure AD, you need tooadd 8x8 Virtual Office from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1e7a5-125">**Wykonaj Office wirtualnych z galerii hello tooadd 8 x 8 hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1e7a5-125">**tooadd 8x8 Virtual Office from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e7a5-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1e7a5-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1e7a5-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="1e7a5-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="1e7a5-133">W polu wyszukiwania hello wpisz **8 x 8 wirtualnych Office**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-133">In hello search box, type **8x8 Virtual Office**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="1e7a5-135">W panelu wyników hello, wybierz **Office wirtualnej 8 x 8**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-135">In hello results panel, select **8x8 Virtual Office**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e7a5-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1e7a5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e7a5-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 8 x 8 Office wirtualnych opartych na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="1e7a5-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1e7a5-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jakie hello odpowiednikiem użytkownik w biurze wirtualnej 8 x 8 jest tooa w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 8x8 Virtual Office is tooa user in Azure AD.</span></span> <span data-ttu-id="1e7a5-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w 8 x 8 wirtualnych Office musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-140">In other words, a link relationship between an Azure AD user and hello related user in 8x8 Virtual Office needs toobe established.</span></span>

<span data-ttu-id="1e7a5-141">W pakiecie Office wirtualnej 8 x 8, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-141">In 8x8 Virtual Office, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1e7a5-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z pakietem Office wirtualnej 8 x 8, należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="1e7a5-142">tooconfigure and test Azure AD single sign-on with 8x8 Virtual Office, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1e7a5-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1e7a5-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e7a5-145">**[Tworzenie użytkownika testowego wirtualnego Office 8 x 8](#creating-a-8x8-virtual-office-test-user)**  -toohave odpowiednikiem Simona Britta w pakiecie Office wirtualnej 8 x 8, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - toohave a counterpart of Britta Simon in 8x8 Virtual Office that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e7a5-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e7a5-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e7a5-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1e7a5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e7a5-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji pakietu Office wirtualnego 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="1e7a5-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z pakietem Office wirtualnej 8 x 8, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1e7a5-150">**tooconfigure Azure AD single sign-on with 8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e7a5-151">W portalu Azure na powitania hello **8 x 8 wirtualnych Office** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-151">In hello Azure portal, on hello **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1e7a5-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="1e7a5-155">Na powitania **8 x 8 wirtualnych Office domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1e7a5-155">On hello **8x8 Virtual Office Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="1e7a5-157">a.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-157">a.</span></span> <span data-ttu-id="1e7a5-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="1e7a5-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="1e7a5-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="1e7a5-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="1e7a5-160">b.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-160">b.</span></span> <span data-ttu-id="1e7a5-161">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="1e7a5-161">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="1e7a5-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="1e7a5-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1e7a5-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-163">These values are not real.</span></span> <span data-ttu-id="1e7a5-164">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-164">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="1e7a5-165">Skontaktuj się z [zespołem pomocy technicznej wirtualnego Office 8 x 8](https://www.8x8.com/about-us/contact-us) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) tooget these values.</span></span>
 


4. <span data-ttu-id="1e7a5-166">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-166">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="1e7a5-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e7a5-170">Na powitania **konfiguracji wirtualnej 8 x 8** kliknij **Office wirtualnego Konfiguruj 8 x 8** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-170">On hello **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1e7a5-171">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="1e7a5-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="1e7a5-173">Dzierżawca wirtualnego Office logowania jednokrotnego tooyour 8 x 8 jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-173">Sign-on tooyour 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="1e7a5-174">Wybierz **Mgr konta Office wirtualnego** w aplikacji panelu.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="1e7a5-176">Wybierz **firm** konta toomanage, a następnie kliknij przycisk **logowania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-176">Select **Business** account toomanage and click **Sign In** button.</span></span>
   
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="1e7a5-178">Kliknij przycisk **kont** kartę hello menu listy.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-178">Click **Accounts** tab in hello menu list.</span></span>
   
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="1e7a5-180">Kliknij przycisk **rejestracji jednokrotnej** hello listy kont.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-180">Click **Single Sign On** in hello list of Accounts.</span></span>
   
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="1e7a5-182">Wybierz **rejestracji jednokrotnej** w obszarze metodę uwierzytelniania i kliknięcie **SAML**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="1e7a5-184">Kopiuj **adres URL logowania jednokrotnego SAML**, **pojedynczego rejestrują się adres URL usługi** i **adres URL wystawcy** z usługi Azure AD za**adres URL logowania**, **adresu URL wylogowania**  i **adres URL wystawcy** w pakiecie Office wirtualnego 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD too**Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="1e7a5-186">Kliknij przycisk **przeglądarki** przycisk tooupload hello certyfikatu, który został pobrany z usługi Azure AD, a następnie kliknij przycisk hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-186">Click **Browser** button tooupload hello certificate which you downloaded from Azure AD, and click hello **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="1e7a5-187">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="1e7a5-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1e7a5-188">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1e7a5-189">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e7a5-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e7a5-190">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7a5-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e7a5-191">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1e7a5-193">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1e7a5-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e7a5-194">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e7a5-196">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e7a5-198">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e7a5-200">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1e7a5-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e7a5-202">a.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-202">a.</span></span> <span data-ttu-id="1e7a5-203">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e7a5-204">b.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-204">b.</span></span> <span data-ttu-id="1e7a5-205">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e7a5-206">c.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-206">c.</span></span> <span data-ttu-id="1e7a5-207">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1e7a5-208">d.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-208">d.</span></span> <span data-ttu-id="1e7a5-209">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="1e7a5-210">Tworzenie użytkownika testowego wirtualnego Office 8 x 8</span><span class="sxs-lookup"><span data-stu-id="1e7a5-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="1e7a5-211">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w pakiecie Office wirtualnej 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-211">hello objective of this section is toocreate a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="1e7a5-212">8 x 8 wirtualnych Office obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1e7a5-213">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-213">There is no action item for you in this section.</span></span> <span data-ttu-id="1e7a5-214">Nowy użytkownik jest tworzona podczas próby tooaccess 8 x 8 Office wirtualnej Jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-214">A new user is created during an attempt tooaccess 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="1e7a5-215">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej wirtualnego Office 8 x 8](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="1e7a5-215">If you need toocreate a user manually, you need toocontact hello [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1e7a5-216">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7a5-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1e7a5-217">W tej sekcji, musisz włączyć Simona Britta toouse Azure logowania jednokrotnego za udzielanie dostępu too8x8 wirtualnych pakietu Office.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too8x8 Virtual Office.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1e7a5-219">**tooassign Simona Britta too8x8 wirtualnych pakietu Office, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1e7a5-219">**tooassign Britta Simon too8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e7a5-220">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1e7a5-222">Z listy aplikacji hello wybierz **8 x 8 wirtualnych Office**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-222">In hello applications list, select **8x8 Virtual Office**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="1e7a5-224">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="1e7a5-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-226">Click **Add** button.</span></span> <span data-ttu-id="1e7a5-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="1e7a5-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1e7a5-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e7a5-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e7a5-232">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1e7a5-232">Testing single sign-on</span></span>

<span data-ttu-id="1e7a5-233">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1e7a5-234">Po kliknięciu kafelka wirtualnego Office hello 8 x 8 w hello Panel dostępu, należy pobrać aplikacji pakietu Office wirtualnego automatycznie zalogowane tooyour 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="1e7a5-234">When you click hello 8x8 Virtual Office tile in hello Access Panel, you should get automatically signed-on tooyour 8x8 Virtual Office application.</span></span>
<span data-ttu-id="1e7a5-235">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="1e7a5-235">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e7a5-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1e7a5-236">Additional resources</span></span>

* [<span data-ttu-id="1e7a5-237">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e7a5-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e7a5-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e7a5-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

