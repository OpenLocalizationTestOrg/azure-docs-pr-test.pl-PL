---
title: "Samouczek: Integracja usługi Azure Active Directory z usługą ArcGIS Online | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ArcGIS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="73eef-103">Samouczek: Integracja usługi Azure Active Directory z usługą ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="73eef-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="73eef-104">Z tego samouczka, dowiesz się, jak toointegrate ArcGIS Online z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73eef-104">In this tutorial, you learn how toointegrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73eef-105">Integrowanie ArcGIS Online z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="73eef-105">Integrating ArcGIS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="73eef-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="73eef-106">You can control in Azure AD who has access tooArcGIS Online</span></span>
- <span data-ttu-id="73eef-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooArcGIS Online (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73eef-107">You can enable your users tooautomatically get signed-on tooArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73eef-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="73eef-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="73eef-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73eef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="73eef-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="73eef-110">Prerequisites</span></span>

<span data-ttu-id="73eef-111">tooconfigure integracji z usługą Azure AD ArcGIS online należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="73eef-111">tooconfigure Azure AD integration with ArcGIS Online, you need hello following items:</span></span>

- <span data-ttu-id="73eef-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73eef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73eef-113">ArcGIS Online jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="73eef-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73eef-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="73eef-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73eef-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="73eef-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73eef-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="73eef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73eef-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73eef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73eef-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="73eef-118">Scenario description</span></span>
<span data-ttu-id="73eef-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="73eef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73eef-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="73eef-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73eef-121">Dodawanie ArcGIS Online z galerii hello</span><span class="sxs-lookup"><span data-stu-id="73eef-121">Adding ArcGIS Online from hello gallery</span></span>
2. <span data-ttu-id="73eef-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="73eef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-hello-gallery"></a><span data-ttu-id="73eef-123">Dodawanie ArcGIS Online z galerii hello</span><span class="sxs-lookup"><span data-stu-id="73eef-123">Adding ArcGIS Online from hello gallery</span></span>
<span data-ttu-id="73eef-124">tooconfigure hello integracji ArcGIS Online z usługą Azure AD, należy tooadd ArcGIS Online z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="73eef-124">tooconfigure hello integration of ArcGIS Online into Azure AD, you need tooadd ArcGIS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="73eef-125">**tooadd ArcGIS Online z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="73eef-125">**tooadd ArcGIS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="73eef-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="73eef-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="73eef-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="73eef-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="73eef-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="73eef-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="73eef-131">Kliknij przycisk **nowej aplikacji** przycisk na powitania górnej części okna dialogowego hello tooadd nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73eef-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="73eef-133">W polu wyszukiwania hello wpisz **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="73eef-133">In hello search box, type **ArcGIS Online**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="73eef-135">W panelu wyników hello, wybierz **ArcGIS Online**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73eef-135">In hello results panel, select **ArcGIS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73eef-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="73eef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73eef-138">W tej sekcji można skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ArcGIS Online na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="73eef-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="73eef-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello ArcGIS online jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73eef-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ArcGIS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="73eef-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w trybie Online ArcGIS musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="73eef-140">In other words, a link relationship between an Azure AD user and hello related user in ArcGIS Online needs toobe established.</span></span>

