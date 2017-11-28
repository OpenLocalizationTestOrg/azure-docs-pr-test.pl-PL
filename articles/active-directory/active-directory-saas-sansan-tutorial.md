---
title: 'Samouczek: Integracji Azure Active Directory z Sansan | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Sansan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: f58cc613a2e3a240e555b61a34db4155eb9dff71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="5b2de-103">Samouczek: Integracji Azure Active Directory z Sansan</span><span class="sxs-lookup"><span data-stu-id="5b2de-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="5b2de-104">Z tego samouczka, dowiesz się, jak toointegrate Sansan w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b2de-104">In this tutorial, you learn how toointegrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b2de-105">Integracja z usługą Azure AD Sansan zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5b2de-105">Integrating Sansan with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b2de-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSansan</span><span class="sxs-lookup"><span data-stu-id="5b2de-106">You can control in Azure AD who has access tooSansan</span></span>
- <span data-ttu-id="5b2de-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSansan (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b2de-107">You can enable your users tooautomatically get signed-on tooSansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b2de-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5b2de-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b2de-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b2de-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b2de-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5b2de-110">Prerequisites</span></span>

<span data-ttu-id="5b2de-111">tooconfigure integracji z usługą Azure AD z Sansan należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5b2de-111">tooconfigure Azure AD integration with Sansan, you need hello following items:</span></span>

- <span data-ttu-id="5b2de-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b2de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b2de-113">Sansan logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5b2de-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b2de-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5b2de-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b2de-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5b2de-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b2de-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5b2de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b2de-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b2de-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b2de-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5b2de-118">Scenario description</span></span>
<span data-ttu-id="5b2de-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5b2de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b2de-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5b2de-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b2de-121">Dodawanie Sansan z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5b2de-121">Adding Sansan from hello gallery</span></span>
2. <span data-ttu-id="5b2de-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5b2de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-hello-gallery"></a><span data-ttu-id="5b2de-123">Dodawanie Sansan z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5b2de-123">Adding Sansan from hello gallery</span></span>
<span data-ttu-id="5b2de-124">tooconfigure hello integracji Sansan do usługi Azure AD, należy tooadd Sansan z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5b2de-124">tooconfigure hello integration of Sansan into Azure AD, you need tooadd Sansan from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b2de-125">**tooadd Sansan z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5b2de-125">**tooadd Sansan from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b2de-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5b2de-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5b2de-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b2de-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5b2de-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5b2de-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5b2de-133">W polu wyszukiwania hello wpisz **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-133">In hello search box, type **Sansan**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="5b2de-135">W panelu wyników hello zaznacz **Sansan**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b2de-135">In hello results panel, select **Sansan**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b2de-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5b2de-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b2de-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Sansan w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5b2de-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b2de-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Sansan jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b2de-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sansan is tooa user in Azure AD.</span></span> <span data-ttu-id="5b2de-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Sansan musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5b2de-140">In other words, a link relationship between an Azure AD user and hello related user in Sansan needs toobe established.</span></span>

