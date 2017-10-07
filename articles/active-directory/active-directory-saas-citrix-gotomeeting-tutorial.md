---
title: 'Samouczek: Integracji Azure Active Directory z Citrix GoToMeeting | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="c0ce9-103">Samouczek: Integracji Azure Active Directory z Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="c0ce9-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="c0ce9-104">Z tego samouczka, dowiesz się, jak toointegrate Citrix GoToMeeting w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0ce9-104">In this tutorial, you learn how toointegrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0ce9-105">Integracja z usługą Azure AD Citrix GoToMeeting zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c0ce9-105">Integrating Citrix GoToMeeting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c0ce9-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="c0ce9-106">You can control in Azure AD who has access tooCitrix GoToMeeting</span></span>
- <span data-ttu-id="c0ce9-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCitrix GoToMeeting (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0ce9-107">You can enable your users tooautomatically get signed-on tooCitrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0ce9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c0ce9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c0ce9-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0ce9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0ce9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c0ce9-110">Prerequisites</span></span>

<span data-ttu-id="c0ce9-111">tooconfigure integracji usługi Azure AD z Citrix GoToMeeting, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c0ce9-111">tooconfigure Azure AD integration with Citrix GoToMeeting, you need hello following items:</span></span>

- <span data-ttu-id="c0ce9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0ce9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0ce9-113">Citrix GoToMeeting jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c0ce9-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0ce9-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0ce9-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c0ce9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0ce9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0ce9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0ce9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0ce9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c0ce9-118">Scenario description</span></span>
<span data-ttu-id="c0ce9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0ce9-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c0ce9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0ce9-121">Dodawanie Citrix GoToMeeting z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c0ce9-121">Adding Citrix GoToMeeting from hello gallery</span></span>
2. <span data-ttu-id="c0ce9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c0ce9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a><span data-ttu-id="c0ce9-123">Dodawanie Citrix GoToMeeting z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c0ce9-123">Adding Citrix GoToMeeting from hello gallery</span></span>
<span data-ttu-id="c0ce9-124">tooconfigure hello integracji Citrix GoToMeeting do usługi Azure AD, należy tooadd Citrix GoToMeeting z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-124">tooconfigure hello integration of Citrix GoToMeeting into Azure AD, you need tooadd Citrix GoToMeeting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c0ce9-125">**tooadd Citrix GoToMeeting z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c0ce9-125">**tooadd Citrix GoToMeeting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0ce9-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c0ce9-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c0ce9-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c0ce9-131">Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c0ce9-133">W polu wyszukiwania hello wpisz **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-133">In hello search box, type **Citrix GoToMeeting**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="c0ce9-135">W panelu wyników hello zaznacz **Citrix GoToMeeting**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-135">In hello results panel, select **Citrix GoToMeeting**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0ce9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c0ce9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0ce9-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Citrix GoToMeeting oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="c0ce9-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c0ce9-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Citrix GoToMeeting jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix GoToMeeting is tooa user in Azure AD.</span></span> <span data-ttu-id="c0ce9-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Citrix GoToMeeting musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-140">In other words, a link relationship between an Azure AD user and hello related user in Citrix GoToMeeting needs toobe established.</span></span>