<span data-ttu-id="73eef-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** ArcGIS online.</span><span class="sxs-lookup"><span data-stu-id="73eef-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="73eef-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ArcGIS Online, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="73eef-142">tooconfigure and test Azure AD single sign-on with ArcGIS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="73eef-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="73eef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="73eef-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="73eef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73eef-145">**[Tworzenie użytkownika testowego ArcGIS Online](#creating-an-arcgis-online-test-user)**  -toohave odpowiednikiem Simona Britta w ArcGIS Online, które zostało połączone toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="73eef-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - toohave a counterpart of Britta Simon in ArcGIS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="73eef-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="73eef-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73eef-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="73eef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73eef-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="73eef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73eef-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w trybie Online ArcGIS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73eef-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="73eef-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z ArcGIS Online wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="73eef-150">**tooconfigure Azure AD single sign-on with ArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="73eef-151">W portalu Azure na powitania hello **ArcGIS Online** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="73eef-151">In hello Azure portal, on hello **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="73eef-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="73eef-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="73eef-155">Na powitania **ArcGIS Online domeny i adres URL** sekcji, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="73eef-155">On hello **ArcGIS Online Domain and URLs** section, perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="73eef-157">W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="73eef-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73eef-158">Ta wartość nie jest prawdziwe hello.</span><span class="sxs-lookup"><span data-stu-id="73eef-158">This value is not hello real.</span></span> <span data-ttu-id="73eef-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="73eef-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="73eef-160">Skontaktuj się z [zespołem pomocy technicznej Online klienta ArcGIS](http://support.esri.com/) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="73eef-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) tooget this value.</span></span> 

4. <span data-ttu-id="73eef-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="73eef-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="73eef-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="73eef-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73eef-165">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy ArcGIS jako administrator.</span><span class="sxs-lookup"><span data-stu-id="73eef-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="73eef-166">Kliknij przycisk **Edytuj ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="73eef-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="73eef-167">![Edytuj ustawienia](./media/active-directory-saas-arcgis-tutorial/ic784742.png "edytować ustawienia")</span><span class="sxs-lookup"><span data-stu-id="73eef-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="73eef-168">Kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="73eef-168">Click **Security**.</span></span>

    <span data-ttu-id="73eef-169">![Zabezpieczenia](./media/active-directory-saas-arcgis-tutorial/ic784743.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="73eef-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="73eef-170">W obszarze **logowania do organizacji**, kliknij przycisk **USTAWIĆ dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="73eef-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="73eef-171">![Logowania do organizacji](./media/active-directory-saas-arcgis-tutorial/ic784744.png "logowania do organizacji")</span><span class="sxs-lookup"><span data-stu-id="73eef-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="73eef-172">Na powitania **ustawić dostawcy tożsamości** konfiguracji wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="73eef-172">On hello **Set Identity Provider** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="73eef-173">![Ustawienie dostawcy tożsamości](./media/active-directory-saas-arcgis-tutorial/ic784745.png "ustawienie dostawcy tożsamości")</span><span class="sxs-lookup"><span data-stu-id="73eef-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="73eef-174">a.</span><span class="sxs-lookup"><span data-stu-id="73eef-174">a.</span></span> <span data-ttu-id="73eef-175">W hello **nazwa** tekstowym, wpisz nazwę organizacji.</span><span class="sxs-lookup"><span data-stu-id="73eef-175">In hello **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="73eef-176">b.</span><span class="sxs-lookup"><span data-stu-id="73eef-176">b.</span></span> <span data-ttu-id="73eef-177">Dla **metadanych dla hello organizacji dostawcy tożsamości dostarczane za pomocą**, wybierz pozycję **plik**.</span><span class="sxs-lookup"><span data-stu-id="73eef-177">For **Metadata for hello Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="73eef-178">c.</span><span class="sxs-lookup"><span data-stu-id="73eef-178">c.</span></span> <span data-ttu-id="73eef-179">tooupload pliku metadanych pobranych, kliknij przycisk **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="73eef-179">tooupload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="73eef-180">d.</span><span class="sxs-lookup"><span data-stu-id="73eef-180">d.</span></span> <span data-ttu-id="73eef-181">Kliknij przycisk **dostawcy tożsamości zestawu**.</span><span class="sxs-lookup"><span data-stu-id="73eef-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="73eef-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="73eef-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="73eef-183">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="73eef-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="73eef-184">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73eef-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73eef-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73eef-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="73eef-186">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="73eef-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="73eef-188">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="73eef-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="73eef-189">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="73eef-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73eef-191">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="73eef-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73eef-193">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="73eef-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73eef-195">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="73eef-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73eef-197">a.</span><span class="sxs-lookup"><span data-stu-id="73eef-197">a.</span></span> <span data-ttu-id="73eef-198">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73eef-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73eef-199">b.</span><span class="sxs-lookup"><span data-stu-id="73eef-199">b.</span></span> <span data-ttu-id="73eef-200">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="73eef-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="73eef-201">c.</span><span class="sxs-lookup"><span data-stu-id="73eef-201">c.</span></span> <span data-ttu-id="73eef-202">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="73eef-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="73eef-203">d.</span><span class="sxs-lookup"><span data-stu-id="73eef-203">d.</span></span> <span data-ttu-id="73eef-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="73eef-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="73eef-205">Tworzenie użytkownika testowego ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="73eef-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="73eef-206">W kolejności tooenable usługi Azure AD użytkownicy toolog do ArcGIS Online musi być przygotowana do ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="73eef-206">In order tooenable Azure AD users toolog into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="73eef-207">W przypadku hello ArcGIS online Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="73eef-207">In hello case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="73eef-208">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="73eef-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="73eef-209">Zaloguj się za tooyour **ArcGIS** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="73eef-209">Log in tooyour **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="73eef-210">Kliknij przycisk **członków zaproszenia**.</span><span class="sxs-lookup"><span data-stu-id="73eef-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="73eef-211">![Zaprosić](./media/active-directory-saas-arcgis-tutorial/ic784747.png "zaprosić")</span><span class="sxs-lookup"><span data-stu-id="73eef-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="73eef-212">Wybierz **automatycznie dodawać członków bez wysyłania wiadomości e-mail**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="73eef-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="73eef-213">![Automatyczne dodawanie członków](./media/active-directory-saas-arcgis-tutorial/ic784748.png "automatycznie dodawać członków")</span><span class="sxs-lookup"><span data-stu-id="73eef-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="73eef-214">Na powitania **członków** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="73eef-214">On hello **Members** dialog page, perform hello following steps:</span></span>
   
     <span data-ttu-id="73eef-215">![Dodaj i przejrzyj](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Dodaj i przejrzyj")</span><span class="sxs-lookup"><span data-stu-id="73eef-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="73eef-216">a.</span><span class="sxs-lookup"><span data-stu-id="73eef-216">a.</span></span> <span data-ttu-id="73eef-217">Wprowadź hello **E-mail**, **imię**, i **nazwisko** ma tooprovision poprawnego konta usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="73eef-217">Enter hello **Email**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision.</span></span>
  
     <span data-ttu-id="73eef-218">b.</span><span class="sxs-lookup"><span data-stu-id="73eef-218">b.</span></span> <span data-ttu-id="73eef-219">Kliknij przycisk **Dodaj i przejrzyj**.</span><span class="sxs-lookup"><span data-stu-id="73eef-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="73eef-220">Przejrzyj hello dane zostały wprowadzone, a następnie kliknij przycisk **Dodaj członków**.</span><span class="sxs-lookup"><span data-stu-id="73eef-220">Review hello data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="73eef-221">![Dodaj element członkowski](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Dodaj element członkowski")</span><span class="sxs-lookup"><span data-stu-id="73eef-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="73eef-222">właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="73eef-222">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="73eef-223">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="73eef-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="73eef-224">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooArcGIS w trybie Online.</span><span class="sxs-lookup"><span data-stu-id="73eef-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooArcGIS Online.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="73eef-226">**tooassign tooArcGIS Simona Britta w trybie Online, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="73eef-226">**tooassign Britta Simon tooArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="73eef-227">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="73eef-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="73eef-229">Z listy aplikacji hello wybierz **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="73eef-229">In hello applications list, select **ArcGIS Online**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="73eef-231">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="73eef-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="73eef-233">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="73eef-233">Click **Add** button.</span></span> <span data-ttu-id="73eef-234">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="73eef-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="73eef-236">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="73eef-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="73eef-237">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="73eef-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73eef-238">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="73eef-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73eef-239">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="73eef-239">Testing single sign-on</span></span>

<span data-ttu-id="73eef-240">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="73eef-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="73eef-241">Po kliknięciu kafelka ArcGIS Online hello w hello Panel dostępu, należy pobrać aplikacji ArcGIS Online tooyour zalogowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="73eef-241">When you click hello ArcGIS Online tile in hello Access Panel, you should get automatically signed-on tooyour ArcGIS Online application.</span></span>
<span data-ttu-id="73eef-242">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73eef-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73eef-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="73eef-243">Additional resources</span></span>

* [<span data-ttu-id="73eef-244">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73eef-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73eef-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73eef-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

