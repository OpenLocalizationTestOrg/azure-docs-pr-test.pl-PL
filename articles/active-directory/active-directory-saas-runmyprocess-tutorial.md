---
title: 'Samouczek: Integracji Azure Active Directory z RunMyProcess | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i RunMyProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="63a0e-103">Samouczek: Integracji Azure Active Directory z RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="63a0e-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="63a0e-104">Z tego samouczka, dowiesz się, jak toointegrate RunMyProcess w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63a0e-104">In this tutorial, you learn how toointegrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63a0e-105">Integracja z usługą Azure AD RunMyProcess zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="63a0e-105">Integrating RunMyProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="63a0e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooRunMyProcess</span><span class="sxs-lookup"><span data-stu-id="63a0e-106">You can control in Azure AD who has access tooRunMyProcess</span></span>
- <span data-ttu-id="63a0e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRunMyProcess (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="63a0e-107">You can enable your users tooautomatically get signed-on tooRunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="63a0e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="63a0e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="63a0e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63a0e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63a0e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="63a0e-110">Prerequisites</span></span>

<span data-ttu-id="63a0e-111">tooconfigure integracji z usługą Azure AD z RunMyProcess należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="63a0e-111">tooconfigure Azure AD integration with RunMyProcess, you need hello following items:</span></span>

- <span data-ttu-id="63a0e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="63a0e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63a0e-113">RunMyProcess logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="63a0e-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63a0e-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="63a0e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63a0e-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="63a0e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63a0e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="63a0e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63a0e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj:[oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63a0e-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63a0e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="63a0e-118">Scenario description</span></span>
<span data-ttu-id="63a0e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="63a0e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63a0e-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="63a0e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63a0e-121">Dodawanie RunMyProcess z galerii hello</span><span class="sxs-lookup"><span data-stu-id="63a0e-121">Adding RunMyProcess from hello gallery</span></span>
2. <span data-ttu-id="63a0e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="63a0e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-hello-gallery"></a><span data-ttu-id="63a0e-123">Dodawanie RunMyProcess z galerii hello</span><span class="sxs-lookup"><span data-stu-id="63a0e-123">Adding RunMyProcess from hello gallery</span></span>
<span data-ttu-id="63a0e-124">tooconfigure hello integracji RunMyProcess do usługi Azure AD, należy tooadd RunMyProcess z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="63a0e-124">tooconfigure hello integration of RunMyProcess into Azure AD, you need tooadd RunMyProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="63a0e-125">**tooadd RunMyProcess z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="63a0e-125">**tooadd RunMyProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="63a0e-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="63a0e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="63a0e-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="63a0e-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="63a0e-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="63a0e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="63a0e-133">W polu wyszukiwania hello wpisz **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-133">In hello search box, type **RunMyProcess**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="63a0e-135">W panelu wyników hello zaznacz **RunMyProcess**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="63a0e-135">In hello results panel, select **RunMyProcess**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63a0e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="63a0e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="63a0e-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z RunMyProcess w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="63a0e-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63a0e-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w RunMyProcess jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63a0e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RunMyProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="63a0e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w RunMyProcess musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="63a0e-140">In other words, a link relationship between an Azure AD user and hello related user in RunMyProcess needs toobe established.</span></span>

