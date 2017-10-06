---
title: 'Samouczek: Integracji Azure Active Directory z SensoScientific bezprzewodowej temperatury monitorowania systemu | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między SensoScientific bezprzewodowej temperatury monitorowania systemu i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="9fe38-103">Samouczek: Integracji Azure Active Directory z SensoScientific bezprzewodowej temperatury monitorowania systemu</span><span class="sxs-lookup"><span data-stu-id="9fe38-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="9fe38-104">Z tego samouczka, dowiesz się, jak toointegrate SensoScientific bezprzewodowej temperatury monitorowania systemu z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9fe38-104">In this tutorial, you learn how toointegrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9fe38-105">Integracja z usługą Azure AD SensoScientific bezprzewodowej temperatury monitorowania systemu zawiera hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9fe38-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9fe38-106">Można kontrolować w usłudze Azure AD mającego tooSensoScientific dostępu bezprzewodowego temperatury monitorowania systemu</span><span class="sxs-lookup"><span data-stu-id="9fe38-106">You can control in Azure AD who has access tooSensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="9fe38-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSensoScientific bezprzewodowej temperatury monitorowania systemu (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe38-107">You can enable your users tooautomatically get signed-on tooSensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9fe38-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9fe38-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9fe38-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9fe38-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fe38-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9fe38-110">Prerequisites</span></span>

<span data-ttu-id="9fe38-111">tooconfigure integracji usługi Azure AD z SensoScientific bezprzewodowej temperatury monitorowania systemu, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9fe38-111">tooconfigure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need hello following items:</span></span>

- <span data-ttu-id="9fe38-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe38-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9fe38-113">SensoScientific bezprzewodowej temperatury monitorowania systemu jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9fe38-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9fe38-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9fe38-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9fe38-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9fe38-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9fe38-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9fe38-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9fe38-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9fe38-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9fe38-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9fe38-118">Scenario description</span></span>
<span data-ttu-id="9fe38-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9fe38-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9fe38-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9fe38-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9fe38-121">Dodawanie SensoScientific bezprzewodowej temperatury monitorowania systemu z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9fe38-121">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
2. <span data-ttu-id="9fe38-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9fe38-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a><span data-ttu-id="9fe38-123">Dodawanie SensoScientific bezprzewodowej temperatury monitorowania systemu z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9fe38-123">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
<span data-ttu-id="9fe38-124">tooconfigure hello integracji SensoScientific bezprzewodowej temperatury monitorowania systemu do usługi Azure AD, należy tooadd SensoScientific bezprzewodowej temperatury monitorowania systemu z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9fe38-124">tooconfigure hello integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9fe38-125">**tooadd SensoScientific bezprzewodowej temperatury monitorowania systemu z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9fe38-125">**tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fe38-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9fe38-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9fe38-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9fe38-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9fe38-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9fe38-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9fe38-133">W polu wyszukiwania hello wpisz **SensoScientific bezprzewodowej temperatury monitorowania systemu**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-133">In hello search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="9fe38-135">W panelu wyników hello, wybierz **SensoScientific bezprzewodowej temperatury monitorowania systemu**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9fe38-135">In hello results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9fe38-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9fe38-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9fe38-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej SensoScientific bezprzewodowej temperatury monitorowania systemu, na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="9fe38-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9fe38-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello SensoScientific bezprzewodowej temperatury monitorowania systemu jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fe38-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SensoScientific Wireless Temperature Monitoring System is tooa user in Azure AD.</span></span> <span data-ttu-id="9fe38-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi SensoScientific bezprzewodowej temperatury monitorowania systemu musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="9fe38-140">In other words, a link relationship between an Azure AD user and hello related user in SensoScientific Wireless Temperature Monitoring System needs toobe established.</span></span>