<span data-ttu-id="5b2de-141">W Sansan, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="5b2de-141">In Sansan, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5b2de-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Sansan, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5b2de-142">tooconfigure and test Azure AD single sign-on with Sansan, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b2de-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b2de-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b2de-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5b2de-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b2de-145">**[Tworzenie użytkownika testowego Sansan](#creating-a-sansan-test-user)**  -toohave odpowiednikiem Simona Britta w Sansan, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5b2de-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - toohave a counterpart of Britta Simon in Sansan that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b2de-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5b2de-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b2de-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5b2de-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b2de-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5b2de-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b2de-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Sansan.</span><span class="sxs-lookup"><span data-stu-id="5b2de-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="5b2de-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Sansan, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5b2de-150">**tooconfigure Azure AD single sign-on with Sansan, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b2de-151">W portalu Azure na powitania hello **Sansan** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-151">In hello Azure portal, on hello **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5b2de-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5b2de-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="5b2de-155">Na powitania **Sansan domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5b2de-155">On hello **Sansan Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="5b2de-157">a.</span><span class="sxs-lookup"><span data-stu-id="5b2de-157">a.</span></span> <span data-ttu-id="5b2de-158">W hello **adres URL logowania** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="5b2de-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | <span data-ttu-id="5b2de-159">Środowisko</span><span class="sxs-lookup"><span data-stu-id="5b2de-159">Environment</span></span> | <span data-ttu-id="5b2de-160">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="5b2de-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="5b2de-161">Komputer w sieci web</span><span class="sxs-lookup"><span data-stu-id="5b2de-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="5b2de-162">Natywnych aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="5b2de-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="5b2de-163">Ustawienia przeglądarki przenośnych</span><span class="sxs-lookup"><span data-stu-id="5b2de-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="5b2de-164">b.</span><span class="sxs-lookup"><span data-stu-id="5b2de-164">b.</span></span> <span data-ttu-id="5b2de-165">W hello **identyfikator** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="5b2de-165">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="5b2de-166">Środowisko</span><span class="sxs-lookup"><span data-stu-id="5b2de-166">Environment</span></span>             | <span data-ttu-id="5b2de-167">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="5b2de-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="5b2de-168">Komputer w sieci web</span><span class="sxs-lookup"><span data-stu-id="5b2de-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="5b2de-169">Natywnych aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="5b2de-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="5b2de-170">Ustawienia przeglądarki przenośnych</span><span class="sxs-lookup"><span data-stu-id="5b2de-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="5b2de-171">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5b2de-171">These values are not real.</span></span> <span data-ttu-id="5b2de-172">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="5b2de-172">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5b2de-173">Skontaktuj się z [zespołem pomocy technicznej klienta Sansan](https://www.sansan.com/form/contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="5b2de-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) tooget these values.</span></span> 

4. <span data-ttu-id="5b2de-174">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5b2de-174">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="5b2de-176">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5b2de-176">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b2de-178">Na powitania **konfiguracji Sansan** kliknij **skonfigurować Sansan** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5b2de-178">On hello **Sansan Configuration** section, click **Configure Sansan** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5b2de-179">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5b2de-179">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="5b2de-181">tooconfigure rejestracji jednokrotnej w **Sansan** strony, należy pobrać hello toosend **certyfikatu**, **Sign-Out URL**, **identyfikator jednostki SAML**, i **SAML pojedynczy znak na adres URL usługi** za[zespołem pomocy technicznej Sansan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="5b2de-181">tooconfigure single sign-on on **Sansan** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="5b2de-182">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="5b2de-182">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="5b2de-183">Ustawienia przeglądarki komputera również działać dla aplikacji mobilnej oraz przeglądarkę dla telefonów wraz z Komputerami w sieci web.</span><span class="sxs-lookup"><span data-stu-id="5b2de-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="5b2de-184">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5b2de-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b2de-185">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5b2de-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b2de-186">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b2de-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b2de-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b2de-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b2de-188">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5b2de-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5b2de-190">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5b2de-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b2de-191">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5b2de-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b2de-193">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b2de-195">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5b2de-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b2de-197">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5b2de-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b2de-199">a.</span><span class="sxs-lookup"><span data-stu-id="5b2de-199">a.</span></span> <span data-ttu-id="5b2de-200">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b2de-201">b.</span><span class="sxs-lookup"><span data-stu-id="5b2de-201">b.</span></span> <span data-ttu-id="5b2de-202">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b2de-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b2de-203">c.</span><span class="sxs-lookup"><span data-stu-id="5b2de-203">c.</span></span> <span data-ttu-id="5b2de-204">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b2de-205">d.</span><span class="sxs-lookup"><span data-stu-id="5b2de-205">d.</span></span> <span data-ttu-id="5b2de-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="5b2de-207">Tworzenie użytkownika testowego Sansan</span><span class="sxs-lookup"><span data-stu-id="5b2de-207">Creating a Sansan test user</span></span>

<span data-ttu-id="5b2de-208">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w SanSan.</span><span class="sxs-lookup"><span data-stu-id="5b2de-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="5b2de-209">Aplikacja SanSan musi toobe użytkownika hello udostępniane w aplikacji hello przed wykonaniem logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="5b2de-209">SanSan application needs hello user toobe provisioned in hello application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="5b2de-210">Jeśli należy ręcznie toocreate użytkownika ani partii użytkowników, należy toocontact hello [zespołem pomocy technicznej Sansan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="5b2de-210">If you need toocreate a user manually or batch of users, you need toocontact hello [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b2de-211">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b2de-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b2de-212">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSansan.</span><span class="sxs-lookup"><span data-stu-id="5b2de-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSansan.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5b2de-214">**tooassign tooSansan Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5b2de-214">**tooassign Britta Simon tooSansan, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b2de-215">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5b2de-217">Z listy aplikacji hello wybierz **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-217">In hello applications list, select **Sansan**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="5b2de-219">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5b2de-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5b2de-221">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5b2de-221">Click **Add** button.</span></span> <span data-ttu-id="5b2de-222">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5b2de-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5b2de-224">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5b2de-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b2de-225">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5b2de-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b2de-226">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5b2de-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b2de-227">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5b2de-227">Testing single sign-on</span></span>

<span data-ttu-id="5b2de-228">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5b2de-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5b2de-229">Po kliknięciu kafelka Sansan hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Sansan aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b2de-229">When you click hello Sansan tile in hello Access Panel, you should get automatically signed-on tooyour Sansan application.</span></span>
<span data-ttu-id="5b2de-230">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5b2de-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b2de-231">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5b2de-231">Additional resources</span></span>

* [<span data-ttu-id="5b2de-232">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b2de-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b2de-233">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b2de-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

