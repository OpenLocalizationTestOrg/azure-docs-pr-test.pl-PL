---
title: 'Samouczek: Integracji Azure Active Directory z O.C. Napisu Czarnecka - AppreciateHub | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i O.C. Napisu Czarnecka - AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="258e4-105">Samouczek: Integracji Azure Active Directory z O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="258e4-106">Napisu Czarnecka - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="258e4-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="258e4-107">Z tego samouczka, dowiesz się, jak toointegrate O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-107">In this tutorial, you learn how toointegrate O.C.</span></span> <span data-ttu-id="258e4-108">Napisu Czarnecka - AppreciateHub z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="258e4-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="258e4-109">Integrowanie O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-109">Integrating O.C.</span></span> <span data-ttu-id="258e4-110">Napisu Czarnecka - AppreciateHub z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="258e4-110">Tanner - AppreciateHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="258e4-111">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooO.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-111">You can control in Azure AD who has access tooO.C.</span></span> <span data-ttu-id="258e4-112">Napisu Czarnecka - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="258e4-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="258e4-113">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooO.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-113">You can enable your users tooautomatically get signed-on tooO.C.</span></span> <span data-ttu-id="258e4-114">Napisu Czarnecka - AppreciateHub (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="258e4-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="258e4-115">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="258e4-115">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="258e4-116">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="258e4-116">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="258e4-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="258e4-117">Prerequisites</span></span>

<span data-ttu-id="258e4-118">tooconfigure integracji z usługą Azure AD z O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-118">tooconfigure Azure AD integration with O.C.</span></span> <span data-ttu-id="258e4-119">Napisu Czarnecka - AppreciateHub, potrzebujesz hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="258e4-119">Tanner - AppreciateHub, you need hello following items:</span></span>

- <span data-ttu-id="258e4-120">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="258e4-120">An Azure AD subscription</span></span>
- <span data-ttu-id="258e4-121">O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-121">A O.C.</span></span> <span data-ttu-id="258e4-122">Napisu Czarnecka - AppreciateHub logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="258e4-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="258e4-123">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="258e4-123">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="258e4-124">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="258e4-124">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="258e4-125">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="258e4-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="258e4-126">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="258e4-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="258e4-127">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="258e4-127">Scenario description</span></span>
<span data-ttu-id="258e4-128">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="258e4-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="258e4-129">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="258e4-129">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="258e4-130">Dodawanie O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-130">Adding O.C.</span></span> <span data-ttu-id="258e4-131">Napisu Czarnecka - AppreciateHub z galerii hello</span><span class="sxs-lookup"><span data-stu-id="258e4-131">Tanner - AppreciateHub from hello gallery</span></span>
2. <span data-ttu-id="258e4-132">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="258e4-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a><span data-ttu-id="258e4-133">Dodawanie O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-133">Adding O.C.</span></span> <span data-ttu-id="258e4-134">Napisu Czarnecka - AppreciateHub z galerii hello</span><span class="sxs-lookup"><span data-stu-id="258e4-134">Tanner - AppreciateHub from hello gallery</span></span>
<span data-ttu-id="258e4-135">Integracja hello tooconfigure O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-135">tooconfigure hello integration of O.C.</span></span> <span data-ttu-id="258e4-136">Napisu Czarnecka - AppreciateHub do usługi Azure AD, należy tooadd O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-136">Tanner - AppreciateHub into Azure AD, you need tooadd O.C.</span></span> <span data-ttu-id="258e4-137">Napisu Czarnecka - AppreciateHub z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="258e4-137">Tanner - AppreciateHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="258e4-138">**tooadd O.C. Napisu Czarnecka - AppreciateHub z galerii hello wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="258e4-138">**tooadd O.C. Tanner - AppreciateHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="258e4-139">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="258e4-139">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="258e4-141">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="258e4-141">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="258e4-142">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="258e4-142">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="258e4-144">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="258e4-144">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="258e4-146">W polu wyszukiwania hello wpisz **O.C. Napisu Czarnecka - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="258e4-146">In hello search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="258e4-148">Wybierz w panelu wyników hello **O.C. Napisu Czarnecka - AppreciateHub**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="258e4-148">In hello results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="258e4-150">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="258e4-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="258e4-151">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="258e4-152">Napisu Czarnecka - AppreciateHub w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="258e4-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="258e4-153">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello w O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-153">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in O.C.</span></span> <span data-ttu-id="258e4-154">Napisu Czarnecka - AppreciateHub jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="258e4-154">Tanner - AppreciateHub is tooa user in Azure AD.</span></span> <span data-ttu-id="258e4-155">Innymi słowy relacja linku między użytkownika usługi Azure AD i hello użytkownikowi w O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-155">In other words, a link relationship between an Azure AD user and hello related user in O.C.</span></span> <span data-ttu-id="258e4-156">Napisu Czarnecka - AppreciateHub musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="258e4-156">Tanner - AppreciateHub needs toobe established.</span></span>

