---
title: "Samouczek: Integracji Azure Active Directory z szkoleń elektronicznych Yardi | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i szkoleń Yardi elektronicznych."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7ea58b54-ec5b-4576-8586-814b11d0f4fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 47c95fe024e76a67aa5c5b3ee6f81cbafc50ff07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yardi-elearning"></a><span data-ttu-id="bd0b7-103">Samouczek: Integracji Azure Active Directory z szkoleń elektronicznych Yardi</span><span class="sxs-lookup"><span data-stu-id="bd0b7-103">Tutorial: Azure Active Directory integration with Yardi eLearning</span></span>

<span data-ttu-id="bd0b7-104">Z tego samouczka, dowiesz się, jak szkoleń elektronicznych Yardi toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd0b7-104">In this tutorial, you learn how toointegrate Yardi eLearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd0b7-105">Integrowanie Yardi szkoleń elektronicznych z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bd0b7-105">Integrating Yardi eLearning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd0b7-106">Można kontrolować w usłudze Azure AD mającego szkoleń elektronicznych tooYardi dostępu</span><span class="sxs-lookup"><span data-stu-id="bd0b7-106">You can control in Azure AD who has access tooYardi eLearning</span></span>
- <span data-ttu-id="bd0b7-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooYardi szkoleń elektronicznych (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd0b7-107">You can enable your users tooautomatically get signed-on tooYardi eLearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd0b7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bd0b7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bd0b7-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd0b7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd0b7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bd0b7-110">Prerequisites</span></span>

<span data-ttu-id="bd0b7-111">tooconfigure integracji usługi Azure AD z szkoleń elektronicznych Yardi należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bd0b7-111">tooconfigure Azure AD integration with Yardi eLearning, you need hello following items:</span></span>

- <span data-ttu-id="bd0b7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd0b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd0b7-113">Yardi szkoleń elektronicznych jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bd0b7-113">A Yardi eLearning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd0b7-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd0b7-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bd0b7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd0b7-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd0b7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd0b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd0b7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bd0b7-118">Scenario description</span></span>
<span data-ttu-id="bd0b7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd0b7-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bd0b7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd0b7-121">Dodawanie szkoleń elektronicznych Yardi z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bd0b7-121">Adding Yardi eLearning from hello gallery</span></span>
2. <span data-ttu-id="bd0b7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bd0b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yardi-elearning-from-hello-gallery"></a><span data-ttu-id="bd0b7-123">Dodawanie szkoleń elektronicznych Yardi z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bd0b7-123">Adding Yardi eLearning from hello gallery</span></span>
<span data-ttu-id="bd0b7-124">tooconfigure hello integracji szkoleń elektronicznych Yardi do usługi Azure AD, należy szkoleń elektronicznych Yardi tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-124">tooconfigure hello integration of Yardi eLearning into Azure AD, you need tooadd Yardi eLearning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd0b7-125">**szkoleń elektronicznych Yardi tooadd z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bd0b7-125">**tooadd Yardi eLearning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd0b7-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bd0b7-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd0b7-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bd0b7-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bd0b7-133">W polu wyszukiwania hello wpisz **szkoleń elektronicznych Yardi**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-133">In hello search box, type **Yardi eLearning**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_search.png)

5. <span data-ttu-id="bd0b7-135">W panelu wyników hello, wybierz **szkoleń elektronicznych Yardi**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-135">In hello results panel, select **Yardi eLearning**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd0b7-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bd0b7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd0b7-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z szkoleń elektronicznych Yardi oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="bd0b7-138">In this section, you configure and test Azure AD single sign-on with Yardi eLearning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bd0b7-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w szkoleń elektronicznych Yardi jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Yardi eLearning is tooa user in Azure AD.</span></span> <span data-ttu-id="bd0b7-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w szkoleń elektronicznych Yardi musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-140">In other words, a link relationship between an Azure AD user and hello related user in Yardi eLearning needs toobe established.</span></span>

<span data-ttu-id="bd0b7-141">W Yardi szkoleń elektronicznych, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-141">In Yardi eLearning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bd0b7-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Yardi szkoleń elektronicznych, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bd0b7-142">tooconfigure and test Azure AD single sign-on with Yardi eLearning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd0b7-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd0b7-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd0b7-145">**[Tworzenie użytkownika testowego szkoleń elektronicznych Yardi](#creating-a-yardi-elearning-test-user)**  -toohave odpowiednikiem Simona Britta w szkoleń elektronicznych Yardi, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-145">**[Creating a Yardi eLearning test user](#creating-a-yardi-elearning-test-user)** - toohave a counterpart of Britta Simon in Yardi eLearning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd0b7-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd0b7-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd0b7-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bd0b7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd0b7-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji szkoleń elektronicznych Yardi.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Yardi eLearning application.</span></span>

<span data-ttu-id="bd0b7-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Yardi szkoleń elektronicznych, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bd0b7-150">**tooconfigure Azure AD single sign-on with Yardi eLearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd0b7-151">W portalu Azure na powitania hello **szkoleń elektronicznych Yardi** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-151">In hello Azure portal, on hello **Yardi eLearning** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bd0b7-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_samlbase.png)

