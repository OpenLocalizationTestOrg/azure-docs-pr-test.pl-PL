---
title: 'Samouczek: Integracji Azure Active Directory z Jive | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: f22bf78a55e8a4a9ea2f0020ef2f535be88b6302
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="e6a68-103">Samouczek: Integracji Azure Active Directory z Jive</span><span class="sxs-lookup"><span data-stu-id="e6a68-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="e6a68-104">Z tego samouczka, dowiesz się, jak toointegrate Jive z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e6a68-104">In this tutorial, you learn how toointegrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e6a68-105">Integracja z usługą Azure AD Jive zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e6a68-105">Integrating Jive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e6a68-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooJive</span><span class="sxs-lookup"><span data-stu-id="e6a68-106">You can control in Azure AD who has access tooJive</span></span>
- <span data-ttu-id="e6a68-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooJive (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6a68-107">You can enable your users tooautomatically get signed-on tooJive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e6a68-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e6a68-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e6a68-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e6a68-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6a68-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e6a68-110">Prerequisites</span></span>

<span data-ttu-id="e6a68-111">tooconfigure integracji z usługą Azure AD z Jive należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e6a68-111">tooconfigure Azure AD integration with Jive, you need hello following items:</span></span>

- <span data-ttu-id="e6a68-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6a68-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e6a68-113">Jive jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e6a68-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e6a68-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e6a68-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e6a68-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e6a68-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e6a68-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e6a68-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e6a68-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e6a68-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e6a68-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e6a68-118">Scenario description</span></span>
<span data-ttu-id="e6a68-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e6a68-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e6a68-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e6a68-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e6a68-121">Dodawanie Jive z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e6a68-121">Adding Jive from hello gallery</span></span>
2. <span data-ttu-id="e6a68-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e6a68-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-hello-gallery"></a><span data-ttu-id="e6a68-123">Dodawanie Jive z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e6a68-123">Adding Jive from hello gallery</span></span>
<span data-ttu-id="e6a68-124">integracji hello tooconfigure Jive do usługi Azure AD, należy tooadd Jive z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e6a68-124">tooconfigure hello integration of Jive into Azure AD, you need tooadd Jive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e6a68-125">**tooadd Jive z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e6a68-125">**tooadd Jive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e6a68-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e6a68-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e6a68-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e6a68-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e6a68-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e6a68-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e6a68-133">W polu wyszukiwania hello wpisz **Jive**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-133">In hello search box, type **Jive**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="e6a68-135">W panelu wyników hello zaznacz **Jive**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e6a68-135">In hello results panel, select **Jive**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e6a68-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e6a68-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e6a68-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jive na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e6a68-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e6a68-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Jive jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6a68-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jive is tooa user in Azure AD.</span></span> <span data-ttu-id="e6a68-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Jive musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e6a68-140">In other words, a link relationship between an Azure AD user and hello related user in Jive needs toobe established.</span></span>

<span data-ttu-id="e6a68-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Jive.</span><span class="sxs-lookup"><span data-stu-id="e6a68-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Jive.</span></span>

<span data-ttu-id="e6a68-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Jive, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e6a68-142">tooconfigure and test Azure AD single sign-on with Jive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e6a68-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e6a68-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e6a68-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e6a68-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e6a68-145">**[Tworzenie użytkownika testowego Jive](#creating-a-jive-test-user)**  -toohave odpowiednikiem Simona Britta w Jive, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e6a68-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - toohave a counterpart of Britta Simon in Jive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e6a68-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e6a68-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e6a68-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e6a68-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e6a68-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e6a68-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e6a68-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Jive.</span><span class="sxs-lookup"><span data-stu-id="e6a68-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="e6a68-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Jive, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e6a68-150">**tooconfigure Azure AD single sign-on with Jive, perform hello following steps:**</span></span>

