---
title: 'Samouczek: Integracji Azure Active Directory z Sugar CRM | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="56b53-103">Samouczek: Integracji Azure Active Directory z Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="56b53-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="56b53-104">Z tego samouczka, dowiesz się, jak toointegrate CRM Sugar w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56b53-104">In this tutorial, you learn how toointegrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56b53-105">Integracja z usługą Azure AD Sugar CRM zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="56b53-105">Integrating Sugar CRM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="56b53-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSugar CRM</span><span class="sxs-lookup"><span data-stu-id="56b53-106">You can control in Azure AD who has access tooSugar CRM</span></span>
- <span data-ttu-id="56b53-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSugar CRM (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="56b53-107">You can enable your users tooautomatically get signed-on tooSugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56b53-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="56b53-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="56b53-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56b53-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56b53-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="56b53-110">Prerequisites</span></span>

<span data-ttu-id="56b53-111">tooconfigure integracji usługi Azure AD z Sugar CRM należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="56b53-111">tooconfigure Azure AD integration with Sugar CRM, you need hello following items:</span></span>

- <span data-ttu-id="56b53-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="56b53-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56b53-113">Sugar CRM logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="56b53-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56b53-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="56b53-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56b53-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="56b53-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56b53-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="56b53-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56b53-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56b53-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56b53-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="56b53-118">Scenario description</span></span>
<span data-ttu-id="56b53-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="56b53-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56b53-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="56b53-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56b53-121">Dodawanie Sugar CRM z galerii hello</span><span class="sxs-lookup"><span data-stu-id="56b53-121">Adding Sugar CRM from hello gallery</span></span>
2. <span data-ttu-id="56b53-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="56b53-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-hello-gallery"></a><span data-ttu-id="56b53-123">Dodawanie Sugar CRM z galerii hello</span><span class="sxs-lookup"><span data-stu-id="56b53-123">Adding Sugar CRM from hello gallery</span></span>
<span data-ttu-id="56b53-124">tooconfigure hello integracji Sugar CRM do usługi Azure AD, należy tooadd Sugar CRM z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="56b53-124">tooconfigure hello integration of Sugar CRM into Azure AD, you need tooadd Sugar CRM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="56b53-125">**tooadd CRM Sugar z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="56b53-125">**tooadd Sugar CRM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="56b53-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="56b53-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="56b53-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="56b53-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="56b53-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="56b53-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="56b53-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="56b53-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="56b53-133">W polu wyszukiwania hello wpisz **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="56b53-133">In hello search box, type **Sugar CRM**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="56b53-135">W panelu wyników hello, wybierz **Sugar CRM**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56b53-135">In hello results panel, select **Sugar CRM**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56b53-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="56b53-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56b53-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z CRM Sugar w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="56b53-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56b53-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Sugar CRM jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56b53-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sugar CRM is tooa user in Azure AD.</span></span> <span data-ttu-id="56b53-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Sugar CRM musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="56b53-140">In other words, a link relationship between an Azure AD user and hello related user in Sugar CRM needs toobe established.</span></span>