<span data-ttu-id="9fe38-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="9fe38-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="9fe38-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SensoScientific bezprzewodowej temperatury monitorowania systemu, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9fe38-142">tooconfigure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9fe38-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9fe38-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9fe38-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9fe38-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9fe38-145">**[Tworzenie użytkownika testowego SensoScientific bezprzewodowej temperatury monitorowania systemu](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave odpowiednikiem Simona Britta w SensoScientific bezprzewodowej temperatury monitorowania systemu, który jest połączony reprezentacja toohello usługi Azure AD użytkownik.</span><span class="sxs-lookup"><span data-stu-id="9fe38-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - toohave a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9fe38-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9fe38-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9fe38-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="9fe38-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9fe38-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9fe38-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9fe38-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="9fe38-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="9fe38-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z SensoScientific bezprzewodowej temperatury monitorowania systemu, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9fe38-150">**tooconfigure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fe38-151">W portalu Azure na powitania hello **SensoScientific bezprzewodowej temperatury monitorowania systemu** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-151">In hello Azure portal, on hello **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9fe38-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9fe38-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="9fe38-155">Na powitania **adresy URL i monitorowania domeny systemu SensoScientific bezprzewodowej temperatury** sekcji nie tooperform potrzeba żadnych czynności jako aplikacji hello już jest wstępna Integracja z usługą Azure:</span><span class="sxs-lookup"><span data-stu-id="9fe38-155">On hello **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need tooperform any steps as hello app is already pre-integrated with Azure:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="9fe38-157">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9fe38-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="9fe38-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9fe38-159">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9fe38-161">Na powitania **monitorowania konfiguracji systemu SensoScientific bezprzewodowej temperatury** kliknij **Konfiguruj SensoScientific bezprzewodowej temperatury monitorowania System** tooopen  **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9fe38-161">On hello **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9fe38-162">Witaj kopii **Sign-Out adres URL, identyfikator jednostki SAML** i **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9fe38-162">Copy hello **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="9fe38-164">Zaloguj się na tooyour SensoScientific bezprzewodowej temperatury monitorowania systemu aplikacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9fe38-164">Sign on tooyour SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="9fe38-165">W menu nawigacji hello na górze powitania kliknij **konfiguracji** i przejdź do **Konfiguruj** w obszarze **rejestracji jednokrotnej** tooopen hello pojedynczy znak na ustawienia.</span><span class="sxs-lookup"><span data-stu-id="9fe38-165">In hello navigation menu on hello top, click **Configuration** and goto **Configure** under **Single Sign On** tooopen hello Single Sign On Settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="9fe38-167">W **pojedynczy znak na ustawienia** formularza wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9fe38-167">In **Single Sign On Settings** form perform hello following steps:</span></span>
 
    <span data-ttu-id="9fe38-168">a.</span><span class="sxs-lookup"><span data-stu-id="9fe38-168">a.</span></span> <span data-ttu-id="9fe38-169">Wybierz **Nazwa wystawcy** jako usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fe38-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="9fe38-170">b.</span><span class="sxs-lookup"><span data-stu-id="9fe38-170">b.</span></span> <span data-ttu-id="9fe38-171">Wklej hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure w tekstowym adres URL wystawcy.</span><span class="sxs-lookup"><span data-stu-id="9fe38-171">Paste hello **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="9fe38-172">c.</span><span class="sxs-lookup"><span data-stu-id="9fe38-172">c.</span></span> <span data-ttu-id="9fe38-173">Wklej hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure w pole tekstowe pojedynczy znak na adres URL usługi.</span><span class="sxs-lookup"><span data-stu-id="9fe38-173">Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="9fe38-174">d.</span><span class="sxs-lookup"><span data-stu-id="9fe38-174">d.</span></span> <span data-ttu-id="9fe38-175">Wklej hello **Sign-Out URL** którego została skopiowana z portalu Azure do pojedynczego adresu URL usługi Sign-Out pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9fe38-175">Paste hello **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="9fe38-176">e.</span><span class="sxs-lookup"><span data-stu-id="9fe38-176">e.</span></span> <span data-ttu-id="9fe38-177">Przeglądaj hello certyfikatu, który został pobrany z portalu Azure i przekaż go tutaj.</span><span class="sxs-lookup"><span data-stu-id="9fe38-177">Browse hello certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="9fe38-178">f.</span><span class="sxs-lookup"><span data-stu-id="9fe38-178">f.</span></span> <span data-ttu-id="9fe38-179">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="9fe38-180">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="9fe38-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9fe38-181">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="9fe38-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9fe38-182">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9fe38-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9fe38-183">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe38-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="9fe38-184">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="9fe38-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9fe38-186">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9fe38-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fe38-187">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9fe38-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9fe38-189">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9fe38-191">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9fe38-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9fe38-193">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9fe38-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9fe38-195">a.</span><span class="sxs-lookup"><span data-stu-id="9fe38-195">a.</span></span> <span data-ttu-id="9fe38-196">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9fe38-197">b.</span><span class="sxs-lookup"><span data-stu-id="9fe38-197">b.</span></span> <span data-ttu-id="9fe38-198">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9fe38-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9fe38-199">c.</span><span class="sxs-lookup"><span data-stu-id="9fe38-199">c.</span></span> <span data-ttu-id="9fe38-200">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9fe38-201">d.</span><span class="sxs-lookup"><span data-stu-id="9fe38-201">d.</span></span> <span data-ttu-id="9fe38-202">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="9fe38-203">Tworzenie użytkownika testowego SensoScientific bezprzewodowej temperatury monitorowania systemu</span><span class="sxs-lookup"><span data-stu-id="9fe38-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="9fe38-204">toolog użytkowników tooenable usługi Azure AD w tooSensoScientific bezprzewodowej temperatury monitorowania systemu, muszą mieć przydzielone do SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="9fe38-204">tooenable Azure AD users toolog in tooSensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="9fe38-205">Praca z [zespołem pomocy technicznej SensoScientific bezprzewodowej temperatury monitorowania systemu](https://www.sensoscientific.com/contact-us/) Aby dodać użytkowników hello hello platforma SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="9fe38-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add hello users in hello SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="9fe38-206">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9fe38-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9fe38-207">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe38-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9fe38-208">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie tooSensoScientific dostępu bezprzewodowego temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="9fe38-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSensoScientific Wireless Temperature Monitoring System.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9fe38-210">**tooassign tooSensoScientific Simona Britta bezprzewodowej temperatury monitorowania systemu, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9fe38-210">**tooassign Britta Simon tooSensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fe38-211">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9fe38-213">Z listy aplikacji hello wybierz **SensoScientific bezprzewodowej temperatury monitorowania systemu**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-213">In hello applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="9fe38-215">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9fe38-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9fe38-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9fe38-217">Click **Add** button.</span></span> <span data-ttu-id="9fe38-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9fe38-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9fe38-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9fe38-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9fe38-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9fe38-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9fe38-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9fe38-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9fe38-223">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9fe38-223">Testing single sign-on</span></span>

<span data-ttu-id="9fe38-224">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9fe38-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="9fe38-225">Kliknij Kafelek SensoScientific bezprzewodowej temperatury monitorowania systemu hello w hello Panel dostępu, można automatycznie zalogowane tooyour SensoScientific bezprzewodowej temperatury systemu monitorowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9fe38-225">Click hello SensoScientific Wireless Temperature Monitoring System tile in hello Access Panel, you will be automatically signed-on tooyour SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="9fe38-226">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9fe38-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9fe38-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9fe38-227">Additional resources</span></span>

* [<span data-ttu-id="9fe38-228">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fe38-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9fe38-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9fe38-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

