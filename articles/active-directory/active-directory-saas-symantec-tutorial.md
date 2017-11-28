---
title: "Samouczek: Integracji Azure Active Directory z usługi zabezpieczeń firmy Symantec w sieci Web (WSS) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usług zabezpieczeń firmy Symantec w sieci Web (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="45149-103">Samouczek: Integracji Azure Active Directory z usługi zabezpieczeń firmy Symantec w sieci Web (WSS)</span><span class="sxs-lookup"><span data-stu-id="45149-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="45149-104">Z tego samouczka, dowiesz się, jak toointegrate Twojej firmy Symantec w sieci Web zabezpieczeń usługi (WSS) konta przy użyciu konta usługi Azure Active Directory (Azure AD), aby WSS można uwierzytelnić użytkownika końcowego udostępniane w hello Azure AD przy użyciu uwierzytelniania SAML i wymuszać użytkownika lub reguły poziomu zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="45149-104">In this tutorial, you will learn how toointegrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in hello Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="45149-105">Integrowanie usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="45149-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="45149-106">Zarządzaj wszystkimi hello użytkowników końcowych i grupy używane przez Twoje konto programu WSS w portalu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45149-106">Manage all of hello end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="45149-107">Pozwolić tooauthenticate użytkownicy końcowi hello programu WSS przy użyciu swoich poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45149-107">Allow hello end users tooauthenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="45149-108">Włącz wymuszania hello użytkownika i grupy poziomu reguł zdefiniowanych w ramach konta programu WSS.</span><span class="sxs-lookup"><span data-stu-id="45149-108">Enable hello enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="45149-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="45149-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45149-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="45149-110">Prerequisites</span></span>