<span data-ttu-id="c0ce9-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="c0ce9-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Citrix GoToMeeting, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c0ce9-142">tooconfigure and test Azure AD single sign-on with Citrix GoToMeeting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c0ce9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c0ce9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0ce9-145">**[Tworzenie użytkownika testowego Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**  -toohave odpowiednikiem Simona Britta w Citrix GoToMeeting, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - toohave a counterpart of Britta Simon in Citrix GoToMeeting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0ce9-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0ce9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0ce9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c0ce9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0ce9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="c0ce9-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Citrix GoToMeeting, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c0ce9-150">**tooconfigure Azure AD single sign-on with Citrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0ce9-151">W portalu Azure na powitania hello **Citrix GoToMeeting** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-151">In hello Azure portal, on hello **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c0ce9-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="c0ce9-155">Na powitania **Citrix GoToMeeting domeny i adres URL** sekcji tooperform nie potrzeba żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-155">On hello **Citrix GoToMeeting Domain and URLs** section, no need tooperform any steps.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="c0ce9-157">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-157">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="c0ce9-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-159">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="c0ce9-161">W sekcji konfiguracji SAML GoToMeeting Citrix hello kliknij polecenie skonfigurować SAML GoToMeeting Citrix tooopen Konfigurowanie logowania jednokrotnego okna.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-161">On hello Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="c0ce9-162">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c0ce9-162">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

6. <span data-ttu-id="c0ce9-163">W oknie innej przeglądarki, zaloguj się za tooyour [Center organizacji Citrix](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="c0ce9-163">In a different browser window, log in tooyour [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="c0ce9-164">Kliknij przycisk hello **dostawcy tożsamości** karcie, a następnie wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c0ce9-164">Click hello **Identity Provider** tab, and then perform hello following steps:</span></span>  
   
    <span data-ttu-id="c0ce9-165">![Instalator SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Instalatora SAML")</span><span class="sxs-lookup"><span data-stu-id="c0ce9-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="c0ce9-166">a.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-166">a.</span></span> <span data-ttu-id="c0ce9-167">Wybierz **ręczne**</span><span class="sxs-lookup"><span data-stu-id="c0ce9-167">Select **Manual**</span></span>

    <span data-ttu-id="c0ce9-168">b.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-168">b.</span></span> <span data-ttu-id="c0ce9-169">W portalu Azure na powitania hello **skonfigurować logowanie jednokrotne w Citrix GoToMeeting** strony okna dialogowego, hello kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej go do hello **strony logowania Adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-169">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="c0ce9-170">c.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-170">c.</span></span> <span data-ttu-id="c0ce9-171">W portalu Azure na powitania hello **skonfigurować logowanie jednokrotne w Citrix GoToMeeting** strony okna dialogowego, hello kopiowania **Sign-Out URL** wartość, a następnie wklej go do hello **adres URL wylogowania strony**pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-171">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **Sign-Out URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="c0ce9-172">d.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-172">d.</span></span> <span data-ttu-id="c0ce9-173">W portalu Azure na powitania hello **skonfigurować logowanie jednokrotne w Citrix GoToMeeting** strony okna dialogowego, hello kopiowania **identyfikator jednostki SAML** wartość, a następnie wklej go do hello **identyfikator jednostki dostawcy tożsamości**  pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-173">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Entity ID** value, and then paste it into hello **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="c0ce9-174">e.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-174">e.</span></span> <span data-ttu-id="c0ce9-175">tooupload pobranego certyfikatu, kliknij przycisk **Przekaż certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-175">tooupload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="c0ce9-176">f.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-176">f.</span></span> <span data-ttu-id="c0ce9-177">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c0ce9-178">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="c0ce9-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c0ce9-179">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c0ce9-180">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0ce9-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0ce9-181">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0ce9-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0ce9-182">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c0ce9-184">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c0ce9-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0ce9-185">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-185">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0ce9-187">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-187">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0ce9-189">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-189">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0ce9-191">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c0ce9-191">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0ce9-193">a.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-193">a.</span></span> <span data-ttu-id="c0ce9-194">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0ce9-195">b.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-195">b.</span></span> <span data-ttu-id="c0ce9-196">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0ce9-197">c.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-197">c.</span></span> <span data-ttu-id="c0ce9-198">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c0ce9-199">d.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-199">d.</span></span> <span data-ttu-id="c0ce9-200">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="c0ce9-201">Tworzenie użytkownika testowego Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="c0ce9-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="c0ce9-202">W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="c0ce9-203">Citrix GoToMeeting obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="c0ce9-204">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-204">There is no action item for you in this section.</span></span> <span data-ttu-id="c0ce9-205">Jeśli użytkownik nie istnieje w Citrix GoToMeeting, nowy jest tworzony podczas próby tooaccess Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt tooaccess Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="c0ce9-206">Jeśli potrzebujesz toocreate użytkownik ręcznie, skontaktuj się z [Citrix GoToMeeting zespołem pomocy technicznej](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="c0ce9-206">If you need toocreate a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c0ce9-207">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0ce9-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c0ce9-208">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix GoToMeeting.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c0ce9-210">**tooassign tooCitrix Simona Britta GoToMeeting, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c0ce9-210">**tooassign Britta Simon tooCitrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0ce9-211">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c0ce9-213">Z listy aplikacji hello wybierz **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-213">In hello applications list, select **Citrix GoToMeeting**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="c0ce9-215">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c0ce9-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-217">Click **Add** button.</span></span> <span data-ttu-id="c0ce9-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c0ce9-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c0ce9-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0ce9-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0ce9-223">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c0ce9-223">Testing single sign-on</span></span>

<span data-ttu-id="c0ce9-224">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c0ce9-225">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c0ce9-225">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="c0ce9-226">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c0ce9-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0ce9-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c0ce9-227">Additional resources</span></span>

* [<span data-ttu-id="c0ce9-228">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0ce9-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0ce9-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0ce9-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c0ce9-230">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="c0ce9-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

