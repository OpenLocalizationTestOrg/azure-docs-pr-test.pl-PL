---
title: 'Samouczek: Integracji Azure Active Directory z TeamSeer | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="c7351-103">Samouczek: Integracji Azure Active Directory z TeamSeer</span><span class="sxs-lookup"><span data-stu-id="c7351-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="c7351-104">Z tego samouczka, dowiesz się, jak toointegrate TeamSeer w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7351-104">In this tutorial, you learn how toointegrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7351-105">Integracja z usługą Azure AD TeamSeer zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c7351-105">Integrating TeamSeer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c7351-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTeamSeer</span><span class="sxs-lookup"><span data-stu-id="c7351-106">You can control in Azure AD who has access tooTeamSeer</span></span>
- <span data-ttu-id="c7351-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTeamSeer (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7351-107">You can enable your users tooautomatically get signed-on tooTeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7351-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c7351-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c7351-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7351-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7351-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c7351-110">Prerequisites</span></span>

<span data-ttu-id="c7351-111">tooconfigure integracji z usługą Azure AD z TeamSeer należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c7351-111">tooconfigure Azure AD integration with TeamSeer, you need hello following items:</span></span>

- <span data-ttu-id="c7351-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7351-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7351-113">TeamSeer jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c7351-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7351-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7351-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7351-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c7351-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7351-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c7351-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7351-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7351-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7351-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c7351-118">Scenario description</span></span>
<span data-ttu-id="c7351-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c7351-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7351-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c7351-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7351-121">Dodawanie TeamSeer z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c7351-121">Adding TeamSeer from hello gallery</span></span>
2. <span data-ttu-id="c7351-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c7351-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-hello-gallery"></a><span data-ttu-id="c7351-123">Dodawanie TeamSeer z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c7351-123">Adding TeamSeer from hello gallery</span></span>
<span data-ttu-id="c7351-124">tooconfigure hello integracji TeamSeer w tooAzure AD, należy tooadd TeamSeer z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c7351-124">tooconfigure hello integration of TeamSeer in tooAzure AD, you need tooadd TeamSeer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c7351-125">**tooadd TeamSeer z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c7351-125">**tooadd TeamSeer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7351-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c7351-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c7351-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c7351-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c7351-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c7351-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c7351-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7351-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c7351-133">W polu wyszukiwania hello wpisz **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="c7351-133">In hello search box, type **TeamSeer**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="c7351-135">W panelu wyników hello zaznacz **TeamSeer**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c7351-135">In hello results panel, select **TeamSeer**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7351-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c7351-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7351-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TeamSeer na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="c7351-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7351-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w TeamSeer jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7351-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TeamSeer is tooa user in Azure AD.</span></span> <span data-ttu-id="c7351-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w TeamSeer musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="c7351-140">In other words, a link relationship between an Azure AD user and hello related user in TeamSeer needs toobe established.</span></span>