3. <span data-ttu-id="bd0b7-155">Na powitania **szkoleń elektronicznych Yardi domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="bd0b7-155">On hello **Yardi eLearning Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_url.png)

    <span data-ttu-id="bd0b7-157">a.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-157">a.</span></span> <span data-ttu-id="bd0b7-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.yardielearning.com/login`</span><span class="sxs-lookup"><span data-stu-id="bd0b7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.yardielearning.com/login`</span></span>

    <span data-ttu-id="bd0b7-159">b.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-159">b.</span></span> <span data-ttu-id="bd0b7-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.yardielearning.com/trust`</span><span class="sxs-lookup"><span data-stu-id="bd0b7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.yardielearning.com/trust`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd0b7-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-161">These values are not real.</span></span> <span data-ttu-id="bd0b7-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bd0b7-163">Skontaktuj się z [zespołem pomocy technicznej klienta szkoleń elektronicznych Yardi](mailto:elearning@yardi.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-163">Contact [Yardi eLearning Client support team](mailto:elearning@yardi.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="bd0b7-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_certificate.png) 

5. <span data-ttu-id="bd0b7-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-yardielearning-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bd0b7-168">tooconfigure rejestracji jednokrotnej w **szkoleń elektronicznych Yardi** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej szkoleń elektronicznych Yardi](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="bd0b7-168">tooconfigure single sign-on on **Yardi eLearning** side, you need toosend hello downloaded **Metadata XML** too[Yardi eLearning support team](mailto:elearning@yardi.com).</span></span> 

> [!TIP]
> <span data-ttu-id="bd0b7-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="bd0b7-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bd0b7-170">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bd0b7-171">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd0b7-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd0b7-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd0b7-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd0b7-173">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bd0b7-175">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bd0b7-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd0b7-176">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd0b7-178">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd0b7-180">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd0b7-182">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bd0b7-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd0b7-184">a.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-184">a.</span></span> <span data-ttu-id="bd0b7-185">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd0b7-186">b.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-186">b.</span></span> <span data-ttu-id="bd0b7-187">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd0b7-188">c.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-188">c.</span></span> <span data-ttu-id="bd0b7-189">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bd0b7-190">d.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-190">d.</span></span> <span data-ttu-id="bd0b7-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-191">Click **Create**.</span></span>
 
### <a name="creating-a-yardi-elearning-test-user"></a><span data-ttu-id="bd0b7-192">Tworzenie użytkownika testowego szkoleń elektronicznych Yardi</span><span class="sxs-lookup"><span data-stu-id="bd0b7-192">Creating a Yardi eLearning test user</span></span>

<span data-ttu-id="bd0b7-193">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Yardi szkoleń elektronicznych.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-193">hello objective of this section is toocreate a user called Britta Simon in Yardi eLearning.</span></span> <span data-ttu-id="bd0b7-194">Szkoleń elektronicznych Yardi obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-194">Yardi eLearning supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="bd0b7-195">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-195">There is no action item for you in this section.</span></span> <span data-ttu-id="bd0b7-196">Nowy użytkownik został utworzony podczas tooaccess próba szkoleń elektronicznych Yardi, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-196">A new user is created during an attempt tooaccess Yardi eLearning if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="bd0b7-197">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej szkoleń elektronicznych Yardi](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="bd0b7-197">If you need toocreate a user manually, you need toocontact hello [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bd0b7-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd0b7-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bd0b7-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie szkoleń elektronicznych tooYardi dostępu.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYardi eLearning.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bd0b7-201">**tooassign Simona Britta tooYardi szkoleń elektronicznych, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="bd0b7-201">**tooassign Britta Simon tooYardi eLearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd0b7-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bd0b7-204">Z listy aplikacji hello wybierz **szkoleń elektronicznych Yardi**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-204">In hello applications list, select **Yardi eLearning**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_app.png) 

3. <span data-ttu-id="bd0b7-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bd0b7-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-208">Click **Add** button.</span></span> <span data-ttu-id="bd0b7-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bd0b7-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd0b7-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd0b7-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bd0b7-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bd0b7-214">Testing single sign-on</span></span>

<span data-ttu-id="bd0b7-215">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bd0b7-216">Po kliknięciu kafelka szkoleń elektronicznych Yardi hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Yardi szkoleń elektronicznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd0b7-216">When you click hello Yardi eLearning tile in hello Access Panel, you should get automatically signed-on tooyour Yardi eLearning application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bd0b7-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bd0b7-217">Additional resources</span></span>

* [<span data-ttu-id="bd0b7-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd0b7-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd0b7-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bd0b7-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_203.png

