---
title: "Samouczek: Integracji Azure Active Directory z detalicznej Infor — Zarządzanie informacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i detaliczne Infor — informacji zarządzania."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 9cd8ab65d41d01832e0611f7f8254aa257120508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="b4050-103">Samouczek: Integracji Azure Active Directory z detalicznej Infor — Zarządzanie informacji</span><span class="sxs-lookup"><span data-stu-id="b4050-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="b4050-104">Z tego samouczka, dowiesz się, jak toointegrate detalicznej Infor — Zarządzanie informacji w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b4050-104">In this tutorial, you learn how toointegrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b4050-105">Integrowanie detalicznej Infor — Zarządzanie informacji z usługi Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b4050-105">Integrating Infor Retail – Information Management with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b4050-106">Można kontrolować w usłudze Azure AD mającego tooInfor dostępu detalicznej — informacji zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b4050-106">You can control in Azure AD who has access tooInfor Retail – Information Management.</span></span>
- <span data-ttu-id="b4050-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooInfor detalicznej — informacji zarządzania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4050-107">You can enable your users tooautomatically get signed-on tooInfor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b4050-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b4050-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b4050-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b4050-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4050-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b4050-110">Prerequisites</span></span>

<span data-ttu-id="b4050-111">tooconfigure integracji usługi Azure AD z detalicznej Infor — Zarządzanie informacji należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b4050-111">tooconfigure Azure AD integration with Infor Retail – Information Management, you need hello following items:</span></span>

- <span data-ttu-id="b4050-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4050-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b4050-113">Detaliczne Infor — jednokrotnego informacji zarządzania dla subskrypcji włączone</span><span class="sxs-lookup"><span data-stu-id="b4050-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b4050-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b4050-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b4050-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b4050-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b4050-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b4050-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b4050-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4050-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b4050-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b4050-118">Scenario description</span></span>
<span data-ttu-id="b4050-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b4050-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b4050-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b4050-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b4050-121">Dodawanie detalicznej Infor — Zarządzanie informacji z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b4050-121">Adding Infor Retail – Information Management from hello gallery</span></span>
2. <span data-ttu-id="b4050-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b4050-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infor-retail--information-management-from-hello-gallery"></a><span data-ttu-id="b4050-123">Dodawanie detalicznej Infor — Zarządzanie informacji z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b4050-123">Adding Infor Retail – Information Management from hello gallery</span></span>
<span data-ttu-id="b4050-124">Integracja hello tooconfigure detalicznej Infor — Zarządzanie informacji do usługi Azure AD, należy tooadd detalicznej Infor — Zarządzanie informacji z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b4050-124">tooconfigure hello integration of Infor Retail – Information Management into Azure AD, you need tooadd Infor Retail – Information Management from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b4050-125">**tooadd detalicznej Infor — Zarządzanie informacji z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b4050-125">**tooadd Infor Retail – Information Management from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4050-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b4050-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="b4050-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b4050-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b4050-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b4050-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="b4050-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b4050-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="b4050-133">W hello wyszukiwania wpisz **detalicznej Infor — Zarządzanie informacji**, wybierz pozycję **detalicznej Infor — Zarządzanie informacji** z panelu wyników następnie kliknij przycisk **Dodaj** hello tooadd przycisku aplikacja.</span><span class="sxs-lookup"><span data-stu-id="b4050-133">In hello search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Infor detalicznej — Zarządzanie informacji hello listy wyników](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b4050-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b4050-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b4050-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z detalicznej Infor — Zarządzanie informacji w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b4050-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b4050-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello w sprzedaży detalicznej Infor — Zarządzanie informacji jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4050-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Infor Retail – Information Management is tooa user in Azure AD.</span></span> <span data-ttu-id="b4050-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w sprzedaży detalicznej Infor — Zarządzanie informacji musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b4050-138">In other words, a link relationship between an Azure AD user and hello related user in Infor Retail – Information Management needs toobe established.</span></span>

<span data-ttu-id="b4050-139">W sprzedaży detalicznej Infor — Zarządzanie informacji, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="b4050-139">In Infor Retail – Information Management, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b4050-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z detalicznej Infor — Zarządzanie informacji należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="b4050-140">tooconfigure and test Azure AD single sign-on with Infor Retail – Information Management, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b4050-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b4050-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b4050-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b4050-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b4050-143">**[Utwórz detalicznej Infor — Zarządzanie informacji użytkownika testowego](#create-an-infor-retail--information-management-test-user)**  - toohave odpowiednikiem Simona Britta w sprzedaży detalicznej Infor — informacji zarządzania toohello połączonej usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b4050-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - toohave a counterpart of Britta Simon in Infor Retail – Information Management that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b4050-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b4050-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b4050-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b4050-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b4050-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b4050-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b4050-147">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci sprzedaży detalicznej Infor — aplikacji informacji zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b4050-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="b4050-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z detalicznej Infor — Zarządzanie informacji, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b4050-148">**tooconfigure Azure AD single sign-on with Infor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4050-149">W portalu Azure na powitania hello **detalicznej Infor — Zarządzanie informacji** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b4050-149">In hello Azure portal, on hello **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="b4050-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b4050-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_samlbase.png)