1. <span data-ttu-id="e6a68-151">W portalu Azure na powitania hello **Jive** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-151">In hello Azure portal, on hello **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e6a68-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e6a68-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="e6a68-155">Na powitania **Jive domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e6a68-155">On hello **Jive Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="e6a68-157">a.</span><span class="sxs-lookup"><span data-stu-id="e6a68-157">a.</span></span> <span data-ttu-id="e6a68-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="e6a68-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="e6a68-159">b.</span><span class="sxs-lookup"><span data-stu-id="e6a68-159">b.</span></span> <span data-ttu-id="e6a68-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="e6a68-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e6a68-161">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e6a68-161">These values are not hello real.</span></span> <span data-ttu-id="e6a68-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="e6a68-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="e6a68-163">Skontaktuj się z [zespołem pomocy technicznej klienta Jive](https://www.jivesoftware.com/services-support/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e6a68-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="e6a68-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e6a68-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="e6a68-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e6a68-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e6a68-168">tooconfigure rejestracji jednokrotnej w **Jive** tooyour obok siebie, logowania jednokrotnego Jive dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="e6a68-168">tooconfigure single sign-on on **Jive** side, sign-on tooyour Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="e6a68-169">W menu hello na górze hello, kliknij przycisk "**Saml**."</span><span class="sxs-lookup"><span data-stu-id="e6a68-169">In hello menu on hello top, Click "**Saml**."</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="e6a68-171">a.</span><span class="sxs-lookup"><span data-stu-id="e6a68-171">a.</span></span> <span data-ttu-id="e6a68-172">Wybierz **włączone** w obszarze hello **ogólne** kartę.</span><span class="sxs-lookup"><span data-stu-id="e6a68-172">Select **Enabled** under hello **General** tab.</span></span>   
    <span data-ttu-id="e6a68-173">b.</span><span class="sxs-lookup"><span data-stu-id="e6a68-173">b.</span></span> <span data-ttu-id="e6a68-174">Kliknij przycisk hello "**Zapisz wszystkie ustawienia saml**" przycisku.</span><span class="sxs-lookup"><span data-stu-id="e6a68-174">Click hello "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="e6a68-175">Przejdź toohello "**metadanych Idp**" kartę.</span><span class="sxs-lookup"><span data-stu-id="e6a68-175">Navigate toohello "**Idp Metadata**" tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="e6a68-177">a.</span><span class="sxs-lookup"><span data-stu-id="e6a68-177">a.</span></span> <span data-ttu-id="e6a68-178">Kopiowanie zawartości hello pliku XML metadanych hello pobrane, a następnie wklej go do hello **metadanych dostawcy tożsamości (IDP)** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="e6a68-178">Copy hello content of hello downloaded metadata XML file, and then paste it into hello **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="e6a68-179">b.</span><span class="sxs-lookup"><span data-stu-id="e6a68-179">b.</span></span> <span data-ttu-id="e6a68-180">Kliknij przycisk hello "**Zapisz wszystkie ustawienia saml**" przycisku.</span><span class="sxs-lookup"><span data-stu-id="e6a68-180">Click hello "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="e6a68-181">Przejdź toohello "**mapowanie atrybutu użytkownika**" kartę.</span><span class="sxs-lookup"><span data-stu-id="e6a68-181">Go toohello "**User Attribute Mapping**" tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="e6a68-183">a.</span><span class="sxs-lookup"><span data-stu-id="e6a68-183">a.</span></span> <span data-ttu-id="e6a68-184">W hello **E-mail** pole tekstowe, kopiowania i wklejania hello nazwę **poczty** wartość.</span><span class="sxs-lookup"><span data-stu-id="e6a68-184">In hello **Email** textbox, copy and paste hello attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="e6a68-185">b.</span><span class="sxs-lookup"><span data-stu-id="e6a68-185">b.</span></span> <span data-ttu-id="e6a68-186">W hello **imię** pole tekstowe, kopiowania i wklejania hello nazwę **givenname** wartości.</span><span class="sxs-lookup"><span data-stu-id="e6a68-186">In hello **First Name** textbox, copy and paste hello attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="e6a68-187">c.</span><span class="sxs-lookup"><span data-stu-id="e6a68-187">c.</span></span> <span data-ttu-id="e6a68-188">W hello **nazwisko** pole tekstowe, kopiowania i wklejania hello nazwę **nazwisko** wartość.</span><span class="sxs-lookup"><span data-stu-id="e6a68-188">In hello **Last Name** textbox, copy and paste hello attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="e6a68-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e6a68-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e6a68-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e6a68-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e6a68-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e6a68-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e6a68-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6a68-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e6a68-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e6a68-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e6a68-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e6a68-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e6a68-196">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e6a68-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e6a68-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e6a68-200">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e6a68-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e6a68-202">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e6a68-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e6a68-204">a.</span><span class="sxs-lookup"><span data-stu-id="e6a68-204">a.</span></span> <span data-ttu-id="e6a68-205">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e6a68-206">b.</span><span class="sxs-lookup"><span data-stu-id="e6a68-206">b.</span></span> <span data-ttu-id="e6a68-207">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e6a68-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e6a68-208">c.</span><span class="sxs-lookup"><span data-stu-id="e6a68-208">c.</span></span> <span data-ttu-id="e6a68-209">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e6a68-210">d.</span><span class="sxs-lookup"><span data-stu-id="e6a68-210">d.</span></span> <span data-ttu-id="e6a68-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="e6a68-212">Tworzenie użytkownika testowego Jive</span><span class="sxs-lookup"><span data-stu-id="e6a68-212">Creating a Jive test user</span></span>

<span data-ttu-id="e6a68-213">Praca z [zespołem pomocy technicznej klienta Jive](https://www.jivesoftware.com/services-support/) tooadd hello użytkowników hello Jive platformy.</span><span class="sxs-lookup"><span data-stu-id="e6a68-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) tooadd hello users in hello Jive platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e6a68-214">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6a68-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e6a68-215">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooJive.</span><span class="sxs-lookup"><span data-stu-id="e6a68-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJive.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e6a68-217">**tooassign tooJive Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e6a68-217">**tooassign Britta Simon tooJive, perform hello following steps:**</span></span>

1. <span data-ttu-id="e6a68-218">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e6a68-220">Z listy aplikacji hello wybierz **Jive**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-220">In hello applications list, select **Jive**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="e6a68-222">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e6a68-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e6a68-224">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e6a68-224">Click **Add** button.</span></span> <span data-ttu-id="e6a68-225">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e6a68-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e6a68-227">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e6a68-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e6a68-228">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e6a68-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e6a68-229">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e6a68-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e6a68-230">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e6a68-230">Testing single sign-on</span></span>

<span data-ttu-id="e6a68-231">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e6a68-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e6a68-232">Po kliknięciu kafelka Jive hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Jive aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e6a68-232">When you click hello Jive tile in hello Access Panel, you should get automatically signed-on tooyour Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e6a68-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e6a68-233">Additional resources</span></span>

* [<span data-ttu-id="e6a68-234">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e6a68-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e6a68-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e6a68-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e6a68-236">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="e6a68-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

