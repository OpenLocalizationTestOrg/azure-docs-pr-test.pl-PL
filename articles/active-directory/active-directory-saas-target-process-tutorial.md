---
title: 'Samouczek: Integracji Azure Active Directory z TargetProcess | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="61dd4-103">Samouczek: Integracji Azure Active Directory z TargetProcess</span><span class="sxs-lookup"><span data-stu-id="61dd4-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="61dd4-104">Z tego samouczka, dowiesz się, jak toointegrate TargetProcess w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61dd4-104">In this tutorial, you learn how toointegrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61dd4-105">Integracja z usługą Azure AD TargetProcess zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="61dd4-105">Integrating TargetProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="61dd4-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTargetProcess</span><span class="sxs-lookup"><span data-stu-id="61dd4-106">You can control in Azure AD who has access tooTargetProcess</span></span>
- <span data-ttu-id="61dd4-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTargetProcess (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="61dd4-107">You can enable your users tooautomatically get signed-on tooTargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61dd4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="61dd4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="61dd4-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="61dd4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61dd4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="61dd4-110">Prerequisites</span></span>

<span data-ttu-id="61dd4-111">tooconfigure integracji z usługą Azure AD z TargetProcess należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="61dd4-111">tooconfigure Azure AD integration with TargetProcess, you need hello following items:</span></span>

- <span data-ttu-id="61dd4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="61dd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61dd4-113">TargetProcess logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="61dd4-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61dd4-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="61dd4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61dd4-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="61dd4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61dd4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="61dd4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61dd4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61dd4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61dd4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="61dd4-118">Scenario description</span></span>
<span data-ttu-id="61dd4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="61dd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61dd4-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="61dd4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61dd4-121">Dodaj TargetProcess z galerii hello</span><span class="sxs-lookup"><span data-stu-id="61dd4-121">Add TargetProcess from hello gallery</span></span>
2. <span data-ttu-id="61dd4-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="61dd4-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-hello-gallery"></a><span data-ttu-id="61dd4-123">Dodaj TargetProcess z galerii hello</span><span class="sxs-lookup"><span data-stu-id="61dd4-123">Add TargetProcess from hello gallery</span></span>
<span data-ttu-id="61dd4-124">tooconfigure hello integracji TargetProcess do usługi Azure AD, należy tooadd TargetProcess z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="61dd4-124">tooconfigure hello integration of TargetProcess into Azure AD, you need tooadd TargetProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="61dd4-125">**tooadd TargetProcess z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="61dd4-125">**tooadd TargetProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="61dd4-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="61dd4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="61dd4-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="61dd4-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="61dd4-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61dd4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="61dd4-133">W polu wyszukiwania hello wpisz **TargetProcess**, wybierz pozycję **TargetProcess** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="61dd4-133">In hello search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Dodaj TargetProcess z galerii](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="61dd4-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="61dd4-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="61dd4-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TargetProcess w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="61dd4-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="61dd4-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w TargetProcess jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61dd4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TargetProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="61dd4-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w TargetProcess musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="61dd4-138">In other words, a link relationship between an Azure AD user and hello related user in TargetProcess needs toobe established.</span></span>

