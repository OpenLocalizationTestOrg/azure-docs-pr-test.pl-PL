---
title: 'Samouczek: Integracji Azure Active Directory z Kronos | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Kronos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 16fd5c203162d10b78f51b00d79017adaf8632c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="65226-103">Samouczek: Integracji Azure Active Directory z Kronos</span><span class="sxs-lookup"><span data-stu-id="65226-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="65226-104">Z tego samouczka, dowiesz się, jak toointegrate Kronos w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65226-104">In this tutorial, you learn how toointegrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65226-105">Integracja z usługą Azure AD Kronos zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="65226-105">Integrating Kronos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65226-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooKronos</span><span class="sxs-lookup"><span data-stu-id="65226-106">You can control in Azure AD who has access tooKronos</span></span>
- <span data-ttu-id="65226-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooKronos (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="65226-107">You can enable your users tooautomatically get signed-on tooKronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65226-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="65226-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="65226-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65226-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65226-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="65226-110">Prerequisites</span></span>

<span data-ttu-id="65226-111">tooconfigure integracji z usługą Azure AD z Kronos należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="65226-111">tooconfigure Azure AD integration with Kronos, you need hello following items:</span></span>

- <span data-ttu-id="65226-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="65226-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65226-113">A **Kronos pracowników centralnej** logowanie Jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="65226-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65226-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="65226-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65226-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="65226-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65226-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="65226-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65226-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65226-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65226-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="65226-118">Scenario description</span></span>
<span data-ttu-id="65226-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="65226-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65226-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="65226-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65226-121">Dodawanie Kronos z galerii hello</span><span class="sxs-lookup"><span data-stu-id="65226-121">Adding Kronos from hello gallery</span></span>
2. <span data-ttu-id="65226-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="65226-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-hello-gallery"></a><span data-ttu-id="65226-123">Dodawanie Kronos z galerii hello</span><span class="sxs-lookup"><span data-stu-id="65226-123">Adding Kronos from hello gallery</span></span>
<span data-ttu-id="65226-124">tooconfigure hello integracji Kronos do usługi Azure AD, należy tooadd Kronos z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="65226-124">tooconfigure hello integration of Kronos into Azure AD, you need tooadd Kronos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="65226-125">**tooadd Kronos z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="65226-125">**tooadd Kronos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="65226-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="65226-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="65226-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="65226-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="65226-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="65226-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="65226-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="65226-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="65226-133">W polu wyszukiwania hello wpisz **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="65226-133">In hello search box, type **Kronos**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="65226-135">W panelu wyników hello zaznacz **Kronos**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="65226-135">In hello results panel, select **Kronos**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65226-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="65226-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65226-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kronos na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="65226-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="65226-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Kronos jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65226-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kronos is tooa user in Azure AD.</span></span> <span data-ttu-id="65226-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Kronos musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="65226-140">In other words, a link relationship between an Azure AD user and hello related user in Kronos needs toobe established.</span></span>

