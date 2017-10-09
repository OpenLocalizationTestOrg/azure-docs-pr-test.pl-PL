---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy przez Facebook | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i miejsca pracy przez usługi Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="5fa3e-103">Samouczek: Integracji Azure Active Directory z miejsca pracy przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="5fa3e-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="5fa3e-104">Z tego samouczka, dowiesz się, jak toointegrate miejsca pracy w serwisie Facebook w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fa3e-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fa3e-105">Integrowanie miejsca pracy przez Facebook z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5fa3e-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5fa3e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooWorkplace przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="5fa3e-106">You can control in Azure AD who has access tooWorkplace by Facebook</span></span>
- <span data-ttu-id="5fa3e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWorkplace przez Facebook (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fa3e-107">You can enable your users tooautomatically get signed-on tooWorkplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5fa3e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5fa3e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5fa3e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5fa3e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fa3e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5fa3e-110">Prerequisites</span></span>

<span data-ttu-id="5fa3e-111">tooconfigure integracji usługi Azure AD z miejsca pracy przez usługi Facebook, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5fa3e-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="5fa3e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fa3e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fa3e-113">Dołączanie w serwisie Facebook logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5fa3e-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fa3e-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fa3e-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5fa3e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fa3e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fa3e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fa3e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fa3e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5fa3e-118">Scenario description</span></span>
<span data-ttu-id="5fa3e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fa3e-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5fa3e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fa3e-121">Dodawanie miejsca pracy przez Facebook z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5fa3e-121">Adding Workplace by Facebook from hello gallery</span></span>
2. <span data-ttu-id="5fa3e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5fa3e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="5fa3e-123">Dodawanie miejsca pracy przez Facebook z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5fa3e-123">Adding Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="5fa3e-124">tooconfigure hello integracji miejsca pracy w serwisie Facebook w usłudze Azure Active Directory, należy tooadd miejsca pracy przez Facebook z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-124">tooconfigure hello integration of Workplace by Facebook into Azure AD, you need tooadd Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5fa3e-125">**tooadd miejsca pracy przez Facebook z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5fa3e-125">**tooadd Workplace by Facebook from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fa3e-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5fa3e-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5fa3e-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5fa3e-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5fa3e-133">W polu wyszukiwania hello wpisz **miejsca pracy przez Facebook**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-133">In hello search box, type **Workplace by Facebook**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="5fa3e-135">W panelu wyników hello, wybierz **miejsca pracy przez Facebook**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-135">In hello results panel, select **Workplace by Facebook**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5fa3e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5fa3e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5fa3e-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z miejsca pracy przez usługi Facebook na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5fa3e-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5fa3e-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w miejscu pracy przez Facebook jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="5fa3e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w miejscu pracy przez Facebook musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-140">In other words, a link relationship between an Azure AD user and hello related user in Workplace by Facebook needs toobe established.</span></span>

