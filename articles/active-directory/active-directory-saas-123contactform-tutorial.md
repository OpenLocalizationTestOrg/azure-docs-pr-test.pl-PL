---
title: 'Samouczek: Integracji Azure Active Directory z 123ContactForm | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="cd245-103">Samouczek: Integracji Azure Active Directory z 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="cd245-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="cd245-104">Z tego samouczka, dowiesz się, jak 123ContactForm toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cd245-104">In this tutorial, you learn how toointegrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd245-105">Integracja z usługą Azure AD 123ContactForm zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="cd245-105">Integrating 123ContactForm with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cd245-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do too123ContactForm</span><span class="sxs-lookup"><span data-stu-id="cd245-106">You can control in Azure AD who has access too123ContactForm</span></span>
- <span data-ttu-id="cd245-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane too123ContactForm (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd245-107">You can enable your users tooautomatically get signed-on too123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd245-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cd245-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cd245-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cd245-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd245-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cd245-110">Prerequisites</span></span>

<span data-ttu-id="cd245-111">tooconfigure integracji z usługą Azure AD z 123ContactForm należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cd245-111">tooconfigure Azure AD integration with 123ContactForm, you need hello following items:</span></span>

- <span data-ttu-id="cd245-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd245-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd245-113">123ContactForm logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cd245-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cd245-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="cd245-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cd245-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="cd245-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd245-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="cd245-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd245-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd245-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cd245-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="cd245-118">Scenario description</span></span>
<span data-ttu-id="cd245-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="cd245-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd245-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="cd245-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd245-121">Dodawanie 123ContactForm z galerii hello</span><span class="sxs-lookup"><span data-stu-id="cd245-121">Adding 123ContactForm from hello gallery</span></span>
2. <span data-ttu-id="cd245-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cd245-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-hello-gallery"></a><span data-ttu-id="cd245-123">Dodawanie 123ContactForm z galerii hello</span><span class="sxs-lookup"><span data-stu-id="cd245-123">Adding 123ContactForm from hello gallery</span></span>
<span data-ttu-id="cd245-124">tooconfigure hello integracji 123ContactForm do usługi Azure AD, należy 123ContactForm tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="cd245-124">tooconfigure hello integration of 123ContactForm into Azure AD, you need tooadd 123ContactForm from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cd245-125">**123ContactForm tooadd z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cd245-125">**tooadd 123ContactForm from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd245-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cd245-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="cd245-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="cd245-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cd245-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cd245-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="cd245-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cd245-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="cd245-133">W polu wyszukiwania hello wpisz **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="cd245-133">In hello search box, type **123ContactForm**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="cd245-135">W panelu wyników hello zaznacz **123ContactForm**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cd245-135">In hello results panel, select **123ContactForm**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cd245-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cd245-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cd245-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 123ContactForm na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="cd245-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cd245-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w 123ContactForm jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd245-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 123ContactForm is tooa user in Azure AD.</span></span> <span data-ttu-id="cd245-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w 123ContactForm musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="cd245-140">In other words, a link relationship between an Azure AD user and hello related user in 123ContactForm needs toobe established.</span></span>

<span data-ttu-id="cd245-141">W 123ContactForm, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="cd245-141">In 123ContactForm, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cd245-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z 123ContactForm, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="cd245-142">tooconfigure and test Azure AD single sign-on with 123ContactForm, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cd245-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cd245-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cd245-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cd245-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd245-145">**[Tworzenie użytkownika testowego 123ContactForm](#creating-a-123contactform-test-user)**  -toohave odpowiednikiem Simona Britta w 123ContactForm, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cd245-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - toohave a counterpart of Britta Simon in 123ContactForm that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cd245-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cd245-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cd245-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="cd245-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cd245-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cd245-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cd245-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="cd245-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="cd245-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z 123ContactForm, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cd245-150">**tooconfigure Azure AD single sign-on with 123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd245-151">W portalu Azure na powitania hello **123ContactForm** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="cd245-151">In hello Azure portal, on hello **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="cd245-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cd245-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="cd245-155">Na powitania **123ContactForm domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cd245-155">On hello **123ContactForm Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="cd245-157">a.</span><span class="sxs-lookup"><span data-stu-id="cd245-157">a.</span></span> <span data-ttu-id="cd245-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="cd245-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="cd245-159">b.</span><span class="sxs-lookup"><span data-stu-id="cd245-159">b.</span></span> <span data-ttu-id="cd245-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="cd245-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="cd245-161">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cd245-161">If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="cd245-163">a.</span><span class="sxs-lookup"><span data-stu-id="cd245-163">a.</span></span> <span data-ttu-id="cd245-164">Kliknij przycisk hello **Pokaż zaawansowane ustawienia adresu URL** opcji</span><span class="sxs-lookup"><span data-stu-id="cd245-164">Click hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="cd245-165">b.</span><span class="sxs-lookup"><span data-stu-id="cd245-165">b.</span></span> <span data-ttu-id="cd245-166">W hello **na adres URL logowania** tekstowym, wpisz adres URL jako:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="cd245-166">In hello **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd245-167">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="cd245-167">These values are not real.</span></span> <span data-ttu-id="cd245-168">Będziesz potrzebować tooupdate te wartości od rzeczywistej adresy URL i identyfikator, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="cd245-168">You'll need tooupdate these value from actual URLs and Identifier which is explained later in hello tutorial.</span></span>
    