<span data-ttu-id="56b53-141">W Sugar CRM, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="56b53-141">In Sugar CRM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="56b53-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Sugar CRM, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="56b53-142">tooconfigure and test Azure AD single sign-on with Sugar CRM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="56b53-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="56b53-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="56b53-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="56b53-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56b53-145">**[Tworzenie użytkownika testowego Sugar CRM](#creating-a-sugar-crm-test-user)**  -toohave odpowiednikiem Simona Britta w aplikacji CRM Sugar toohello połączonej usługi Azure AD reprezentacja użytkownika.</span><span class="sxs-lookup"><span data-stu-id="56b53-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - toohave a counterpart of Britta Simon in Sugar CRM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="56b53-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="56b53-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56b53-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="56b53-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56b53-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="56b53-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="56b53-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="56b53-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="56b53-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Sugar CRM wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="56b53-150">**tooconfigure Azure AD single sign-on with Sugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="56b53-151">W portalu Azure na powitania hello **Sugar CRM** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="56b53-151">In hello Azure portal, on hello **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="56b53-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="56b53-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="56b53-155">Na powitania **Sugar CRM domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="56b53-155">On hello **Sugar CRM Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="56b53-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="56b53-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="56b53-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="56b53-158">hello value is not real.</span></span> <span data-ttu-id="56b53-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="56b53-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="56b53-160">Skontaktuj się z [zespołem pomocy technicznej klienta CRM Sugar](https://support.sugarcrm.com/) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="56b53-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="56b53-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="56b53-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="56b53-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="56b53-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="56b53-165">Na powitania **konfiguracji CRM Sugar** kliknij **skonfigurować CRM Sugar** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="56b53-165">On hello **Sugar CRM Configuration** section, click **Configure Sugar CRM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="56b53-166">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="56b53-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="56b53-168">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Sugar CRM tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="56b53-168">In a different web browser window, log in tooyour Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="56b53-169">Przejdź za**Admin**.</span><span class="sxs-lookup"><span data-stu-id="56b53-169">Go too**Admin**.</span></span>
   
    <span data-ttu-id="56b53-170">![Administrator](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="56b53-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="56b53-171">W hello **administracji** kliknij **zarządzania hasłami**.</span><span class="sxs-lookup"><span data-stu-id="56b53-171">In hello **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="56b53-172">![Administracja](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="56b53-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="56b53-173">Wybierz **włączyć uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="56b53-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="56b53-174">![Administracja](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="56b53-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="56b53-175">W hello **uwierzytelnianie SAML** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="56b53-175">In hello **SAML Authentication** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="56b53-176">![Uwierzytelnianie SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="56b53-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="56b53-177">a.</span><span class="sxs-lookup"><span data-stu-id="56b53-177">a.</span></span> <span data-ttu-id="56b53-178">W hello **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="56b53-178">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="56b53-179">b.</span><span class="sxs-lookup"><span data-stu-id="56b53-179">b.</span></span> <span data-ttu-id="56b53-180">W hello **SLO URL** pole tekstowe, Wklej hello wartość **Sign-Out adres URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="56b53-180">In hello **SLO URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="56b53-181">c.</span><span class="sxs-lookup"><span data-stu-id="56b53-181">c.</span></span> <span data-ttu-id="56b53-182">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej hello cały certyfikat do **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="56b53-182">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="56b53-183">d.</span><span class="sxs-lookup"><span data-stu-id="56b53-183">d.</span></span> <span data-ttu-id="56b53-184">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="56b53-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="56b53-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="56b53-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="56b53-186">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="56b53-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="56b53-187">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56b53-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56b53-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="56b53-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="56b53-189">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="56b53-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="56b53-191">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="56b53-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="56b53-192">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="56b53-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56b53-194">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="56b53-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56b53-196">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="56b53-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56b53-198">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="56b53-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56b53-200">a.</span><span class="sxs-lookup"><span data-stu-id="56b53-200">a.</span></span> <span data-ttu-id="56b53-201">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56b53-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56b53-202">b.</span><span class="sxs-lookup"><span data-stu-id="56b53-202">b.</span></span> <span data-ttu-id="56b53-203">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56b53-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56b53-204">c.</span><span class="sxs-lookup"><span data-stu-id="56b53-204">c.</span></span> <span data-ttu-id="56b53-205">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="56b53-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="56b53-206">d.</span><span class="sxs-lookup"><span data-stu-id="56b53-206">d.</span></span> <span data-ttu-id="56b53-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="56b53-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="56b53-208">Tworzenie użytkownika testowego Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="56b53-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="56b53-209">Użytkownicy usługi Azure AD toolog kolejności tooenable w tooSugar CRM muszą być elastycznie tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="56b53-209">In order tooenable Azure AD users toolog in tooSugar CRM, they must be provisioned tooSugar CRM.</span></span>

<span data-ttu-id="56b53-210">W przypadku hello Sugar CRM Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="56b53-210">In hello case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="56b53-211">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="56b53-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="56b53-212">Zaloguj się za tooyour **Sugar CRM** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="56b53-212">Log in tooyour **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="56b53-213">Przejdź za**Admin**.</span><span class="sxs-lookup"><span data-stu-id="56b53-213">Go too**Admin**.</span></span>
   
    <span data-ttu-id="56b53-214">![Administrator](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="56b53-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="56b53-215">W hello **administracji** kliknij **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="56b53-215">In hello **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="56b53-216">![Administracja](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="56b53-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="56b53-217">Przejdź za**użytkowników \> Tworzenie nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="56b53-217">Go too**Users \> Create New User**.</span></span>
   
    <span data-ttu-id="56b53-218">![Utwórz nowego użytkownika](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Utwórz nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="56b53-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="56b53-219">Na powitania **profilu użytkownika** karcie, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="56b53-219">On hello **User Profile** tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="56b53-220">![Nowy użytkownik](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="56b53-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="56b53-221">a.</span><span class="sxs-lookup"><span data-stu-id="56b53-221">a.</span></span> <span data-ttu-id="56b53-222">Typ hello **nazwy użytkownika**, **nazwisko**, i **adres e-mail** z prawidłowym użytkownikiem usługi Azure Active Directory do hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="56b53-222">Type hello **user name**, **last name**, and **email address** of a valid Azure Active Directory user into hello related textboxes.</span></span>
  
6. <span data-ttu-id="56b53-223">Jako **stan**, wybierz pozycję **Active**.</span><span class="sxs-lookup"><span data-stu-id="56b53-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="56b53-224">Na karcie hasło hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="56b53-224">On hello Password tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="56b53-225">![Nowy użytkownik](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="56b53-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="56b53-226">a.</span><span class="sxs-lookup"><span data-stu-id="56b53-226">a.</span></span> <span data-ttu-id="56b53-227">Wpisz hasło hello na powitania związanych z pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="56b53-227">Type hello password into hello related textbox.</span></span>

    <span data-ttu-id="56b53-228">b.</span><span class="sxs-lookup"><span data-stu-id="56b53-228">b.</span></span> <span data-ttu-id="56b53-229">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="56b53-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="56b53-230">Możesz użyć innych Sugar CRM użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Sugar CRM kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="56b53-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="56b53-231">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="56b53-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="56b53-232">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="56b53-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSugar CRM.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="56b53-234">**tooassign tooSugar Simona Britta CRM, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="56b53-234">**tooassign Britta Simon tooSugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="56b53-235">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="56b53-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="56b53-237">Z listy aplikacji hello wybierz **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="56b53-237">In hello applications list, select **Sugar CRM**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="56b53-239">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="56b53-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="56b53-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="56b53-241">Click **Add** button.</span></span> <span data-ttu-id="56b53-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="56b53-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="56b53-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="56b53-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="56b53-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="56b53-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56b53-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="56b53-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="56b53-247">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="56b53-247">Testing single sign-on</span></span>

<span data-ttu-id="56b53-248">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="56b53-248">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="56b53-249">Po kliknięciu kafelka Sugar CRM hello w hello Panel dostępu, należy pobrać aplikacji Sugar CRM tooyour zalogowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="56b53-249">When you click hello Sugar CRM tile in hello Access Panel, you should get automatically signed-on tooyour Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56b53-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="56b53-250">Additional resources</span></span>

* [<span data-ttu-id="56b53-251">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56b53-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56b53-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56b53-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

