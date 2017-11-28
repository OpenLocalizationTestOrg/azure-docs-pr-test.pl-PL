---
title: 'Samouczek: Integracji Azure Active Directory z przodu | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między Azure Active Directory i do przodu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="a198a-103">Samouczek: Integracji Azure Active Directory z przodu</span><span class="sxs-lookup"><span data-stu-id="a198a-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="a198a-104">Z tego samouczka, dowiesz się, jak toointegrate przodu z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a198a-104">In this tutorial, you learn how toointegrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a198a-105">Integrowanie przodu z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a198a-105">Integrating Front with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a198a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFront.</span><span class="sxs-lookup"><span data-stu-id="a198a-106">You can control in Azure AD who has access tooFront.</span></span>
- <span data-ttu-id="a198a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFront (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a198a-107">You can enable your users tooautomatically get signed-on tooFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a198a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a198a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a198a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a198a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a198a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a198a-110">Prerequisites</span></span>

<span data-ttu-id="a198a-111">Integracja tooconfigure usługi Azure AD z przodu, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a198a-111">tooconfigure Azure AD integration with Front, you need hello following items:</span></span>

- <span data-ttu-id="a198a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a198a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a198a-113">Front logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a198a-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a198a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a198a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a198a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a198a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a198a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a198a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a198a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a198a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a198a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a198a-118">Scenario description</span></span>
<span data-ttu-id="a198a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a198a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a198a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a198a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a198a-121">Dodawanie przodu z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a198a-121">Adding Front from hello gallery</span></span>
2. <span data-ttu-id="a198a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a198a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-hello-gallery"></a><span data-ttu-id="a198a-123">Dodawanie przodu z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a198a-123">Adding Front from hello gallery</span></span>
<span data-ttu-id="a198a-124">tooconfigure hello integracji przodu do usługi Azure AD, należy tooadd przodu z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a198a-124">tooconfigure hello integration of Front into Azure AD, you need tooadd Front from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a198a-125">**tooadd przodu z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a198a-125">**tooadd Front from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a198a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a198a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="a198a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a198a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a198a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a198a-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="a198a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a198a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="a198a-133">W polu wyszukiwania hello wpisz **Front**, wybierz pozycję **Front** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a198a-133">In hello search box, type **Front**, select **Front** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Front hello listy wyników](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a198a-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a198a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a198a-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przodu w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="a198a-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a198a-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow na wierzchu użytkownika odpowiednikiem hello jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a198a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Front is tooa user in Azure AD.</span></span> <span data-ttu-id="a198a-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi na wierzchu musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="a198a-138">In other words, a link relationship between an Azure AD user and hello related user in Front needs toobe established.</span></span>

<span data-ttu-id="a198a-139">Na wierzchu przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="a198a-139">In Front, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a198a-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z przodu, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a198a-140">tooconfigure and test Azure AD single sign-on with Front, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a198a-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a198a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a198a-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a198a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a198a-143">**[Tworzenie użytkownika testowego przodu](#create-a-front-test-user)**  -toohave Simona Britta w odpowiednikiem na wierzchu toohello połączonej usługi Azure AD reprezentacja użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a198a-143">**[Create a Front test user](#create-a-front-test-user)** - toohave a counterpart of Britta Simon in Front that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a198a-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a198a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a198a-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="a198a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a198a-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a198a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a198a-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne do przodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a198a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="a198a-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z przodu, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a198a-148">**tooconfigure Azure AD single sign-on with Front, perform hello following steps:**</span></span>

1. <span data-ttu-id="a198a-149">W portalu Azure na powitania hello **Front** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a198a-149">In hello Azure portal, on hello **Front** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="a198a-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a198a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="a198a-153">Na powitania **Front domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="a198a-153">On hello **Front Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="a198a-155">a.</span><span class="sxs-lookup"><span data-stu-id="a198a-155">a.</span></span> <span data-ttu-id="a198a-156">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="a198a-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="a198a-157">b.</span><span class="sxs-lookup"><span data-stu-id="a198a-157">b.</span></span> <span data-ttu-id="a198a-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="a198a-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="a198a-159">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="a198a-159">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="a198a-161">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="a198a-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a198a-162">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a198a-162">These values are not real.</span></span> <span data-ttu-id="a198a-163">Aktualizacja tych wartości za pomocą hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, które opisano szczegółowo w dalszej części samouczka lub skontaktuj się z [zespołem pomocy technicznej klienta Front](mailto:support@frontapp.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="a198a-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) tooget these values.</span></span> 

5. <span data-ttu-id="a198a-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a198a-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="a198a-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a198a-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a198a-168">Na powitania **konfiguracji frontonu** kliknij **skonfigurować Front** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="a198a-168">On hello **Front Configuration** section, click **Configure Front** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a198a-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="a198a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="a198a-171">Dzierżawca przodu tooyour logowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a198a-171">Sign-on tooyour Front tenant as an administrator.</span></span>

9. <span data-ttu-id="a198a-172">Przejdź za**ustawień (koło zębate ikonę u dołu po lewej stronie paska bocznego hello hello) > Preferencje**.</span><span class="sxs-lookup"><span data-stu-id="a198a-172">Go too**Settings (cog icon at hello bottom of hello left sidebar) > Preferences**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="a198a-174">Kliknij przycisk **rejestracji jednokrotnej** łącza.</span><span class="sxs-lookup"><span data-stu-id="a198a-174">Click **Single Sign On** link.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="a198a-176">Wybierz **SAML** liście rozwijanej hello **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="a198a-176">Select **SAML** in hello drop-down list of **Single Sign On**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="a198a-178">W hello **punktu wejścia** pole tekstowe umieścić wartość hello **pojedynczy znak na adres URL usługi** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a198a-178">In hello **Entry Point** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="a198a-180">Otwórz z pobranego **Certificate(Base64)** pliku w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu podpisywania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a198a-180">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Signing certificate** textbox.</span></span>
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="a198a-182">Na powitania **ustawień dostawcy usług** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a198a-182">On hello **Service provider settings** section, perform hello following steps:</span></span>

    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="a198a-184">a.</span><span class="sxs-lookup"><span data-stu-id="a198a-184">a.</span></span> <span data-ttu-id="a198a-185">Skopiuj wartość hello **identyfikator jednostki** i wklej go do hello **identyfikator** textbox w **Front domeny i adres URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a198a-185">Copy hello value of **Entity ID** and paste it into hello **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="a198a-186">b.</span><span class="sxs-lookup"><span data-stu-id="a198a-186">b.</span></span> <span data-ttu-id="a198a-187">Skopiuj wartość hello **adres URL usługi ACS** i wklej go do hello **adres URL logowania** textbox w **Front domeny i adres URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a198a-187">Copy hello value of **ACS URL** and paste it into hello **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="a198a-188">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a198a-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="a198a-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="a198a-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a198a-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="a198a-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a198a-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a198a-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a198a-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a198a-192">Create an Azure AD test user</span></span>

<span data-ttu-id="a198a-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="a198a-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="a198a-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a198a-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a198a-196">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a198a-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a198a-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a198a-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a198a-200">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="a198a-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a198a-202">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a198a-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a198a-204">a.</span><span class="sxs-lookup"><span data-stu-id="a198a-204">a.</span></span> <span data-ttu-id="a198a-205">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a198a-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a198a-206">b.</span><span class="sxs-lookup"><span data-stu-id="a198a-206">b.</span></span> <span data-ttu-id="a198a-207">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a198a-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a198a-208">c.</span><span class="sxs-lookup"><span data-stu-id="a198a-208">c.</span></span> <span data-ttu-id="a198a-209">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="a198a-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a198a-210">d.</span><span class="sxs-lookup"><span data-stu-id="a198a-210">d.</span></span> <span data-ttu-id="a198a-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a198a-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="a198a-212">Tworzenie użytkownika testowego przodu</span><span class="sxs-lookup"><span data-stu-id="a198a-212">Create a Front test user</span></span>

<span data-ttu-id="a198a-213">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta na wierzchu.</span><span class="sxs-lookup"><span data-stu-id="a198a-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="a198a-214">Praca z [zespołem pomocy technicznej klienta Front](mailto:support@frontapp.com) do dodawania użytkowników hello hello przodu platformy.</span><span class="sxs-lookup"><span data-stu-id="a198a-214">Work with [Front Client support team](mailto:support@frontapp.com) to add hello users in hello Front platform.</span></span> <span data-ttu-id="a198a-215">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a198a-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a198a-216">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a198a-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a198a-217">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooFront.</span><span class="sxs-lookup"><span data-stu-id="a198a-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFront.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="a198a-219">**tooassign tooFront Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a198a-219">**tooassign Britta Simon tooFront, perform hello following steps:**</span></span>

1. <span data-ttu-id="a198a-220">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a198a-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a198a-222">Z listy aplikacji hello wybierz **Front**.</span><span class="sxs-lookup"><span data-stu-id="a198a-222">In hello applications list, select **Front**.</span></span>

    ![łącze przodu Hello na liście aplikacji hello](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="a198a-224">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a198a-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="a198a-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a198a-226">Click **Add** button.</span></span> <span data-ttu-id="a198a-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a198a-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="a198a-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a198a-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a198a-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a198a-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a198a-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a198a-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a198a-232">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a198a-232">Test single sign-on</span></span>

<span data-ttu-id="a198a-233">Celem Hello w tej sekcji jest tootest przy użyciu usługi Azure AD SSOconfiguration hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a198a-233">hello objective of this section is tootest your Azure AD SSOconfiguration using hello Access Panel.</span></span>

<span data-ttu-id="a198a-234">Po kliknięciu kafelka przodu hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour przodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a198a-234">When you click hello Front tile in hello Access Panel, you should get automatically signed-on tooyour Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a198a-235">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a198a-235">Additional resources</span></span>

* [<span data-ttu-id="a198a-236">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a198a-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a198a-237">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a198a-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