<span data-ttu-id="258e4-157">W O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-157">In O.C.</span></span> <span data-ttu-id="258e4-158">Napisu Czarnecka - AppreciateHub, przypisz hello wartość hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="258e4-158">Tanner - AppreciateHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="258e4-159">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-159">tooconfigure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="258e4-160">Napisu Czarnecka - AppreciateHub, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="258e4-160">Tanner - AppreciateHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="258e4-161">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="258e4-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="258e4-162">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="258e4-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="258e4-163">**[Tworzenie O.C. Napisu Czarnecka - użytkownika testowego AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**  -toohave odpowiednikiem Simona Britta w O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - toohave a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="258e4-164">Napisu Czarnecka - AppreciateHub, który jest połączony toohello reprezentacja użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="258e4-164">Tanner - AppreciateHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="258e4-165">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="258e4-165">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="258e4-166">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="258e4-166">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="258e4-167">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="258e4-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="258e4-168">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w sieci O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-168">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="258e4-169">Napisu Czarnecka - AppreciateHub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="258e4-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="258e4-170">**tooconfigure usługi Azure AD rejestracji jednokrotnej z O.C. Napisu Czarnecka - AppreciateHub, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="258e4-170">**tooconfigure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="258e4-171">W portalu Azure na powitania hello **O.C. Napisu Czarnecka - AppreciateHub** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="258e4-171">In hello Azure portal, on hello **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="258e4-173">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="258e4-173">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="258e4-175">Na powitania **O.C. Napisu Czarnecka - AppreciateHub domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="258e4-175">On hello **O.C. Tanner - AppreciateHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="258e4-177">a.</span><span class="sxs-lookup"><span data-stu-id="258e4-177">a.</span></span> <span data-ttu-id="258e4-178">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="258e4-178">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="258e4-179">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="258e4-179">This value is not real.</span></span> <span data-ttu-id="258e4-180">Zaktualizuj tę wartość przy hello rzeczywisty adres URL odpowiedzi służący.</span><span class="sxs-lookup"><span data-stu-id="258e4-180">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="258e4-181">Skontaktuj się z [O.C. Napisu Czarnecka - zespołem pomocy technicznej AppreciateHub](mailto:sso@octanner.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="258e4-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) tooget this value.</span></span>

    <span data-ttu-id="258e4-182">b.</span><span class="sxs-lookup"><span data-stu-id="258e4-182">b.</span></span> <span data-ttu-id="258e4-183">Plik metadanych hello Otwórz za pomocą hello następującego łącza: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="258e4-183">Open hello metadata file using hello following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="258e4-184">c.</span><span class="sxs-lookup"><span data-stu-id="258e4-184">c.</span></span> <span data-ttu-id="258e4-185">Zlokalizuj hello **md:AssertionConsumerService** węzła.</span><span class="sxs-lookup"><span data-stu-id="258e4-185">Locate hello **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="258e4-186">d.</span><span class="sxs-lookup"><span data-stu-id="258e4-186">d.</span></span> <span data-ttu-id="258e4-187">Skopiuj wartość hello hello **lokalizacji** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="258e4-187">Copy hello value of hello **Location** attribute.</span></span> 
   
    ![Konfiguruj ustawienia aplikacji][12]
   
    <span data-ttu-id="258e4-189">e.</span><span class="sxs-lookup"><span data-stu-id="258e4-189">e.</span></span> <span data-ttu-id="258e4-190">W hello **na adres URL logowania** pole tekstowe po uzyskaniu w poprzednim kroku hello wartość hello.</span><span class="sxs-lookup"><span data-stu-id="258e4-190">In hello **Sign On URL** textbox, past hello value you have obtained in hello previous step.</span></span>