5. <span data-ttu-id="cd245-169">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="cd245-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="cd245-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cd245-171">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="cd245-173">tooconfigure rejestracji jednokrotnej w **123ContactForm** po stronie znajduje się zbyt[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cd245-173">tooconfigure single sign-on on **123ContactForm** side, go too[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="cd245-175">a.</span><span class="sxs-lookup"><span data-stu-id="cd245-175">a.</span></span> <span data-ttu-id="cd245-176">W hello **E-mail** pole tekstowe, adres e-mail hello typu hello tj użytkownika</span><span class="sxs-lookup"><span data-stu-id="cd245-176">In hello **Email** textbox, type hello email of hello user i.e</span></span> <span data-ttu-id="cd245-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="cd245-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="cd245-178">b.</span><span class="sxs-lookup"><span data-stu-id="cd245-178">b.</span></span> <span data-ttu-id="cd245-179">Kliknij przycisk **przekazać** i Przeglądaj hello pliku XML metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cd245-179">Click **Upload** and browse hello Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="cd245-180">c.</span><span class="sxs-lookup"><span data-stu-id="cd245-180">c.</span></span> <span data-ttu-id="cd245-181">Kliknij przycisk **przesyłania formularza**.</span><span class="sxs-lookup"><span data-stu-id="cd245-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="cd245-182">Na powitania **Konfigurowanie ustawień aplikacji Microsoft Azure AD — logowanie jednokrotne -** wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cd245-182">On hello **Microsoft Azure AD - Single sign-on - Configure App Settings** perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="cd245-184">a.</span><span class="sxs-lookup"><span data-stu-id="cd245-184">a.</span></span> <span data-ttu-id="cd245-185">Jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb**, hello kopiowania **identyfikator** wartość dla swojego wystąpienia, a następnie wklej je **identyfikator** textbox w **123ContactForm domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cd245-185">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="cd245-186">b.</span><span class="sxs-lookup"><span data-stu-id="cd245-186">b.</span></span> <span data-ttu-id="cd245-187">Jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb**, hello kopiowania **adres URL odpowiedzi** wartość dla swojego wystąpienia, a następnie wklej je **adres URL odpowiedzi służący** textbox w **123ContactForm domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cd245-187">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="cd245-188">c.</span><span class="sxs-lookup"><span data-stu-id="cd245-188">c.</span></span> <span data-ttu-id="cd245-189">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb**, hello kopiowania **adres URL logowania na** wartość dla swojego wystąpienia, a następnie wklej je **na adres URL logowania** textbox w **123ContactForm domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cd245-189">If you wish tooconfigure hello application in **SP initiated mode**, copy hello **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="cd245-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="cd245-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cd245-191">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="cd245-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cd245-192">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cd245-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cd245-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd245-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="cd245-194">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="cd245-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="cd245-196">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cd245-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd245-197">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cd245-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cd245-199">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="cd245-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cd245-201">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cd245-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cd245-203">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cd245-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd245-205">a.</span><span class="sxs-lookup"><span data-stu-id="cd245-205">a.</span></span> <span data-ttu-id="cd245-206">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cd245-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd245-207">b.</span><span class="sxs-lookup"><span data-stu-id="cd245-207">b.</span></span> <span data-ttu-id="cd245-208">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cd245-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd245-209">c.</span><span class="sxs-lookup"><span data-stu-id="cd245-209">c.</span></span> <span data-ttu-id="cd245-210">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="cd245-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cd245-211">d.</span><span class="sxs-lookup"><span data-stu-id="cd245-211">d.</span></span> <span data-ttu-id="cd245-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cd245-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="cd245-213">Tworzenie użytkownika testowego 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="cd245-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="cd245-214">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="cd245-214">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cd245-215">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd245-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cd245-216">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu too123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="cd245-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too123ContactForm.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="cd245-218">**tooassign too123ContactForm Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cd245-218">**tooassign Britta Simon too123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd245-219">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cd245-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="cd245-221">Z listy aplikacji hello wybierz **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="cd245-221">In hello applications list, select **123ContactForm**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="cd245-223">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="cd245-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="cd245-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cd245-225">Click **Add** button.</span></span> <span data-ttu-id="cd245-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cd245-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="cd245-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cd245-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cd245-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cd245-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd245-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cd245-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cd245-231">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cd245-231">Testing single sign-on</span></span>

<span data-ttu-id="cd245-232">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="cd245-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cd245-233">Po kliknięciu kafelka 123ContactForm hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour 123ContactForm aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd245-233">When you click hello 123ContactForm tile in hello Access Panel, you should get automatically signed-on tooyour 123ContactForm application.</span></span>
<span data-ttu-id="cd245-234">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cd245-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cd245-235">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="cd245-235">Additional resources</span></span>

* [<span data-ttu-id="cd245-236">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd245-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd245-237">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cd245-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