<span data-ttu-id="61dd4-139">W TargetProcess, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="61dd4-139">In TargetProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="61dd4-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z TargetProcess, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="61dd4-140">tooconfigure and test Azure AD single sign-on with TargetProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="61dd4-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="61dd4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="61dd4-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="61dd4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="61dd4-143">**[Tworzenie użytkownika testowego TargetProcess](#create-a-targetprocess-test-user)**  -toohave odpowiednikiem Simona Britta w TargetProcess, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="61dd4-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - toohave a counterpart of Britta Simon in TargetProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="61dd4-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="61dd4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="61dd4-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="61dd4-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="61dd4-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="61dd4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="61dd4-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="61dd4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="61dd4-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z TargetProcess, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="61dd4-148">**tooconfigure Azure AD single sign-on with TargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="61dd4-149">W portalu Azure na powitania hello **TargetProcess** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-149">In hello Azure portal, on hello **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="61dd4-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="61dd4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="61dd4-153">Na powitania **TargetProcess domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="61dd4-153">On hello **TargetProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Sekcja TargetProcess domeny i adresy URL](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="61dd4-155">a.</span><span class="sxs-lookup"><span data-stu-id="61dd4-155">a.</span></span> <span data-ttu-id="61dd4-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="61dd4-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="61dd4-157">b.</span><span class="sxs-lookup"><span data-stu-id="61dd4-157">b.</span></span> <span data-ttu-id="61dd4-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="61dd4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61dd4-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="61dd4-159">These values are not real.</span></span> <span data-ttu-id="61dd4-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="61dd4-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="61dd4-161">Skontaktuj się z [zespołem pomocy technicznej klienta TargetProcess](mailto:support@targetprocess.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="61dd4-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="61dd4-162">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="61dd4-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="61dd4-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="61dd4-164">Click **Save** button.</span></span>

    ![Przyciskiem Zapisz](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="61dd4-166">Na powitania **konfiguracji TargetProcess** kliknij **skonfigurować TargetProcess** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="61dd4-166">On hello **TargetProcess Configuration** section, click **Configure TargetProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="61dd4-167">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="61dd4-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sekcja konfiguracji TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="61dd4-169">Zaloguj się na tooyour TargetProcess aplikacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="61dd4-169">Sign-on tooyour TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="61dd4-170">W menu hello na górze hello, kliknij przycisk **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-170">In hello menu on hello top, click **Setup**.</span></span>
   
    ![Konfiguracja](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="61dd4-172">Kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-172">Click **Settings**.</span></span>
   
    ![Ustawienia](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="61dd4-174">Kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-174">Click **Single Sign-on**.</span></span>
   
    ![Kliknij przycisk rejestracji jednokrotnej](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="61dd4-176">Na powitania rejestracji jednokrotnej okno dialogowe Ustawienia należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="61dd4-176">On hello Single Sign-on settings dialog, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="61dd4-178">a.</span><span class="sxs-lookup"><span data-stu-id="61dd4-178">a.</span></span> <span data-ttu-id="61dd4-179">Kliknij przycisk **Włącz rejestrację jednokrotną**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="61dd4-180">b.</span><span class="sxs-lookup"><span data-stu-id="61dd4-180">b.</span></span> <span data-ttu-id="61dd4-181">W **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="61dd4-181">In **Sign-on URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="61dd4-182">c.</span><span class="sxs-lookup"><span data-stu-id="61dd4-182">c.</span></span> <span data-ttu-id="61dd4-183">Otwórz pobrany certyfikat w Notatniku, hello kopiowania zawartości, a następnie wklej go do hello **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="61dd4-183">Open your downloaded certificate in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="61dd4-184">d.</span><span class="sxs-lookup"><span data-stu-id="61dd4-184">d.</span></span> <span data-ttu-id="61dd4-185">Kliknij przycisk **włączyć udostępniania JIT**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="61dd4-186">e.</span><span class="sxs-lookup"><span data-stu-id="61dd4-186">e.</span></span> <span data-ttu-id="61dd4-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="61dd4-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="61dd4-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="61dd4-189">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="61dd4-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="61dd4-190">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61dd4-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="61dd4-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="61dd4-191">Create an Azure AD test user</span></span>
<span data-ttu-id="61dd4-192">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="61dd4-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="61dd4-194">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="61dd4-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="61dd4-195">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="61dd4-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="61dd4-197">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![toodisplay hello listę użytkowników](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="61dd4-199">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61dd4-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Dodawanie przycisku](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="61dd4-201">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="61dd4-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Sekcja użytkownika](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61dd4-203">a.</span><span class="sxs-lookup"><span data-stu-id="61dd4-203">a.</span></span> <span data-ttu-id="61dd4-204">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61dd4-205">b.</span><span class="sxs-lookup"><span data-stu-id="61dd4-205">b.</span></span> <span data-ttu-id="61dd4-206">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="61dd4-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="61dd4-207">c.</span><span class="sxs-lookup"><span data-stu-id="61dd4-207">c.</span></span> <span data-ttu-id="61dd4-208">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="61dd4-209">d.</span><span class="sxs-lookup"><span data-stu-id="61dd4-209">d.</span></span> <span data-ttu-id="61dd4-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="61dd4-211">Tworzenie użytkownika testowego TargetProcess</span><span class="sxs-lookup"><span data-stu-id="61dd4-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="61dd4-212">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="61dd4-212">hello objective of this section is toocreate a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="61dd4-213">TargetProcess obsługę w czasie.</span><span class="sxs-lookup"><span data-stu-id="61dd4-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="61dd4-214">Została już włączona w [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="61dd4-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="61dd4-215">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="61dd4-215">There is no action item for you in this section.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="61dd4-216">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="61dd4-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="61dd4-217">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTargetProcess.</span><span class="sxs-lookup"><span data-stu-id="61dd4-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTargetProcess.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="61dd4-219">**tooassign tooTargetProcess Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="61dd4-219">**tooassign Britta Simon tooTargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="61dd4-220">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="61dd4-222">Z listy aplikacji hello wybierz **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-222">In hello applications list, select **TargetProcess**.</span></span>

    ![TargetProcess listy aplikacji](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="61dd4-224">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="61dd4-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="61dd4-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="61dd4-226">Click **Add** button.</span></span> <span data-ttu-id="61dd4-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61dd4-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="61dd4-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="61dd4-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="61dd4-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61dd4-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="61dd4-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61dd4-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="61dd4-232">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="61dd4-232">Test single sign-on</span></span>

<span data-ttu-id="61dd4-233">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="61dd4-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="61dd4-234">Po kliknięciu powitalne TargetProcess kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour TargetProcess aplikacji.</span><span class="sxs-lookup"><span data-stu-id="61dd4-234">When you click hello TargetProcess tile in hello Access Panel, you should get automatically signed-on tooyour TargetProcess application.</span></span> <span data-ttu-id="61dd4-235">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61dd4-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61dd4-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="61dd4-236">Additional resources</span></span>

* [<span data-ttu-id="61dd4-237">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61dd4-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="61dd4-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61dd4-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