4. <span data-ttu-id="258e4-191">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="258e4-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="258e4-193">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="258e4-193">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="258e4-195">tooconfigure rejestracji jednokrotnej w **O.C. Napisu Czarnecka - AppreciateHub** strony, należy pobrać hello toosend **XML metadanych** zbyt[O.C. Napisu Czarnecka - zespołem pomocy technicznej AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="258e4-195">tooconfigure single sign-on on **O.C. Tanner - AppreciateHub** side, you need toosend hello downloaded **Metadata XML** too[O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="258e4-196">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="258e4-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="258e4-197">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="258e4-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="258e4-198">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="258e4-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="258e4-199">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="258e4-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="258e4-200">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="258e4-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="258e4-202">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="258e4-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="258e4-203">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="258e4-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="258e4-205">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="258e4-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="258e4-207">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="258e4-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="258e4-209">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="258e4-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="258e4-211">a.</span><span class="sxs-lookup"><span data-stu-id="258e4-211">a.</span></span> <span data-ttu-id="258e4-212">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="258e4-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="258e4-213">b.</span><span class="sxs-lookup"><span data-stu-id="258e4-213">b.</span></span> <span data-ttu-id="258e4-214">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="258e4-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="258e4-215">c.</span><span class="sxs-lookup"><span data-stu-id="258e4-215">c.</span></span> <span data-ttu-id="258e4-216">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="258e4-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="258e4-217">d.</span><span class="sxs-lookup"><span data-stu-id="258e4-217">d.</span></span> <span data-ttu-id="258e4-218">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="258e4-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="258e4-219">Tworzenie O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-219">Creating a O.C.</span></span> <span data-ttu-id="258e4-220">Napisu Czarnecka - AppreciateHub użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="258e4-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="258e4-221">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-221">hello objective of this section is toocreate a user called Britta Simon in O.C.</span></span> <span data-ttu-id="258e4-222">Napisu Czarnecka - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="258e4-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="258e4-223">**toocreate użytkownik wywołuje Simona Britta O.C. Napisu Czarnecka - AppreciateHub, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="258e4-223">**toocreate a user called Britta Simon in O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

<span data-ttu-id="258e4-224">Skontaktuj się z [O.C. Napisu Czarnecka - zespołem pomocy technicznej AppreciateHub](mailto:sso@octanner.com) toocreate użytkownika, takiej jak hello atrybutu nameID samą wartość jak nazwa użytkownika hello Simona Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="258e4-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) toocreate a user that has as nameID attribute hello same value as hello user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="258e4-225">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="258e4-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="258e4-226">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooO.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooO.C.</span></span> <span data-ttu-id="258e4-227">Napisu Czarnecka - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="258e4-227">Tanner - AppreciateHub.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="258e4-229">**tooassign tooO.C Simona Britta. Napisu Czarnecka - AppreciateHub, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="258e4-229">**tooassign Britta Simon tooO.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="258e4-230">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="258e4-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="258e4-232">Z listy aplikacji hello wybierz **O.C. Napisu Czarnecka - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="258e4-232">In hello applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="258e4-234">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="258e4-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="258e4-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="258e4-236">Click **Add** button.</span></span> <span data-ttu-id="258e4-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="258e4-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="258e4-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="258e4-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="258e4-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="258e4-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="258e4-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="258e4-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="258e4-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="258e4-242">Testing single sign-on</span></span>

<span data-ttu-id="258e4-243">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="258e4-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="258e4-244">Po kliknięciu hello O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-244">When you click hello O.C.</span></span> <span data-ttu-id="258e4-245">Napisu Czarnecka - AppreciateHub kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour O.C.</span><span class="sxs-lookup"><span data-stu-id="258e4-245">Tanner - AppreciateHub tile in hello Access Panel, you should get automatically signed-on tooyour O.C.</span></span> <span data-ttu-id="258e4-246">Napisu Czarnecka - AppreciateHub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="258e4-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="258e4-247">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="258e4-247">Additional resources</span></span>

* [<span data-ttu-id="258e4-248">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="258e4-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="258e4-249">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="258e4-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