<span data-ttu-id="5fa3e-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="5fa3e-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z miejsca pracy przez usługi Facebook, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5fa3e-142">tooconfigure and test Azure AD single sign-on with Workplace by Facebook, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5fa3e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5fa3e-144">**[Konfigurowanie częstotliwości ponowne uwierzytelnianie](#configuring-reauthentication-frequency)**  -tooconfigure tooprompt dołączanie sprawdzania SAML.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - tooconfigure Workplace tooprompt for a SAML check.</span></span>
3. <span data-ttu-id="5fa3e-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="5fa3e-146">**[Tworzenie pracy przez użytkownika testowego Facebook](#creating-a-workplace-by-facebook-test-user)**  -toohave odpowiednikiem Simona Britta w miejscu pracy przez usługi Facebook, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - toohave a counterpart of Britta Simon in Workplace by Facebook that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="5fa3e-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="5fa3e-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5fa3e-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5fa3e-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5fa3e-150">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w miejscu pracy przez aplikację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="5fa3e-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z miejsca pracy przez Facebook, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5fa3e-151">**tooconfigure Azure AD single sign-on with Workplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fa3e-152">W portalu Azure na powitania hello **miejsca pracy przez Facebook** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-152">In hello Azure portal, on hello **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5fa3e-154">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="5fa3e-156">Na powitania **miejsca pracy przez domenę usługi Facebook i adresy URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5fa3e-156">On hello **Workplace by Facebook Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="5fa3e-158">a.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-158">a.</span></span> <span data-ttu-id="5fa3e-159">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="5fa3e-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="5fa3e-160">b.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-160">b.</span></span> <span data-ttu-id="5fa3e-161">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="5fa3e-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5fa3e-162">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-162">These values are not hello real.</span></span> <span data-ttu-id="5fa3e-163">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5fa3e-164">Skontaktuj się z [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="5fa3e-165">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="5fa3e-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5fa3e-169">Na powitania **miejsca pracy przez konfigurację usługi Facebook** , kliknij przycisk **skonfigurować miejsca pracy przez Facebook** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-169">On hello **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5fa3e-170">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5fa3e-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="5fa3e-172">W oknie przeglądarki innej witryny sieci web, tooyour logowania miejsca pracy przez Facebook witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-172">In a different web browser window, login tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="5fa3e-173">W ramach procesu uwierzytelniania SAML hello miejsce pracy mogą używać ciągów zapytań się too2.5 kilobajtów rozmiar w kolejności toopass parametry tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-173">As part of hello SAML authentication process, Workplace may utilize query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="5fa3e-174">W hello **pulpitu nawigacyjnego firmy**, przejdź toohello **uwierzytelniania** kartę.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-174">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="5fa3e-175">W obszarze **uwierzytelnianie SAML**, wybierz pozycję **logowania jednokrotnego tylko** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-175">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="5fa3e-176">Wartości wejściowe hello skopiowanych z **miejsca pracy przez konfigurację usługi Facebook** sekcji hello portalu Azure do odpowiednich pól hello:</span><span class="sxs-lookup"><span data-stu-id="5fa3e-176">Input hello values copied from **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="5fa3e-177">W **adres URL SAML** pole tekstowe, Wklej wartość hello **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-177">In **SAML URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="5fa3e-178">W **pole tekstowe adres URL wystawcy SAML**, Wklej wartość hello **SAML identyfikator jednostki**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-178">In **SAML Issuer URL textbox**, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="5fa3e-179">W **przekierowania wylogowania SAML** (opcjonalnie), Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-179">In **SAML Logout Redirect** (Optional), paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="5fa3e-180">Otwórz z **certyfikatu algorytmem base-64** w Notatniku pobrany z portalu Azure, skopiuj zawartość hello go do Schowka, a następnie wklej go toothe **certyfikatu SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="5fa3e-181">Może być konieczne tooenter hello odbiorców adres URL, adres URL odbiorcy, i adres URL ACS (usługa konsumenta potwierdzenia) w folderze hello **Konfiguracja SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-181">You may need tooenter hello Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="5fa3e-182">Przewiń toohello dolnej części sekcji hello i kliknij przycisk hello **Test rejestracji Jednokrotnej** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-182">Scroll toohello bottom of hello section and click hello **Test SSO** button.</span></span> <span data-ttu-id="5fa3e-183">Ten wyniki w oknie podręcznym znajdujących się ze strony logowania usługi Azure AD przedstawione.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="5fa3e-184">Wprowadź swoje poświadczenia w jako normalne tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-184">Enter your credentials in as normal tooauthenticate.</span></span> 

    <span data-ttu-id="5fa3e-185">**Rozwiązywanie problemów:** adres e-mail hello upewnij się, że zostały zwrócone z usługi Azure AD jest hello tak samo jak hello są rejestrowane przy użyciu konta w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-185">**Troubleshooting:** Ensure hello email address being returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="5fa3e-186">Po pomyślnym zakończeniu testu hello, przewiń toohello u dołu strony hello i kliknij przycisk hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-186">Once hello test has been completed successfully, scroll toohello bottom of hello page and click hello **Save** button.</span></span>

14. <span data-ttu-id="5fa3e-187">Wszyscy użytkownicy korzystający z miejsca pracy zostanie teraz wyświetlone strony logowania usługi Azure AD do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="5fa3e-188">**SAML wylogowania przekierowania (opcjonalnie)** -</span><span class="sxs-lookup"><span data-stu-id="5fa3e-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="5fa3e-189">Możesz skonfigurować toooptionally adresu Url wylogowania SAML, które mogą być używane toopoint na strony wylogowania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-189">You can choose toooptionally configure a SAML Logout Url, which can be used toopoint at Azure AD's logout page.</span></span> <span data-ttu-id="5fa3e-190">Gdy to ustawienie jest włączone i skonfigurowane, hello użytkownika nie będzie strony wylogowania toohello bezpośrednie miejsca pracy.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-190">When this setting is enabled and configured, hello user will no longer be directed toohello Workplace logout page.</span></span> <span data-ttu-id="5fa3e-191">Zamiast tego użytkownik hello będzie toohello przekierowany adres url, który został dodany w ustawieniu przekierowania wylogowania SAML hello.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-191">Instead, hello user will be redirected toohello url that was added in hello SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="5fa3e-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5fa3e-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5fa3e-193">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5fa3e-194">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5fa3e-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="5fa3e-195">Konfigurowanie częstotliwości ponowne uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="5fa3e-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="5fa3e-196">Można skonfigurować tooprompt pracy dotyczących sprawdzania SAML codziennie, trzy dni tygodnia, dwóch tygodni, miesięcy lub nigdy.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-196">You can configure Workplace tooprompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="5fa3e-197">Hello minimalną wartość sprawdzania SAML hello w aplikacjach mobilnych ustawiono tooone tygodnia.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-197">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="5fa3e-198">Możesz też wymusić SAML zresetować dla wszystkich użytkowników za pomocą przycisku hello: Wymagaj SAML uwierzytelnianie dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-198">You can also force a SAML reset for all users using hello button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5fa3e-199">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fa3e-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="5fa3e-200">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5fa3e-202">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5fa3e-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fa3e-203">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5fa3e-205">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5fa3e-207">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5fa3e-209">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5fa3e-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5fa3e-211">a.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-211">a.</span></span> <span data-ttu-id="5fa3e-212">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5fa3e-213">b.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-213">b.</span></span> <span data-ttu-id="5fa3e-214">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5fa3e-215">c.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-215">c.</span></span> <span data-ttu-id="5fa3e-216">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5fa3e-217">d.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-217">d.</span></span> <span data-ttu-id="5fa3e-218">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="5fa3e-219">Tworzenie pracy przez użytkownika testowego usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="5fa3e-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="5fa3e-220">W tej sekcji o nazwie Simona Britta tworzenia użytkownika w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="5fa3e-221">Obszar roboczy w serwisie Facebook obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="5fa3e-222">Brak akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-222">There is no action for you in this section.</span></span> <span data-ttu-id="5fa3e-223">Jeśli użytkownik nie istnieje w miejscu pracy przez usługi Facebook, nowy jest tworzona podczas próby tooaccess miejsca pracy przez Facebook.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="5fa3e-224">Jeśli potrzebujesz toocreate użytkownik ręcznie, skontaktuj się z [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="5fa3e-224">If you need toocreate a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5fa3e-225">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fa3e-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5fa3e-226">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWorkplace przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkplace by Facebook.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5fa3e-228">**tooassign tooWorkplace Simona Britta przez Facebook, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5fa3e-228">**tooassign Britta Simon tooWorkplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fa3e-229">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5fa3e-231">Z listy aplikacji hello wybierz **miejsca pracy przez Facebook**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-231">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="5fa3e-233">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5fa3e-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-235">Click **Add** button.</span></span> <span data-ttu-id="5fa3e-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5fa3e-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5fa3e-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fa3e-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5fa3e-241">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5fa3e-241">Testing single sign-on</span></span>

<span data-ttu-id="5fa3e-242">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5fa3e-242">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>
<span data-ttu-id="5fa3e-243">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5fa3e-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5fa3e-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5fa3e-244">Additional resources</span></span>

* [<span data-ttu-id="5fa3e-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fa3e-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5fa3e-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5fa3e-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5fa3e-247">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="5fa3e-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