3. <span data-ttu-id="b4050-153">Na powitania **Infor detalicznej — informacje o domenie zarządzania i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz tooconfigure aplikacji hello w rozszerzeniu IDP zainicjował tryb hello:</span><span class="sxs-lookup"><span data-stu-id="b4050-153">On hello **Infor Retail – Information Management Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Informacje logowania jednokrotnego IDP pojedynczy infor detalicznej — informacje o domenie zarządzania i adres URL](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url.png)

    <span data-ttu-id="b4050-155">a.</span><span class="sxs-lookup"><span data-stu-id="b4050-155">a.</span></span> <span data-ttu-id="b4050-156">W hello **identyfikator** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="b4050-156">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    |   |
    | -- |
    | `https://<company name>.mingle.infor.com` |
    | `http://<company name>.mingledev.infor.com` |

    <span data-ttu-id="b4050-157">b.</span><span class="sxs-lookup"><span data-stu-id="b4050-157">b.</span></span> <span data-ttu-id="b4050-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="b4050-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>

4. <span data-ttu-id="b4050-159">Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="b4050-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Infor detalicznej — informacje o domenie zarządzania i adresy URL pojedynczego logowania jednokrotnego informacji SP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url1.png)

    <span data-ttu-id="b4050-161">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="b4050-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b4050-162">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b4050-162">These values are not real.</span></span> <span data-ttu-id="b4050-163">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="b4050-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b4050-164">Skontaktuj się z [detalicznej Infor — informacje o kliencie zarządzania zespołem pomocy technicznej](mailto:innovate@infor.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="b4050-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) tooget these values.</span></span> 

5. <span data-ttu-id="b4050-165">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b4050-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_certificate.png) 

6. <span data-ttu-id="b4050-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b4050-167">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="b4050-169">tooconfigure rejestracji jednokrotnej w **detalicznej Infor — Zarządzanie informacji** strony, należy pobrać hello toosend **XML metadanych** zbyt[detalicznej Infor — informacji zarządzania zespołem pomocy technicznej ](mailto:innovate@infor.com).</span><span class="sxs-lookup"><span data-stu-id="b4050-169">tooconfigure single sign-on on **Infor Retail – Information Management** side, you need toosend hello downloaded **Metadata XML** too[Infor Retail – Information Management support team](mailto:innovate@infor.com).</span></span> <span data-ttu-id="b4050-170">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="b4050-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b4050-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b4050-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b4050-172">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b4050-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b4050-173">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b4050-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b4050-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4050-174">Create an Azure AD test user</span></span>

<span data-ttu-id="b4050-175">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b4050-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="b4050-177">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b4050-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4050-178">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b4050-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b4050-180">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b4050-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b4050-182">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="b4050-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b4050-184">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b4050-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b4050-186">a.</span><span class="sxs-lookup"><span data-stu-id="b4050-186">a.</span></span> <span data-ttu-id="b4050-187">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b4050-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b4050-188">b.</span><span class="sxs-lookup"><span data-stu-id="b4050-188">b.</span></span> <span data-ttu-id="b4050-189">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b4050-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b4050-190">c.</span><span class="sxs-lookup"><span data-stu-id="b4050-190">c.</span></span> <span data-ttu-id="b4050-191">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="b4050-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b4050-192">d.</span><span class="sxs-lookup"><span data-stu-id="b4050-192">d.</span></span> <span data-ttu-id="b4050-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b4050-193">Click **Create**.</span></span>
 
### <a name="create-an-infor-retail--information-management-test-user"></a><span data-ttu-id="b4050-194">Utwórz detalicznej Infor — Zarządzanie informacji użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="b4050-194">Create an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="b4050-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w sprzedaży detalicznej Infor — Zarządzanie informacji.</span><span class="sxs-lookup"><span data-stu-id="b4050-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="b4050-196">We współpracy z [detalicznej Infor — zespołem pomocy technicznej informacji zarządzania](mailto:innovate@infor.com) tooadd hello użytkowników w hello detalicznej Infor — platformy zarządzania informacji.</span><span class="sxs-lookup"><span data-stu-id="b4050-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) tooadd hello users in hello Infor Retail – Information Management platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b4050-197">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4050-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b4050-198">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooInfor detalicznej — informacji zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b4050-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInfor Retail – Information Management.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="b4050-200">**tooassign Simona Britta tooInfor detalicznej — Zarządzanie informacji, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b4050-200">**tooassign Britta Simon tooInfor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4050-201">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b4050-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b4050-203">Z listy aplikacji hello wybierz **detalicznej Infor — Zarządzanie informacji**.</span><span class="sxs-lookup"><span data-stu-id="b4050-203">In hello applications list, select **Infor Retail – Information Management**.</span></span>

    ![Witaj Infor detalicznej — Zarządzanie informacji łącze w listę aplikacji hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_app.png)  

3. <span data-ttu-id="b4050-205">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b4050-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="b4050-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b4050-207">Click **Add** button.</span></span> <span data-ttu-id="b4050-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b4050-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="b4050-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b4050-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b4050-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b4050-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b4050-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b4050-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b4050-213">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b4050-213">Test single sign-on</span></span>

<span data-ttu-id="b4050-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b4050-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b4050-215">Po kliknięciu hello detalicznej Infor — Zarządzanie informacji kafelka w hello panelu dostępu należy pobrać automatycznie zalogowane tooyour detalicznej Infor — Zarządzanie informacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4050-215">When you click hello Infor Retail – Information Management tile in hello Access Panel, you should get automatically signed-on tooyour Infor Retail – Information Management application.</span></span>
<span data-ttu-id="b4050-216">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b4050-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b4050-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b4050-217">Additional resources</span></span>

* [<span data-ttu-id="b4050-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4050-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b4050-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b4050-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_203.png