<span data-ttu-id="63a0e-141">W RunMyProcess, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="63a0e-141">In RunMyProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="63a0e-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z RunMyProcess, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="63a0e-142">tooconfigure and test Azure AD single sign-on with RunMyProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="63a0e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="63a0e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="63a0e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="63a0e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63a0e-145">**[Tworzenie użytkownika testowego RunMyProcess](#creating-a-runmyprocess-test-user)**  -toohave odpowiednikiem Simona Britta w RunMyProcess, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63a0e-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - toohave a counterpart of Britta Simon in RunMyProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="63a0e-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="63a0e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63a0e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="63a0e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63a0e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="63a0e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="63a0e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="63a0e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="63a0e-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z RunMyProcess, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="63a0e-150">**tooconfigure Azure AD single sign-on with RunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="63a0e-151">W portalu Azure na powitania hello **RunMyProcess** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-151">In hello Azure portal, on hello **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="63a0e-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="63a0e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="63a0e-155">Na powitania **RunMyProcess domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="63a0e-155">On hello **RunMyProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="63a0e-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="63a0e-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="63a0e-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="63a0e-158">hello value is not real.</span></span> <span data-ttu-id="63a0e-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="63a0e-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="63a0e-160">Skontaktuj się z [zespołem pomocy technicznej klienta RunMyProcess](mailto:support@runmyprocess.com) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="63a0e-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) tooget hello value.</span></span> 

4. <span data-ttu-id="63a0e-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="63a0e-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="63a0e-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="63a0e-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="63a0e-165">Na powitania **konfiguracji RunMyProcess** kliknij **skonfigurować RunMyProcess** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="63a0e-165">On hello **RunMyProcess Configuration** section, click **Configure RunMyProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="63a0e-166">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="63a0e-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="63a0e-168">W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour RunMyProcess dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="63a0e-168">In a different web browser window, sign-on tooyour RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="63a0e-169">W lewym panelu nawigacyjnym kliknij **konta** i wybierz **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="63a0e-171">Przejdź za**metodę uwierzytelniania** sekcji i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="63a0e-171">Go too**Authentication method** section and perform below steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="63a0e-173">a.</span><span class="sxs-lookup"><span data-stu-id="63a0e-173">a.</span></span> <span data-ttu-id="63a0e-174">Jako **metody**, wybierz pozycję **rejestracji Jednokrotnej z Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="63a0e-175">b.</span><span class="sxs-lookup"><span data-stu-id="63a0e-175">b.</span></span> <span data-ttu-id="63a0e-176">W hello **przekierowania logowania jednokrotnego** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="63a0e-176">In hello **SSO redirect** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="63a0e-177">c.</span><span class="sxs-lookup"><span data-stu-id="63a0e-177">c.</span></span> <span data-ttu-id="63a0e-178">W hello **przekierowania wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="63a0e-178">In hello **Logout redirect** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="63a0e-179">d.</span><span class="sxs-lookup"><span data-stu-id="63a0e-179">d.</span></span> <span data-ttu-id="63a0e-180">W hello **Format identyfikatora nazwy** pole tekstowe, wartość hello typu **Format identyfikatora nazwy** jako **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-180">In hello **Name Id Format** textbox, type hello value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="63a0e-181">e.</span><span class="sxs-lookup"><span data-stu-id="63a0e-181">e.</span></span> <span data-ttu-id="63a0e-182">Kopiowanie zawartości hello hello pliku pobranego certyfikatu, a następnie wklej go do hello **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="63a0e-182">Copy hello content of hello downloaded certificate file and then paste it into hello **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="63a0e-183">f.</span><span class="sxs-lookup"><span data-stu-id="63a0e-183">f.</span></span> <span data-ttu-id="63a0e-184">Kliknij przycisk **zapisać** ikony.</span><span class="sxs-lookup"><span data-stu-id="63a0e-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="63a0e-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="63a0e-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="63a0e-186">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="63a0e-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="63a0e-187">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63a0e-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63a0e-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="63a0e-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="63a0e-189">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="63a0e-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="63a0e-191">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="63a0e-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="63a0e-192">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="63a0e-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="63a0e-194">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="63a0e-196">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="63a0e-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="63a0e-198">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="63a0e-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="63a0e-200">a.</span><span class="sxs-lookup"><span data-stu-id="63a0e-200">a.</span></span> <span data-ttu-id="63a0e-201">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63a0e-202">b.</span><span class="sxs-lookup"><span data-stu-id="63a0e-202">b.</span></span> <span data-ttu-id="63a0e-203">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="63a0e-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="63a0e-204">c.</span><span class="sxs-lookup"><span data-stu-id="63a0e-204">c.</span></span> <span data-ttu-id="63a0e-205">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="63a0e-206">d.</span><span class="sxs-lookup"><span data-stu-id="63a0e-206">d.</span></span> <span data-ttu-id="63a0e-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="63a0e-208">Tworzenie użytkownika testowego RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="63a0e-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="63a0e-209">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooRunMyProcess muszą mieć przydzielone do RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="63a0e-209">In order tooenable Azure AD users toolog in tooRunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="63a0e-210">W przypadku hello RunMyProcess Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="63a0e-210">In hello case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="63a0e-211">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="63a0e-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="63a0e-212">Zaloguj się za tooyour RunMyProcess witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="63a0e-212">Log in tooyour RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="63a0e-213">Kliknij przycisk **konta** i wybierz **użytkowników** w panelu nawigacyjnym po lewej stronie, następnie kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="63a0e-214">![Nowy użytkownik](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="63a0e-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="63a0e-215">W hello **ustawienia użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="63a0e-215">In hello **User Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="63a0e-216">![Profil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "profilu")</span><span class="sxs-lookup"><span data-stu-id="63a0e-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="63a0e-217">a.</span><span class="sxs-lookup"><span data-stu-id="63a0e-217">a.</span></span> <span data-ttu-id="63a0e-218">Hello typu **nazwa** i **E-mail** prawidłowy Azure konta AD mają tooprovision w hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="63a0e-218">Type hello **Name** and **E-mail** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="63a0e-219">b.</span><span class="sxs-lookup"><span data-stu-id="63a0e-219">b.</span></span> <span data-ttu-id="63a0e-220">Wybierz **IDE języka**, **języka**, i **profilu**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="63a0e-221">c.</span><span class="sxs-lookup"><span data-stu-id="63a0e-221">c.</span></span> <span data-ttu-id="63a0e-222">Wybierz **wysyłania toome e-mail tworzenia konta**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-222">Select **Send account creation e-mail toome**.</span></span> 

    <span data-ttu-id="63a0e-223">d.</span><span class="sxs-lookup"><span data-stu-id="63a0e-223">d.</span></span> <span data-ttu-id="63a0e-224">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="63a0e-225">Możesz użyć innych RunMyProcess użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision RunMyProcess usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="63a0e-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess tooprovision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="63a0e-226">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="63a0e-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="63a0e-227">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="63a0e-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRunMyProcess.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="63a0e-229">**tooassign tooRunMyProcess Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="63a0e-229">**tooassign Britta Simon tooRunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="63a0e-230">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="63a0e-232">Z listy aplikacji hello wybierz **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-232">In hello applications list, select **RunMyProcess**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="63a0e-234">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="63a0e-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="63a0e-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="63a0e-236">Click **Add** button.</span></span> <span data-ttu-id="63a0e-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="63a0e-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="63a0e-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="63a0e-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="63a0e-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="63a0e-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63a0e-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="63a0e-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="63a0e-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="63a0e-242">Testing single sign-on</span></span>

<span data-ttu-id="63a0e-243">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="63a0e-243">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="63a0e-244">Po kliknięciu powitalne RunMyProcess kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour RunMyProcess aplikacji.</span><span class="sxs-lookup"><span data-stu-id="63a0e-244">When you click hello RunMyProcess tile in hello Access Panel, you should get automatically signed-on tooyour RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="63a0e-245">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="63a0e-245">Additional resources</span></span>

* [<span data-ttu-id="63a0e-246">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63a0e-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63a0e-247">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63a0e-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

