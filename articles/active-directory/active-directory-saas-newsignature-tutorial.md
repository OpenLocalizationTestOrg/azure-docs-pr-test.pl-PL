---
title: "Samouczek: Integracji Azure Active Directory za pomocą portalu zarządzania w chmurze Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i chmury portalu zarządzania Microsoft Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9596826e3dc1289b95009bf01ec8b86f823ef345
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="b2fff-103">Samouczek: Integracji Azure Active Directory za pomocą portalu zarządzania w chmurze Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b2fff-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="b2fff-104">Z tego samouczka, dowiesz się, jak toointegrate chmury portalu zarządzania Microsoft Azure w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b2fff-104">In this tutorial, you learn how toointegrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b2fff-105">Integrowanie portalu zarządzania w chmurze platformy Microsoft Azure z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b2fff-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b2fff-106">Można kontrolować w usłudze Azure AD mającego tooCloud dostęp do portalu zarządzania Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b2fff-106">You can control in Azure AD who has access tooCloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="b2fff-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCloud portalu zarządzania Microsoft Azure (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2fff-107">You can enable your users tooautomatically get signed-on tooCloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b2fff-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b2fff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b2fff-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b2fff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2fff-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b2fff-110">Prerequisites</span></span>

<span data-ttu-id="b2fff-111">tooconfigure integracji usługi Azure AD za pomocą portalu zarządzania w chmurze Microsoft Azure, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b2fff-111">tooconfigure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need hello following items:</span></span>

- <span data-ttu-id="b2fff-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2fff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b2fff-113">Portal zarządzania chmury dla Microsoft Azure jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b2fff-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b2fff-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b2fff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b2fff-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b2fff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b2fff-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b2fff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b2fff-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b2fff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b2fff-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b2fff-118">Scenario description</span></span>
<span data-ttu-id="b2fff-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b2fff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b2fff-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b2fff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b2fff-121">Dodawanie z galerii hello chmury portalu zarządzania Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b2fff-121">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
2. <span data-ttu-id="b2fff-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b2fff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-hello-gallery"></a><span data-ttu-id="b2fff-123">Dodawanie z galerii hello chmury portalu zarządzania Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b2fff-123">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
<span data-ttu-id="b2fff-124">tooconfigure hello integracji chmury portalu zarządzania Microsoft Azure w usłudze Azure Active Directory, należy tooadd chmury portalu zarządzania Microsoft Azure z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b2fff-124">tooconfigure hello integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need tooadd Cloud Management Portal for Microsoft Azure from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b2fff-125">**tooadd chmury portalu zarządzania Microsoft Azure z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b2fff-125">**tooadd Cloud Management Portal for Microsoft Azure from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2fff-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b2fff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b2fff-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b2fff-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b2fff-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b2fff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b2fff-133">W polu wyszukiwania hello wpisz **chmury portalu zarządzania Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-133">In hello search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="b2fff-135">W panelu wyników hello, wybierz **chmury portalu zarządzania Microsoft Azure**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b2fff-135">In hello results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b2fff-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b2fff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b2fff-138">W tej sekcji skonfigurować i przetestować usługi Azure AD logowania jednokrotnego za pomocą portalu zarządzania w chmurze platformy Microsoft Azure w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b2fff-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b2fff-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w chmurze Portal zarządzania platformy Microsoft Azure jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2fff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cloud Management Portal for Microsoft Azure is tooa user in Azure AD.</span></span> <span data-ttu-id="b2fff-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze Portal zarządzania platformy Microsoft Azure musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b2fff-140">In other words, a link relationship between an Azure AD user and hello related user in Cloud Management Portal for Microsoft Azure needs toobe established.</span></span>

