---
title: "Samouczek: Integracji Azure Active Directory z usługi zabezpieczeń firmy Symantec w sieci Web (WSS) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usług zabezpieczeń firmy Symantec w sieci Web (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: f4575e6f5eb63cd0e1d63edd35e30be3cacc3382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="c5d9c-103">Samouczek: Integracji Azure Active Directory z usługi zabezpieczeń firmy Symantec w sieci Web (WSS)</span><span class="sxs-lookup"><span data-stu-id="c5d9c-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="c5d9c-104">Z tego samouczka, dowiesz się, jak toointegrate firmy Symantec w sieci Web zabezpieczeń usługi (WSS) z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5d9c-104">In this tutorial, you learn how toointegrate Symantec Web Security Service (WSS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5d9c-105">Integrowanie usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c5d9c-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5d9c-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooSymantec usługi zabezpieczeń sieci Web (WSS)</span><span class="sxs-lookup"><span data-stu-id="c5d9c-106">You can control in Azure AD who has access tooSymantec Web Security Service (WSS)</span></span>
- <span data-ttu-id="c5d9c-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSymantec usługi zabezpieczeń sieci Web (WSS) (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5d9c-107">You can enable your users tooautomatically get signed-on tooSymantec Web Security Service (WSS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5d9c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c5d9c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5d9c-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5d9c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5d9c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c5d9c-110">Prerequisites</span></span>

<span data-ttu-id="c5d9c-111">tooconfigure integracji z usługą Azure AD z usługi zabezpieczeń firmy Symantec w sieci Web (WSS), należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c5d9c-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="c5d9c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5d9c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5d9c-113">Usługi zabezpieczeń firmy Symantec w sieci Web (WSS) logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c5d9c-113">A Symantec Web Security Service (WSS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5d9c-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5d9c-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c5d9c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5d9c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5d9c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5d9c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5d9c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c5d9c-118">Scenario description</span></span>
<span data-ttu-id="c5d9c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5d9c-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c5d9c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5d9c-121">Dodawanie usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c5d9c-121">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
2. <span data-ttu-id="c5d9c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c5d9c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="c5d9c-123">Dodawanie usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c5d9c-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="c5d9c-124">tooconfigure hello integracji usługi zabezpieczeń firmy Symantec w sieci Web (WSS) do usługi Azure AD, należy tooadd usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5d9c-125">**tooadd firmy Symantec w sieci Web zabezpieczeń usługi (WSS) z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c5d9c-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5d9c-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c5d9c-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5d9c-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c5d9c-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c5d9c-133">W polu wyszukiwania hello wpisz **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-133">In hello search box, type **Symantec Web Security Service (WSS)**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. <span data-ttu-id="c5d9c-135">W panelu wyników hello, wybierz **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-135">In hello results panel, select **Symantec Web Security Service (WSS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5d9c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c5d9c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5d9c-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z firmy Symantec w sieci Web zabezpieczeń usługi (WSS) w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-138">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5d9c-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w sieci Web usług zabezpieczeń (WSS) firmy Symantec jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="c5d9c-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w sieci Web usług zabezpieczeń (WSS) firmy Symantec musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-140">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="c5d9c-141">W firmy Symantec w sieci Web zabezpieczeń usługi (WSS), przypisz wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-141">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5d9c-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi zabezpieczeń firmy Symantec w sieci Web (WSS), należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c5d9c-142">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5d9c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5d9c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5d9c-145">**[Tworzenie użytkownika testowego usługi zabezpieczeń firmy Symantec w sieci Web (WSS)](#creating-a-symantec-web-security-service-wss-test-user)**  -toohave odpowiednikiem Simona Britta w firmy Symantec sieci Web zabezpieczeń usługi (WSS), który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-145">**[Creating a Symantec Web Security Service (WSS) test user](#creating-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5d9c-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5d9c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5d9c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c5d9c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5d9c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji usługi zabezpieczeń firmy Symantec w sieci Web (WSS).</span><span class="sxs-lookup"><span data-stu-id="c5d9c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="c5d9c-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z firmy Symantec w sieci Web zabezpieczeń usługi (WSS), wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c5d9c-150">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="c5d9c-151">W portalu Azure na powitania hello **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-151">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c5d9c-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="c5d9c-155">Na powitania **domeny usługi (WSS) zabezpieczeń firmy Symantec w sieci Web i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c5d9c-155">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="c5d9c-157">a.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-157">a.</span></span> <span data-ttu-id="c5d9c-158">W hello **adres URL logowania** pole tekstowe, adres url hello informację, który ma tooblock zgodnie z toohello zasady blokowania hello usługi zabezpieczeń firmy Symantec w sieci Web (WSS).</span><span class="sxs-lookup"><span data-stu-id="c5d9c-158">In hello **Sign-on URL** textbox, mention hello url, which you want tooblock according toohello blocking policy of hello Symantec Web Security Service (WSS).</span></span>  
    
    <span data-ttu-id="c5d9c-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-159">b.</span></span> <span data-ttu-id="c5d9c-160">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="c5d9c-160">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5d9c-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-161">These values are not real.</span></span> <span data-ttu-id="c5d9c-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c5d9c-163">Skontaktuj się z [zespołem pomocy technicznej klienta usługi zabezpieczeń firmy Symantec w sieci Web (WSS)](https://www.symantec.com/contact-us) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-163">Contact [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="c5d9c-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="c5d9c-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5d9c-168">tooconfigure rejestracji jednokrotnej w **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)** strony, należy pobrać hello toosend **XML metadanych** zbyt[zespołuobsługiusługizabezpieczeńfirmySymantecwsieciWeb(WSS)](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="c5d9c-168">tooconfigure single sign-on on **Symantec Web Security Service (WSS)** side, you need toosend hello downloaded **Metadata XML** too[Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="c5d9c-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="c5d9c-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5d9c-170">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5d9c-171">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5d9c-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5d9c-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5d9c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5d9c-173">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c5d9c-175">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c5d9c-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5d9c-176">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5d9c-178">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5d9c-180">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5d9c-182">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c5d9c-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5d9c-184">a.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-184">a.</span></span> <span data-ttu-id="c5d9c-185">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5d9c-186">b.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-186">b.</span></span> <span data-ttu-id="c5d9c-187">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5d9c-188">c.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-188">c.</span></span> <span data-ttu-id="c5d9c-189">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5d9c-190">d.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-190">d.</span></span> <span data-ttu-id="c5d9c-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-191">Click **Create**.</span></span>
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="c5d9c-192">Tworzenie użytkownika testowego usługi zabezpieczeń firmy Symantec w sieci Web (WSS)</span><span class="sxs-lookup"><span data-stu-id="c5d9c-192">Creating a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="c5d9c-193">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w sieci Web usług zabezpieczeń (WSS) firmy Symantec.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-193">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="c5d9c-194">Praca z [usługi zabezpieczeń firmy Symantec w sieci Web (WSS) obsługuje zespołu](https://www.symantec.com/contact-us) do dodawania użytkowników hello hello usługi zabezpieczeń firmy Symantec w sieci Web (WSS) platformy.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-194">Work with [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) to add hello users in hello Symantec Web Security Service (WSS) platform.</span></span> <span data-ttu-id="c5d9c-195">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-195">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="c5d9c-196">Również wraz z hello użytkownika szczegółowe informacje możesz muszą toosend hello publiczny adres IP maszyny hello, z którym próbujesz tooaccess hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-196">Also along with hello user details you need toosend hello public IPaddress of hello machine from which you are trying tooaccess hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="c5d9c-197">Sprawdź [kliknij tutaj](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget komputera na publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-197">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5d9c-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5d9c-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5d9c-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSymantec usługi zabezpieczeń sieci Web (WSS).</span><span class="sxs-lookup"><span data-stu-id="c5d9c-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c5d9c-201">**tooassign tooSymantec Simona Britta usługi zabezpieczeń sieci Web (WSS) wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c5d9c-201">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="c5d9c-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c5d9c-204">Z listy aplikacji hello wybierz **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-204">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. <span data-ttu-id="c5d9c-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c5d9c-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-208">Click **Add** button.</span></span> <span data-ttu-id="c5d9c-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c5d9c-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5d9c-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5d9c-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5d9c-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c5d9c-214">Testing single sign-on</span></span>

<span data-ttu-id="c5d9c-215">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5d9c-216">Po kliknięciu powitalne usługi zabezpieczeń firmy Symantec w sieci Web (WSS) kafelka w hello Panel dostępu, możesz uzyskać przekierowanego toohello strony, dla którego skonfigurowano hello blokuje zasad blokowania.</span><span class="sxs-lookup"><span data-stu-id="c5d9c-216">When you click hello Symantec Web Security Service (WSS) tile in hello Access Panel, you get redirected toohello blocking page for which hello blocking policy has been configured.</span></span>
<span data-ttu-id="c5d9c-217">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5d9c-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5d9c-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c5d9c-218">Additional resources</span></span>

* [<span data-ttu-id="c5d9c-219">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5d9c-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5d9c-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5d9c-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