<span data-ttu-id="45149-111">tooconfigure integracji z usługą Azure AD z usługi zabezpieczeń firmy Symantec w sieci Web (WSS), należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="45149-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="45149-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="45149-112">An Azure AD subscription</span></span>
- <span data-ttu-id="45149-113">Konto usługi zabezpieczeń firmy Symantec w sieci Web (WSS)</span><span class="sxs-lookup"><span data-stu-id="45149-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="45149-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu konta programu WSS, który jest obecnie używana w celu produkcji.</span><span class="sxs-lookup"><span data-stu-id="45149-114">tootest hello steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="45149-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="45149-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="45149-116">Nie należy używać konta programu WSS, który jest obecnie używana w celu produkcji dla tego testu, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="45149-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="45149-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45149-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="45149-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="45149-118">Scenario description</span></span>
<span data-ttu-id="45149-119">W tym samouczku skonfigurujesz programu Azure AD tooenable pojedynczego logowania jednokrotnego tooWSS przy użyciu poświadczeń użytkownika końcowego hello zdefiniowane w ramach konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45149-119">In this tutorial, you will configure your Azure AD tooenable single sign-on tooWSS using hello end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="45149-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="45149-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="45149-121">Dodawanie aplikacji usługi zabezpieczeń firmy Symantec w sieci Web (WSS) hello z galerii hello</span><span class="sxs-lookup"><span data-stu-id="45149-121">Adding hello Symantec Web Security Service (WSS) app from hello gallery</span></span>
2. <span data-ttu-id="45149-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="45149-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="45149-123">Dodawanie usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z galerii hello</span><span class="sxs-lookup"><span data-stu-id="45149-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="45149-124">tooconfigure hello integracji usługi zabezpieczeń firmy Symantec w sieci Web (WSS) do usługi Azure AD, należy tooadd usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="45149-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="45149-125">**tooadd firmy Symantec w sieci Web zabezpieczeń usługi (WSS) z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="45149-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="45149-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="45149-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="45149-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="45149-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="45149-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="45149-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="45149-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="45149-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="45149-133">W polu wyszukiwania hello wpisz **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)**, wybierz pozycję **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)** z panelu wyników następnie kliknij przycisk **Dodaj** hello tooadd przycisku aplikacja.</span><span class="sxs-lookup"><span data-stu-id="45149-133">In hello search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Symantec Web zabezpieczeń usługi (WSS) na liście wyników hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="45149-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="45149-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="45149-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z firmy Symantec w sieci Web zabezpieczeń usługi (WSS) w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="45149-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="45149-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w sieci Web usług zabezpieczeń (WSS) firmy Symantec jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45149-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="45149-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w sieci Web usług zabezpieczeń (WSS) firmy Symantec musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="45149-138">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="45149-139">W firmy Symantec w sieci Web zabezpieczeń usługi (WSS), przypisz wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="45149-139">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="45149-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi zabezpieczeń firmy Symantec w sieci Web (WSS), należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="45149-140">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="45149-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="45149-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="45149-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="45149-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="45149-143">**[Tworzenie użytkownika testowego usługi zabezpieczeń firmy Symantec w sieci Web (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave odpowiednikiem Simona Britta w firmy Symantec sieci Web zabezpieczeń usługi (WSS), który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="45149-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="45149-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="45149-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="45149-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="45149-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="45149-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="45149-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="45149-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji usługi zabezpieczeń firmy Symantec w sieci Web (WSS).</span><span class="sxs-lookup"><span data-stu-id="45149-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="45149-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z firmy Symantec w sieci Web zabezpieczeń usługi (WSS), wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="45149-148">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="45149-149">W portalu Azure na powitania hello **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="45149-149">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="45149-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="45149-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="45149-153">Na powitania **domeny usługi (WSS) zabezpieczeń firmy Symantec w sieci Web i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="45149-153">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Domena usługi zabezpieczeń firmy Symantec w sieci Web (WSS) i adresy URL pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="45149-155">a.</span><span class="sxs-lookup"><span data-stu-id="45149-155">a.</span></span> <span data-ttu-id="45149-156">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="45149-156">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="45149-157">b.</span><span class="sxs-lookup"><span data-stu-id="45149-157">b.</span></span> <span data-ttu-id="45149-158">W hello **adres URL odpowiedzi** pole tekstowe, wprowadź adres URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="45149-158">In hello **Reply URL** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="45149-159">Skontaktuj się z hello [zespołem pomocy technicznej klienta usługi zabezpieczeń firmy Symantec w sieci Web (WSS)](https://www.symantec.com/contact-us) Jeśli hello wartości hello **identyfikator** i **adres URL odpowiedzi** jakiegoś powodu nie działają.</span><span class="sxs-lookup"><span data-stu-id="45149-159">Please contact hello [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if hello values for hello **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="45149-160">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="45149-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="45149-162">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="45149-162">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="45149-164">tooconfigure rejestracji jednokrotnej na powitania po stronie usługi zabezpieczeń firmy Symantec w sieci Web (WSS), zapoznaj się z dokumentacją online programu WSS toohello.</span><span class="sxs-lookup"><span data-stu-id="45149-164">tooconfigure single sign-on on hello Symantec Web Security Service (WSS) side, refer toohello WSS online documentation.</span></span> <span data-ttu-id="45149-165">Witaj pobrane **XML metadanych** pliku będzie konieczne toobe importowane do portalu programu WSS hello.</span><span class="sxs-lookup"><span data-stu-id="45149-165">hello downloaded **Metadata XML** file will need toobe imported into hello WSS portal.</span></span> <span data-ttu-id="45149-166">Skontaktuj się z pomocą hello [usługi zabezpieczeń firmy Symantec w sieci Web (WSS) obsługuje zespołu](https://www.symantec.com/contact-us) Jeśli potrzebujesz pomocy przy konfiguracji hello w portalu programu WSS hello.</span><span class="sxs-lookup"><span data-stu-id="45149-166">Contact hello [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with hello configuration on hello WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="45149-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="45149-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="45149-168">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="45149-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="45149-169">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="45149-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="45149-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="45149-170">Create an Azure AD test user</span></span>

<span data-ttu-id="45149-171">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="45149-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="45149-173">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="45149-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="45149-174">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="45149-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="45149-176">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="45149-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="45149-178">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="45149-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="45149-180">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="45149-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="45149-182">a.</span><span class="sxs-lookup"><span data-stu-id="45149-182">a.</span></span> <span data-ttu-id="45149-183">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="45149-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="45149-184">b.</span><span class="sxs-lookup"><span data-stu-id="45149-184">b.</span></span> <span data-ttu-id="45149-185">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="45149-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="45149-186">c.</span><span class="sxs-lookup"><span data-stu-id="45149-186">c.</span></span> <span data-ttu-id="45149-187">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="45149-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="45149-188">d.</span><span class="sxs-lookup"><span data-stu-id="45149-188">d.</span></span> <span data-ttu-id="45149-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="45149-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="45149-190">Tworzenie użytkownika testowego usługi zabezpieczeń firmy Symantec w sieci Web (WSS)</span><span class="sxs-lookup"><span data-stu-id="45149-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="45149-191">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w sieci Web usług zabezpieczeń (WSS) firmy Symantec.</span><span class="sxs-lookup"><span data-stu-id="45149-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="45149-192">Nazwa użytkownika końcowego odpowiedniego Hello można ręcznie utworzyć w portalu programu WSS hello lub poczekać hello użytkowników/grupy udostępniane w hello Azure AD synchronizowane toobe toohello WSS portalu po kilku minutach (~ 15 minut).</span><span class="sxs-lookup"><span data-stu-id="45149-192">hello corresponding end username can be manually created in hello WSS portal or you can wait for hello users/groups provisioned in hello Azure AD toobe synchronized toohello WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="45149-193">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="45149-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="45149-194">publiczny adres IP Hello hello maszyny użytkownika końcowego, który będzie używany toobrowse witryn sieci Web może też być konieczne toobe udostępniane w portalu usługi zabezpieczeń firmy Symantec w sieci Web (WSS) hello.</span><span class="sxs-lookup"><span data-stu-id="45149-194">hello public IP address of hello end user machine, which will be used toobrowse websites also need toobe provisioned in hello Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="45149-195">Sprawdź [kliknij tutaj](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget komputera na publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="45149-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="45149-196">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="45149-196">Assign hello Azure AD test user</span></span>

<span data-ttu-id="45149-197">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSymantec usługi zabezpieczeń sieci Web (WSS).</span><span class="sxs-lookup"><span data-stu-id="45149-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="45149-199">**tooassign tooSymantec Simona Britta usługi zabezpieczeń sieci Web (WSS) wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="45149-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="45149-200">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="45149-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="45149-202">Z listy aplikacji hello wybierz **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="45149-202">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![łącze usługi zabezpieczeń firmy Symantec w sieci Web (WSS) Hello na liście aplikacji hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="45149-204">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="45149-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="45149-206">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="45149-206">Click **Add** button.</span></span> <span data-ttu-id="45149-207">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="45149-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="45149-209">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="45149-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="45149-210">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="45149-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="45149-211">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="45149-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="45149-212">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="45149-212">Test single sign-on</span></span>

<span data-ttu-id="45149-213">W tej sekcji przetestujesz hello pojedynczego logowania jednokrotnego funkcji teraz, gdy skonfigurowano programu WSS toouse konta usługi Azure AD do uwierzytelniania SAML.</span><span class="sxs-lookup"><span data-stu-id="45149-213">In this section, you'll test hello single sign-on functionality now that you've configured your WSS account toouse your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="45149-214">Po skonfigurowaniu sieci web przeglądarce tooproxy ruchu tooWSS, po otwarciu przeglądarki sieci web i spróbuj toobrowse tooa lokacji, a następnie będzie strony przekierowanego toohello Azure logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="45149-214">After you have configured your web browser tooproxy traffic tooWSS, when you open your web browser and try toobrowse tooa site then you'll be redirected toohello Azure sign-on page.</span></span> <span data-ttu-id="45149-215">Wprowadź poświadczenia hello hello testu użytkownika, że obsługa została zainicjowana w hello Azure AD (czyli BrittaSimon) oraz skojarzone hasło.</span><span class="sxs-lookup"><span data-stu-id="45149-215">Enter hello credentials of hello test end user that has been provisioned in hello Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="45149-216">Po uwierzytelnieniu, będziesz w stanie toobrowse toohello witryny sieci Web, które wybrano.</span><span class="sxs-lookup"><span data-stu-id="45149-216">Once authenticated, you'll be able toobrowse toohello website that you chose.</span></span> <span data-ttu-id="45149-217">Należy można utworzyć reguły na powitania WSS po stronie tooblock BrittaSimon z przeglądania tooa określonej lokacji, a następnie powinna zostać wyświetlona strona bloku WSS hello przy próbie toobrowse toothat lokacji jako użytkownik BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="45149-217">Should you create a policy rule on hello WSS side tooblock BrittaSimon from browsing tooa particular site then you should see hello WSS block page when you attempt toobrowse toothat site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="45149-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="45149-218">Additional resources</span></span>

* [<span data-ttu-id="45149-219">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45149-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="45149-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="45149-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

