---
title: 'Samouczek: Integracji Azure Active Directory z Tangoe polecenia Premium Mobile | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Tangoe polecenie Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="94e0b-103">Samouczek: Integracji Azure Active Directory z Tangoe polecenia Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="94e0b-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="94e0b-104">Z tego samouczka, dowiesz się, jak toointegrate Tangoe polecenia Premium Mobile w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94e0b-104">In this tutorial, you learn how toointegrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94e0b-105">Integracja z usługą Azure AD Tangoe polecenia Premium Mobile zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="94e0b-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="94e0b-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooTangoe polecenia mobilnych — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="94e0b-106">You can control in Azure AD who has access tooTangoe Command Premium Mobile</span></span>
- <span data-ttu-id="94e0b-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTangoe polecenia mobilnych — wersja Premium (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="94e0b-107">You can enable your users tooautomatically get signed-on tooTangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94e0b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="94e0b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="94e0b-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="94e0b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94e0b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="94e0b-110">Prerequisites</span></span>

<span data-ttu-id="94e0b-111">tooconfigure integracji usługi Azure AD z Tangoe polecenia Premium Mobile należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="94e0b-111">tooconfigure Azure AD integration with Tangoe Command Premium Mobile, you need hello following items:</span></span>

- <span data-ttu-id="94e0b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="94e0b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94e0b-113">Mobile Premium polecenia Tangoe logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="94e0b-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94e0b-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="94e0b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94e0b-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="94e0b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94e0b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="94e0b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94e0b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94e0b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94e0b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="94e0b-118">Scenario description</span></span>
<span data-ttu-id="94e0b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="94e0b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94e0b-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="94e0b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94e0b-121">Dodaj Mobile Premium polecenie Tangoe z galerii hello</span><span class="sxs-lookup"><span data-stu-id="94e0b-121">Add Tangoe Command Premium Mobile from hello gallery</span></span>
2. <span data-ttu-id="94e0b-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="94e0b-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a><span data-ttu-id="94e0b-123">Dodaj Mobile Premium polecenie Tangoe z galerii hello</span><span class="sxs-lookup"><span data-stu-id="94e0b-123">Add Tangoe Command Premium Mobile from hello gallery</span></span>
<span data-ttu-id="94e0b-124">tooconfigure hello integracji Tangoe polecenia Premium Mobile w usłudze Azure Active Directory, należy tooadd Mobile Premium polecenie Tangoe z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="94e0b-124">tooconfigure hello integration of Tangoe Command Premium Mobile into Azure AD, you need tooadd Tangoe Command Premium Mobile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="94e0b-125">**tooadd Tangoe polecenia Premium Mobile z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="94e0b-125">**tooadd Tangoe Command Premium Mobile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="94e0b-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="94e0b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="94e0b-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="94e0b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="94e0b-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="94e0b-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="94e0b-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="94e0b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="94e0b-133">W hello wyszukiwania wpisz **Tangoe polecenia Premium Mobile**, wybierz pozycję **Tangoe polecenia Premium Mobile** z panelu wyników kliknięcie **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="94e0b-133">In hello search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![<span data-ttu-id="94e0b-134">Dodaj Mobile Premium polecenie Tangoe z galerii</span><span class="sxs-lookup"><span data-stu-id="94e0b-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="94e0b-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="94e0b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="94e0b-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mobile Premium polecenia Tangoe w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="94e0b-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94e0b-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Tangoe polecenia Premium Mobile jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94e0b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tangoe Command Premium Mobile is tooa user in Azure AD.</span></span> <span data-ttu-id="94e0b-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Tangoe polecenia Premium Mobile musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="94e0b-138">In other words, a link relationship between an Azure AD user and hello related user in Tangoe Command Premium Mobile needs toobe established.</span></span>

<span data-ttu-id="94e0b-139">W Tangoe polecenia Premium urządzeń przenośnych, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="94e0b-139">In Tangoe Command Premium Mobile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="94e0b-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Tangoe polecenia Premium Mobile, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="94e0b-140">tooconfigure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="94e0b-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="94e0b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="94e0b-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="94e0b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94e0b-143">**[Tworzenie użytkownika testowego Mobile Premium polecenia Tangoe](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave odpowiednikiem Simona Britta w Tangoe polecenia Premium Mobile, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="94e0b-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - toohave a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="94e0b-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="94e0b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94e0b-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="94e0b-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="94e0b-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="94e0b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="94e0b-147">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne do aplikacji mobilnych — wersja Premium polecenia Tangoe.</span><span class="sxs-lookup"><span data-stu-id="94e0b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="94e0b-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z urządzeń przenośnych Premium polecenia Tangoe, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="94e0b-148">**tooconfigure Azure AD single sign-on with Tangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="94e0b-149">W portalu Azure na powitania hello **Tangoe polecenia Premium Mobile** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="94e0b-149">In hello Azure portal, on hello **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="94e0b-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="94e0b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="94e0b-153">Na powitania **Tangoe polecenia Premium Mobile domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="94e0b-153">On hello **Tangoe Command Premium Mobile Domain and URLs** section, perform hello following steps:</span></span>

    ![Polecenie Tangoe Premium przenośnych domeny i adres URL](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="94e0b-155">a.</span><span class="sxs-lookup"><span data-stu-id="94e0b-155">a.</span></span> <span data-ttu-id="94e0b-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="94e0b-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="94e0b-157">b.</span><span class="sxs-lookup"><span data-stu-id="94e0b-157">b.</span></span> <span data-ttu-id="94e0b-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="94e0b-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="94e0b-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="94e0b-159">These values are not real.</span></span> <span data-ttu-id="94e0b-160">Adres URL odpowiedzi rzeczywiste hello i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="94e0b-160">Update these values with hello actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="94e0b-161">Skontaktuj się z [zespołem pomocy technicznej klienta Mobile Premium polecenia Tangoe](https://www.tangoe.com/contact-2/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="94e0b-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooget these values.</span></span> 

4. <span data-ttu-id="94e0b-162">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="94e0b-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="94e0b-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="94e0b-164">Click **Save** button.</span></span>

    ![Przyciskiem Zapisz](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="94e0b-166">Na powitania **konfigurację Mobile Premium polecenia Tangoe** , kliknij przycisk **skonfigurować Mobile Premium polecenia Tangoe** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="94e0b-166">On hello **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="94e0b-167">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="94e0b-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sekcja konfiguracji Mobile Premium polecenia Tangoe](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="94e0b-169">tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z Twojego [zespołem pomocy technicznej klienta Mobile Premium polecenia Tangoe](https://www.tangoe.com/contact-2/) i podaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="94e0b-169">tooget SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide hello following:</span></span>

   - <span data-ttu-id="94e0b-170">Plik metadanych pobranych Hello</span><span class="sxs-lookup"><span data-stu-id="94e0b-170">hello downloaded metadata file</span></span>
   - <span data-ttu-id="94e0b-171">Witaj **identyfikator jednostki SAML**</span><span class="sxs-lookup"><span data-stu-id="94e0b-171">hello **SAML Entity ID**</span></span>
   - <span data-ttu-id="94e0b-172">Witaj **SAML pojedynczy znak na adres URL usługi**</span><span class="sxs-lookup"><span data-stu-id="94e0b-172">hello **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="94e0b-173">Witaj **Sign-Out adresu URL**</span><span class="sxs-lookup"><span data-stu-id="94e0b-173">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="94e0b-174">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="94e0b-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="94e0b-175">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="94e0b-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="94e0b-176">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="94e0b-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="94e0b-177">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="94e0b-177">Create an Azure AD test user</span></span>
<span data-ttu-id="94e0b-178">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="94e0b-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="94e0b-180">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="94e0b-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="94e0b-181">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="94e0b-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94e0b-183">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="94e0b-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Użytkownicy i grupy -> Wszyscy użytkownicy](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94e0b-185">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="94e0b-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Dodawanie użytkownika](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94e0b-187">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="94e0b-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Strony okna dialogowego użytkownika](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94e0b-189">a.</span><span class="sxs-lookup"><span data-stu-id="94e0b-189">a.</span></span> <span data-ttu-id="94e0b-190">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94e0b-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94e0b-191">b.</span><span class="sxs-lookup"><span data-stu-id="94e0b-191">b.</span></span> <span data-ttu-id="94e0b-192">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="94e0b-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94e0b-193">c.</span><span class="sxs-lookup"><span data-stu-id="94e0b-193">c.</span></span> <span data-ttu-id="94e0b-194">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="94e0b-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="94e0b-195">d.</span><span class="sxs-lookup"><span data-stu-id="94e0b-195">d.</span></span> <span data-ttu-id="94e0b-196">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="94e0b-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="94e0b-197">Tworzenie użytkownika testowego Tangoe polecenia Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="94e0b-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="94e0b-198">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Tangoe polecenia Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="94e0b-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="94e0b-199">Aplikacji mobilnych — wersja Premium polecenia Tangoe musi wszystkich toobe użytkowników hello udostępniane w aplikacji hello przed wykonaniem rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="94e0b-199">Tangoe Command Premium Mobile application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="94e0b-200">Pracy, dlatego należy z hello [zespołem pomocy technicznej klienta Mobile Premium polecenia Tangoe](https://www.tangoe.com/contact-2/) tooprovision tych użytkowników do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="94e0b-200">So please work with hello [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooprovision all these users into hello application.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="94e0b-201">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="94e0b-201">Assign hello Azure AD test user</span></span>

<span data-ttu-id="94e0b-202">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTangoe Mobile Premium polecenia.</span><span class="sxs-lookup"><span data-stu-id="94e0b-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTangoe Command Premium Mobile.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="94e0b-204">**tooassign tooTangoe Simona Britta polecenia Premium urządzeń przenośnych, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="94e0b-204">**tooassign Britta Simon tooTangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="94e0b-205">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="94e0b-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="94e0b-207">Z listy aplikacji hello wybierz **Tangoe polecenia Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="94e0b-207">In hello applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe polecenia Premium Mobile listy aplikacji](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="94e0b-209">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="94e0b-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="94e0b-211">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="94e0b-211">Click **Add** button.</span></span> <span data-ttu-id="94e0b-212">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="94e0b-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="94e0b-214">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="94e0b-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="94e0b-215">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="94e0b-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94e0b-216">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="94e0b-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="94e0b-217">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="94e0b-217">Test single sign-on</span></span>

<span data-ttu-id="94e0b-218">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="94e0b-218">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="94e0b-219">Po kliknięciu kafelka Tangoe polecenia Premium Mobile hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji mobilnych — wersja Premium polecenia Tangoe.</span><span class="sxs-lookup"><span data-stu-id="94e0b-219">When you click hello Tangoe Command Premium Mobile tile in hello Access Panel, you should get automatically signed-on tooyour Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="94e0b-220">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="94e0b-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="94e0b-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="94e0b-221">Additional resources</span></span>

* [<span data-ttu-id="94e0b-222">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94e0b-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94e0b-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="94e0b-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