<span data-ttu-id="b2fff-141">W chmurze Portal zarządzania platformy Microsoft Azure, przypisz wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="b2fff-141">In Cloud Management Portal for Microsoft Azure, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b2fff-142">tooconfigure i testowanie usługi Azure AD logowania jednokrotnego za pomocą portalu zarządzania w chmurze Microsoft Azure, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b2fff-142">tooconfigure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b2fff-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b2fff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b2fff-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b2fff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b2fff-145">**[Tworzenie chmury Portal zarządzania dla użytkownika testowego Microsoft Azure](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)**  -toohave odpowiednikiem Simona Britta w chmurze Portal zarządzania platformy Microsoft Azure, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b2fff-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - toohave a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b2fff-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b2fff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b2fff-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b2fff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b2fff-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b2fff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b2fff-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w portalu zarządzania usługi chmury dla aplikacji Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="b2fff-150">**tooconfigure usługi Azure AD logowania jednokrotnego za pomocą portalu zarządzania chmury Microsoft Azure, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b2fff-150">**tooconfigure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2fff-151">W portalu Azure na powitania hello **chmury portalu zarządzania Microsoft Azure** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-151">In hello Azure portal, on hello **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b2fff-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b2fff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="b2fff-155">Na powitania **chmury portalu zarządzania Microsoft Azure domeny i adresów URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b2fff-155">On hello **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="b2fff-157">a.</span><span class="sxs-lookup"><span data-stu-id="b2fff-157">a.</span></span> <span data-ttu-id="b2fff-158">W hello **adres URL logowania** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="b2fff-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="b2fff-159">b.</span><span class="sxs-lookup"><span data-stu-id="b2fff-159">b.</span></span> <span data-ttu-id="b2fff-160">W hello **identyfikator** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="b2fff-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="b2fff-161">c.</span><span class="sxs-lookup"><span data-stu-id="b2fff-161">c.</span></span> <span data-ttu-id="b2fff-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="b2fff-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="b2fff-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b2fff-163">These values are not real.</span></span> <span data-ttu-id="b2fff-164">Zaktualizować te wartości hello rzeczywisty adres URL logowania, identyfikator i odpowiedzi adres URL.</span><span class="sxs-lookup"><span data-stu-id="b2fff-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="b2fff-165">Skontaktuj się z [chmurze Portal zarządzania dla klienta platformy Microsoft Azure z pomocą techniczną](mailto:jczernuszka@newsignature.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="b2fff-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="b2fff-166">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b2fff-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="b2fff-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b2fff-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b2fff-170">Na powitania **chmurze Portal zarządzania dla programu Microsoft Azure Configuration** kliknij **skonfigurować Portal zarządzania chmury Microsoft Azure** tooopen **Konfigurowanie logowania jednokrotnego**okna.</span><span class="sxs-lookup"><span data-stu-id="b2fff-170">On hello **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b2fff-171">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b2fff-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="b2fff-173">tooconfigure rejestracji jednokrotnej w **chmury portalu zarządzania Microsoft Azure** strony, należy pobrać hello toosend **certyfikatu**, **Sign-Out URL**, **SAML pojedynczy znak na adres URL usługi** i **identyfikator jednostki SAML** za[chmurze Portal zarządzania dla zespołu pomocy technicznej Microsoft Azure](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="b2fff-173">tooconfigure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="b2fff-174">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="b2fff-174">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b2fff-175">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b2fff-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b2fff-176">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b2fff-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b2fff-177">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b2fff-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b2fff-178">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2fff-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="b2fff-179">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b2fff-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b2fff-181">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b2fff-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2fff-182">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b2fff-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b2fff-184">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b2fff-186">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b2fff-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b2fff-188">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b2fff-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b2fff-190">a.</span><span class="sxs-lookup"><span data-stu-id="b2fff-190">a.</span></span> <span data-ttu-id="b2fff-191">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b2fff-192">b.</span><span class="sxs-lookup"><span data-stu-id="b2fff-192">b.</span></span> <span data-ttu-id="b2fff-193">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b2fff-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b2fff-194">c.</span><span class="sxs-lookup"><span data-stu-id="b2fff-194">c.</span></span> <span data-ttu-id="b2fff-195">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b2fff-196">d.</span><span class="sxs-lookup"><span data-stu-id="b2fff-196">d.</span></span> <span data-ttu-id="b2fff-197">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="b2fff-198">Tworzenie chmury Portal zarządzania dla użytkownika testowego Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b2fff-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="b2fff-199">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w chmurze portalu zarządzania Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fff-199">hello objective of this section is toocreate a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="b2fff-200">We współpracy z [chmurze Portal zarządzania dla zespołu pomocy technicznej Microsoft Azure](mailto:jczernuszka@newsignature.com) tooadd hello użytkowników w hello chmurze Portal zarządzania dla konta Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fff-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) tooadd hello users in hello Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b2fff-201">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2fff-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b2fff-202">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCloud portalu zarządzania Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fff-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloud Management Portal for Microsoft Azure.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b2fff-204">**tooassign tooCloud Simona Britta portalu zarządzania Microsoft Azure, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b2fff-204">**tooassign Britta Simon tooCloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2fff-205">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b2fff-207">Z listy aplikacji hello wybierz **chmury portalu zarządzania Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-207">In hello applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="b2fff-209">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b2fff-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b2fff-211">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b2fff-211">Click **Add** button.</span></span> <span data-ttu-id="b2fff-212">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b2fff-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b2fff-214">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b2fff-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b2fff-215">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b2fff-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b2fff-216">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b2fff-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b2fff-217">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b2fff-217">Testing single sign-on</span></span>

<span data-ttu-id="b2fff-218">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b2fff-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="b2fff-219">Po kliknięciu hello chmury portalu zarządzania Microsoft Azure kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour chmurze Portal zarządzania dla aplikacji Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fff-219">When you click hello Cloud Management Portal for Microsoft Azure tile in hello Access Panel, you should get automatically signed-on tooyour Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="b2fff-220">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b2fff-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b2fff-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b2fff-221">Additional resources</span></span>

* [<span data-ttu-id="b2fff-222">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2fff-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b2fff-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b2fff-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