<span data-ttu-id="c7351-141">W TeamSeer, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="c7351-141">In TeamSeer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c7351-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z TeamSeer, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c7351-142">tooconfigure and test Azure AD single sign-on with TeamSeer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c7351-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c7351-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c7351-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c7351-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7351-145">**[Tworzenie użytkownika testowego TeamSeer](#creating-a-teamseer-test-user)**  -toohave odpowiednikiem Simona Britta w TeamSeer, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c7351-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - toohave a counterpart of Britta Simon in TeamSeer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7351-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c7351-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7351-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="c7351-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7351-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c7351-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7351-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="c7351-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="c7351-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z TeamSeer, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c7351-150">**tooconfigure Azure AD single sign-on with TeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7351-151">W portalu Azure na powitania hello **TeamSeer** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c7351-151">In hello Azure portal, on hello **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c7351-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c7351-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="c7351-155">Na powitania **TeamSeer domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c7351-155">On hello **TeamSeer Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="c7351-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="c7351-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7351-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c7351-158">hello value is not real.</span></span> <span data-ttu-id="c7351-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="c7351-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c7351-160">Skontaktuj się z [zespołem pomocy technicznej klienta TeamSeer](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="c7351-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello value.</span></span> 
 
4. <span data-ttu-id="c7351-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c7351-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="c7351-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c7351-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7351-165">Na powitania **konfiguracji TeamSeer** kliknij **skonfigurować TeamSeer** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c7351-165">On hello **TeamSeer Configuration** section, click **Configure TeamSeer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c7351-166">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c7351-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="c7351-168">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy TeamSeer tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c7351-168">In a different web browser window, log in tooyour TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="c7351-169">Przejdź za**HR Admin**.</span><span class="sxs-lookup"><span data-stu-id="c7351-169">Go too**HR Admin**.</span></span>
   
    <span data-ttu-id="c7351-170">![Administrator HR](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR administratora")</span><span class="sxs-lookup"><span data-stu-id="c7351-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="c7351-171">Kliknij przycisk **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="c7351-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="c7351-172">![Instalator](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="c7351-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="c7351-173">Kliknij przycisk **konfigurowanie szczegóły dostawcy SAML**.</span><span class="sxs-lookup"><span data-stu-id="c7351-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="c7351-174">![Ustawienia SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "ustawienia SAML")</span><span class="sxs-lookup"><span data-stu-id="c7351-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="c7351-175">W sekcji Szczegóły dostawcy SAML hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c7351-175">In hello SAML provider details section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c7351-176">![Ustawienia SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "ustawienia SAML")</span><span class="sxs-lookup"><span data-stu-id="c7351-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="c7351-177">a.</span><span class="sxs-lookup"><span data-stu-id="c7351-177">a.</span></span> <span data-ttu-id="c7351-178">Wklej hello **pojedynczy znak na adres URL usługi** wartość toohello **adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c7351-178">Paste hello **Single Sign-On Service URL** value in toohello **URL** textbox.</span></span>
          
    <span data-ttu-id="c7351-179">b.</span><span class="sxs-lookup"><span data-stu-id="c7351-179">b.</span></span> <span data-ttu-id="c7351-180">Otwórz certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go w Schowku tooyour, a następnie wklej go toohello **certyfikatu publicznego IdP** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c7351-180">Open your base-64 encoded certificate in notepad, copy hello content of it in tooyour clipboard, and then paste it toohello **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="c7351-181">Witaj toocomplete SAML dostawcy konfiguracji, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c7351-181">toocomplete hello SAML provider configuration, perform hello following steps:</span></span>
    
    <span data-ttu-id="c7351-182">![Ustawienia SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "ustawienia SAML")</span><span class="sxs-lookup"><span data-stu-id="c7351-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="c7351-183">a.</span><span class="sxs-lookup"><span data-stu-id="c7351-183">a.</span></span> <span data-ttu-id="c7351-184">W hello **Test adresy E-mail**, wpisz adres e-mail użytkownika testowego hello.</span><span class="sxs-lookup"><span data-stu-id="c7351-184">In hello **Test Email Addresses**, type hello test user’s email address.</span></span> 
  
    <span data-ttu-id="c7351-185">b.</span><span class="sxs-lookup"><span data-stu-id="c7351-185">b.</span></span> <span data-ttu-id="c7351-186">W hello **wystawcy** pole tekstowe, typ hello adres URL wystawcy hello dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="c7351-186">In hello **Issuer** textbox, type hello Issuer URL of hello service provider.</span></span> 
  
    <span data-ttu-id="c7351-187">c.</span><span class="sxs-lookup"><span data-stu-id="c7351-187">c.</span></span> <span data-ttu-id="c7351-188">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c7351-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c7351-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="c7351-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c7351-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="c7351-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c7351-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7351-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7351-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7351-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7351-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="c7351-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c7351-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c7351-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7351-196">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c7351-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7351-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c7351-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7351-200">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7351-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7351-202">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c7351-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7351-204">a.</span><span class="sxs-lookup"><span data-stu-id="c7351-204">a.</span></span> <span data-ttu-id="c7351-205">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7351-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7351-206">b.</span><span class="sxs-lookup"><span data-stu-id="c7351-206">b.</span></span> <span data-ttu-id="c7351-207">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7351-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7351-208">c.</span><span class="sxs-lookup"><span data-stu-id="c7351-208">c.</span></span> <span data-ttu-id="c7351-209">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c7351-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c7351-210">d.</span><span class="sxs-lookup"><span data-stu-id="c7351-210">d.</span></span> <span data-ttu-id="c7351-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c7351-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="c7351-212">Tworzenie użytkownika testowego TeamSeer</span><span class="sxs-lookup"><span data-stu-id="c7351-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="c7351-213">toolog użytkowników tooenable usługi Azure AD w tooTeamSeer, muszą mieć przydzielone w tooShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="c7351-213">tooenable Azure AD users toolog in tooTeamSeer, they must be provisioned in tooShiftPlanning.</span></span> <span data-ttu-id="c7351-214">W przypadku hello TeamSeer Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="c7351-214">In hello case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="c7351-215">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c7351-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7351-216">Zaloguj się za tooyour **TeamSeer** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c7351-216">Log in tooyour **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="c7351-217">Wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c7351-217">Perform hello following steps:</span></span>
   
    <span data-ttu-id="c7351-218">![Administrator HR](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR administratora")</span><span class="sxs-lookup"><span data-stu-id="c7351-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="c7351-219">a.</span><span class="sxs-lookup"><span data-stu-id="c7351-219">a.</span></span> <span data-ttu-id="c7351-220">Przejdź za**HR Admin \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="c7351-220">Go too**HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="c7351-221">b.</span><span class="sxs-lookup"><span data-stu-id="c7351-221">b.</span></span> <span data-ttu-id="c7351-222">Kliknij przycisk **Uruchom Kreatora nowego użytkownika hello**.</span><span class="sxs-lookup"><span data-stu-id="c7351-222">Click **Run hello New User wizard**.</span></span>

3. <span data-ttu-id="c7351-223">W hello **szczegóły użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c7351-223">In hello **User Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c7351-224">![Szczegóły użytkownika](./media/active-directory-saas-teamseer-tutorial/ic789641.png "szczegóły użytkownika")</span><span class="sxs-lookup"><span data-stu-id="c7351-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="c7351-225">a.</span><span class="sxs-lookup"><span data-stu-id="c7351-225">a.</span></span> <span data-ttu-id="c7351-226">Typ hello **imię**, **nazwisko**, **nazwę użytkownika (adres E-mail)** z prawidłowego konta usługi AAD ma tooprovision w toohello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="c7351-226">Type hello **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want tooprovision in toohello related textboxes.</span></span>
  
    <span data-ttu-id="c7351-227">b.</span><span class="sxs-lookup"><span data-stu-id="c7351-227">b.</span></span> <span data-ttu-id="c7351-228">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="c7351-228">Click **Next**.</span></span>

4. <span data-ttu-id="c7351-229">Wykonaj hello na ekranie instrukcje dotyczące dodawania nowego użytkownika, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="c7351-229">Follow hello on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="c7351-230">Możesz użyć innych TeamSeer użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez TeamSeer tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7351-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c7351-231">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7351-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c7351-232">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTeamSeer.</span><span class="sxs-lookup"><span data-stu-id="c7351-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTeamSeer.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c7351-234">**tooassign tooTeamSeer Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c7351-234">**tooassign Britta Simon tooTeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7351-235">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c7351-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c7351-237">Z listy aplikacji hello wybierz **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="c7351-237">In hello applications list, select **TeamSeer**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="c7351-239">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c7351-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c7351-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c7351-241">Click **Add** button.</span></span> <span data-ttu-id="c7351-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7351-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c7351-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c7351-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c7351-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7351-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7351-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7351-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7351-247">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c7351-247">Testing single sign-on</span></span>

<span data-ttu-id="c7351-248">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c7351-248">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="c7351-249">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7351-249">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7351-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c7351-250">Additional resources</span></span>

* [<span data-ttu-id="c7351-251">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7351-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7351-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7351-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