<span data-ttu-id="65226-141">W Kronos, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="65226-141">In Kronos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="65226-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Kronos, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="65226-142">tooconfigure and test Azure AD single sign-on with Kronos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="65226-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="65226-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="65226-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="65226-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65226-145">**[Tworzenie użytkownika testowego Kronos](#creating-a-kronos-test-user)**  -toohave odpowiednikiem Simona Britta w Kronos, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65226-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - toohave a counterpart of Britta Simon in Kronos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="65226-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="65226-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65226-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="65226-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65226-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="65226-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65226-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Kronos.</span><span class="sxs-lookup"><span data-stu-id="65226-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="65226-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Kronos, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="65226-150">**tooconfigure Azure AD single sign-on with Kronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="65226-151">W portalu Azure na powitania hello **Kronos** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="65226-151">In hello Azure portal, on hello **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="65226-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="65226-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="65226-155">Na powitania **Kronos domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="65226-155">On hello **Kronos Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="65226-157">a.</span><span class="sxs-lookup"><span data-stu-id="65226-157">a.</span></span> <span data-ttu-id="65226-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="65226-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="65226-159">b.</span><span class="sxs-lookup"><span data-stu-id="65226-159">b.</span></span> <span data-ttu-id="65226-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="65226-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="65226-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="65226-161">These values are not real.</span></span> <span data-ttu-id="65226-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="65226-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="65226-163">Skontaktuj się z [Kronos obsługuje zespołu](https://www.kronos.in/contact/en-in/form) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="65226-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) tooget these values.</span></span>
 
4. <span data-ttu-id="65226-164">Aplikacja Kronos oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="65226-164">Your Kronos application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="65226-165">Praca z [Kronos obsługuje zespołu](https://www.kronos.in/contact/en-in/form) pierwszego tooidentify hello poprawny identyfikator użytkownika, która jest mapowana do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="65226-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first tooidentify hello correct user identifier, which is mapped into hello application.</span></span> <span data-ttu-id="65226-166">Należy również wziąć hello wskazówek dotyczących hello atrybut, który ma toouse Aby to mapowanie.</span><span class="sxs-lookup"><span data-stu-id="65226-166">Also please take hello guidance about hello attribute, which they want toouse for this mapping.</span></span>
 
     <span data-ttu-id="65226-167">Firma Microsoft zaleca używanie hello **"NameIdentifier"** atrybut jako identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65226-167">Microsoft recommends using hello **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="65226-168">Można zarządzać hello wartości tych atrybutów z hello **"Atrybuty użytkownika"** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65226-168">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="65226-169">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="65226-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="65226-170">W tym miejscu zostały zamapowane hello **identyfikator użytkownika (nameid)** z **ExtractMailPrefix()** funkcji **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="65226-170">Here we have mapped hello **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="65226-171">Dzięki temu wartość prefiksu hello adres e-mail użytkownika hello, co jest hello Unikatowy identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65226-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="65226-172">Każdy odpowiedź oznaczająca Powodzenie to wysyłane toohello Kronos aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65226-172">This is sent toohello Kronos application in every successful response.</span></span> 
     
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="65226-174">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="65226-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="65226-175">a.</span><span class="sxs-lookup"><span data-stu-id="65226-175">a.</span></span> <span data-ttu-id="65226-176">Z listy rozwijanej hello identyfikator użytkownika wybierz **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="65226-176">In hello User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="65226-177">b.</span><span class="sxs-lookup"><span data-stu-id="65226-177">b.</span></span> <span data-ttu-id="65226-178">W hello **poczty** listy rozwijanej wybierz **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="65226-178">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="65226-179">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="65226-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="65226-181">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="65226-181">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="65226-183">tooconfigure rejestracji jednokrotnej w **Kronos** strony, należy pobrać hello toosend **XML metadanych** za[Kronos obsługuje zespołu](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="65226-183">tooconfigure single sign-on on **Kronos** side, you need toosend hello downloaded **Metadata XML** too[Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="65226-184">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="65226-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="65226-185">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="65226-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65226-186">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65226-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65226-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="65226-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="65226-188">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="65226-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="65226-190">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="65226-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="65226-191">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="65226-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65226-193">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="65226-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65226-195">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="65226-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65226-197">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="65226-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65226-199">a.</span><span class="sxs-lookup"><span data-stu-id="65226-199">a.</span></span> <span data-ttu-id="65226-200">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65226-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65226-201">b.</span><span class="sxs-lookup"><span data-stu-id="65226-201">b.</span></span> <span data-ttu-id="65226-202">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65226-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65226-203">c.</span><span class="sxs-lookup"><span data-stu-id="65226-203">c.</span></span> <span data-ttu-id="65226-204">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="65226-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="65226-205">d.</span><span class="sxs-lookup"><span data-stu-id="65226-205">d.</span></span> <span data-ttu-id="65226-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="65226-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="65226-207">Tworzenie użytkownika testowego Kronos</span><span class="sxs-lookup"><span data-stu-id="65226-207">Creating a Kronos test user</span></span>

<span data-ttu-id="65226-208">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Kronos.</span><span class="sxs-lookup"><span data-stu-id="65226-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="65226-209">Aplikacja Kronos musi wszystkich toobe użytkowników hello udostępniane w aplikacji hello przed wykonaniem logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="65226-209">Kronos application needs all hello users toobe provisioned in hello application before doing SSO.</span></span> 

<span data-ttu-id="65226-210">Praca z hello [Kronos obsługuje zespołu](https://www.kronos.in/contact/en-in/form) tooprovision tych użytkowników do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="65226-210">Work with hello [Kronos support team](https://www.kronos.in/contact/en-in/form) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="65226-211">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="65226-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="65226-212">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooKronos.</span><span class="sxs-lookup"><span data-stu-id="65226-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKronos.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="65226-214">**tooassign tooKronos Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="65226-214">**tooassign Britta Simon tooKronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="65226-215">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="65226-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="65226-217">Z listy aplikacji hello wybierz **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="65226-217">In hello applications list, select **Kronos**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="65226-219">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="65226-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="65226-221">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="65226-221">Click **Add** button.</span></span> <span data-ttu-id="65226-222">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="65226-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="65226-224">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="65226-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="65226-225">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="65226-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65226-226">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="65226-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65226-227">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="65226-227">Testing single sign-on</span></span>

<span data-ttu-id="65226-228">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="65226-228">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="65226-229">Po kliknięciu powitalne Kronos kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Kronos aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65226-229">When you click hello Kronos tile in hello Access Panel, you should get automatically signed-on tooyour Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65226-230">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="65226-230">Additional resources</span></span>

* [<span data-ttu-id="65226-231">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65226-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65226-232">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65226-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

